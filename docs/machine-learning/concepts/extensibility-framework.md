---
title: Arquitetura de extensibilidade
description: Este artigo descreve a arquitetura da estrutura de extensibilidade para executar um script externo de R ou Python nos Serviços de Machine Learning do SQL Server. O script é executado em um ambiente de runtime de linguagem como uma extensão para o principal mecanismo de banco de dados.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 053639f8ff25d50e7cad9c05d82cfcac6a0ee071
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956507"
---
# <a name="extensibility-architecture-in-sql-server-machine-learning-services"></a>Arquitetura de extensibilidade no Serviços de Machine Learning do SQL Server 
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Este artigo descreve a arquitetura da estrutura de extensibilidade para executar um script externo de R ou Python nos Serviços de Machine Learning do SQL Server. O script é executado em um ambiente de runtime de linguagem como uma extensão para o principal mecanismo de banco de dados.

## <a name="background"></a>Segundo plano

A estrutura de extensibilidade foi introduzida no SQL Server 2016 para dar suporte ao runtime do R com o [R Services](../r/sql-server-r-services.md). O SQL Server 2017 e posteriores têm suporte para Python com o [Serviços de Machine Learning](../sql-server-machine-learning-services.md).

A finalidade da estrutura de extensibilidade é oferecer uma interface entre o SQL Server e as linguagens de ciência de dados, como R e Python. A meta é reduzir o conflito ao mover soluções de ciência de dados para produção e proteger os dados expostos durante o processo de desenvolvimento. Executando uma linguagem de script confiável dentro de uma estrutura segura gerenciada pelo SQL Server, os administradores de banco de dados podem manter a segurança enquanto permitem que os cientistas de dados acessem dados empresariais.

O diagrama a seguir descreve visualmente as oportunidades e os benefícios da arquitetura extensível.

  ![Metas de integração com o SQL Server](../media/ml-service-value-add.png "Adição de valor dos Serviços de Machine Learning")

Um script externo pode ser executado chamando um procedimento armazenado e os resultados são retornados como resultados tabulares diretamente para o SQL Server. Isso facilita a geração ou o consumo de aprendizado de máquina de qualquer aplicativo que pode enviar uma consulta SQL e manipular os resultados.

+ A execução de script externo está sujeita à segurança de dados do SQL Server. Um usuário que executa um script externo só pode acessar dados que estão igualmente disponíveis em uma consulta SQL. Se uma consulta falhar devido a uma permissão insuficiente, um script executado pelo mesmo usuário também falhará pelo mesmo motivo. A segurança do SQL Server é imposta na tabela, no banco de dados e no nível de instância. Os administradores de banco de dados podem gerenciar o acesso do usuário, os recursos usados por scripts externos e as bibliotecas de código externo adicionadas ao servidor.  

+ As oportunidades de escala e otimização têm uma base dupla: ganhos por meio da plataforma de banco de dados (índices ColumnStore, [governança de recursos](../../machine-learning/administration/resource-governor.md)) e ganhos específicos da extensão, por exemplo, quando as bibliotecas da Microsoft para R e Python são usadas para modelos de ciência de dados. Enquanto o R é single-threaded, as funções RevoScaleR são multi-threaded, capazes de distribuir uma carga de trabalho em vários núcleos.

+ A implantação usa metodologias do SQL Server. Elas podem ser procedimentos armazenados encapsulando as consultas de script externo, SQL inseridas ou T-SQL que chamam funções como PREDICT para retornar resultados de modelos de previsão persistentes no servidor.

+ Os desenvolvedores com habilidades estabelecidas em ferramentas e IDEs específicos podem escrever código nessas ferramentas e, em seguida, portar o código para o SQL Server.

## <a name="architecture-diagram"></a>Diagrama de arquitetura

A arquitetura é criada de modo que os scripts externos são executados em um processo separado do SQL Server, mas com componentes que gerenciam internamente a cadeia de solicitações para dados e operações no SQL Server. Dependendo da versão do SQL Server, as extensões de linguagem compatíveis incluem [R](extension-r.md), [Python](extension-python.md) e linguagens de terceiros, como Java e .NET.

  ***Arquitetura de componente no Windows:***
  
  ![Arquitetura de componente do Windows](../media/generic-architecture-windows.png "Arquitetura de componente")
  
  ***Arquitetura de componente no Linux:***

  ![Arquitetura de componente do Linux](../media/generic-architecture-linux.png "Arquitetura de componente")
  
