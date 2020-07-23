---
title: Agente de Distribuição de Replicação | Microsoft Docs
description: Mova um instantâneo e as transações mantidas nas tabelas do banco de dados de distribuição para as tabelas de destino dos Assinantes usando o Agente de Distribuição de Replicação.
ms.custom: ''
ms.date: 10/29/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Distribution Agent, executables
- agents [SQL Server replication], Distribution Agent
- Distribution Agent, parameter reference
- command prompt [SQL Server replication]
ms.assetid: 7b4fd480-9eaf-40dd-9a07-77301e44e2ac
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: cbb2df105e6ed9172bd271d81f563cf017db110a
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918080"
---
# <a name="replication-distribution-agent"></a>Agente de Distribuição de Replicação
[!INCLUDE[sql-asdb](../../../includes/applies-to-version/sql-asdb.md)]
  O Replication Agente de Distribuição é um executável que move o instantâneo (para replicação de instantâneo e replicação transacional) e as transações mantidas nas tabelas do banco de dados de distribuição (para replicação transacional) para as tabelas de destino nos Assinantes.  
  
> [!NOTE]  
>  Os parâmetros podem ser especificados em qualquer ordem. Quando não são especificados parâmetros opcionais, são usados valores de configurações de registro predefinidos no computador local.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
distrib [-?]  
-Publisher server_name[\instance_name]  
-PublisherDB publisher_database  
-Subscriber server_name[\instance_name]  
-SubscriberDB subscriber_database   
[-AltSnapshotFolder alt_snapshot_folder_path]   
[-BcpBatchSize bcp_batch_size]  
[-CommitBatchSize commit_batch_size]  
[-CommitBatchThreshold commit_batch_threshold]  
[-Continuous]  
[-DefinitionFile def_path_and_file_name]  
[-Distributor distributor]  
[-DistributorLogin distributor_login]  
[-DistributorPassword distributor_password]  
[-DistributorSecurityMode [0|1]]  
[-EncryptionLevel [0|1|2]]  
[-ErrorFile error_path_and_file_name]  
[-ExtendedEventConfigFile configuration_path_and_file_name]  
[-FileTransferType [0|1]]  
[-FtpAddress ftp_address]  
[-FtpPassword ftp_password]   
[-FtpPort ftp_port]  
[-FtpUserName ftp_user_name]  
[-HistoryVerboseLevel [0|1|2|3]]  
[-Hostname host_name]  
[-KeepAliveMessageInterval keep_alive_message_interval_seconds]  
[-LoginTimeOut login_time_out_seconds]  
[-MaxBcpThreads]  
[-MaxDeliveredTransactions number_of_transactions]  
[-MessageInterval message_interval]  
[-MultiSubnetFailover [0|1]]
[-OledbStreamThreshold oledb_stream_threshold]  
[-Output output_path_and_file_name]  
[-OutputVerboseLevel [0|1|2]]  
[-PacketSize packet_size]  
[-PollingInterval polling_interval]  
[-ProfileName profile_name]  
[-Publication publication]  
[-QueryTimeOut query_time_out_seconds]  
[-QuotedIdentifier quoted_identifier]  
[-SkipErrors native_error_id [:...n]]  
[-SubscriberDatabasePath subscriber_path]  
[-SubscriberLogin subscriber_login]  
[-SubscriberPassword subscriber_password]  
[-SubscriberSecurityMode [0|1]]  
[-SubscriberType [0|1|3]]  
[-SubscriptionStreams [1|2|...64]]  
[-SubscriptionTableName subscription_table]  
[-SubscriptionType [0|1|2]]  
[-TransactionsPerHistory [0|1|...10000]]  
[-UseDTS]  
[-UseInprocLoader]  
[-UseOledbStreaming]  
```  
  
## <a name="arguments"></a>Argumentos  
 **-?**  
 Imprime todos os parâmetros disponíveis.  
  
 **-Publisher** _server_name_[ **\\** _instance_name_]  
 É o nome do Publicador. Especifica *server_name* para a instância padrão do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nesse servidor. Especifique _server_name_ **\\** _instance_name_ para uma instância nomeada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] naquele servidor.  
  
 **-PublisherDB** _publisher_database_  
 É o nome do banco de dados Publicador.  
  
 **-Subscriber** _server_name_[ **\\** _instance_name_]  
 É o nome do Assinante. Especifica *server_name* para a instância padrão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] naquele servidor. Especifique _server_name_ **\\** _instance_name_ para uma instância nomeada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] naquele servidor.  
  
 **-SubscriberDB** _subscriber_database_  
 É o nome do banco de dados do Assinante.  
  
 **-AltSnapshotFolder** _alt_snapshot_folder_path_  
 É o caminho para a pasta que contém o instantâneo inicial para uma assinatura.  
  
 **-BcpBatchSize** _bcp_batch_size_  
 É o número de linhas a ser enviado em uma operação de cópia em massa. Ao executar uma operação **bcp in** , o tamanho do lote é o número de linhas a ser enviado ao servidor como uma transação e também o número de linhas que deve ser enviado antes que o Agente de Distribuição registre uma mensagem de progresso **bcp** . Ao executar uma operação **bcp out** , um tamanho fixo de lote **1000** é usado.  
  
 **-CommitBatchSize** _commit_batch_size_  
 É o número de transações a ser emitido para o Assinante antes de uma instrução COMMIT ser emitida. O padrão é 100 e o máximo é 10000.
  
 **-CommitBatchThreshold** _commit_batch_threshold_  
 É o número de comandos de replicação a ser emitido para o Assinante antes de uma instrução COMMIT ser emitida. O padrão é 1000 e o máximo é 10000. 
  
 **-Continuous**  
 Especifica se o agente tenta sondar transações replicadas continuamente. Se especificado, o agente sondará as transações replicadas da origem em intervalos de sondagem, mesmo que não haja transações pendentes.  
  
 **-DefinitionFile** _def_path_and_file_name_  
 É o caminho do arquivo de definição de agente. Um arquivo de definição de agente contém argumentos de prompt de comando para o agente. O conteúdo do arquivo é analisado como um arquivo executável. Use aspas duplas (") para especificar valores de argumentos que contêm caracteres arbitrários.  
  
 **-Distributor** _distributor_  
 É o nome do Distribuidor. Para distribuição (push) do Distribuidor, o nome assume o padrão do Distribuidor local.  
  
 **-DistributorLogin** _distributor_login_  
 É o nome de logon do Distribuidor.  
  
 **-DistributorPassword** _distributor_password_  
 É a senha do Distribuidor.  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 Especifica o modo de segurança do Distribuidor. Um valor 0 indica Modo de Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e um valor 1 indica Modo de Autenticação do Windows (padrão).  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 É o nível da criptografia TLS (Transport Layer Security), antes conhecida como SSL (Secure Sockets Layer), usada pelo Agente de Distribuição ao fazer conexões.  
  
|Valor EncryptionLevel|Descrição|  
|---------------------------|-----------------|  
|**0**|Especifica que o TLS não é usado.|  
|**1**|Especifica que o TLS é usado, mas que o agente não verifica se o certificado de servidor TSL/SSL é assinado por um emissor confiável.|  
|**2**|Especifica que o TLS é usado e que o certificado é verificado.|  
 
 > [!NOTE]  
 >  É definido um certificado TLS/SSL válido com um nome de domínio totalmente qualificado do SQL Server. Para que o agente seja conectado com êxito ao definir -EncryptionLevel como 2, crie um alias no SQL Server local. O parâmetro ‘Alias Name’ deve ser o nome do servidor e o parâmetro ‘Server’ deve ser definido como o nome totalmente qualificado do SQL Server.

 Confira mais informações em [Exibir e modificar as configurações de replicação de segurança](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 **-ErrorFile** _error_path_and_file_name_  
 É o caminho e nome de arquivo do arquivo de erros gerados pelo Agente de Distribuição. Esse arquivo é gerado em qualquer ponto onde a falha ocorreu durante a aplicação de transações de replicação no Assinante. Os erros que ocorrem no Publicador ou no Distribuidor não são registrados nesse arquivo. Esse arquivo contém as transações de replicação com falha e mensagens de erro associadas. Quando não especificado, o arquivo de erros é gerado no diretório atual do Agente de Distribuição. O nome do arquivo de erro é o nome do Agente de Distribuição com uma extensão .err. Se o nome de arquivo especificado existir, serão anexadas mensagens de erro ao arquivo. Esse parâmetro pode ter um máximo de 256 caracteres Unicode.  
  
 **-ExtendedEventConfigFile** _configuration_path_and_file_name_  
 Especifica o caminho e o nome do arquivo de configuração XML de eventos estendidos. O arquivo de configuração de eventos estendidos permite configurar sessões e habilitar eventos para acompanhamento.  
  
 **-FileTransferType** [ **0**| **1**]  
 Especifica o tipo de transferência de arquivo. Um valor **0** indica UNC (convenção de nomenclatura universal) e um valor **1** indica FTP (File Transfer Protocol).  
  
 **-FtpAddress** _ftp_address_  
 É o endereço de rede do serviço FTP para o Distribuidor. Quando não especificado, **DistributorAddress** é usado. Se **DistributorAddress** não for especificado, **Distributor** será usado.  
  
 **-FtpPassword** _ftp_password_  
 É a senha de usuário usada para se conectar ao serviço FTP.  
  
 **-FtpPort** _ftp_port_  
 É o número da porta do serviço FTP para o Distribuidor. Quando não especificado, o número da porta padrão para serviço de FTP (21) é usado.  
  
 **-FtpUserName**  _ftp_user_name_  
 É o nome de usuário usado para se conectar ao serviço FTP. Quando não especificado, **anonymous** é usado.  
  
 **-HistoryVerboseLevel** [ **0** | **1** | **2** | **3** ]  
 Especifica a quantidade de histórico registrada durante uma operação de distribuição. Você pode minimizar o efeito de desempenho do registro de histórico selecionando **1**.  
  
|Valor HistoryVerboseLevel|Descrição|  
|-------------------------------|-----------------|  
|**0**|Mensagens de Progresso são gravadas no console ou em um arquivo de saída. Registros de histórico não são registrados no banco de dados de distribuição.|  
|**1**|Padrão. Sempre atualiza uma mensagem de histórico anterior do mesmo status (inicialização, andamento, êxito, etc.). Se nenhum registro anterior com o mesmo status existir, insira um registro novo.|  
|**2**|Insira novos registros de histórico, a menos que o registro seja para coisas como mensagens ociosas ou mensagens de trabalho de execução longa; em tal caso, atualize os registros anteriores.|  
|**3**|Sempre insira novos registros, a menos que seja para mensagens ociosas.|  
  
 **-Hostname** _host_name_  
 É o nome do host usado na conexão com o Publicador. Esse parâmetro pode ter um máximo de 128 caracteres Unicode.  
  
 **-KeepAliveMessageInterval** _keep_alive_message_interval_seconds_  
 É o número de segundos antes que o thread de histórico verifique se alguma das conexões existentes está esperando por uma resposta do servidor. Esse valor pode ser diminuído para evitar que o agente de verificação marque o Agente de Distribuição como suspeito ao executar um lote de execução longa. O padrão é **300** segundos.  
  
 **-LoginTimeOut** _login_time_out_seconds_  
 É o número de segundos antes que o logon expire. O padrão é **15** segundos.  
  
 **-MaxBcpThreads** _number_of_threads_  
 Especifica o número de operações de cópia em massa que podem ser executadas em paralelo. O número máximo de threads e conexões ODBC que existe simultaneamente no menor dos **MaxBcpThreads** ou o número de solicitações de cópia em massa que aparece na transação sincronizada no banco de dados de distribuição. **MaxBcpThreads** deve ter um valor maior que **0** e não tem um limite superior embutido em código. O padrão é **2** vezes o número de processadores, até um valor máximo de **8**. Ao aplicar um instantâneo gerado no Publicador usando a opção de instantâneo simultânea, um thread é usado, independentemente do número especificado para **MaxBcpThreads**.  
  
 **-MaxDeliveredTransactions** _number_of_transactions_  
 É o número máximo de transações push ou pull aplicado aos Assinantes em uma sincronização. Um valor **0** indica que o máximo é um número infinito de transações. Outros valores podem ser usados por Assinantes para encurtar a duração de uma sincronização que está sendo recebida de um Publicador.  
  
> [!NOTE]  
>  Se -MaxDeliveredTransactions and -Continuous estiverem ambos especificados, o Agente de Distribuição entrega o número especificado de transações e então para (embora -Continuous seja especificado). Você deve reiniciar o Agente de Distribuição depois que o trabalho for concluído.  
  
 **-MessageInterval**  _message_interval_  
 É o intervalo de tempo usado para registro de histórico. Um evento de histórico é registrado quando um destes parâmetros é alcançado:  
  
-   O valor de **TransactionsPerHistory** é atingido depois que o último evento de histórico é registrado.  
  
-   O valor de **MessageInterval** é atingido depois que o último evento de histórico é registrado.  
  
 Se não houver nenhuma transação replicada disponível na origem, o agente informará uma mensagem de não transação ao Distributor. Essa opção especifica quanto tempo o agente espera antes de informar outro mensagem de não transação. O agente sempre informa uma mensagem de não transação quando detecta que não há transações disponíveis na origem após transações replicadas de processamento anterior. O padrão é 60 segundos.  

**-MultiSubnetFailover** Especifica se a propriedade MultiSubnetFailover está habilitada ou não. Se o seu aplicativo estiver se conectando a um AG (grupo de disponibilidade) AlwaysOn em diferentes sub-redes, definir MultiSubnetFailover como true fornece uma detecção e uma conexão mais rápida ao servidor (atualmente) ativo.
  
 **-OledbStreamThreshold** _oledb_stream_threshold_  
 Especifica o tamanho mínimo, em bytes, para dados de objeto binário grande acima do qual os dados serão associados como um fluxo. Você deve especificar **-UseOledbStreaming** para usar esse parâmetro. Os valores podem variar de 400 a 1048576 bytes, com um padrão de 16384 bytes.  
  
 **-Output** _output_path_and_file_name_  
 É o caminho do arquivo de saída do agente. Se o nome de arquivo não for fornecido, a saída será enviada ao console. Se o nome do arquivo especificado existir, a saída será anexada ao arquivo.  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2**]  
 Especifica se a saída deve ser detalhada. Se o nível detalhado for **0**, só mensagens de erro serão impressas. Se o nível detalhado for **1**, todas as mensagens de relatório de progresso serão impressas. Se o nível detalhado for **2** (padrão), todas as mensagens de erro e de relatório de progresso serão impressas, o que é útil na depuração.  
  
 **-PacketSize** _packet_size_  
 É o tamanho do pacote, em bytes. O padrão é 4096 (bytes).  
  
 **-PollingInterval** _polling_interval__  
 É com que frequência, em segundos, o banco de dados de distribuição é consultado para transações replicadas. O padrão é 5 segundos.  
  
 **-ProfileName** _profile_name_  
 Especifica um perfil de agente a ser usado para parâmetros de agente. Se **ProfileName** for NULL, o perfil de agente será desabilitado. Se **ProfileName** não for especificado, o perfil padrão de tipo de agente será usado. Para obter mais informações, consulte [Perfis do agente de replicação](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 **-Publication** _publication_  
 É o nome da publicação. Esse parâmetro só é válido se a publicação estiver definida para ter sempre um instantâneo disponível para assinaturas novas ou reiniciadas.  
  
 **-QueryTimeOut** _query_time_out_seconds_  
 É o número de segundos antes que a consulta expire. O padrão é 1800 segundos.  
  
 **-QuotedIdentifier** _quoted_identifier_  
 Especifica o identificador entre aspas a ser usado. O primeiro caractere do valor indica o valor que o Agente de Distribuição usa. Se **QuotedIdentifier** for usado sem valor, o Agente de Distribuição usará um espaço. Se **QuotedIdentifier** não for usado, o Agente de Distribuição usará qualquer identificador entre aspas com suporte no Assinante.  
  
 **-SkipErrors** _native_error_id_ [ **:** _...n_]  
 É uma lista separada por dois pontos que especifica o número de erros a ser ignorado por esse agente.  
  
 **-SubscriberDatabasePath** _subscriber_database_path_  
 É o caminho para o banco de dados Jet (arquivo .mdb) se **SubscriberType** for **2** (permite uma conexão com o banco de dados Jet sem o DSN (Nome da Fonte de Dados) ODBC).  
  
 **-SubscriberLogin** _subscriber_login_  
 É o nome de logon do Assinante. Se **SubscriberSecurityMode** for **0** (para Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ), esse parâmetro deverá ser especificado.  
  
 **-SubscriberPassword** _subscriber_password_  
 É a senha de Assinante. Se **SubscriberSecurityMode** for **0** (para Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ), esse parâmetro deverá ser especificado.  
  
 **-SubscriberSecurityMode** [ **0**| **1**]  
 Especifica o modo de segurança do Assinante. Um valor **0** indica Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e um valor **1** indica Modo de Autenticação do Windows (padrão).  
  
 **-SubscriberType** [ **0**| **1**| **3**]  
 Especifica o tipo de conexão de Assinante usado pelo Agente de Distribuição.  
  
|Valor SubscriberType|Descrição|  
|--------------------------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|  
|**1**|Fonte de dados ODBC|  
|**3**|Fonte de dados OLE DB|  
  
 **-SubscriptionStreams** [**0**|**1**|**2**|...**64**]  
 É o número de conexões permitido por Agente de Distribuição para aplicar lotes de alterações em paralelo a um Assinante, mantendo muitas das características transacionais presentes ao usar um thread único. Para um Publicador [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , há suporte para um intervalo de valores de 1 a 64. Esse parâmetro só tem suporte quando o Publicador e o Distribuidor estão sendo executados no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou versões posteriores. Esse parâmetro não tem suporte ou deve ser 0 para Assinantes não [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou assinaturas ponto a ponto.  
  
> [!NOTE]  
>  Se uma das conexões falhar na execução ou na confirmação, todas as conexões abortarão o lote atual, e o agente usará um fluxo único para repetir os lotes com falha. Antes de concluir a fase de repetição pode haver inconsistências transacionais temporárias no Assinante. Depois que os lotes com falha são confirmados com êxito, o Assinante é levado de volta a um estado de consistência transacional.  
  
> [!IMPORTANT]  
>  Quando você especifica um valor 2 ou maior para **-SubscriptionStreams**, a ordem em que as transações são recebidas no Assinante pode diferir da ordem em que elas foram feitas no Publicador. Se esse comportamento causar violações de restrição durante a sincronização, você deve usar a opção NOT FOR REPLICATION para desabilitar a imposição da restrição durante a sincronização. Para obter mais informações, consulte [Controlar o comportamento de gatilhos e restrições durante a sincronização &#40;programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md).  
  
> [!NOTE]  
>  Fluxos de assinatura não funcionam em artigos configurados para entrega [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Para usar fluxos de assinatura, configure os artigos para entregar chamadas de procedimento armazenado.  
  
 **-SubscriptionTableName** _subscription_table_  
 É o nome da tabela de assinatura gerada ou usada no determinado Assinante. Quando não for especificado, a tabela [MSreplication_subscriptions &#40;Transact-SQL&#41;](../../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) será usada. Use essa opção para DBMS (sistemas de gerenciamento de banco de dados) que não oferecem suporte a nomes de arquivo longos.  
  
 **-SubscriptionType** [ **0**| **1**| **2**]  
 Especifica o tipo de assinatura para distribuição. Um valor **0** indica uma assinatura push, um valor **1** indica uma assinatura pull e um valor **2** indica uma assinatura anônima.  
  
 **-TransactionsPerHistory** [ **0**| **1**|... **10000**]  
 Especifica o intervalo da transação para registro de histórico. Se o número de transações confirmadas depois da última instância de registro de histórico for maior do que essa opção, uma mensagem de histórico será registrada. O padrão é 100. Um valor **0** indica **TransactionsPerHistory**. See the preceding **–MessageInterval**parameter.  
  
 **-UseDTS**  
 Deve ser especificado como um parâmetro para uma publicação que permite transformação de dados.  
  
 **-UseInprocLoader**  
 Aprimora o desempenho do instantâneo inicial fazendo com que o Agente de Distribuição use o comando BULK INSERT ao aplicar arquivos de instantâneo no Assinante. Esse parâmetro é preterido porque não é compatível com o tipo de dados de XML. Se você não estiver replicando dados XML, esse parâmetro poderá ser usado. Esse parâmetro não pode ser usado com instantâneos de modo de caractere ou Assinantes não [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se você usar esse parâmetro, a conta de serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Assinante deverá ter permissões de leitura no diretório onde os arquivos de dados .bcp de instantâneo estão localizados. Quando esse parâmetro não é usado, o agente (para Assinantes não [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) ou o driver ODBC carregado pelo agente (para Assinantes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ) lê dos arquivos, portanto o contexto de segurança da conta de serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não é usado.  
  
 **-UseOledbStreaming**  
 Quando especificado, habilita a associação de dados de objeto binário grande como um fluxo. Use **-OledbStreamThreshold** para especificar o tamanho, em bytes, acima do qual um fluxo será usado. **UseOledbStreaming** está habilitado por padrão. **UseOledbStreaming** grava na pasta **C:\Program Files\Microsoft SQL Server\\<version\>\COM**.  
  
## <a name="remarks"></a>Comentários  
  
> [!IMPORTANT]  
>  Se você instalou o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent para ser executado com uma conta Sistema Local em vez de uma conta de usuário de domínio (o padrão), o serviço só poderá acessar o computador local. Se o Agente de Distribuição executado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent for configurado para usar o Modo de Autenticação do Windows ao fazer logon em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o Agente de Distribuição falhará. A configuração padrão é Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obter informações em como alterar contas de segurança, consulte [View and Modify Replication Security Settings](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 Para iniciar o Agente de Distribuição, execute **distrib.exe** no prompt de comando. Para obter informações, consulte [Conceitos dos executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## <a name="change-history"></a>Histórico de alterações  
  
|Conteúdo atualizado|  
|---------------------|  
|Adicionado o parâmetro **-ExtendedEventConfigFile** .|  
|Adicionado o parâmetro **-MultiSubnetFailover**.|  
  
## <a name="see-also"></a>Consulte Também  
 [Administração do agente de replicação](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  
