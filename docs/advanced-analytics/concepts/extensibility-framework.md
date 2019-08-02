---
title: Arquitetura de extensibilidade para linguagem R e script Python
description: Suporte a código externo para o mecanismo de banco de dados SQL Server, com arquitetura dupla para executar script R e Python em dados relacionais.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 49c45fa39cd271140ba78c2b1b32ee8a2f9c1a7a
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715250"
---
# <a name="extensibility-architecture-in-sql-server-machine-learning-services"></a>Arquitetura de extensibilidade no SQL Server Serviços de Machine Learning 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server tem uma estrutura de extensibilidade para executar script externo, como R ou Python no servidor. O script é executado em um ambiente de tempo de execução de linguagem como uma extensão para o mecanismo de banco de dados principal. 

## <a name="background"></a>Informações preliminares

A estrutura de extensibilidade foi introduzida no SQL Server 2016 para dar suporte ao tempo de execução de R. SQL Server 2017 e posteriores têm suporte para Python.

A finalidade da estrutura de extensibilidade é fornecer uma interface entre SQL Server e linguagens de ciência de dados como R e Python, reduzindo o conflito ao mover soluções de ciência de dados para produção e proteger os dados expostos durante o desenvolvimento Process. Ao executar uma linguagem de script confiável em uma estrutura segura gerenciada pelo SQL Server, os administradores de banco de dados podem manter a segurança e, ao mesmo tempo, permitir que os cientistas de dados acessem dados corporativos.

O diagrama a seguir descreve visualmente as oportunidades e os benefícios da arquitetura extensível.

  ![Metas de integração com o SQL Server](../media/ml-service-value-add.png "Adição de valor de serviços de Machine Learning")

Qualquer script de R ou Python pode ser executado chamando um procedimento armazenado e os resultados são retornados como resultados tabulares diretamente para SQL Server, facilitando a geração ou o consumo de aprendizado de máquina de qualquer aplicativo que possa enviar uma consulta SQL e manipular os resultados.

+ A execução de script externo está sujeita a SQL Server segurança de dados, em que um usuário que executa o script externo só pode acessar dados que estão igualmente disponíveis em uma consulta SQL. Se uma consulta falhar devido a permissões insuficientes, o script executado pelo mesmo usuário também falhará pelo mesmo motivo. SQL Server segurança é imposta na tabela, no banco de dados e no nível de instância. Os administradores de banco de dados podem gerenciar o acesso do usuário, os recursos usados por scripts externos e as bibliotecas de código externo adicionadas ao servidor.  

+ As oportunidades de escala e otimização têm uma base dupla: ganhos pela plataforma de banco de dados (índices ColumnStore, [governança de recursos](../../advanced-analytics/r/resource-governance-for-r-services.md)) e ganhos específicos de extensão quando as bibliotecas da Microsoft para R e Python são usadas para modelos de ciência de dados. Enquanto o R é de thread único, as funções RevoScaleR são multi-threaded, capazes de distribuir uma carga de trabalho em vários núcleos.

+ A implantação usa metodologias SQL Server: os procedimentos armazenados que encapsulam o script externo, o SQL inserido ou as consultas T-SQL que chamam funções como PREDICT para retornar resultados de modelos de previsão persistiram no servidor.

+ Os desenvolvedores de R e Python com habilidades estabelecidas em ferramentas e IDEs específicos podem escrever código nessas ferramentas e, em seguida, código de porta para SQL Server.

## <a name="architecture-diagram"></a>Diagrama de arquitetura

A arquitetura é projetada de modo que os scripts externos sejam executados em um processo separado do SQL Server, mas com componentes que gerenciam internamente a cadeia de solicitações de dados e operações em SQL Server. Dependendo da versão do SQL Server, as extensões de idioma com suporte incluem R e Python. 

  ![Arquitetura do componente](../media/generic-architecture.png "Arquitetura do componente")

Os componentes incluem um serviço **Launchpad** usado para invocar os iniciadores específicos de um idioma (R ou Python), a linguagem e a lógica específica da biblioteca para o carregamento de intérpretes e bibliotecas. O iniciador carrega um tempo de execução de idioma, além de quaisquer módulos proprietários. Por exemplo, se o código incluir funções RevoScaleR, um intérprete RevoScaleR será carregado. **BxlServer** e **SQL Satellite** gerenciam a comunicação e a transferência de dados com SQL Server.

<a name="launchpad"></a>

## <a name="launchpad"></a>Launchpad

O [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] é um serviço que gerencia e executa scripts externos, semelhante ao modo como o serviço de indexação e consulta de texto completo inicia um host separado para o processamento de consultas de texto completo. O serviço Launchpad pode iniciar somente inicializadores confiáveis que são publicados pela Microsoft ou que foram certificados pela Microsoft como requisitos de reunião para o gerenciamento de recursos e desempenho.

| Inicializadores confiáveis | Extensão | Versões do SQL Server |
|-------------------|-----------|---------------------|
| RLauncher. dll para a linguagem R | [Extensão de R](extension-r.md) | SQL Server 2016 e posterior |
| Pythonlauncher. dll para Python 3,5 | [Extensão do Python](extension-python.md) | SQL Server 2017 e posterior |

O serviço [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] é executado em sua própria conta de usuário. Se você alterar a conta que executa o Launchpad, certifique-se de fazer isso usando SQL Server Configuration Manager, para garantir que as alterações sejam gravadas em arquivos relacionados.