Os componentes incluem um serviço **Launchpad** usado para invocar runtimes externos e lógica específica da biblioteca para o carregamento de interpretadores e bibliotecas. O inicializador carrega um runtime de linguagem, além de módulos proprietários. Por exemplo, se o código incluir funções RevoScaleR, um interpretador RevoScaleR será carregado. O **BxlServer** e o **Satélite SQL** gerenciam a comunicação e a transferência de dados com o SQL Server. 

No Linux, o SQL usa um serviço **Launchpad** para se comunicar com um processo Launchpad separado para cada usuário.

<a name="launchpad"></a>

## <a name="launchpad"></a>Launchpad

O [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] é um serviço que gerencia e executa scripts externos, semelhantes à forma com que o serviço de indexação e consulta de texto completo inicia um host separado para o processamento de consultas de texto completo. O serviço Launchpad pode iniciar somente inicializadores confiáveis que foram publicados pela Microsoft ou que tenham sido certificados pela Microsoft como atendendo aos requisitos de desempenho e gerenciamento de recursos.

| Inicializadores confiáveis | Extensão | Versões do SQL Server |
|-------------------|-----------|---------------------|
| RLauncher.dll para a linguagem R para Windows | [Extensão R](extension-r.md) | SQL Server 2016 e posterior |
| Pythonlauncher.dll para Python 3.5 para Windows | [Extensão Python](extension-python.md) | SQL Server 2017 e posteriores |
| RLauncher.so para a linguagem R para Linux | [Extensão R](extension-r.md) | SQL Server 2019 e posteriores |
| Pythonlauncher.so para Python 3.5 para Linux | [Extensão Python](extension-python.md) | SQL Server 2019 e posteriores |

O serviço [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] é executado em sua própria conta de usuário. Se você alterar a conta que executa o Launchpad, faça isso usando o SQL Server Configuration Manager, para garantir que as alterações sejam gravadas em arquivos relacionados.

No Windows, um serviço [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] separado é criado para cada instância do mecanismo de banco de dados à qual você adicionou Serviços de Machine Learning do SQL Server. Há um serviço Launchpad para cada instância de mecanismo de banco de dados; portanto, se você tiver várias instâncias com suporte a script externo, você terá um serviço Launchpad para cada um. Uma instância do mecanismo de banco de dados está associada ao serviço Launchpad criado para ela. Todas as invocações de script externo em um procedimento armazenado ou T-SQL resultam no serviço SQL Server chamando o serviço Launchpad criado para a mesma instância.

Para executar tarefas em uma linguagem compatível específica, o Launchpad obtém uma conta de trabalho protegida do pool e inicia um processo satélite para gerenciar o runtime externo. Cada processo satélite herda a conta de usuário do Launchpad e usa essa conta de trabalho durante a execução do script. Se o script usar processos paralelos, eles serão criados na mesma conta de trabalho individual.

No Linux, há suporte para apenas uma instância do mecanismo de banco de dados e há um serviço Launchpad associado à instância. Quando um script é executado, o serviço Launchpad inicia um processo do Launchpad separado com a conta de usuário com poucos privilégios **mssql_satellite**. Cada processo satélite herda a conta de usuário mssql_satellite e usa essa conta durante a execução do script.

## <a name="bxlserver-and-sql-satellite"></a>BxlServer e Satélite SQL

O **BxlServer** é um executável fornecido pela Microsoft que gerencia a comunicação entre o SQL Server e o runtime da linguagem. Ele cria os objetos de trabalho do Windows para Windows (ou os namespaces para Linux) que são usados para conter sessões de script externo. Ele também provisiona pastas de trabalho seguras para cada trabalho de script externo e usa o Satélite SQL para gerenciar a transferência de dados entre o runtime externo e o SQL Server. Se executar o [Explorador de Processos](/sysinternals/downloads/process-explorer) enquanto um trabalho estiver em execução, você poderá ver uma ou várias instâncias do BxlServer.

