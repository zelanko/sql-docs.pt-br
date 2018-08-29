---
title: sys. Databases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- databases
- databases_TSQL
- sys.databases
- sys.databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.databases catalog view
ms.assetid: 46c288c1-3410-4d68-a027-3bbf33239289
caps.latest.revision: 152
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b9280a340991982831b885416ef8512a127549b5
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43073907"
---
# <a name="sysdatabases-transact-sql"></a>sys.databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contém uma linha por banco de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se um banco de dados não for `ONLINE`, ou `AUTO_CLOSE` é definido como `ON` e o banco de dados estiver fechado, os valores de algumas colunas podem ser `NULL`. Se um banco de dados for `OFFLINE`, a linha correspondente não é visível para usuários com poucos privilégios. Para ver a linha correspondente, se o banco de dados `OFFLINE`, um usuário deve ter pelo menos as `ALTER ANY DATABASE` permissão de nível de servidor, ou o `CREATE DATABASE` permissão no `master` banco de dados.  
  

  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do banco de dados, exclusivo em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou em um servidor do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
|**database_id**|**int**|ID do banco de dados, exclusivo em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou em um servidor do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
|**source_database_id**|**int**|Non-NULL = ID do banco de dados de origem deste instantâneo do banco de dados.<br /> NULL = Não é um instantâneo do banco de dados.|  
|**owner_sid**|**varbinary(85)**|SID (Identificador de Segurança) do proprietário externo do banco de dados, como registrado para o servidor. Para obter informações sobre quem pode possuir um banco de dados, consulte o **ALTER AUTHORIZATION para bancos de dados** seção [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md).|  
|**create_date**|**datetime**|Data em que o banco de dados foi criado ou renomeado. Para **tempdb**, esse valor é alterado sempre que o servidor for reiniciado.|  
|**compatibility_level**|**tinyint**|Inteiro que corresponde à versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o qual o comportamento é compatível:<br /> **Valor** : **aplica-se a**<br /> 70: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /> 80: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /> 90: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]<br /> 100: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 110: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 120: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 130: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] |  
|**collation_name**|**sysname**|Agrupamento do banco de dados. Funciona como o agrupamento padrão no banco de dados.<br /> NULL = banco de dados não está online ou AUTO_CLOSE está definida como ON e o banco de dados está fechado.|  
|**user_access**|**tinyint**|Configuração de acesso do usuário:<br /> 0 = MULTI_USER especificado<br /> 1 = SINGLE_USER especificado<br /> 2 = RESTRICTED_USER especificado|  
|**user_access_desc**|**nvarchar(60)**|Descrição da configuração do acesso do usuário.|  
|**is_read_only**|**bit**|1 = O banco de dados é READ_ONLY<br /> 0 = O banco de dados é READ_WRITE|  
|**is_auto_close_on**|**bit**|1 = AUTO_CLOSE está ON<br /> 0 = AUTO_CLOSE está OFF|  
|**is_auto_shrink_on**|**bit**|1 = AUTO_SHRINK está ON<br /> 0 = AUTO_SHRINK está OFF|  
|**state**|**tinyint**|**Valor &#124; aplica-se a**<br /> 0 = ONLINE <br /> 1 = RESTORING <br /> 2 = RECOVERING: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 3 = RECOVERY_PENDING: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 4 = SUSPECT <br /> 5 = EMERGÊNCIA: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 6 = off-line: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 7 = CÓPIA: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] <br /> 10 = OFFLINE_SECONDARY: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] <br /><br /> **Observação:** para bancos de dados AlwaysOn, consulte a `database_state` ou `database_state_desc` colunas de [DM hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md).|  
|**state_desc**|**nvarchar(60)**|Descrição do estado do banco de dados. Consulte o estado.|  
|**is_in_standby**|**bit**|O banco de dados é somente leitura para log de restauração.|  
|**is_cleanly_shutdown**|**bit**|1 = Banco de dados desligado corretamente. Nenhuma recuperação é necessária na inicialização<br /> 0 = Banco de dados não desligado corretamente. Recuperação é necessária na inicialização|  
|**is_supplemental_logging_enabled**|**bit**|1 = SUPPLEMENTAL_LOGGING está ON<br /> 0 = SUPPLEMENTAL_LOGGING está OFF|  
|**snapshot_isolation_state**|**tinyint**|Estado de transações de isolamento de instantâneo permitidas, conforme definido pela opção ALLOW_SNAPSHOT_ISOLATION:<br /> 0 = O estado de isolamento de instantâneo está OFF (padrão). O isolamento de instantâneo não é permitido.<br /> 1 = O estado de isolamento de instantâneo está ON. O isolamento de instantâneo é permitido.<br /> 2 = O estado de isolamento de instantâneo está em transição para o estado OFF. Todas as transações têm suas modificações controladas por versão. Não é possível iniciar novas transações usando isolamento de instantâneo. O banco de dados permanece na transição para o estado OFF até que todas as transações que estavam ativas quando ALTER DATABASE foi executado possam ser concluídas.<br /> 3 = O estado de isolamento de instantâneo está em transição para o estado ON. Novas transações têm suas modificações controladas por versão. As transações não podem usar isolamento de instantâneo até que o estado de isolamento de instantâneo se torne 1 (ON). O banco de dados permanece na transição para o estado ON até que todas as transações de atualização que estavam ativas quando ALTER DATABASE foi executado possam ser concluídas.|  
|**snapshot_isolation_state_desc**|**nvarchar(60)**|Descrição do estado de transações de isolamento de instantâneo permitidas, conforme definido pela opção ALLOW_SNAPSHOT_ISOLATION.|  
|**is_read_committed_snapshot_on**|**bit**|1 = A opção READ_COMMITTED_SNAPSHOT está ON. Operações de leitura sob o nível de isolamento confirmado por leitura são baseados em varreduras de instantâneo e não adquirem bloqueios.<br /> 0 = A opção de READ_COMMITTED_SNAPSHOT está OFF (padrão). Operações de leitura sob o nível de isolamento confirmado por leitura usam bloqueios de compartilhamento.|  
|**recovery_model**|**tinyint**|Modelo de recuperação selecionado:<br /> 1 = FULL<br /> 2 = BULK_LOGGED<br /> 3 = SIMPLE|  
|**recovery_model_desc**|**nvarchar(60)**|Descrição de modelo de recuperação selecionado.|  
|**page_verify_option**|**tinyint**|Configuração da opção PAGE_VERIFY:<br /> 0 = NONE<br /> 1 = TORN_PAGE_DETECTION<br /> 2 = CHECKSUM|  
|**page_verify_option_desc**|**nvarchar(60)**|Descrição da configuração da opção PAGE_VERIFY.|  
|**is_create_stats_on**|**bit**|1 = AUTO_CREATE_STATISTICS está ON<br /> 0 = AUTO_CREATE_STATISTICS está OFF|  
|**is_auto_create_stats_incremental_on**|**bit**|Indica a configuração padrão para a opção incremental de estatísticas automáticas.<br /> 0 = as estatísticas criadas automaticamente não são incrementais<br /> 1 = as estatísticas criadas automaticamente são incrementais se possível<br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**is_update_stats_on**|**bit**|1 = AUTO_UPDATE_STATISTICS está ON<br /> 0 = AUTO_UPDATE_STATISTICS está OFF|  
|**is_auto_update_stats_async_on**|**bit**|1 = AUTO_UPDATE_STATISTICS_ASYNC está ON<br /> 0 = AUTO_UPDATE_STATISTICS_ASYNC está OFF|  
|**is_ansi_null_default_on**|**bit**|1 = ANSI_NULL_DEFAULT está ON<br /> 0 = ANSI_NULL_DEFAULT está OFF|  
|**is_ansi_nulls_on**|**bit**|1 = ANSI_NULLS está ON<br /> 0 = ANSI_NULLS está OFF|  
|**is_ansi_padding_on**|**bit**|1 = ANSI_PADDING está ON<br /> 0 = ANSI_PADDING está OFF|  
|**is_ansi_warnings_on**|**bit**|1 = ANSI_WARNINGS está ON<br /> 0 = ANSI_WARNINGS está OFF|  
|**is_arithabort_on**|**bit**|1 = ARITHABORT está ON<br /> 0 = ARITHABORT está OFF|  
|**is_concat_null_yields_null_on**|**bit**|1 = CONCAT_NULL_YIELDS_NULL está ON<br /> 0 = CONCAT_NULL_YIELDS_NULL está OFF|  
|**is_numeric_roundabort_on**|**bit**|1 = NUMERIC_ROUNDABORT está ON<br /> 0 = NUMERIC_ROUNDABORT está OFF|  
|**is_quoted_identifier_on**|**bit**|1 = QUOTED_IDENTIFIER está ON<br /> 0 = QUOTED_IDENTIFIER está OFF|  
|**is_recursive_triggers_on**|**bit**|1 = RECURSIVE_TRIGGERS está ON<br /> 0 = RECURSIVE_TRIGGERS está OFF|  
|**is_cursor_close_on_commit_on**|**bit**|1 = CURSOR_CLOSE_ON_COMMIT está ON<br /> 0 = CURSOR_CLOSE_ON_COMMIT está OFF|  
|**is_local_cursor_default**|**bit**|1 = CURSOR_DEFAULT é local<br /> 0 = CURSOR_DEFAULT é global|  
|**is_fulltext_enabled**|**bit**|1 = Texto completo habilitado para o banco de dados<br /> 0 = Texto completo desabilitado para o banco de dados|  
|**is_db_trustworthy_on**|**bit**|1 = O banco de dados foi marcado como confiável<br /> 0 = O banco de dados não foi marcado como confiável|  
|**is_db_chaining_on**|**bit**|1 = O encadeamento de propriedades de bancos de dados está ON<br /> 0 = O encadeamento de propriedades de bancos de dados está OFF|  
|**is_parameterization_forced**|**bit**|1 = A parametrização é FORCED<br /> 0 = A parametrização é SIMPLE|  
|**is_master_key_encrypted_by_server**|**bit**|1 = O banco de dados tem uma chave mestra criptografada<br /> 0 = O banco de dados não tem uma chave mestra criptografada|  
|**is_query_store_on**|**bit**|1 = a consulta de repositório é habilitado para este banco de dados. Verifique [database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md) para exibir o status do repositório de consulta.<br /> 0 = a consulta de repositório não está habilitado<br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
|**is_published**|**bit**|1 = O banco de dados é um banco de dados de publicação em uma topologia de replicação transacional ou de instantâneo<br /> 0 = Não é um banco de dados de publicação|  
|**is_subscribed**|**bit**|Esta coluna não é usada. Sempre retornará 0, independentemente do status de assinante do banco de dados.|  
|**is_merge_published**|**bit**|1 = O banco de dados é um banco de dados de publicação em uma topologia de replicação de mesclagem<br /> 0 = Não é um banco de dados de publicação em uma topologia de replicação de mesclagem|  
|**is_distributor**|**bit**|1 = O banco de dados é o banco de dados de distribuição de uma topologia de replicação<br /> 0 = Não é o banco de dados de distribuição de uma topologia de replicação|  
|**is_sync_with_backup**|**bit**|1 = O banco de dados está marcado para sincronização de replicação com backup<br /> 0 = Não está marcado para sincronização de replicação com backup|  
|**service_broker_guid**|**uniqueidentifier**|Identificador do service broker para este banco de dados. Usado como o **broker_instance** do destino na tabela de roteamento.|  
|**is_broker_enabled**|**bit**|1 = O agente neste banco de dados está enviando e recebendo mensagens atualmente.<br /> 0 = Todas as mensagens enviadas permanecerão na fila de transmissão e as mensagens recebidas não serão colocadas nas filas deste banco de dados.<br /> Por padrão, bancos de dados restaurados ou anexados têm o agente desabilitado. A exceção é espelhamento de banco de dados onde o agente é habilitado após failover.|  
|**log_reuse_wait**|**tinyint**|Reutilização de espaço de log de transações está esperando atualmente um dos seguintes a partir do último ponto de verificação. (Para obter mais explicações sobre esses valores, consulte [o Log de transações](../../relational-databases/logs/the-transaction-log-sql-server.md).)<br /> 0 = Nada<br />   1 = Checkpoint (quando um banco de dados usar um modelo de recuperação e tiver um grupo de arquivos de dados com otimização de memória, você possivelmente verá a coluna log_reuse_wait indicar checkpoint ou xtp_checkpoint.) **Aplica-se ao** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  2 = Backup de log **aplica-se ao** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  3 = Active Directory backup ou restauração **aplica-se ao** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  4 = transação ativa **aplica-se ao** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  5 = espelhamento de banco de dados **aplica-se ao** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  6 = replicação **aplica-se ao** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  7 = criação de instantâneo do banco de dados **aplica-se ao** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  8 = verificação de log **aplica-se a**<br />  9 = uma grupos de disponibilidade AlwaysOn réplica secundária está aplicando registros de log de transações desse banco de dados para um banco de dados secundário correspondente. **Aplica-se ao** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Em versões anteriores do SQL Server, 9 = Outro (Transitório).<br />  10 = somente para uso interno **aplica-se ao** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  11 = somente para uso interno **aplica-se ao** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 12 = somente para uso interno **aplica-se ao** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />13 = página mais antiga **aplica-se ao** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 14 = outro **aplica-se ao** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  16 = XTP_CHECKPOINT (Quando um banco de dados usar um modelo de recuperação e tiver um grupo de arquivos de dados com otimização de memória, você possivelmente verá a coluna log_reuse_wait indicar checkpoint ou xtp_checkpoint.) **Aplica-se ao** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|**log_reuse_wait_desc**|**nvarchar(60)**|No momento, a descrição da reutilização de espaço do log de transações está aguardando como um dos últimos pontos de verificação.|  
|**is_date_correlation_on**|**bit**|1 = DATE_CORRELATION_OPTIMIZATION está ON<br /> 0 = DATE_CORRELATION_OPTIMIZATION está OFF|  
|**is_cdc_enabled**|**bit**|1 = O banco de dados está habilitado para Change Data Capture. Para obter mais informações, consulte [sp_cdc_enable_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md).|  
|**is_encrypted**|**bit**|Indica se o banco de dados está criptografado (reflete o último estado definido usando a cláusula ALTER DATABASE SET ENCRYPTION). Pode ser um dos seguintes valores:<br /> 1 = Criptografado<br /> 0 = Não criptografado<br /> Para obter mais informações sobre a criptografia do banco de dados, confira [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).<br /> Se o banco de dados está no processo de ser descriptografado, **is_encrypted** mostra um valor de 0. Você pode ver o estado do processo de criptografia usando o [DM database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) exibição de gerenciamento dinâmico.|  
|**is_honor_broker_priority_on**|**bit**|Indica se o banco de dados cumpre prioridades de conversa (reflete o último estado definido por meio da cláusula ALTER DATABASE SET HONOR_BROKER_PRIORITY). Pode ser um dos seguintes valores:<br /> 1 = HONOR_BROKER_PRIORITY está ON<br /> 0 = HONOR_BROKER_PRIORITY está OFF|  
|**replica_id**|**uniqueidentifier**|Identificador exclusivo da réplica de disponibilidade local do [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] do grupo de disponibilidade, se houver, no qual o banco de dados está participando.<br /> NULL = o banco de dados não faz parte de uma réplica de disponibilidade em um grupo de disponibilidade.<br /> **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**group_database_id**|**uniqueidentifier**|Identificador exclusivo do banco de dados dentro de um sempre no grupo de disponibilidade, se houver, no qual o banco de dados está participando. **group_database_id** é o mesmo para este banco de dados na réplica primária e em cada réplica secundária na qual o banco de dados foi unido ao grupo de disponibilidade.<br /> NULL = o banco de dados não faz parte de uma réplica de disponibilidade em nenhum grupo de disponibilidade.<br /> **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**resource_pool_id**|**int**|A ID do pool de recursos que é mapeado para esse banco de dados. Esse conjunto de recursos controla a memória total disponível para tabelas com otimização de memória nesse banco de dados.<br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|**default_language_lcid**|**smallint**|Indica a lcid (id local) do idioma padrão de um banco de dados independente.<br /> **Observação** funciona como o [configurar a opção de configuração de servidor default language](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) de **sp_configure**. Esse valor é **nulo** para um banco de dados dependente.<br /> **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_language_name**|**nvarchar(128)**|Indica o idioma padrão de um banco de dados independente.<br /> Esse valor é **nulo** para um banco de dados dependente.<br /> **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_fulltext_language_lcid**|**int**|Indica a lcid (id local) do idioma de texto completo padrão do banco de dados independente.<br /> **Observação** funciona como o padrão [configurar o idioma de texto completo padrão Server Configuration Option](../../database-engine/configure-windows/configure-the-default-full-text-language-server-configuration-option.md) de **sp_configure**. Esse valor é **nulo** para um banco de dados dependente.<br /> **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_fulltext_language_name**|**nvarchar(128)**|Indica o idioma de texto completo padrão do banco de dados independente.<br /> Esse valor é **nulo** para um banco de dados dependente.<br /> **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_nested_triggers_on**|**bit**|Indica se gatilhos aninhados são permitidos no banco de dados independente.<br /> 0 = gatilhos aninhados não são permitidos<br /> 1 = gatilhos aninhados são permitidos<br /> **Observação** funciona como o [configurar a opção de configuração de servidor nested triggers](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md) de **sp_configure**. Esse valor é **nulo** para um banco de dados dependente. Ver [sys. Configurations &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) para obter mais informações.<br /> **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_transform_noise_words_on**|**bit**|Indica se palavras de ruído devem ser transformadas no banco de dados independente.<br /> 0 = palavras de ruído não devem ser transformadas.<br /> 1 = palavras de ruído devem ser transformadas.<br /> **Observação** funciona como o [opção de configuração de servidor transform noise words](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md) de **sp_configure**. Esse valor é **nulo** para um banco de dados dependente. Ver [sys. Configurations &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) para obter mais informações.<br /> **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|**two_digit_year_cutoff**|**smallint**|Indica um valor de um número entre 1753 e 9999 para representar o ano de corte para interpretar anos com dois dígitos como anos de quatro dígitos.<br /> **Observação** funciona como o [configurar o ano de dois dígitos cutoff Server Configuration Option](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) de **sp_configure**. Esse valor é **nulo** para um banco de dados dependente. Ver [sys. Configurations &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) para obter mais informações.<br /> **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**containment**|**tinyint não nulo**|Indica o status de contenção do banco de dados.<br />  0 = a contenção do banco de dados está desativada. **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 1 = banco de dados está em contenção parcial **aplica-se ao**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|**containment_desc**|**nvarchar(60) não nulo**|Indica o status de contenção do banco de dados.<br /> NONE = banco de dados herdado (contenção zero)<br /> PARCIAL = banco de dados parcialmente independente<br /> **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**target_recovery_time_in_seconds**|**int**|A hora estimada para recuperar o banco de dados, em segundos. Anulável.<br /> **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**delayed_durability**|**int**|A configuração de durabilidade atrasada:<br /> 0 = DESABILITADO<br /> 1 = PERMITIDO<br /> 2 = FORÇADO<br /> Para obter mais informações, veja [Controlar a durabilidade da transação](../../relational-databases/logs/control-transaction-durability.md).<br /> **Aplica-se ao**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] por meio [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
|**delayed_durability_desc**|**nvarchar(60)**|A configuração de durabilidade atrasada:<br /> DISABLED<br /> ALLOWED<br /> FORCED<br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**is_memory_optimized_elevate_to_snapshot_on**|**bit**|As tabelas com otimização de memória são acessadas usando o isolamento SNAPSHOT quando a configuração de sessão TRANSACTION ISOLATION LEVEL é definida como um nível de isolamento inferior, READ COMMITTED ou READ UNCOMMITTED.<br /> 1 = O nível de isolamento mínimo SNAPSHOT.<br /> 0 = O nível de isolamento não é elevado.|  
|**is_federation_member**|**bit**|Indica se o banco de dados é membro de uma federação.<br /> **Aplica-se ao**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_remote_data_archive_enabled**|**bit**|Indica se o banco de dados está sendo estendido.<br /> 0 = o banco de dados não está habilitado para Stretch.<br /> 1 = o banco de dados está habilitado para Stretch.<br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> Para obter mais informações, consulte [Stretch Database](../../sql-server/stretch-database/stretch-database.md).|  
|**is_mixed_page_allocation_on**|**bit**|Indica se tabelas e índices no banco de dados podem alocar páginas iniciais de extensões mistas.<br /> 0 = tabelas e índices no banco de dados sempre alocar páginas iniciais de extensões uniformes.<br /> 1 = tabelas e índices no banco de dados podem alocar páginas iniciais de extensões mistas.<br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> Para obter mais informações, consulte a opção SET MIXED_PAGE_ALLOCATION de [opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).|  
|**is_temporal_retention_enabled**|**bit**|Indica se a tarefa de limpeza de política de retenção temporal está habilitada.<br /> **Aplica-se a**: banco de dados SQL do Azure|
|**catalog_collation_type**|**int**|A configuração de agrupamento de catálogo:<br />0 = DATABASE_DEFAULT<br />2 = SQL_Latin_1_General_CP1_CI_AS<br /> **Aplica-se a**: banco de dados SQL do Azure|
|**catalog_collation_type_desc**|**nvarchar(60)**|A configuração de agrupamento de catálogo:<br />DATABASE_DEFAULT<br />SQL_Latin_1_General_CP1_CI_AS<br /> **Aplica-se a**: banco de dados SQL do Azure|
  
## <a name="permissions"></a>Permissões  
 Se o chamador de `sys.databases` não for o proprietário do banco de dados e o banco de dados não é `master` ou `tempdb`, as permissões mínimas necessárias para ver a linha correspondente serão `ALTER ANY DATABASE` ou o `VIEW ANY DATABASE` permissão de nível de servidor, ou `CREATE DATABASE` permissão no `master` banco de dados. O banco de dados ao qual o chamador está conectado sempre pode ser exibido em `sys.databases`.  
  
> [!IMPORTANT]  
>  Por padrão, a função pública tem o `VIEW ANY DATABASE` permissão, permitindo que todos os logons vejam informações do banco de dados. Para impedir que um logon da capacidade de detectar um banco de dados `REVOKE` as `VIEW ANY DATABASE` permissão de `public`, ou `DENY` a ' a permissão VIEW ANY DATABASE para logons individuais.  
  
## <a name="includesssdsincludessssds-mdmd-remarks"></a>[!INCLUDE[ssSDS](../../includes/sssds-md.md)] Comentários  
 Na [!INCLUDE[ssSDS](../../includes/sssds-md.md)], essa exibição está disponível no `master` banco de dados e em bancos de dados do usuário. No `master` banco de dados, essa exibição retorna as informações sobre o `master` banco de dados e todos os bancos de dados de usuário no servidor. Em um banco de dados de usuário, essa exibição retorna informações apenas sobre o banco de dados atual e o banco de dados mestre.  
  
 Use a exibição de `sys.databases` no banco de dados `master` do servidor de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] em que o novo banco de dados está sendo criado. Depois que a cópia de banco de dados é iniciado, você pode consultar a `sys.databases` e o `sys.dm_database_copies` exibições do `master` banco de dados do servidor de destino para recuperar mais informações sobre o andamento da cópia.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-query-the-sysdatabases-view"></a>A. Consultar a exibição do sys.databases  
 O exemplo a seguir retorna algumas das colunas disponíveis no `sys.databases` modo de exibição.  
  
