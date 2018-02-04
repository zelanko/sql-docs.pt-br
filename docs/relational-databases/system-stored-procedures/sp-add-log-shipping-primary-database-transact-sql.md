---
title: sp_add_log_shipping_primary_database (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_primary_database
- sp_add_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_primary_database
ms.assetid: 69531611-113f-46b5-81a6-7bf496d0353c
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 24a1158b85bc9c53070c0c6cd16f2b6b36dcfe92
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="spaddlogshippingprimarydatabase-transact-sql"></a>sp_add_log_shipping_primary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Instala o banco de dados primário para uma configuração de envio de log, incluindo o trabalho de backup, registro de monitor local e registro de monitor remoto.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_add_log_shipping_primary_database [ @database = ] 'database',   
[ @backup_directory = ] 'backup_directory',   
[ @backup_share = ] 'backup_share',   
[ @backup_job_name = ] 'backup_job_name',   
[, [ @backup_retention_period = ] backup_retention_period]  
[, [ @monitor_server = ] 'monitor_server']  
[, [ @monitor_server_security_mode = ] monitor_server_security_mode]  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
[, [ @backup_threshold = ] backup_threshold ]   
[, [ @threshold_alert = ] threshold_alert ]   
[, [ @threshold_alert_enabled = ] threshold_alert_enabled ]   
[, [ @history_retention_period = ] history_retention_period ]  
[, [ @backup_job_id = ] backup_job_id OUTPUT ]  
[, [ @primary_id = ] primary_id OUTPUT]  
[, [ @backup_compression = ] backup_compression_option ]  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@database=** ] '*banco de dados*'  
 É o nome do banco de dados primário de envio de logs. *banco de dados* é **sysname**, sem padrão, e não pode ser NULL.  
  
 [ **@backup_directory=** ] '*backup_directory*'  
 É o caminho para a pasta de backup no servidor primário. *backup_directory* é **nvarchar (500)**, sem padrão, e não pode ser NULL.  
  
 [ **@backup_share=** ] '*backup_share*'  
 É o caminho da rede para o diretório de backup no servidor primário. *backup_share* é **nvarchar (500)**, sem padrão, e não pode ser NULL.  
  
 [ **@backup_job_name=** ] '*backup_job_name*'  
 É o nome do trabalho do SQL Server Agent no servidor primário que copia o backup na pasta de backup. *backup_job_name* é **sysname** e não pode ser NULL.  
  
 [  **@backup_retention_period=** ] *backup_retention_period*  
 É o período de tempo, em minutos, para reter o arquivo de backup de logs no diretório de backup no servidor primário. *backup_retention_period* é **int**, sem padrão, e não pode ser NULL.  
  
 [ **@monitor_server=** ] '*monitor_server*'  
 É o nome do servidor monitor. *Monitor_server* é **sysname**, sem padrão, e não pode ser NULL.  
  
 [ **@monitor_server_security_mode=** ] *monitor_server_security_mode*  
 O modo de segurança usado para conexão ao servidor monitor.  
  
 1 = Autenticação do Windows.  
  
 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. *monitor_server_security_mode* é **bit** e não pode ser NULL.  
  
 [ **@monitor_server_login=** ] '*monitor_server_login*'  
 É o nome de usuário da conta usada para acessar o servidor monitor.  
  
 [ **@monitor_server_password=** ] '*monitor_server_password*'  
 Senha da conta usada para acessar o servidor monitor.  
  
 [ **@backup_threshold=** ] *backup_threshold*  
 É o período de tempo, em minutos, após o último backup antes de um *threshold_alert* erro será gerado. *backup_threshold* é **int**, com um padrão de 60 minutos.  
  
 [ **@threshold_alert=** ] *threshold_alert*  
 É o alerta a ser gerado quando o limite do backup for excedido. *threshold_alert* é **int**, com um padrão de 14.420.  
  
 [ **@threshold_alert_enabled=** ] *threshold_alert_enabled*  
 Especifica se um alerta será gerado quando *backup_threshold* for excedido. O valor zero (0), o padrão, significa que o alerta está desabilitado e não será aumentado. *threshold_alert_enabled* é **bit**.  
  
 [  **@history_retention_period=** ] *history_retention_period*  
 É a duração de tempo em minutos na qual o histórico será retido. *history_retention_period* é **int**, com um padrão NULL. Se nenhum valor for especificado, será usado o valor 14.420.  
  
 [  **@backup_job_id=** ] *backup_job_id* saída  
 A ID de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent associada ao trabalho de backup no servidor primário. *backup_job_id* é **uniqueidentifier** e não pode ser NULL.  
  
 [  **@primary_id=** ] *primary_id* saída  
 A ID do banco de dados primário para a configuração de envio de log. *primary_id* é **uniqueidentifier** e não pode ser NULL.  
  
 [ **@backup_compression**= ] *backup_compression_option*  
 Especifica se uma configuração de envio de log usa [compactação de backup](../../relational-databases/backup-restore/backup-compression-sql-server.md). Este parâmetro é suportado somente no [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (ou em uma versão posterior).  
  
 0 = Desabilitado. Nunca compacte backups de log.  
  
 1 = Habilitado. Sempre compacte backups de log.  
  
 2 = use a configuração do [exibir ou configurar a opção de configuração de servidor backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md). Este é o valor padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Remarks  
 **sp_add_log_shipping_primary_database** deve ser executado a partir de **mestre** banco de dados no servidor primário. Esse procedimento armazenado executa as seguintes funções:  
  
1.  Gera uma ID primária e adiciona uma entrada para o banco de dados primário na tabela **log_shipping_primary_databases** usando os argumentos fornecidos.  
  
2.  Cria um trabalho de backup para o banco de dados primário que está desabilitado.  
  
3.  Define a ID do trabalho de backup no **log_shipping_primary_databases** entrada para a ID do trabalho do trabalho de backup.  
  
4.  Adiciona um registro de monitor local na tabela **log_shipping_monitor_primary** no servidor primário usando os argumentos fornecidos.  
  
5.  Se o servidor monitor for diferente do servidor primário, adiciona um registro de monitor em **log_shipping_monitor_primary** no monitor de servidor usando os argumentos fornecidos.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função fixa de servidor pode executar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo adiciona o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] como banco de dados primário em uma configuração de envio de log.  
  
```  
DECLARE @LS_BackupJobId AS uniqueidentifier ;  
DECLARE @LS_PrimaryId AS uniqueidentifier ;  
  
EXEC master.dbo.sp_add_log_shipping_primary_database   
@database = N'AdventureWorks'   
,@backup_directory = N'c:\lsbackup'   
,@backup_share = N'\\tribeca\lsbackup'   
,@backup_job_name = N'LSBackup_AdventureWorks'   
,@backup_retention_period = 1440  
,@monitor_server = N'rockaway'   
,@monitor_server_security_mode = 1   
,@backup_threshold = 60   
,@threshold_alert = 0   
,@threshold_alert_enabled = 0   
,@history_retention_period = 1440   
,@backup_job_id = @LS_BackupJobId OUTPUT   
,@primary_id = @LS_PrimaryId OUTPUT   
,@overwrite = 1   
,@backup_compression = 0;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Sobre o envio de logs &#40; SQL Server &#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
