---
title: Agente de instantâneo de replicação | Microsoft Docs
description: No SQL Server, a o Agente de Instantâneo de Replicação prepara arquivos de instantâneo, armazena-os em uma pasta e registra trabalhos de sincronização no banco de dados de distribuição.
ms.custom: ''
ms.date: 10/29/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Snapshot Agent, executables
- agents [SQL Server replication], Snapshot Agent
- command prompt [SQL Server replication]
- Snapshot Agent, parameter reference
ms.assetid: 2028ba45-4436-47ed-bf79-7c957766ea04
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 9fd89016895d2e106e6c9ff9dcab4873824c7515
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364233"
---
# <a name="replication-snapshot-agent"></a>Replication Snapshot Agent
[!INCLUDE[sql-asdb](../../../includes/applies-to-version/sql-asdb.md)]
  O Replication Snapshot Agent é um arquivo executável que prepara arquivos de instantâneo contendo esquema e dados de tabelas publicadas e objetos do banco de dados, armazena os arquivos na pasta de instantâneo e registra trabalhos de sincronização no banco de dados de distribuição.  
  
> [!NOTE]  
>  - Os parâmetros podem ser especificados em qualquer ordem.  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="syntax"></a>Sintaxe  
  
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
[-PrefetchTables [0|1] ]  
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
  
## <a name="arguments"></a>Argumentos  
 **-?**  
 Imprime todos os parâmetros disponíveis.  
  
 **-Publisher**  _server_name_[ **\\** _instance\_name_]  
 É o nome do Publicador. Especifica server_name para a instância padrão do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nesse servidor. Especifica _nome_do\_servidor_ **\\** _nome_da\_instância_ para uma instância nomeada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] naquele servidor.  
  
 **-Publication** _publication_  
 É o nome da publicação. Esse parâmetro só é válido se a publicação estiver definida para ter sempre um instantâneo disponível para assinaturas novas ou reiniciadas.  
  
 **-70Subscribers**  
 Deve ser usado se qualquer Assinante estiver executando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] versão 7.0.  
  
 **-BcpBatchSize** _bcp_\_ *batch*\_ *size*  
 É o número de linhas a ser enviado em uma operação de cópia em massa. Ao executar uma operação **bcp in** , o tamanho do lote é o número de linhas a ser enviado ao servidor como uma transação e também o número de linhas que deve ser enviado antes que o Agente de Distribuição registre uma mensagem de progresso **bcp** . Ao executar uma operação **bcp out** , um tamanho fixo de lote de 1000 é usado. Um valor de 0 indica que não houve registro de mensagem.  
  
 **-DefinitionFile** _def_path_and_file_name_  
 É o caminho do arquivo de definição de agente. Um arquivo de definição de agente contém argumentos de linha de comando para o agente. O conteúdo do arquivo é analisado como um arquivo executável. Use aspas duplas (") para especificar valores de argumentos que contêm caracteres arbitrários.  
  
 **-Distributor** _server_name_[ **\\** _instance\_name_]  
 É o nome do Distribuidor. Especifica *server_name* para a instância padrão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] naquele servidor. Especifica _nome_do\_servidor_ **\\** _nome_da\_instância_ para uma instância nomeada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] naquele servidor.  
  
 **-DistributorDeadlockPriority** [ **-1**|**0**|**1**]  
 É a prioridade da conexão do Snapshot Agent com o Distribuidor quando um deadlock ocorre. Esse parâmetro é especificado para resolver deadlocks que possam ocorrer entre o Snapshot Agent e aplicativos de usuário durante a geração de instantâneo.  
  
