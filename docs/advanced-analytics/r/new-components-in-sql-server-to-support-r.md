---
title: Componentes do SQL Server para dar suporte a R | Microsoft Docs
ms.custom: 
ms.date: 04/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 54e9ef3f-1136-471e-865a-7cf013673186
caps.latest.revision: "9"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f3a6387f16e567c09c233cfd2c4de71d567f2ce7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="components-in-sql-server-to-support-r"></a>Componentes do SQL Server para dar suporte a R

No SQL Server 2016 e de 2017, o mecanismo de banco de dados inclui os componentes opcionais que oferecem suporte à extensibilidade para idiomas de script externo, incluindo o R e Python. Foi adicionado suporte para a linguagem R no SQL Server 2016; Python foi adicionado suporte para nos serviços de aprendizado de máquina do SQL Server de 2017.

Este tópico descreve os novos componentes que funcionam especificamente com a linguagem R. Para obter uma discussão de como esses componentes funcionam com software livre R, consulte [interoperabilidade de R](r-interoperability-in-sql-server.md)

## <a name="components-and-providers"></a>Componentes e provedores

Além do shell que carrega o R e executa código R conforme descrito na visão geral da arquitetura, o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] inclui os componentes adicionais a seguir.

### <a name="launchpad"></a>Launchpad 

O [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] é um serviço fornecido por [!INCLUDE[ssCurrent_md](../../includes/sscurrent-md.md)] para dar suporte a execução de scripts externos, semelhantes ao modo que o serviço de indexação e consulta de texto completo inicia um host separado para processar consultas de texto completo.

O serviço Launchpad iniciará somente inicializadores confiáveis que sejam publicados pela Microsoft ou que tenham sido certificados pela Microsoft como atendendo aos requisitos de desempenho e gerenciamento de recursos. A nomeação para os iniciadores de idioma específico é simples:

  + R - RLauncher.dll
  + Python - PythonLauncher.dll

O serviço [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] é executado em sua própria conta de usuário. Cada processo satélite para um tempo de execução de linguagem específica herdará a conta de usuário do Launchpad. Para obter mais informações sobre a configuração e o contexto de segurança da barra inicial, consulte [visão geral de segurança](../../advanced-analytics/r/security-overview-sql-server-r.md).

### <a name="bxlserver-and-sql-satellite"></a>BxlServer e satélite SQL

BxlServer é um executável fornecido pela Microsoft que gerencia a comunicação entre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e o tempo de execução de R e também implementa funções RevoScaleR. Ele cria os objetos de trabalho do Windows que são usados para conter as sessões do R, provisiona pastas de trabalho seguras para cada trabalho do R e usa o Satélite SQL para gerenciar a transferência de dados entre o R e o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

Na verdade, o BxlServer é um complemento para o R que funciona com o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] para dar suporte à integração do R com o SQL Server. BXL significa linguagem Exchange binário e refere-se para o formato de dados usado para mover dados com eficiência entre o SQL Server e processos externos, como R. BxlServer.dll também é instalado quando você instala o cliente do Microsoft R ou Microsoft R Server.

O Satélite SQL é uma nova API de extensibilidade no SQL Server 2016 que é fornecida pelo mecanismo de banco de dados para dar suporte a código externo ou tempos de execução externos implementados usando C ou C++. O BxlServer usa o Satélite SQL para comunicação com o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

O Satélite SQL usa um formato de dados personalizado que é otimizado para a transferência de dados rápida entre o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e linguagens de script externo. Ele executa conversões de tipo e define os esquemas dos conjuntos de dados de entrada e de saída durante as comunicações entre o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e o R.

O BxlServer usa o Satélite SQL para estas tarefas:

  + Ler dados de entrada
  + Gravar dados de saída
  + Obter argumentos de entrada
  + Gravar argumentos de saída
  + Manipulação de erros
  + Gravar saída padrão e erros de volta para o cliente

O Satélite SQL pode ser monitorado usando Eventos Estendidos. Para saber mais, confira [Eventos estendidos para o SQL Server R Services](extended-events-for-sql-server-r-services.md).

## <a name="communication-channels-between-components"></a>Canais de comunicação entre os componentes

+ **TCP/IP**

    Por padrão, as comunicações internas entre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e o satélite de SQL usar TCP/IP.

+ **Pipes nomeados**

    Transferência de dados interna entre o BxlServer e [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] via satélite de SQL usa um formato de dados do proprietário e compactado para melhorar o desempenho. Dados da memória do R para o BxlServer são trocados por pipes nomeados no formato BXL.

