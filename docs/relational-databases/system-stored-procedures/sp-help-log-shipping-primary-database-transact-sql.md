---
title: sp_help_log_shipping_primary_database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_primary_database_TSQL
- sp_help_log_shipping_primary_database
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_primary_database
ms.assetid: e711b01c-ef29-4eb6-a016-0e647e337818
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 85d45de0ec858766bea51e983e80087d93d94ec2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47826624"
---
# <a name="sphelplogshippingprimarydatabase-transact-sql"></a>sp_help_log_shipping_primary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Recupera as configurações do banco de dados primário.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_log_shipping_primary_database  
[ @database = ] 'database' OR  
[ @primary_id = ] 'primary_id'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@database =** ] '*banco de dados*'  
 É o nome do banco de dados primário de envio de logs. *banco de dados* está **sysname**, sem padrão, e não pode ser NULL.  
  
 [  **@primary_id =** ] '*primary_id*'  
 A ID do banco de dados primário para a configuração de envio de log. *primary_id* está **uniqueidentifier** e não pode ser NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Description|  
|-----------------|-----------------|  
|**primary_id**|A ID do banco de dados primário para a configuração de envio de log.|  
|**primary_database**|O nome do banco de dados primário na configuração de envio de log.|  
|**backup_directory**|O diretório onde os arquivos de backup de log de transações do servidor primário são armazenados.|  
|**backup_share**|A rede ou o caminho UNC para o diretório de backup.|  
|**backup_retention_period**|A quantidade de tempo, em minutos, que um arquivo de backup log é retido no diretório de backups antes de ser excluído.|  
|**backup_compression**|Indica se a configuração de envio de logs usa [compactação de backup](../../relational-databases/backup-restore/backup-compression-sql-server.md).<br /><br /> **0** = desabilitado. Nunca compacte backups de log.<br /><br /> **1** = habilitado. Sempre compacte backups de log.<br /><br /> **2** = use a configuração do [exibir ou configurar a opção de configuração de servidor backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md). Este é o valor padrão.<br /><br /> A compactação de backup é suportada somente no [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (ou em uma versão posterior). Em outras edições, o valor é sempre 2.|  
|**backup_job_id**|O [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ID do agente de trabalho associado com o trabalho de backup no servidor primário.|  
|**monitor_server**|O nome da instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usado como servidor monitor na configuração de envio de log.|  
|**monitor_server_security_mode**|O modo de segurança usado para conexão ao servidor monitor.<br /><br /> 1 = Autenticação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.|  
|**backup_threshold**|O número de minutos permitidos a decorrer entre operações de backup antes que um alerta seja gerado.|  
|**threshold_alert**|O alerta a ser emitido quando o limite do backup for excedido.|  
|**threshold_alert_enabled**|Determina se os alertas de limite de backup foram habilitados.<br /><br /> **1** = habilitado.<br /><br /> **0** = desabilitado.|  
|**last_backup_file**|O caminho absoluto de backup de log de transações mais recente.|  
|**last_backup_date**|A hora e a data da última operação de backup de log.|  
|**last_backup_date_utc**|A hora e data da última operação de backup de log de transação no banco de dados primário, expressas no Tempo Universal Coordenado.|  
|**history_retention_period**|A quantidade de tempo, em minutos, que os registros do histórico do envio de log são mantidos para um determinado banco de dados primário antes de serem excluídos.|  
  
## <a name="remarks"></a>Comentários  
 **sp_help_log_shipping_primary_database** deve ser executado a partir de **mestre** banco de dados no servidor primário.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa pode executar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo ilustra o uso **sp_help_log_shipping_primary_database** recuperar as configurações de banco de dados primário para o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
EXEC master.dbo.sp_help_log_shipping_primary_database @database=N'AdventureWorks2012';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
