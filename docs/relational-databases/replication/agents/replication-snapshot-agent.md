---
title: "Replication Snapshot Agent | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Agente de Instantâneo, executáveis"
  - "agentes [replicação do SQL Server], Agente de Instantâneo"
  - "prompt de comando [replicação do SQL Server]"
  - "Agente de Instantâneo, referência de parâmetro"
ms.assetid: 2028ba45-4436-47ed-bf79-7c957766ea04
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# Replication Snapshot Agent
  O Replication Snapshot Agent é um arquivo executável que prepara arquivos de instantâneo contendo esquema e dados de tabelas publicadas e objetos do banco de dados, armazena os arquivos na pasta de instantâneo e registra trabalhos de sincronização no banco de dados de distribuição.  
  
> [!NOTE]  
>  Os parâmetros podem ser especificados em qualquer ordem.  
  
## Sintaxe  
  
```  
  
snapshot [ -?]   
-Publisher server_name[\instance_name]   
-Publication publication_name   
[-70Subscribers]   
[-BcpBatchSize bcp_batch_size]  
[-DefinitionFile def_path_and_file_name]  
[-Distributor server_name[\instance_name]]  
[-DistributorDeadlockPriority [-1|0|1] ]  
[-DistributorLogin distributor_login]  
[-DistributorPassword distributor_password]  
[-DistributorSecurityMode [0|1] ]  
[-DynamicFilterHostName dynamic_filter_host_name]  
[-DynamicFilterLogin dynamic_filter_login]  
[-DynamicSnapshotLocation dynamic_snapshot_location]   
[-EncryptionLevel [0|1|2]]  
[-FieldDelimiter field_delimiter]  
[-HistoryVerboseLevel [0|1|2|3] ]  
[-HRBcpBlocks number_of_blocks ]  
[-HRBcpBlockSize block_size ]  
[-HRBcpDynamicBlocks ]  
[-KeepAliveMessageInterval keep_alive_interval]  
[-LoginTimeOut login_time_out_seconds]  
[-MaxBcpThreads number_of_threads ]  
[-MaxNetworkOptimization [0|1]]  
[-Output output_path_and_file_name]  
[-OutputVerboseLevel [0|1|2] ]  
[-PacketSize packet_size]  
[-ProfileName profile_name]  
[-PublisherDB publisher_database]  
[-PublisherDeadlockPriority [-1|0|1] ]  
[-PublisherFailoverPartner server_name[\instance_name] ]  
[-PublisherLogin publisher_login]  
[-PublisherPassword publisher_password]   
[-PublisherSecurityMode [0|1] ]  
[-QueryTimeOut query_time_out_seconds]  
[-ReplicationType [1|2] ]  
[-RowDelimiter row_delimiter]  
[-StartQueueTimeout start_queue_timeout_seconds]  
[-UsePerArticleContentsView use_per_article_contents_view]  
```  
  