Um serviço [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] separado é criado para cada instância do mecanismo de banco de dados à qual você adicionou SQL Server serviços de Machine Learning. Há um serviço Launchpad para cada instância do mecanismo de banco de dados, portanto, se você tiver várias instâncias com suporte a scripts externos, terá um serviço Launchpad para cada um. Uma instância do mecanismo de banco de dados está associada ao serviço Launchpad criado para ele. Todas as invocações de script externo em um procedimento armazenado ou T-SQL resultam no serviço de SQL Server chamando o serviço Launchpad criado para a mesma instância.

Para executar tarefas em um idioma com suporte específico, o Launchpad Obtém uma conta de trabalho protegida do pool e inicia um processo de satélite para gerenciar o tempo de execução externo. Cada processo de satélite herda a conta de usuário do Launchpad e usa essa conta de trabalho pela duração da execução do script. Se o script usar processos paralelos, eles serão criados na mesma conta de trabalho único.

## <a name="bxlserver-and-sql-satellite"></a>Satélite BxlServer e SQL

**BxlServer** é um executável fornecido pela Microsoft que gerencia a comunicação entre SQL Server e Python ou R. Ele cria os objetos de trabalho do Windows que são usados para conter sessões de script externo, provisiona pastas de trabalho seguras para cada trabalho de script externo e usa o satélite do SQL para gerenciar a transferência de dados entre o tempo de execução externo e SQL Server. Se você executar o [Gerenciador de processos](https://technet.microsoft.com/sysinternals/processexplorer.aspx) enquanto um trabalho estiver em execução, você poderá ver uma ou várias instâncias do BxlServer.

Na verdade, o BxlServer é um complemento para um ambiente de tempo de execução de linguagem que funciona com SQL Server para transferir dados e gerenciar tarefas. BXL significa linguagem de troca binária e refere-se ao formato de dados usado para mover dados com eficiência entre SQL Server e processos externos. O BxlServer também é uma parte importante dos produtos relacionados, como Microsoft R Client e Microsoft R Server.

O **satélite do SQL** é uma API de extensibilidade, incluída no mecanismo de banco de dados, que dá suporte a código externo ou C++a tempos de execução externos implementados usando C ou.

O BxlServer usa o Satélite SQL para estas tarefas:

+ Ler dados de entrada
+ Gravar dados de saída
+ Obter argumentos de entrada
+ Gravar argumentos de saída
+ Manipulação de erros
+ Gravar STDOUT e STDERR de volta para o cliente

O satélite do SQL usa um formato de dados personalizado que é otimizado para transferência rápida de dados entre SQL Server e as linguagens de script externo. Ele executa conversões de tipo e define os esquemas dos conjuntos de dados de entrada e saída durante as comunicações entre SQL Server e o tempo de execução de script externo.

O satélite do SQL pode ser monitorado usando xEvents (eventos estendidos do Windows). Para obter mais informações, consulte [eventos estendidos para R](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md) e [eventos estendidos para Python](../../advanced-analytics/python/extended-events-for-python.md).

## <a name="communication-channels-between-components"></a>Canais de comunicação entre componentes

Os protocolos de comunicação entre componentes e plataformas de dados são descritos nesta seção.

+ **TCP/IP**

  Por padrão, as comunicações internas entre SQL Server e o satélite SQL usam TCP/IP.

+ **Pipes nomeados**

  O transporte de dados interno entre o BxlServer e o SQL Server por meio do satélite SQL usa um formato de dados proprietário e compactado para melhorar o desempenho. Os dados são trocados entre tempos de execução de idioma e BxlServer no formato BXL, usando pipes nomeados.

+ **ODBC**

  As comunicações entre clientes de ciência de dados externos e uma instância de SQL Server remota usam ODBC. A conta que envia os trabalhos de script para SQL Server deve ter ambas as permissões para se conectar à instância e executar scripts externos.

  Além disso, dependendo da tarefa, a conta pode precisar dessas permissões:

  + Ler dados usados pelo trabalho
  + Gravar dados em tabelas: por exemplo, ao salvar resultados em uma tabela
  + Criar objetos de banco de dados: por exemplo, se salvar o script externo como parte de um novo procedimento armazenado.

  Quando SQL Server é usado como o contexto de computação para o script executado de um cliente remoto e o executável deve recuperar dados de uma fonte externa, o ODBC é usado para Write-back. SQL Server mapeia a identidade do usuário que está emitindo o comando remoto para a identidade do usuário na instância atual e executa o comando ODBC usando as credenciais desse usuário. A cadeia de conexão necessária para executar essa chamada ODBC é obtida do código cliente.

+ **RODBC (somente R)** 

  Chamadas ODBC adicionais podem ser feitas dentro do script usando **RODBC**. RODBC é um pacote de R popular usado para acessar dados em bancos de dados relacionais; no entanto, seu desempenho geralmente é mais lento do que os provedores comparáveis usados pelo SQL Server. Muitos scripts R usam chamadas inseridas para RODBC como uma maneira de recuperar os conjuntos de dados "secundários" para uso em análises. Por exemplo, o procedimento armazenado que treina um modelo pode definir uma consulta SQL para obter os dados para treinar um modelo, mas usar uma chamada RODBC inserida para obter os fatores adicionais, para realizar pesquisas ou para obter novos dados de fontes externas, tais como arquivos de texto ou Excel.

  O código a seguir ilustra uma chamada RODBC inserida em um script R:

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **Outros protocolos**

  Os processos que podem precisar trabalhar em "partes" ou transferir dados de volta para um cliente remoto também podem usar o [formato de arquivo Xdf](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf). A transferência de dados real é por meio de BLOBs codificados.

## <a name="see-also"></a>Consulte também

+ [Extensão do R no SQL Server](extension-r.md)
+ [Extensão do Python no SQL Server](extension-python.md)