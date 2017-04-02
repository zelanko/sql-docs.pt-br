---
title: "Novos componentes do SQL Server para oferecer suporte a servi&#231;os de R | Microsoft Docs"
ms.custom: ""
ms.date: "06/03/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 54e9ef3f-1136-471e-865a-7cf013673186
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 9
---
# Novos componentes do SQL Server para oferecer suporte a servi&#231;os de R

[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] inclui novos componentes, fornecidos pelo [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mecanismo de banco de dados, que oferecem suporte a extensibilidade da linguagem R. Segurança para esses componentes é gerenciada pelo [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e serão discutidas em detalhes mais tarde.

## Provedores e novos componentes do SQL Server

Além do shell que carrega R e executa o código R conforme descrito na visão geral da arquitetura, [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] inclui os seguintes componentes adicionais.

### **Barra inicial** 
  O [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] é um novo serviço fornecido pelo [!INCLUDE[ssCurrent_md](../../includes/sscurrent-md.md)] para oferecer suporte a execução de scripts externos, semelhantes à forma com que o serviço de indexação e consulta de texto completo inicia um host separado para o processamento de consultas de texto completo. 
  
  O serviço Launchpad será iniciado somente confiáveis iniciadores que são publicados pela Microsoft, ou que tenham sido certificados pela Microsoft como atendem às necessidades de desempenho e gerenciamento de recursos. Em [!INCLUDE[ssCurrent_md](../../includes/sscurrent-md.md)], R atualmente é a linguagem apenas externa com suporte a [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)].
  
  O [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] serviço é executado em sua própria conta de usuário. Cada processo de satélite para um runtime de linguagem específica herdará a conta de usuário da barra inicial. Para obter mais informações sobre a configuração e o contexto de segurança da barra inicial, consulte [Visão geral de segurança](../../advanced-analytics/r-services/security-overview-sql-server-r-services.md).

### **BxlServer e satélite SQL**
  BxlServer é um executável fornecido pela Microsoft que gerencia a comunicação entre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e o tempo de execução de R e também implementa funções ScaleR. Ele cria os objetos de trabalho do Windows que são usados para conter as sessões de R, pastas de trabalho segura provisões para cada trabalho de R e usa SQL satélite para gerenciar a transferência de dados entre R e [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].  

  Na verdade, BxlServer é um complemento para R funciona com [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] para oferecer suporte à integração de R com o SQL Server. BXL representa o idioma do Exchange binário e refere-se para o formato de dados usado para mover dados com eficiência entre o SQL Server e processos externos, como R. 

 O satélite de SQL é uma nova API de extensibilidade no SQL Server 2016 fornecida pelo mecanismo de banco de dados para dar suporte a código externo ou externo runtimes implementado usando C ou C++. Atualmente, R é o tempo de execução único com suporte. BxlServer usa SQL satélite para comunicação com [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
 
  O satélite SQL usa um formato de dados personalizado que é otimizado para a transferência de dados rápidos entre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e linguagens de script externo. Ele executa conversões de tipo e define os esquemas de conjuntos de dados de entrada e saídos durante as comunicações entre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e r.

  BxlServer usa SQL satélite para estas tarefas: 
  - Lendo dados de entrada
  - Gravação de dados de saída
  - Obtendo argumentos de entrada
  - Argumentos de saída de escrita
  - Manipulação de erros
  - Gravar STDOUT e STDERR de volta ao cliente

  O satélite SQL pode ser monitorado usando eventos estendidos. Para obter mais informações, consulte [eventos estendidos do SQL Server R Services](../../advanced-analytics/r-services/extended-events-for-sql-server-r-services.md).


## Canais de comunicação entre componentes

+ **TCP/IP** por padrão, as comunicações internas entre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e o satélite SQL usar TCP/IP.

+ **Pipes nomeados**

  Transporte de dados interna entre o BxlServer e [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] por meio de satélite SQL usa um formato de dados proprietários, compactado para melhorar o desempenho. Dados de memória de R para BxlServer são trocados pipes nomeados no formato BXL. 
  
+ **ODBC** as comunicações entre clientes de ciência de dados externa e a [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instância usar o ODBC. A conta que envia o R trabalhos ao [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] deve ter as permissões para se conectar à instância e executar scripts externos. Além disso, a conta deve ter permissão para acessar quaisquer dados usados pelo trabalho de gravar dados (por exemplo, se salvar os resultados em uma tabela) ou para criar objetos de banco de dados (por exemplo, se salvar funções R como parte de um novo procedimento armazenado).

  Quando [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] é usado como o contexto de computação para um trabalho de R são enviadas de um cliente remoto e o comando R deve recuperar dados de uma fonte externa, o ODBC é usado para write-back. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] irá mapear a identidade do usuário que emite o comando R remoto para a identidade do usuário na instância atual e execute o comando ODBC usando as credenciais do usuário. A cadeia de conexão necessária para executar essa chamada ODBC é obtida do código do cliente.
  
  Chamadas ODBC adicionais podem ser feitas dentro do script usando **RODBC**. RODBC é um pacote R popular usado para acessar dados em bancos de dados relacionais; No entanto, o desempenho é geralmente mais lento do que comparável provedores usados por [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Muitos scripts R usam chamadas incorporadas para RODBC como uma maneira de recuperar os conjuntos de dados "secundários" para uso em análises. Por exemplo, o procedimento armazenado que treina um modelo pode definir uma consulta SQL para obter os dados para um modelo de treinamento, mas usar uma chamada RODBC incorporada para obter os fatores adicionais, para realizar pesquisas, ou para obter novos dados de fontes externas, como arquivos de texto ou Excel.

  O código a seguir ilustra uma chamada RODBC inserida em um script R:
   ~~~~
  library(RODBC);
  connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
  dbhandle <- odbcDriverConnect(connStr)
  OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
  ~~~~

+ **Outros protocolos** processos que precisam trabalhar em "partes" ou transferir dados para um cliente remoto também podem usar o. Formato XDF com suporte pelo Microsoft r real transferência de dados é via blobs codificados.

## Interação dos componentes

Arquitetura do componente que acabei de descrever foi fornecida para garantir que o código-fonte aberto R pode trabalhar "como está", enquanto fornece muito melhor desempenho para o código que é executado em um [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] computador. O mecanismo de como os componentes interagem com o runtime de R e o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] difere do mecanismo de banco de dados um pouco, dependendo de como o código R for iniciado. Os cenários principais são resumidos nesta seção. 
 
### Scripts de R executados a partir do SQL Server (no banco de dados)

Código de R que é executado a partir de "interna" [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] é executada chamando um procedimento armazenado. Portanto, qualquer aplicativo que possa chama um procedimento armazenado pode iniciar a execução de código R.  Depois disso [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] gerencia a execução de código R, como resumido no diagrama a seguir.

![rsql_indb780-01](../../advanced-analytics/r-services/media/rsql-indb780-01.png)

1. Uma solicitação para o tempo de execução de R é indicada pelo parâmetro _@language = 'R'_ passado para o procedimento armazenado, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] envia a solicitação para o serviço Launchpad.
2. O serviço Launchpad inicia o iniciador apropriado; Neste caso, RLauncher.
3. RLauncher inicia o processo de R externo.
4. Coordenadas BxlServer com o tempo de execução de R para gerenciar a troca de dados com [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e o armazenamento de resultados de trabalho.
5. Durante todo esse processo, SQL satélite gerencia comunicações sobre tarefas relacionadas e processos com [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
6. BxlServer usa SQL satélite para comunicar o status e os resultados para [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
7. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] obtém resultados e fecha a processos e tarefas relacionadas. 


### Scripts de R executados a partir de um cliente remoto

Ao conectar-se de um cliente de ciência de dados remotos que dá suporte a Microsoft R, você pode executar funções de R no contexto de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] usando as funções ScaleR. Esse é um fluxo de trabalho diferente da anterior e é resumido no diagrama a seguir.


![rsql_fromR2db-01](../../advanced-analytics/r-services/media/rsql-fromr2db-01.png)

1. Para funções de ScaleR, o tempo de execução de R chama uma função de vinculação que por sua vez chama BxlServer. 
2. BxlServer é fornecido com o Microsoft R e é executado em um processo separado do tempo de execução do R.
3. BxlServer determina o destino da conexão e inicia uma conexão usando o ODBC, passando as credenciais fornecidas como parte da cadeia de conexão no objeto de fonte de dados de R.
4. BxlServer abre uma conexão com o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instância.
5. Para uma chamada de R, a barra inicial serviço é chamado, que é a vez inicia o iniciador apropriado, RLauncher. Depois disso, o processamento do código R é semelhante ao processo para executar o código R em T-SQL.
6. RLauncher faz uma chamada para a instância de tempo de execução R instalado no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] computador. 
7. Resultados são retornados ao BxlServer.
8. SQL satélite gerencia a comunicação com [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e limpeza de objetos de trabalho relacionados.
9. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] passa os resultados para o cliente.

## Consulte também
[Visão geral sobre arquitetura](../../advanced-analytics/r-services/architecture-overview-sql-server-r-services.md)
