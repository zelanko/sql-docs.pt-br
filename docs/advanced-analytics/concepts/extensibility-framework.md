---
title: Arquitetura de extensibilidade no SQL Server Machine Learning Services | Microsoft Docs
description: Suporte para código externo para o mecanismo de banco de dados do SQL Server, com a arquitetura dual para executar o script de R e Python em dados relacionais.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: fae8beb4f865c537f00fa8b58a01cafe09541d71
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43892848"
---
# <a name="extensibility-architecture-in-sql-server-machine-learning-services"></a>Arquitetura de extensibilidade em serviços do SQL Server Machine Learning 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server tem uma estrutura de extensibilidade para a execução de script externo, como R ou Python no servidor. Script é executado em um ambiente de tempo de execução de linguagem como uma extensão para o mecanismo de banco de dados principal. 

## <a name="background"></a>Plano de fundo

A estrutura de extensibilidade foi introduzida no SQL Server 2016 para dar suporte o tempo de execução de R. Adiciona o suporte para Python para SQL Server 2017

O objetivo da estrutura de extensibilidade é fornecer uma interface entre o SQL Server e linguagens de ciência de dados, como R e Python, reduzindo a fricção quando soluções de ciência de dados movendo para a produção e proteger os dados expostos durante o desenvolvimento processo. Executando uma linguagem de script confiável dentro de uma estrutura segura gerenciada pelo SQL Server, os administradores de banco de dados podem manter a segurança, permitindo que os cientistas de dados acesso a dados corporativos.

O diagrama a seguir descreve visualmente oportunidades e os benefícios da arquitetura extensível.

  ![Metas da integração com o SQL Server](../media/ml-service-value-add.png "serviços de valor agregado do Machine Learning")

Qualquer script de R ou Python pode ser executado ao chamar um procedimento armazenado, e os resultados são retornados como resultados tabulares diretamente para o SQL Server, tornando mais fácil gerar ou consumir o aprendizado de máquina a partir de qualquer aplicativo que possa enviar uma consulta SQL e lidar com os resultados.

+ Execução de script externo está sujeito a segurança de dados do SQL Server, em que um usuário que está executando o script externo pode acessar somente os dados que é igualmente disponíveis em uma consulta SQL. Se uma consulta falhar devido a permissões insuficientes, o script executado pelo mesmo usuário também falharia pelo mesmo motivo. Segurança do SQL Server é imposta no banco de dados, tabela e nível de instância. Os administradores de banco de dados podem gerenciar acesso do usuário, recursos usados pelos scripts externos e bibliotecas de código externo adicionadas ao servidor.  

+ Escala e a otimização de oportunidades para ter uma base dupla: ganhos por meio da plataforma de banco de dados (índices ColumnStore, [governança de recursos](../../advanced-analytics/r/resource-governance-for-r-services.md)) e ganhos específicas à extensão quando bibliotecas da Microsoft para R e Python são usadas para dados modelos de ciência. Enquanto o R é single-threaded, funções de RevoScaleR são multi-threaded, capaz de distribuir uma carga de trabalho ao longo de vários núcleos.

+ A implantação usa metodologias do SQL Server: procedimentos armazenados, quebra automática de script externo, embedded SQL ou o T-SQL consulta chamando funções como PREDICT para retornar os resultados de modelos de previsão são persistentes no servidor.

+ Os desenvolvedores de R e Python com estabelecida habilidades em ferramentas específicas e IDEs podem escrever código em dessas ferramentas e, em seguida, portar o código para o SQL Server.

## <a name="architecture-diagram"></a>Diagrama da arquitetura

A arquitetura é projetada, de modo que os scripts externos executados em um processo separado do SQL Server, mas com componentes que gerenciam internamente a cadeia de solicitações de dados e operações no SQL Server. Dependendo da versão do SQL Server, extensões de linguagem com suporte incluem o R e Python. 

  ![Arquitetura do componente](../media/generic-architecture.png "arquitetura do componente")

Os componentes incluem uma **Launchpad** usado para invocar o idioma de iniciadores específicos do idioma (R ou Python) e lógica específica da biblioteca de carregamento de interpretadores e bibliotecas de serviço. O iniciador carrega um tempo de execução de linguagem, além de quaisquer módulos proprietários. Por exemplo, se seu código inclui funções RevoScaleR, carrega um interpretador do RevoScaleR. **O BxlServer** e **satélite SQL** gerenciar a comunicação e transferência de dados com o SQL Server.

## <a name="launchpad"></a>Launchpad

O Launchpad confiável do SQL Server é um serviço que gerencia e executa scripts externos, semelhantes à maneira que o serviço de indexação e consulta de texto completo inicia um host separado para o processamento de consultas de texto completo. O serviço Launchpad pode iniciar somente inicializadores confiáveis que são publicadas pela Microsoft ou que tenham sido certificados pela Microsoft como atendendo aos requisitos de desempenho e gerenciamento de recursos.

| Inicializadores confiáveis | Extensão | Versões do SQL Server |
|-------------------|-----------|---------------------|
| Rlauncher. dll para a linguagem R | [Extensão de R](extension-r.md) | SQL Server 2016, SQL Server 2017 |
| Pythonlauncher.dll para o Python 3.5 | [Extensão do Python](extension-python.md) | SQL Server 2017 |