|Valor DistributorDeadlockPriority|Descrição|  
|---------------------------------------|-----------------|  
|**-1**|Aplicativos diferentes do Snapshot Agent têm prioridade quando ocorre um deadlock no Distribuidor.|  
|**0** (padrão)|A prioridade não é atribuída.|  
|**1**|O Snapshot Agent tem prioridade quando um deadlock ocorre no Distribuidor.|  
  
 **-DistributorLogin** _distributor_login_  
 É o logon usado ao se conectar ao Distribuidor usando a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 **-DistributorPassword** _distributor_password_  
 É a senha usada ao se conectar ao Distribuidor usando a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . .  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 Especifica o modo de segurança do Distribuidor. Um valor de **0** indica Modo (padrão) de Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e um valor de **1** indica Modo de Autenticação do Windows.  
  
 **-DynamicFilterHostName** _dynamic_filter_host_name_  
 É usado para definir um valor para [HOST_NAME &#40;Transact-SQL&#41;](../../../t-sql/functions/host-name-transact-sql.md) na filtragem quando um instantâneo dinâmico é criado. Por exemplo, se a cláusula de filtro de subconjunto `rep_id = HOST_NAME()` for especificada para um artigo e você definir a propriedade **DynamicFilterHostName** como "FBJones" antes de chamar o Merge Agent, somente linhas com "FBJones" na coluna **rep_id** serão replicadas.  
  
 **-DynamicFilterLogin** _dynamic_filter_login_  
 É usado para definir um valor para [SUSER_SNAME &#40;Transact-SQL&#41;](../../../t-sql/functions/suser-sname-transact-sql.md) na filtragem quando um instantâneo dinâmico é criado. Por exemplo, se a cláusula de filtro de subconjunto `user_id = SUSER_SNAME()` for especificada para um artigo e você definir a propriedade **DynamicFilterLogin** como "rsmith" antes de chamar o método **Run** do objeto **SQLSnapshot** , somente linhas com "rsmith" na coluna **user_id** serão incluídas no instantâneo.  
  
 **-DynamicSnapshotLocation** _dynamic_snapshot_location_  
 É o local onde o instantâneo dinâmico deve ser gerado.  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 É o nível de protocolo TLS, antes conhecido como protocolo SSL, usado pelo Agente de Instantâneo ao fazer conexões.  
  
|Valor EncryptionLevel|Descrição|  
|---------------------------|-----------------|  
|**0**|Especifica que o TLS não é usado.|  
|**1**|Especifica que o TLS é usado, mas que o agente não verifica se o certificado de servidor TSL/SSL é assinado por um emissor confiável.|  
|**2**|Especifica que o TLS é usado e que o certificado é verificado.|  

 > [!NOTE]  
 >  É definido um certificado TLS/SSL válido com um nome de domínio totalmente qualificado do SQL Server. Para que o agente seja conectado com êxito ao definir -EncryptionLevel como 2, crie um alias no SQL Server local. O parâmetro ‘Alias Name’ deve ser o nome do servidor e o parâmetro ‘Server’ deve ser definido como o nome totalmente qualificado do SQL Server.
  
 Confira mais informações em [Exibir e modificar as configurações de replicação de segurança](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 **-FieldDelimiter** _field_delimiter_  
 É o caractere ou cadeia de caracteres que marca o fim de um campo no arquivo de dados de cópia em massa no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . O padrão é \n\<x$3>\n.  
  
 **-HistoryVerboseLevel** [ **1**| **2**| **3**]  
 Especifica a quantidade de histórico registrada durante uma operação de instantâneo. Você pode minimizar o efeito de registro de histórico no desempenho selecionando **1**.  
  
|Valor HistoryVerboseLevel|Descrição|  
|-------------------------------|-----------------|  
|**0**|Mensagens de Progresso são gravadas no console ou em um arquivo de saída. Registros de histórico não são registrados no banco de dados de distribuição.|  
|**1**|Sempre atualiza uma mensagem de histórico anterior do mesmo status (inicialização, andamento, êxito, etc.). Se nenhum registro anterior com o mesmo status existir, insira um registro novo.|  
|**2** (padrão)|Insira novos registros de histórico, a menos que o registro seja para coisas como mensagens ociosas ou mensagens de trabalho de execução longa; em tal caso, atualize os registros anteriores.|  
|**3**|Sempre insira novos registros, a menos que seja para mensagens ociosas.|  
  
 **-HRBcpBlocks** _number_of_blocks_  
 É o número de blocos de dados **bcp** enfileirados entre os threads de leitura e gravação. O valor padrão é 50. **HRBcpBlocks** só é usado com publicações Oracle.  
  
> [!NOTE]  
>  Esse parâmetro é usado para ajuste de desempenho do desempenho de **bcp** de um Publicador Oracle.  
  
 -**HRBcpBlockSize**_block\_size_  
 É o tamanho, em kilobyte (KB), de cada bloco de dados **bcp** . O valor padrão é 64 KB. **HRBcpBlocks** só é usado com publicações Oracle.  
  
> [!NOTE]  
>  Esse parâmetro é usado para ajuste de desempenho do desempenho de **bcp** de um Publicador Oracle.  
  
 **-HRBcpDynamicBlocks**  
 Se o tamanho de cada bloco de dados **bcp** pode ou não crescer dinamicamente. **HRBcpBlocks** só é usado com publicações Oracle.  
  
> [!NOTE]  
>  Esse parâmetro é usado para ajuste de desempenho do desempenho de **bcp** de um Publicador Oracle.  
  
 **-KeepAliveMessageInterval** _keep_alive_interval_  
 É a quantidade de tempo, em segundos, que o Snapshot Agent aguarda antes de registrar "aguardando por mensagem de back-end" na tabela [MSsnapshot_history](../../../relational-databases/system-tables/mssnapshot-history-transact-sql.md) . O valor padrão é 300 segundos.  
  
 **-LoginTimeOut** _login_time_out_seconds_  
 É o número de segundos antes que o logon expire. O padrão é **15** segundos.  
  
 **-MaxBcpThreads** _number_of_threads_  
 Especifica o número de operações de cópia em massa que podem ser executadas em paralelo. O número máximo de threads e conexões ODBC que existe simultaneamente no menor dos **MaxBcpThreads** ou o número de solicitações de cópia em massa que aparece na transação sincronizada no banco de dados de distribuição. **MaxBcpThreads** deve ter um valor maior que **0** e não tem um limite superior embutido em código. O padrão é o dobro do número de processadores.  
 
 > [!NOTE]
 > Se o objeto replicado tiver um filtro, o agente de instantâneo vai gerar apenas um arquivo BCP para esse artigo em vez de gerar vários arquivos BCP. 
  
 \- **MaxNetworkOptimization** [ **0**| **1**]  
 Se exclusões irrelevantes forem enviadas ao Assinante. Exclusões irrelevantes são comandos DELETE enviados aos Assinantes por linhas que não pertencem à partição do Assinante. Exclusões irrelevantes não afetam a integridade ou convergência dos dados, mas podem resultar em tráfego de rede desnecessário. O valor padrão de **MaxNetworkOptimization** é **0**. Definindo **MaxNetworkOptimization** como **1** minimiza as chances de exclusões irrelevantes, reduzindo o tráfego de rede e maximizando a otimização da rede. A definição desse parâmetro como **1** também aumenta o armazenamento de metadados e causa degradação de desempenho no Publicador se vários níveis de filtro de junção e filtros de subconjuntos complexos estiverem presentes. Você deve avaliar com cuidado a topologia da replicação e definir **MaxNetworkOptimization** como **1** somente se o tráfego de rede de exclusões irrelevantes estiver inaceitavelmente alto.  
  
> [!NOTE]
>  A configuração desse parâmetro como **1** só é útil quando a opção de otimização de sincronização da publicação de mesclagem é definida como **true** (o parâmetro `@keep_partition_changes**` de [sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)).  
  
 **-Output** _output_path_and_file_name_  
 É o caminho do arquivo de saída do agente. Se o nome de arquivo não for fornecido, a saída será enviada ao console. Se o nome do arquivo especificado existir, a saída será anexada ao arquivo.  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2**]  
 Especifica se a saída deve ser detalhada.  
  
|Valor OutputVerboseLevel|Descrição|  
|------------------------------|-----------------|  
|**0**|Somente mensagens de erro são impressas.|  
|**1** (padrão)|Todas as mensagens de relatório de progresso são impressas (padrão).|  
|**2**|Todas as mensagens de erro e mensagens de relatório de progresso são impressas, o que é útil na depuração.|  
  
 **-PacketSize** _packet_size_  
 É o tamanho de pacote (em bytes) usado pelo Snapshot Agent na conexão com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O valor padrão é 8192 bytes.  
  
> [!NOTE]  
>  Não altere o tamanho do pacote a menos que você tenha certeza que melhorará o desempenho. Para a maioria dos aplicativos, o tamanho do pacote padrão é o melhor.  

**-PrefetchTables** [ **0**| **1**]  
 Parâmetro opcional que especifica se será feita a pré-busca de objetos de tabela e se eles serão armazenados em cache.  O comportamento padrão é executar a pré-busca de determinadas propriedades de tabela usando o componente SMO com base em um cálculo interno.  Esse parâmetro pode ser útil em cenários em que a operação de pré-busca de SMO leva um tempo consideravelmente maior para ser executada. Se esse parâmetro não for usado, essa decisão será tomada no runtime com base na porcentagem de tabelas adicionadas como artigos na publicação.  
  
|Valor OutputVerboseLevel|Descrição|  
|------------------------------|-----------------|  
|**0**|A chamada ao método Pré-busca do componente de SMO está desativada.|  
|**1**|O Agente de Instantâneo chamará o método Pré-busca para armazenar em cache algumas propriedades de tabela usando SMO|  

 **-ProfileName** _profile_name_  
 Especifica um perfil de agente a ser usado para parâmetros de agente. Se **ProfileName** for NULL, o perfil de agente será desabilitado. Se **ProfileName** não for especificado, o perfil padrão de tipo de agente será usado. Para obter mais informações, consulte [Perfis do agente de replicação](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 **-PublisherDB** _publisher_database_  
 É o nome do banco de dados de publicação. *Esse parâmetro não tem suporte para Editores Oracle*.  
  
 **-PublisherDeadlockPriority** [ **-1**|**0**|**1**]  
 É a prioridade da conexão do Snapshot Agent com o Publicador quando um deadlock ocorre. Esse parâmetro é especificado para resolver deadlocks que possam ocorrer entre o Snapshot Agent e aplicativos de usuário durante a geração de instantâneo.  
  
|Valor PublisherDeadlockPriority|Descrição|  
|-------------------------------------|-----------------|  
|**-1**|Aplicativos diferentes do Snapshot Agent têm prioridade quando ocorre um deadlock no Publicador.|  
|**0** (padrão)|A prioridade não é atribuída.|  
|**1**|O Snapshot Agent tem prioridade quando um deadlock ocorre no Publicador.|  
  
 **-PublisherFailoverPartner** _server_name_[ **\\** _instance\_name_]  
 Especifica a instância de parceiro de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que participa de uma sessão de espelhamento de banco de dados com o banco de dados de publicação. Para obter mais informações, consulte [Espelhamento e replicação de banco de dados &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md).  
  
 **-PublisherLogin** _publisher_login_  
 É o logon usado ao se conectar ao Publicador usando a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 **-PublisherPassword**  _publisher_password_  
 É a senha usada ao se conectar ao Publicador usando a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . .  
  
 **-PublisherSecurityMode** [ **0**| **1**]  
 Especifica o modo de segurança do Publicador. Um valor de **0** indica Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (padrão), e um valor de **1** indica Modo de Autenticação do Windows.  
  
 **-QueryTimeOut** _query_time_out_seconds_  
 É o número de segundos antes que a consulta expire. O padrão é 1800 segundos.  
  
 **-ReplicationType** [ **1**| **2**]  
 Especifica o tipo de replicação. Um valor de **1** indica replicação transacional e um valor de **2** indica replicação de mesclagem.  
  
 **-RowDelimiter** _row_delimiter_  
 É o caractere ou cadeia de caracteres que marca o fim de uma linha no arquivo de dados de cópia em massa no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . O padrão é \n\<,@g>\n.  
  
 **-StartQueueTimeout** _start_queue_timeout_seconds_  
 É o número máximo de segundos que o Agente de Instantâneo aguarda quando o número de processos simultâneos de instantâneo dinâmico em execução está no limite definido pela propriedade `@max_concurrent_dynamic_snapshots` de [sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Se o número máximo de segundos for alcançado e o Snapshot Agent ainda estiver esperando, será fechado. Um valor de 0 significa que o agente espera indefinidamente, embora possa ser cancelado.  
  
 \- **UsePerArticleContentsView** _use_per_article_contents_view_  
 Esse parâmetro foi preterido e só tem suporte para compatibilidade com versões anteriores.  
  
## <a name="remarks"></a>Comentários  
  
> [!IMPORTANT]  
>  Se você instalou o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent para ser executado com uma conta Sistema Local em vez de uma conta de Usuário de Domínio (o padrão), o serviço só poderá acessar o computador local. Se o Snapshot Agent executado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent for configurado para usar o Modo de Autenticação do Windows ao fazer logon no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o Snapshot Agent falhará. A configuração padrão é Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Para iniciar o Snapshot Agent, execute **snapshot.exe** no prompt do comando. Para obter informações, consulte [Executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Administração do agente de replicação](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  