Na verdade, o BxlServer é um complemento para um ambiente de runtime de linguagem que funciona com o SQL Server para transferir dados e gerenciar tarefas. BXL significa linguagem de troca binária e refere-se ao formato de dados usado para mover dados com eficiência entre o SQL Server e processos externos como o R. O BxlServer também é uma parte importante dos produtos relacionados, como o Microsoft R Client e o Microsoft R Server.

O **Satélite SQL** é uma API de extensibilidade, inclusa no mecanismo de banco de dados, que é compatível com código externo ou runtimes externos implementados usando C ou C++.

O BxlServer usa o Satélite SQL para estas tarefas:

+ Ler dados de entrada
+ Gravar dados de saída
+ Obter argumentos de entrada
+ Gravar argumentos de saída
+ Tratamento de erros
+ Gravar STDOUT e STDERR de volta para o cliente

O Satélite SQL usa um formato de dados personalizado que é otimizado para a transferência de dados rápida entre o SQL Server e as linguagens de script externo. Ele executa conversões de tipo e define os esquemas dos conjuntos de dados de entrada e de saída durante as comunicações entre o SQL Server e o runtime do script externo.

O Satélite SQL pode ser monitorado usando eventos estendidos do Windows (xEvents). Para saber mais, confira [Eventos estendidos para os Serviços de Machine Learning do SQL Server](../../machine-learning/administration/extended-events.md).

## <a name="communication-channels-between-components"></a>Canais de comunicação entre componentes

Os protocolos de comunicação entre componentes e plataformas de dados são descritos nesta seção.

+ **TCP/IP**

  Por padrão, as comunicações internas entre o SQL Server e o Satélite SQL usam TCP/IP.

+ **Pipes nomeados**

  O transporte de dados internos entre o BxlServer e o SQL Server por meio do Satélite SQL usa um formato de dados proprietários e compactados para melhorar o desempenho. Os dados são trocados entre os tempos de execução de linguagem e o BxlServer no formato BXL, usando pipes nomeados.

+ **ODBC**

  As comunicações entre clientes de ciência de dados externos e uma instância remota do SQL Server usam o ODBC. A conta que envia os trabalhos de script para o SQL Server deve ter permissões tanto para se conectar à instância quanto para executar scripts externos.

  Além disso, dependendo da tarefa, a conta talvez precise destas permissões:

  + Ler os dados usados pelo trabalho
  + Escrever dados em tabelas: por exemplo, ao salvar os resultados em uma tabela
  + Criar objetos de banco de dados: por exemplo, ao salvar o script externo como parte de um novo procedimento armazenado.

  Quando o SQL Server é usado como o contexto de computação para o script executado de um cliente remoto e o executável deve recuperar dados de uma fonte externa, a ODBC é usada para write-back. O SQL Server mapeia a identidade do usuário que emite o comando remoto para a identidade do usuário na instância atual e, em seguida, executa o comando ODBC usando as credenciais desse usuário. A cadeia de conexão necessária para executar essa chamada ODBC é obtida do código cliente.

+ **RODBC (somente R)** 

  Chamadas ODBC adicionais podem ser feitas dentro do script usando **RODBC**. RODBC é um pacote R popular usado para acessar dados em bancos de dados relacionais; no entanto, o desempenho dele é geralmente mais lento do que provedores comparáveis usados pelo SQL Server. Muitos scripts R usam chamadas inseridas para RODBC como uma maneira de recuperar os conjuntos de dados "secundários" para uso em análises. Por exemplo, o procedimento armazenado que treina um modelo pode definir uma consulta SQL para obter os dados para treinar um modelo, mas usar uma chamada RODBC inserida para obter os fatores adicionais, para realizar pesquisas ou para obter novos dados de fontes externas, tais como arquivos de texto ou Excel.

  O código a seguir ilustra uma chamada RODBC inserida em um script R:

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **Outros protocolos**

  Processos que precisam trabalhar em partes ou transferir dados para um cliente remoto também podem usar o [formato de arquivo XDF](/machine-learning-server/r/concept-what-is-xdf). A transferência de dados real é feita por meio de blobs codificados.

## <a name="see-also"></a>Consulte Também

+ [Extensão do R no SQL Server](extension-r.md)
+ [Extensão do Python no SQL Server](extension-python.md)