---
title: Agente de Leitor de Log de replicação | Microsoft Docs
ms.custom: ''
ms.date: 10/29/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Log Reader Agent, executables
- Log Reader Agent, parameter reference
- agents [SQL Server replication], Log Reader Agent
- command prompt [SQL Server replication]
ms.assetid: 5487b645-d99b-454c-8bd2-aff470709a0e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 58ff313686f1f37643068a28d4e30ac93eddd2ce
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528180"
---
# <a name="replication-log-reader-agent"></a>Replication Agente de Leitor de Log
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  O Replication Agente de Leitor de Log é um executável que monitora o log de transações de cada banco de dados configurado para replicação transacional e copia as transações marcadas para replicação do log de transações no banco de dados de distribuição.  
  
> [!NOTE]  
>  Os parâmetros podem ser especificados em qualquer ordem. Quando não são especificados parâmetros opcionais, são usados valores predefinidos com base no perfil de agente padrão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
logread [-?]   
-Publisher server_name[\instance_name]   
-PublisherDB publisher_database   
[-Continuous]  
[-DefinitionFile def_path_and_file_name]  
[-Distributor server_name[\instance_name]]  
[-DistributorLogin distributor_login]  
[-DistributorPassword distributor_password]  
[-DistributorSecurityMode [0|1]]  
[-EncryptionLevel [0|1|2]]  
[-ExtendedEventConfigFile configuration_path_and_file_name]  
[-HistoryVerboseLevel [0|1|2]]  
[-KeepAliveMessageInterval keep_alive_message_interval_seconds]  
[-LoginTimeOut login_time_out_seconds]  
[-LogScanThreshold scan_threshold]  
[-MaxCmdsInTran number_of_commands]  
[-MessageInterval message_interval]  
[-Output output_path_and_file_name]  
[-OutputVerboseLevel [0|1|2|3|4]]  
[-PacketSize packet_size]  
[-PollingInterval polling_interval]  
[-ProfileName profile_name]   
[-PublisherFailoverPartner server_name[\instance_name] ]  
[-PublisherSecurityMode [0|1]]  
[-PublisherLogin publisher_login]  
[-PublisherPassword publisher_password]   
[-QueryTimeOut query_time_out_seconds]  
[-ReadBatchSize number_of_transactions]   
[-ReadBatchThreshold read_batch_threshold]  
[-RecoverFromDataErrors]  
```  
  
## <a name="arguments"></a>Argumentos  
 **-?**  
 Exibe informações de uso.  
  
 **-Publisher** _server_name_[ **\\** _instance_name_]  
 É o nome do Publicador. Especifica *server_name* para a instância padrão do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nesse servidor. Especifique _server_name_ **\\** _instance_name_ para uma instância nomeada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] naquele servidor.  
  
 **-PublisherDB** _publisher_database_  
 É o nome do banco de dados Publicador.  
  
 **-Continuous**  
 Especifica se o agente tenta ou não sondar transações replicadas continuamente. Se especificado, o agente sondará as transações replicadas da origem em intervalos de sondagem, mesmo que não haja transações pendentes.  
  
 **-DefinitionFile** _def_path_and_file_name_  
 É o caminho do arquivo de definição de agente. Um arquivo de definição de agente contém argumentos de linha de comando para o agente. O conteúdo do arquivo é analisado como um arquivo executável. Use aspas duplas (") para especificar os valores de argumentos que contêm caracteres arbitrários.  
  
 **-Distributor** _server_name_[ **\\** _instance_name_]  
 É o nome do Distribuidor. Especifica *server_name* para a instância padrão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] naquele servidor. Especifique _server_name_ **\\** _instance_name_ para uma instância nomeada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] naquele servidor.  
  
 **-DistributorLogin** _distributor_login_  
 É o nome de logon do Distribuidor.  
  
 **-DistributorPassword** _distributor_password_  
 É a senha do Distribuidor.  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 Especifica o modo de segurança do Distribuidor. Um valor **0** indica Modo de Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (padrão) e um valor **1** indica [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Modo de Autenticação do Windows.  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 É o nível da criptografia TLS (Transport Layer Security), anteriormente conhecida como SSL (Secure Sockets Layer), que é usada pelo Agente de Leitor de Log ao fazer conexões.  
  
|Valor EncryptionLevel|Descrição|  
|---------------------------|-----------------|  
|**0**|Especifica que o TLS não é usado.|  
|**1**|Especifica que o TLS é usado, mas que o agente não verifica se o certificado de servidor TSL/SSL é assinado por um emissor confiável.|  
|**2**|Especifica que o TLS é usado e que o certificado é verificado.|  

 > [!NOTE]  
 >  É definido um certificado TLS/SSL válido com um nome de domínio totalmente qualificado do SQL Server. Para que o agente seja conectado com êxito ao definir -EncryptionLevel como 2, crie um alias no SQL Server local. O parâmetro ‘Alias Name’ deve ser o nome do servidor e o parâmetro ‘Server’ deve ser definido como o nome totalmente qualificado do SQL Server.
 
 Confira mais informações em [Exibir e modificar as configurações de replicação de segurança](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 **-ExtendedEventConfigFile** _configuration_path_and_file_name_  
 Especifica o caminho e o nome do arquivo de configuração XML de eventos estendidos. O arquivo de configuração de eventos estendidos permite configurar sessões e habilitar eventos para acompanhamento.  
  
 **-HistoryVerboseLevel** [ **0**| **1**| **2**]  
 Especifica a quantidade de histórico registrada durante uma operação de leitura de log. Você pode minimizar o efeito de desempenho do registro de histórico selecionando **1**.  
  
|Valor HistoryVerboseLevel|Descrição|  
|-------------------------------|-----------------|  
|**0**||  
|**1**|Padrão. Sempre atualiza uma mensagem de histórico anterior do mesmo status (inicialização, andamento, êxito, etc.). Se nenhum registro anterior com o mesmo status existir, insira um registro novo.|  
|**2**|Insira novos registros de histórico, a menos que o registro seja para coisas como mensagens ociosas ou mensagens de trabalho de execução longa; em tal caso, atualize os registros anteriores.|  
  
 **-KeepAliveMessageInterval** _keep_alive_message_interval_seconds_  
 É o número de segundos antes que o thread de histórico verifique se alguma das conexões existentes está esperando por uma resposta do servidor. Esse valor pode ser diminuído para evitar que o agente de verificação marque o Agente de Leitor de Log como suspeito ao executar um lote de execução longa. O padrão é 300 segundos.  
  
 **-LoginTimeOut** _login_time_out_seconds_  
 É o número de segundos antes que o logon expire. O padrão é 15 segundos.  
  
 **-LogScanThreshold** _scan_threshold_  
 Somente para uso interno.  
  
 **-MaxCmdsInTran** _number_of_commands_  
 Especifica o número máximo de instruções agrupadas em uma transação à medida que o Log Reader grava comandos no banco de dados de distribuição. O uso desse parâmetro permite que o Agente de Leitor de Log e o Agente de Distribuição divida grandes transações (consistindo em muitos comandos) no Publicador em várias transações menores quando aplicadas no Assinante. A especificação desse parâmetro pode reduzir a contenção no Distribuidor e pode reduzir a latência entre o Publicador e o Assinante. Como a transação original é aplicada em unidades menores, o Assinante pode acessar linhas de uma transação lógica de Publicador antes do fim da transação original, O padrão é **0**, que preserva os limites de transação do Publicador.  
  
> [!NOTE]
>  Esse parâmetro é ignorado para publicações que não são do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte a seção que "Configurando o trabalho de conjunto das transações" em [Performance Tuning for Oracle Publishers](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md).  
  
 **-MessageInterval** _message_interval_  
 É o intervalo de tempo usado para registro de histórico. Um evento de histórico é registrado quando o valor **MessageInterval** é alcançado depois que o ultimo evento de histórico é registrado.  
  
 Se não houver nenhuma transação replicada disponível na origem, o agente informará uma mensagem de não transação ao Distributor. Essa opção especifica quanto tempo o agente espera antes de informar outro mensagem de não transação. O agente sempre informa uma mensagem de não transação quando detecta que não há transações disponíveis na origem após transações replicadas de processamento anterior. O padrão é 60 segundos.  
  
 **-Output** _output_path_and_file_name_  
 É o caminho do arquivo de saída do agente. Se o nome de arquivo não for fornecido, a saída será enviada ao console. Se o nome do arquivo especificado existir, a saída será anexada ao arquivo.  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2** | **3** | **4** ]  
 Especifica se a saída deve ser detalhada.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Somente mensagens de erro são impressas.|  
|**1**|Todas as mensagens de relatório de progresso do agente são impressas.|  
|**2** (padrão)|Todas as mensagens de relatório de progresso do agente e de erro são impressas.|  
|**3**|Os primeiros 100 bytes de cada comando replicado são impressos.|  
|**4**|Todos os comandos replicados são impressos.|  
  
 Os valores 2-4 são úteis na depuração.  
  
 **-PacketSize** _packet_size_  
 É o tamanho do pacote, em bytes. O padrão é 4096 (bytes).  
  
 **-PollingInterval** _polling_interval_  
 É a frequência, em segundos, que o log é consultado para transações replicadas. O padrão é 5 segundos.  
  
 **-ProfileName** _profile_name_  
 Especifica um perfil de agente a ser usado para parâmetros de agente. Se **ProfileName** for NULL, o perfil de agente será desabilitado. Se **ProfileName** não for especificado, o perfil padrão de tipo de agente será usado. Para obter mais informações, consulte [Perfis do agente de replicação](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 **-PublisherFailoverPartner** _server_name_[ **\\** _instance_name_]  
 Especifica a instância de parceiro de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que participa de uma sessão de espelhamento de banco de dados com o banco de dados de publicação. Para obter mais informações, consulte [Espelhamento e replicação de banco de dados &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md).  
  
 **-PublisherSecurityMode** [ **0**| **1**]  
 Especifica o modo de segurança do Publicador. Um valor de **0** indica Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (padrão), e um valor de **1** indica Modo de Autenticação do Windows.  
  
 **-PublisherLogin** _publisher_login_  
 É o nome de logon do Publicador.  
  
 **-PublisherPassword** _publisher_password_  
 É a senha do Publicador.  
  
 **-QueryTimeOut** _query_time_out_seconds_  
 É o número de segundos antes que a consulta expire. O padrão é 1800 segundos.  
  
 **-ReadBatchSize** _number_of_transactions_  
 É o número máximo de transações lidas de um log de transações do banco de dados de publicação por ciclo de processamento, com um padrão de 500 e máximo de 10 mil. O agente continuará lendo transações em lotes até que todas as transações tenham sido lidas do log. Esse parâmetro não tem suporte para Publicadores Oracle.  
  
 **-ReadBatchThreshold** _number_of_commands_  
 É o número de comandos de replicação a serem lidos no log de transações, antes de ser emitido para o Assinante pelo Agente de Distribuição. O padrão é 0. Se o parâmetro não for especificado, o Agente de Leitor de Log lerá até a parte final do log ou até o número especificado em **-ReadBatchSize** (número de transações).  
  
 **-RecoverFromDataErrors**  
 Especifica que o Agente de Leitor de Log continuará a executar, quando encontrar erros em dados de colunas publicados de um Publicador não SQL Server. Por padrão, tais erros fazem o Agente de Leitor de Log falhar. Quando você usa **-RecoverFromDataErrors**, dados de coluna são replicados erroneamente como NULL ou como um valor não nulo apropriado e as mensagens de aviso são registradas na tabela [MSlogreader_history](../../../relational-databases/system-tables/mslogreader-history-transact-sql.md) . Esse parâmetro só tem suporte para Editores Oracle.  
  
## <a name="remarks"></a>Comentários  
  
> [!IMPORTANT]  
>  Se você instalou o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent para executar com uma conta Sistema Local em vez de uma conta de usuário de domínio (o padrão), o serviço só poderá acessar o computador local. Se o Agente de Leitor de Log executado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent for configurado para usar o Modo de Autenticação do Windows ao fazer logon no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o Agente de Leitor de Log falhará. A configuração padrão é Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obter informações em como alterar contas de segurança, consulte [View and Modify Replication Security Settings](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 Para iniciar o Agente de Leitor de Log, execute **logread.exe** no prompt de comando. Para obter informações, consulte [Conceitos dos executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## <a name="change-history"></a>Histórico de alterações  
  
|Conteúdo atualizado|  
|---------------------|  
|Adicionado o parâmetro **-ExtendedEventConfigFile** .|  
  
## <a name="see-also"></a>Consulte Também  
 [Administração do agente de replicação](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  