## Argumentos  
 **-?**  
 Imprime todos os parâmetros disponíveis.  
  
 **-Publicador**  *nome_do_servidor*[**\\***instance_name*]    
 É o nome do Publicador. Especifica server_name para a instância padrão do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nesse servidor. Especifique *nome_do_servidor***\\***nome_da_instância* para uma instância nomeada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nesse servidor.  
  
 **-Publicação** *publicação*  
 É o nome da publicação. Esse parâmetro só é válido se a publicação estiver definida para ter sempre um instantâneo disponível para assinaturas novas ou reiniciadas.  
  
 **-70Subscribers**  
 Deve ser usado se nenhum assinante estiver executando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] versão 7.0.  
  
 **-BcpBatchSize** *bcp*_ *lote*\_ *tamanho*  
 É o número de linhas a ser enviado em uma operação de cópia em massa. Ao executar uma operação **bcp in** , o tamanho do lote é o número de linhas a ser enviado ao servidor como uma transação, e também o número de linhas que deve ser enviado antes que o Agente de Distribuição registre uma mensagem de progresso **bcp** . Ao executar uma operação **bcp out** , um tamanho fixo de lote de 1000 é usado. Um valor de 0 indica que não houve registro de mensagem.  
  
 **-DefinitionFile** *def_path_and_file_name*  
 É o caminho do arquivo de definição de agente. Um arquivo de definição de agente contém argumentos de linha de comando para o agente. O conteúdo do arquivo é analisado como um arquivo executável. Use aspas duplas (") para especificar valores de argumentos que contêm caracteres arbitrários.  
  
 **-Distribuidor** *nome_do_servidor*[**\\***instance_name*]  
 É o nome do Distribuidor. Especifique *nome_do_servidor* para a instância padrão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nesse servidor. Especifique *nome_do_servidor***\\***nome_da_instância* para uma instância nomeada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nesse servidor.  
  
 **-DistributorDeadlockPriority** [**-1**|**0**|**1**]  
 É a prioridade da conexão do Snapshot Agent com o Distribuidor quando um deadlock ocorre. Esse parâmetro é especificado para resolver deadlocks que possam ocorrer entre o Snapshot Agent e aplicativos de usuário durante a geração de instantâneo.  
  
|Valor DistributorDeadlockPriority|Descrição|  
|---------------------------------------|-----------------|  
|**-1**|Aplicativos diferentes do Snapshot Agent têm prioridade quando ocorre um deadlock no Distribuidor.|  
|**0** (padrão)|A prioridade não é atribuída.|  
|**1**|O Snapshot Agent tem prioridade quando um deadlock ocorre no Distribuidor.|  
  
 **Parâmetros - DistributorLogin** *distributor_login*  
 É o logon usado ao se conectar ao Distribuidor usando a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **-DistributorPassword** *distributor_password*  
 É a senha usada ao se conectar ao Distribuidor usando a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. .  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 Especifica o modo de segurança do Distribuidor. Um valor de **0** indica [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] modo de autenticação (padrão) e um valor de **1** indica o modo de autenticação do Windows.  
  
 **-DynamicFilterHostName** *dynamic_filter_host_name*  
 É usado para definir um valor para [HOST_NAME & #40. O Transact-SQL e 41;](../../../t-sql/functions/host-name-transact-sql.md) na filtragem quando um instantâneo dinâmico é criado. Por exemplo, se a cláusula de filtro de subconjunto `rep_id = HOST_NAME()` é especificado para um artigo, e você definir o **DynamicFilterHostName** propriedade como "FBJones" antes de chamar o Merge Agent, somente linhas com "FBJones" **rep_id** coluna será replicada.  
  
 **-DynamicFilterLogin** *valores de dynamic_filter_login*  
 É usado para definir um valor para [SUSER_SNAME & #40. O Transact-SQL e 41;](../../../t-sql/functions/suser-sname-transact-sql.md)na filtragem quando um instantâneo dinâmico é criado. Por exemplo, se a cláusula de filtro de subconjunto `user_id = SUSER_SNAME()` é especificado para um artigo, e definir o **DynamicFilterLogin** propriedade como "rsmith" antes de chamar o **executar** método do **SQLSnapshot** do objeto, somente as linhas com "rsmith" **user_id** coluna será incluída no instantâneo.  
  
 **-DynamicSnapshotLocation** *dynamic_snapshot_location*  
 É o local onde o instantâneo dinâmico deve ser gerado.  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 É o nível da criptografia SSL (Secure Sockets Layer) usada pelo Snapshot Agent ao fazer conexões.  
  
|Valor EncryptionLevel|Descrição|  
|---------------------------|-----------------|  
|**0**|Especifica que o SSL não é usado.|  
|**1**|Especifica que o SSL é usado, mas que +o agente não verifica se o certificado de servidor SSL é assinado por um emissor confiável.|  
|**2**|Especifica que o SSL é usado, e que o certificado é verificado.|  
  
 Para obter mais informações, consulte [Visão geral de segurança e 40; Replicação e 41;](../../../relational-databases/replication/security/security-overview-replication.md).  
  
 **-FieldDelimiter** *field_delimiter*  
 É o caractere ou cadeia de caracteres que marca o fim de um campo no arquivo de dados de cópia em massa no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O padrão é \n\<x$3>\n.  
  
 **-HistoryVerboseLevel** [ **1**| **2**| **3**]  
 Especifica a quantidade de histórico registrada durante uma operação de instantâneo. Você pode minimizar o efeito de registro de histórico no desempenho selecionando **1**.  
  
|Valor HistoryVerboseLevel|Descrição|  
|-------------------------------|-----------------|  
|**0**|Mensagens de Progresso são gravadas no console ou em um arquivo de saída. Registros de histórico não são registrados no banco de dados de distribuição.|  
|**1**|Sempre atualiza uma mensagem de histórico anterior do mesmo status (inicialização, andamento, êxito, etc.). Se nenhum registro anterior com o mesmo status existir, insira um registro novo.|  
|**2** (padrão)|Insira novos registros de histórico, a menos que o registro seja para coisas como mensagens ociosas ou mensagens de trabalho de execução longa; em tal caso, atualize os registros anteriores.|  
|**3**|Sempre insira novos registros, a menos que seja para mensagens ociosas.|  
  
 **-HRBcpBlocks** *number_of_blocks*  
 É o número de **bcp** blocos de dados que são colocadas em fila entre os threads de leitor e gravador. O valor padrão é 50. **HRBcpBlocks** só é usado com publicações Oracle.  
  
> [!NOTE]  
>  Esse parâmetro é usado para ajuste de desempenho de **bcp** desempenho de um editor Oracle.  
  
 -**HRBcpBlockSize***block_size*  
 É o tamanho, em quilobytes (KB) de cada **bcp** Bloco de dados. O valor padrão é 64 KB. **HRBcpBlocks** só é usado com publicações Oracle.  
  
> [!NOTE]  
>  Esse parâmetro é usado para ajuste de desempenho de **bcp** desempenho de um editor Oracle.  
  
 **-HRBcpDynamicBlocks**  
 É ou não o tamanho de cada **bcp** Bloco de dados pode crescer dinamicamente. **HRBcpBlocks** só é usado com publicações Oracle.  
  
> [!NOTE]  
>  Esse parâmetro é usado para ajuste de desempenho de **bcp** desempenho de um editor Oracle.  
  
 **-KeepAliveMessageInterval** *keep_alive_interval*  
 É o período de tempo, em segundos, que o Snapshot Agent aguarda antes de fazer logon "Aguardando até que a mensagem de back-end" para o [MSsnapshot_history](../../../relational-databases/system-tables/mssnapshot-history-transact-sql.md) tabela. O valor padrão é 300 segundos.  
  
 **-LoginTimeOut** *login_time_out_seconds*  
 É o número de segundos antes que o logon expire. O padrão é **15** segundos.  
  
 **-MaxBcpThreads** *number_of_threads*  
 Especifica o número de operações de cópia em massa que podem ser executadas em paralelo. O número máximo de threads e conexões ODBC que existe simultaneamente no menor dos **MaxBcpThreads** ou o número de solicitações de cópia em massa que aparece na transação sincronizada no banco de dados de distribuição. **MaxBcpThreads** deve ter um valor maior que **0** e sem limite superior embutido em código. O padrão é **1**.  
  
 \- **MaxNetworkOptimization** [ **0**| **1**]  
 Se exclusões irrelevantes forem enviadas ao Assinante. Exclusões irrelevantes são comandos DELETE enviados aos Assinantes por linhas que não pertencem à partição do Assinante. Exclusões irrelevantes não afetam a integridade ou convergência dos dados, mas podem resultar em tráfego de rede desnecessário. O valor padrão de **MaxNetworkOptimization** é **0**. Definindo **MaxNetworkOptimization** como **1** minimiza as chances de exclusões irrelevantes, reduzindo o tráfego de rede e maximizando a otimização da rede. A definição desse parâmetro como **1** também aumenta o armazenamento de metadados e causa degradação de desempenho no Publicador se vários níveis de filtro de junção e filtros de subconjuntos complexos estiverem presentes. Você deve avaliar com cuidado a topologia da replicação e definir **MaxNetworkOptimization** como **1** somente se o tráfego de rede de exclusões irrelevantes estiver inaceitavelmente alto.  
  
> [!NOTE]  
>  Definir esse parâmetro para **1** é útil somente quando a opção de otimização de sincronização da publicação de mesclagem é definida como **true** (o **@keep_partition_changes** parâmetro [sp_addmergepublication & 40; Transact-SQL & 41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)).  
  
 **-Saída** *output_path_and_file_name*  
 É o caminho do arquivo de saída do agente. Se o nome de arquivo não for fornecido, a saída será enviada ao console. Se o nome do arquivo especificado existir, a saída será anexada ao arquivo.  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2**]  
 Especifica se a saída deve ser detalhada.  
  
|Valor OutputVerboseLevel|Descrição|  
|------------------------------|-----------------|  
|**0**|Somente mensagens de erro são impressas.|  
|**1** (padrão)|Todas as mensagens de relatório de progresso são impressas (padrão).|  
|**2**|Todas as mensagens de erro e mensagens de relatório de progresso são impressas, o que é útil na depuração.|  
  
 **Tamanho do pacote -** *packet_size*  
 É o tamanho de pacote (em bytes) usado pelo Snapshot Agent na conexão com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O valor padrão é 8192 bytes.  
  
> [!NOTE]  
>  Não altere o tamanho do pacote a menos que você tenha certeza que melhorará o desempenho. Para a maioria dos aplicativos, o tamanho do pacote padrão é o melhor.  
  
 **-ProfileName** *profile_name*  
 Especifica um perfil de agente a ser usado para parâmetros de agente. Se **ProfileName** for NULL, o perfil de agente será desabilitado. Se **ProfileName** não for especificado, o perfil padrão de tipo de agente será usado. Para obter informações, consulte [perfis do Replication Agent](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 **-PublisherDB** *publisher_database*  
 É o nome do banco de dados de publicação. *Esse parâmetro não tem suporte para Editores Oracle*.  
  
 **-PublisherDeadlockPriority** [**-1**|**0**|**1**]  
 É a prioridade da conexão do Snapshot Agent com o Publicador quando um deadlock ocorre. Esse parâmetro é especificado para resolver deadlocks que possam ocorrer entre o Snapshot Agent e aplicativos de usuário durante a geração de instantâneo.  
  
|Valor PublisherDeadlockPriority|Descrição|  
|-------------------------------------|-----------------|  
|**-1**|Aplicativos diferentes do Snapshot Agent têm prioridade quando ocorre um deadlock no Publicador.|  
|**0** (padrão)|A prioridade não é atribuída.|  
|**1**|O Snapshot Agent tem prioridade quando um deadlock ocorre no Publicador.|  
  
 **-PublisherFailoverPartner** *nome_do_servidor*[**\\***instance_name*]  
 Especifica a instância de parceiro de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que participa de uma sessão de espelhamento de banco de dados com o banco de dados de publicação. Para obter mais informações, consulte [espelhamento de banco de dados, replicação e 40; SQL Server & 41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md).  
  
 **-PublisherLogin** *publisher_login*  
 É o logon usado ao se conectar ao Publicador usando a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **-PublisherPassword**  *publisher_password*  
 É a senha usada ao se conectar ao Publicador usando a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. .  
  
 **-PublisherSecurityMode** [ **0**| **1**]  
 Especifica o modo de segurança do Publicador. Um valor de **0** indica [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] autenticação (padrão) e um valor de **1** indica o modo de autenticação do Windows.  
  
 **-QueryTimeOut** *query_time_out_seconds*  
 É o número de segundos antes que a consulta expire. O padrão é 1800 segundos.  
  
 **-ReplicationType** [ **1**| **2**]  
 Especifica o tipo de replicação. Um valor de **1** indica replicação transacional e um valor de **2** indica replicação de mesclagem.  
  
 **-RowDelimiter** *row_delimiter*  
 É o caractere ou cadeia de caracteres que marca o fim de uma linha no arquivo de dados de cópia em massa no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O padrão é \n\<,@g>\n.  
  
 **-StartQueueTimeout** *start_queue_timeout_seconds*  
 É o número máximo de segundos que o Snapshot Agent aguarda quando o número de processos de instantâneo dinâmico simultâneos em execução está no limite definido **@max_concurrent_dynamic_snapshots** propriedade [sp_addmergepublication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Se o número máximo de segundos for alcançado e o Snapshot Agent ainda estiver esperando, será fechado. Um valor de 0 significa que o agente espera indefinidamente, embora possa ser cancelado.  
  
 \- **UsePerArticleContentsView** *use_per_article_contents_view*  
 Esse parâmetro foi preterido e só tem suporte para compatibilidade com versões anteriores.  
  
## Comentários  
  
> [!IMPORTANT]  
>  Se você instalou o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent para ser executado com uma conta Sistema Local em vez de uma conta de Usuário de Domínio (o padrão), o serviço só poderá acessar o computador local. Se o Snapshot Agent executado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent for configurado para usar o Modo de Autenticação do Windows ao fazer logon no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o Snapshot Agent falhará. A configuração padrão é Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Para iniciar o Snapshot Agent, execute **snapshot.exe** no prompt do comando. Para obter informações, consulte [Executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## Consulte também  
 [Administração do agente de replicação](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  