```  
SELECT name, user_access_desc, is_read_only, state_desc, recovery_model_desc  
FROM sys.databases;  
```  
  
### <a name="b-check-the-copying-status-in-includesssdsincludessssds-mdmd"></a>B. Verificar o status de cópia em [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
 A exemplo a seguir consulta a `sys.databases` e `sys.dm_database_copies` operação de cópia de modos de exibição para retornar informações sobre um banco de dados.  
  
**Aplica-se a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
  
```  
-- Execute from the master database.  
SELECT a.name, a.state_desc, b.start_date, b.modify_date, b.percentage_complete  
FROM sys.databases AS a  
INNER JOIN sys.dm_database_copies AS b ON a.database_id = b.database_id  
WHERE a.state = 7;  
```  
### <a name="c-check-the-temporal-retention-policy-status-in-includesssdsincludessssds-mdmd"></a>C. Verifique o status da política de retenção temporal em [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
 A exemplo a seguir consulta o `sys.databases` para retornar informações se a tarefa de limpeza de retenção temporal está habilitada. Lembre-se de que, após a operação de restauração retenção temporal é desabilitada por padrão. Use `ALTER DATABASE` para habilitá-lo explicitamente.
  
**Aplica-se ao**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
```  
-- Execute from the master database.  
SELECT a.name, a.is_temporal_history_retention_enabled 
FROM sys.databases AS a;
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [sys. database_recovery_status &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-recovery-status-transact-sql.md)   
 [Exibição de catálogo do bancos de dados e de arquivos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [sys.dm_database_copies &#40;Banco de Dados SQL do Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)  
  
  