O serviço [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] é executado em sua própria conta de usuário. Se você alterar a conta que executa o Launchpad, certifique-se de fazer isso usar o SQL Server Configuration Manager, para garantir que as alterações são gravadas para arquivos relacionados.

Para executar tarefas em um determinado idioma com suporte, a barra inicial obtém uma conta de trabalho protegida do pool e inicia um processo de satélite para gerenciar o tempo de execução externo. Cada processo satélite herda a conta de usuário do Launchpad e usa a conta de trabalho para a duração da execução do script. Se o script usa processos paralelos, eles são criados sob a conta de trabalho mesmo, único.

## <a name="bxlserver-and-sql-satellite"></a>O BxlServer e satélite SQL

**O BxlServer** é um executável fornecido pela Microsoft que gerencia a comunicação entre o SQL Server e o Python ou R. Ele cria os objetos de trabalho do Windows que são usados para conter as sessões do script externo, as pastas de trabalho seguras provisões para cada trabalho de script externo e usa o satélite SQL para gerenciar a transferência de dados entre o tempo de execução externo e o SQL Server. Se você executar [Process Explorer](https://technet.microsoft.com/sysinternals/processexplorer.aspx) enquanto um trabalho está em execução, você poderá ver uma ou várias instâncias do BxlServer.

Na verdade, o BxlServer é um complemento para uma linguagem de executar o ambiente de tempo que funciona com o SQL Server para transferir dados e gerenciar tarefas. BXL significa linguagem de troca binária e refere-se para o formato de dados usado para mover dados com eficiência entre o SQL Server e processos externos. O BxlServer também é uma parte importante de produtos relacionados, como o Microsoft R Client e Microsoft R Server.

**Satélite SQL** é uma API de extensibilidade, incluído no mecanismo de banco de dados a partir do SQL Server 2016, que dá suporte a código externo ou tempos de execução externos implementados usando C ou C++.

O BxlServer usa o Satélite SQL para estas tarefas:

+ Ler dados de entrada
+ Gravar dados de saída
+ Obter argumentos de entrada
+ Gravar argumentos de saída
+ Manipulação de erros
+ Gravar STDOUT e STDERR de volta para o cliente

Satélite SQL usa um formato de dados personalizado que é otimizado para transferência de dados rápida entre o SQL Server e linguagens de script externo. Ele executa conversões de tipo e define os esquemas dos conjuntos de dados de entrada e saídos durante a comunicação entre o SQL Server e o tempo de execução do script externo.

O satélite SQL pode ser monitorado usando eventos estendidos (xEvents) do windows. Para obter mais informações, consulte [eventos estendidos para R](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md) e [eventos estendidos para o Python](../../advanced-analytics/python/extended-events-for-python.md).

## <a name="communication-channels-between-components"></a>Canais de comunicação entre componentes

Protocolos de comunicação entre os componentes e plataformas de dados são descritos nesta seção.

+ **TCP/IP**

  Por padrão, as comunicações internas entre o SQL Server e o satélite SQL usam TCP/IP.

+ **Pipes nomeados**

  Transporte de dados internos entre o BxlServer e o SQL Server por meio do satélite SQL usa um formato de dados proprietários e compactados para melhorar o desempenho. Dados são trocados entre os tempos de execução de linguagem e BxlServer no formato BXL, usando Pipes nomeados.

+ **ODBC**

  As comunicações entre clientes de ciência de dados externa e uma instância remota do SQL Server usam o ODBC. A conta que envia os trabalhos de script para o SQL Server deve ter ambas as permissões para se conectar à instância e executar scripts externos.

  Além disso, dependendo da tarefa, a conta talvez seja necessário essas permissões:

  + Ler os dados usados pelo trabalho
  + Gravar dados em tabelas: por exemplo, quando salvar resultados em uma tabela
  + Criar objetos de banco de dados: por exemplo, se salvar script externo como parte de um novo procedimento armazenado.

  Quando o SQL Server é usado como o contexto de computação para o script executado a partir de um cliente remoto e o executável devem recuperar dados de uma fonte externa, ODBC é usado para write-back. SQL Server mapeia a identidade do usuário que emite o comando remoto para a identidade do usuário na instância atual e executa o comando ODBC usando as credenciais do usuário. A cadeia de conexão necessária para executar essa chamada ODBC é obtida do código cliente.

+ **RODBC (R)** 

  Chamadas ODBC adicionais podem ser feitas dentro do script usando **RODBC**. RODBC é um pacote R popular usado para acessar dados em bancos de dados relacionais; No entanto, seu desempenho é geralmente mais lento do que provedores comparáveis usados pelo SQL Server. Muitos scripts R usam chamadas inseridas para RODBC como uma maneira de recuperar os conjuntos de dados "secundários" para uso em análises. Por exemplo, o procedimento armazenado que treina um modelo pode definir uma consulta SQL para obter os dados para treinar um modelo, mas usar uma chamada RODBC inserida para obter os fatores adicionais, para realizar pesquisas ou para obter novos dados de fontes externas, tais como arquivos de texto ou Excel.

  O código a seguir ilustra uma chamada RODBC inserida em um script R:

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **Outros protocolos**

  Processos que precisam trabalhar em "partes" ou transferir dados para um cliente remoto também podem usar o [formato de arquivo XDF](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf). Transferência de dados real é via blobs codificados.

## <a name="see-also"></a>Consulte também

+ [Extensão do R no SQL Server](extension-r.md)
+ [Extensão do Python no SQL Server](extension-python.md)