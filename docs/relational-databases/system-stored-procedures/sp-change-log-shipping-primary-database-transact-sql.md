---
title: sp_change_log_shipping_primary_database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_primary_database
- sp_change_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_primary_database
ms.assetid: 8c9dce6b-d2a3-4ca7-a832-8f59a5adb214
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 02ba9c11d9c74daa6cc88051ada7037edc16f35b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85715930"
---
# <a name="sp_change_log_shipping_primary_database-transact-sql"></a>sp_change_log_shipping_primary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Altera as configurações do banco de dados primário.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_change_log_shipping_primary_database [ @database = ] 'database'  
[, [ @backup_directory = ] 'backup_directory']   
[, [ @backup_share = ] 'backup_share']   
[, [ @backup_retention_period = ] 'backup_retention_period']  
[, [ @monitor_server_security_mode = ] 'monitor_server_security_mode']  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
[, [ @backup_threshold = ] 'backup_threshold']   
[, [ @threshold_alert = ] 'threshold_alert']   
[, [ @threshold_alert_enabled = ] 'threshold_alert_enabled']   
[, [ @history_retention_period = ] 'history_retention_period']  
[, [ @backup_compression = ] backup_compression_option ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @database = ] 'database'`É o nome do banco de dados no servidor primário. *primary_database* é **sysname**, sem padrão.  
  
`[ @backup_directory = ] 'backup_directory'`É o caminho para a pasta de backup no servidor primário. *backup_directory* é **nvarchar (500)**, sem padrão, e não pode ser NULL.  
  
`[ @backup_share = ] 'backup_share'`É o caminho de rede para o diretório de backup no servidor primário. *backup_share* é **nvarchar (500)**, sem padrão, e não pode ser NULL.  
  
`[ @backup_retention_period = ] 'backup_retention_period'`É o período de tempo, em minutos, para reter o arquivo de backup de log no diretório de backup no servidor primário. *backup_retention_period* é **int**, sem padrão, e não pode ser NULL.  
  
`[ @monitor_server_security_mode = ] 'monitor_server_security_mode'`O modo de segurança usado para se conectar ao servidor monitor.  
  
 1 = Autenticação do Windows.  
  
 0 = Autenticação do SQL Server.  
  
 *monitor_server_security_mode* é **bit** e não pode ser nulo.  
  
`[ @monitor_server_login = ] 'monitor_server_login'`É o nome de usuário da conta usada para acessar o servidor monitor.  
  
`[ @monitor_server_password = ] 'monitor_server_password'`É a senha da conta usada para acessar o servidor monitor.  
  
`[ @backup_threshold = ] 'backup_threshold'`É o período de tempo, em minutos, após o último backup antes que um erro de *threshold_alert* seja gerado. *backup_threshold* é **int**, com um padrão de 60 minutos.  
  
`[ @threshold_alert = ] 'threshold_alert'`O alerta a ser gerado quando o limite de backup for excedido. *threshold_alert* é **int** e não pode ser NULL.  
  
`[ @threshold_alert_enabled = ] 'threshold_alert_enabled'`Especifica se um alerta é gerado quando *backup_threshold* é excedido.  
  
 1 = habilitado.  
  
 0 = desabilitado.  
  
 *threshold_alert_enabled* é **bit** e não pode ser nulo.  
  
`[ @history_retention_period = ] 'history_retention_period'`É o período de tempo em minutos em que o histórico é retido. *history_retention_period* é **int**. Um valor de 14420 será usado se nenhum for especificado.  
  
`[ @backup_compression = ] backup_compression_option`Especifica se uma configuração de envio de logs usa [compactação de backup](../../relational-databases/backup-restore/backup-compression-sql-server.md). Este parâmetro é suportado somente no [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (ou em uma versão posterior).  
  
 0 = Desabilitado. Nunca compacte backups de log.  
  
 1 = Habilitado. Sempre compacte backups de log.  
  
 2 = usar a configuração da [exibição ou configurar a opção de configuração de servidor de compactação de backup padrão](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md). Esse é o valor padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 **sp_change_log_shipping_primary_database** deve ser executado do banco de dados **mestre** no servidor primário. Esse procedimento armazenado faz o seguinte:  
  
1.  Altera as configurações no registro de **log_shipping_primary_database** , se necessário.  
  
2.  Altera o registro local em **log_shipping_monitor_primary** no servidor primário usando argumentos fornecidos, se necessário.  
  
3.  Se o servidor monitor for diferente do servidor primário, o registro de alterações no **log_shipping_monitor_primary** no servidor monitor usando argumentos fornecidos, se necessário.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo ilustra o uso de **sp_change_log_shipping_primary_database** para atualizar as configurações associadas ao banco de dados primário [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
```  
EXEC master.dbo.sp_change_log_shipping_primary_database   
 @database = N'AdventureWorks'   
, @backup_directory = N'c:\LogShipping'   
, @backup_share = N'\\tribeca\LogShipping'   
, @backup_retention_period = 1440   
, @backup_threshold = 60   
, @threshold_alert = 0   
, @threshold_alert_enabled = 1   
, @history_retention_period = 1440   
,@monitor_server_security_mode = 1  
,@backup_compression = 1;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [log_shipping_primary_databases &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md)  
  
  
