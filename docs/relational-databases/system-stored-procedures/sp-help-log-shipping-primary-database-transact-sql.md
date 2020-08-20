---
description: sp_help_log_shipping_primary_database (Transact-SQL)
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
ms.openlocfilehash: b3dea602c3464fb4fee36281a2430f2fef39b7ec
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493189"
---
# <a name="sp_help_log_shipping_primary_database-transact-sql"></a>sp_help_log_shipping_primary_database (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Recupera as configurações do banco de dados primário.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_log_shipping_primary_database  
[ @database = ] 'database' OR  
[ @primary_id = ] 'primary_id'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @database = ] 'database'` É o nome do banco de dados primário de envio de logs. o *banco de dados* é **sysname**, sem padrão, e não pode ser nulo.  
  
`[ @primary_id = ] 'primary_id'` A ID do banco de dados primário para a configuração de envio de logs. *primary_id* é **uniqueidentifier** e não pode ser NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Descrição|  
|-----------------|-----------------|  
|**primary_id**|A ID do banco de dados primário para a configuração de envio de log.|  
|**primary_database**|O nome do banco de dados primário na configuração de envio de log.|  
|**backup_directory**|O diretório onde os arquivos de backup de log de transações do servidor primário são armazenados.|  
|**backup_share**|A rede ou o caminho UNC para o diretório de backup.|  
|**backup_retention_period**|A quantidade de tempo, em minutos, que um arquivo de backup log é retido no diretório de backups antes de ser excluído.|  
|**backup_compression**|Indica se a configuração de envio de logs usa [compactação de backup](../../relational-databases/backup-restore/backup-compression-sql-server.md).<br /><br /> **0** = desabilitado. Nunca compacte backups de log.<br /><br /> **1** = habilitado. Sempre compacte backups de log.<br /><br /> **2** = usar a configuração da [exibição ou configurar a opção de configuração de servidor de compactação de backup padrão](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md). Este é o valor padrão.<br /><br /> A compactação de backup é suportada somente no [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (ou em uma versão posterior). Em outras edições, o valor é sempre 2.|  
|**backup_job_id**|A ID de trabalho do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent associada ao trabalho de backup no servidor primário.|  
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
 **sp_help_log_shipping_primary_database** deve ser executado do banco de dados **mestre** no servidor primário.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo ilustra o uso de **sp_help_log_shipping_primary_database** para recuperar as configurações de banco de dados primário do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
```  
EXEC master.dbo.sp_help_log_shipping_primary_database @database=N'AdventureWorks2012';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