+ **ODBC**

    As comunicações entre clientes de ciência de dados externa e a [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instância usar o ODBC. A conta que envia os trabalhos do R ao [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] deve ter permissões tanto para se conectar à instância quanto para executar scripts externos. Além disso, a conta deve ter permissão para acessar quaisquer dados usados pelo trabalho, para gravar dados (por exemplo, ao salvar os resultados em uma tabela) ou para criar objetos de banco de dados (por exemplo, ao salvar funções do R como parte de um novo procedimento armazenado).

    Quando [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] é usado como o contexto de computação para um trabalho de R enviado de um cliente remoto e o comando do R deve recuperar dados de uma fonte externa, o ODBC é usado para write-back. O [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mapeará a identidade do usuário que emite o comando do R remoto para a identidade do usuário na instância atual e, em seguida, executará o comando ODBC usando as credenciais desse usuário. A cadeia de conexão necessária para executar essa chamada ODBC é obtida do código cliente.

    Chamadas ODBC adicionais podem ser feitas dentro do script usando **RODBC**. RODBC é um pacote R popular usado para acessar dados em bancos de dados relacionais; no entanto, o desempenho dele é geralmente mais lento do que provedores comparáveis usados pelo [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Muitos scripts R usam chamadas inseridas para RODBC como uma maneira de recuperar os conjuntos de dados "secundários" para uso em análises. Por exemplo, o procedimento armazenado que treina um modelo pode definir uma consulta SQL para obter os dados para treinar um modelo, mas usar uma chamada RODBC inserida para obter os fatores adicionais, para realizar pesquisas ou para obter novos dados de fontes externas, tais como arquivos de texto ou Excel.

    O código a seguir ilustra uma chamada RODBC inserida em um script R:

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **Outros protocolos**

    Processos que precisam trabalhar em "blocos" ou transferir dados para um cliente remoto também podem usar o. Formato XDF com suporte pelo Microsoft R. real transferência de dados é por meio de blobs codificados.

## <a name="interaction-of-components"></a>Interação de componentes

Arquitetura do componente que acabei de descrever foi fornecida para assegurar que o código R de software livre possa trabalhar "como está", enquanto fornece um desempenho muito melhor para o código que é executado em um computador com o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. O mecanismo de como os componentes interagem com o tempo de execução de R e o mecanismo de banco de dados do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] difere um pouco, dependendo de como o código R é iniciado. Os cenários principais são resumidos nesta seção.

### <a name="r-scripts-executed-from-sql-server-in-database"></a>Scripts de R executados a partir do SQL Server no banco de dados

Código R que é executado de "dentro" do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] é executado chamando um procedimento armazenado. Portanto, qualquer aplicativo que possa fazer uma chamada de procedimento armazenado pode iniciar a execução de código R.  Então, o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] gerencia a execução de código R, conforme resumido no diagrama a seguir.

![rsql_indb780-01](media/script_in-db-r.png)

1. Uma solicitação para o tempo de execução de R é indicada pelo parâmetro _@language='R'_ passado para o procedimento armazenado, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] envia essa solicitação para o serviço Launchpad.
2. O serviço Launchpad inicia o inicializador apropriado; neste caso, RLauncher.
3. O RLauncher inicia o processo de R externo.
4. O BxlServer coordena-se com o tempo de execução do R para gerenciar a troca de dados com [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e o armazenamento de resultados funcionais.
5. Satélite de SQL gerencia comunicações sobre tarefas relacionadas e processa a [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
6. O BxlServer usa Satélite SQL para comunicar o status e os resultados para o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
7. O [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] obtém resultados e fecha os processos e tarefas relacionados.

### <a name="r-scripts-executed-from-a-remote-client"></a>Scripts R executados de um cliente remoto

Ao conectar-se de um cliente de ciência de dados remotos que dá suporte ao Microsoft R, você pode executar funções de R no contexto de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] usando as funções RevoScaleR. Esse é um fluxo de trabalho diferente do anterior e é resumido no diagrama a seguir.

![rsql_fromR2db-01](media/remote-sqlcc-from-r2.png)

1. Para funções de RevoScaleR, o tempo de execução de R chama uma função de vinculação que, por sua vez, chama BxlServer.
2. O BxlServer é fornecido com o Microsoft R e é executado em um processo separado do tempo de execução do R.
3. O BxlServer determina o destino da conexão e inicia uma conexão usando o ODBC, passando as credenciais fornecidas como parte da cadeia de conexão no objeto de fonte de dados do R.
4. O BxlServer abre uma conexão para a instância do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
5. Para uma chamada de R, a barra inicial do serviço é chamado, o que é por sua vez inicia o iniciador apropriado, RLauncher. Depois disso, o processamento do código R é semelhante ao processo para executar o código R de T-SQL.
6. O RLauncher faz uma chamada para a instância de tempo de execução do R instalada no computador do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
7. Os resultados são retornados ao BxlServer.
8. O Satélite SQL gerencia a comunicação com o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e a limpeza dos objetos de trabalho relacionados.
9. O [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] passa os resultados de volta para o cliente.

## <a name="next-steps"></a>Próximas etapas

[Visão geral da arquitetura](architecture-overview-sql-server-r.md)

[Visão geral de segurança](security-overview-sql-server-r.md)

[Considerações sobre segurança](security-considerations-for-the-r-runtime-in-sql-server.md)
