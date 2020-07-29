---
title: Arquitetura de extensibilidade nas Extensões de Linguagem do SQL Server
titleSuffix: ''
description: Saiba mais sobre a arquitetura de extensibilidade usada para as Extensões de Linguagem do SQL Server, que permite executar código externo no SQL Server. No SQL Server 2019, há suporte para Java. O código é executado em um ambiente de runtime de linguagem como uma extensão para o principal mecanismo de banco de dados.
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3e52727922f03a6ae078477b8af6cf0171acd053
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85722556"
---
# <a name="extensibility-architecture-in-sql-server-language-extensions"></a>Arquitetura de extensibilidade nas Extensões de Linguagem do SQL Server

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Saiba mais sobre a arquitetura de extensibilidade usada para as Extensões de Linguagem do SQL Server, que permite executar código externo no SQL Server. No SQL Server 2019, há suporte para Java. O código é executado em um ambiente de runtime de linguagem como uma extensão para o principal mecanismo de banco de dados.

## <a name="background"></a>Segundo plano

A finalidade da estrutura de extensibilidade é oferecer uma interface entre o SQL Server e as linguagens externas, como Java. Executando uma linguagem confiável dentro de uma estrutura segura gerenciada pelo SQL Server, os administradores de banco de dados podem manter a segurança enquanto permitem que os cientistas de dados acessem dados empresariais.

<!-- We need to get a diagram like the one below.
The following diagram visually describes opportunities and benefits of the extensible architecture.

  ![Goals of integration with SQL Server](../media/ml-service-value-add.png "Machine Learning Services Value Add")
-->

Qualquer linguagem externa com suporte pode ser executada chamando um procedimento armazenado e os resultados são retornados como resultados tabulares diretamente para o SQL Server. Isso facilita o uso da linguagem externa de qualquer aplicativo que pode enviar uma consulta SQL e manipular os resultados.

## <a name="architecture-diagrams"></a>Diagramas de arquitetura

A arquitetura é criada de modo que o código externo é executado em um processo separado do SQL Server, mas com componentes que gerenciam internamente a cadeia de solicitações para dados e operações no SQL Server. 
  
  ***Arquitetura de componente no Windows:***

  ![Arquitetura de componente no Windows](../media/generic-architecture-windows.png "Arquitetura de componente no Windows")
  
  ***Arquitetura de componente no Linux:***
  
  ![Arquitetura de componente no Linux](../media/generic-architecture-linux.png "Arquitetura de componente no Linux")
  
Os componentes incluem um serviço **Launchpad** usado para invocar tempos de execução externos (por exemplo, Java) e lógica específica da biblioteca para o carregamento de interpretadores e bibliotecas.

<a name="launchpad"></a>

## <a name="launchpad"></a>Launchpad

O [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] é um serviço que gerencia os limites de tempo de vida, recursos e segurança do processo externo responsável pela execução do script. Isso é semelhantes à forma com que o serviço de indexação e consulta de texto completo inicia um host separado para o processamento de consultas de texto completo. O serviço Launchpad pode iniciar somente inicializadores confiáveis que foram publicados pela Microsoft ou que tenham sido certificados pela Microsoft como atendendo aos requisitos de desempenho e gerenciamento de recursos.

| Inicializadores confiáveis | Extensão | Versões do SQL Server |
|-------------------|-----------|---------------------|
| JavaLauncher.dll para Java | Extensão de Java | SQL Server 2019 |

O serviço [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] é executado em **SQLRUserGroup** que usa [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation) para isolamento de execução.

Um serviço [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] separado é criado para cada instância do mecanismo de banco de dados à qual você adicionou Extensões de Linguagem de Computador do SQL Server. Há um serviço Launchpad para cada instância de mecanismo de banco de dados; portanto, se você tiver várias instâncias com suporte a script externo, você terá um serviço Launchpad para cada um. Uma instância do mecanismo de banco de dados está associada ao serviço Launchpad criado para ela. Todas as invocações de script externo em um procedimento armazenado ou T-SQL resultam no serviço SQL Server chamando o serviço Launchpad criado para a mesma instância.

Para executar tarefas em uma linguagem compatível específica, o Launchpad obtém uma conta de trabalho protegida do pool e inicia um processo satélite para gerenciar o runtime externo. Cada processo satélite herda a conta de usuário do Launchpad e usa essa conta de trabalho durante a execução do script. Se o script usar processos paralelos, eles serão criados na mesma conta de trabalho individual.

## <a name="communication-channels-between-components"></a>Canais de comunicação entre componentes

Os protocolos de comunicação entre componentes e plataformas de dados são descritos nesta seção.

+ **TCP/IP**

  Por padrão, as comunicações internas entre o SQL Server e o Satélite SQL usam TCP/IP.

+ **ODBC**

  As comunicações entre clientes de ciência de dados externos e uma instância remota do SQL Server usam o ODBC. A conta que envia os trabalhos de script para o SQL Server deve ter permissões tanto para se conectar à instância quanto para executar scripts externos.

  Além disso, dependendo da tarefa, a conta talvez precise destas permissões:

  + Ler os dados usados pelo trabalho
  + Escrever dados em tabelas: por exemplo, ao salvar os resultados em uma tabela
  + Criar objetos de banco de dados: por exemplo, ao salvar o script externo como parte de um novo procedimento armazenado.

  Quando o SQL Server é usado como o contexto de computação para o script executado de um cliente remoto e o executável deve recuperar dados de uma fonte externa, a ODBC é usada para write-back. O SQL Server mapeia a identidade do usuário que emite o comando remoto para a identidade do usuário na instância atual e, em seguida, executa o comando ODBC usando as credenciais desse usuário. A cadeia de conexão necessária para executar essa chamada ODBC é obtida do código cliente.

+ **Outros protocolos**

  Processos que precisam trabalhar em partes ou transferir dados para um cliente remoto também podem usar o [formato de arquivo XDF](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf). A transferência de dados real é feita por meio de blobs codificados.

## <a name="next-steps"></a>Próximas etapas

+ [O que são Extensões de Linguagem?](../language-extensions-overview.md)
