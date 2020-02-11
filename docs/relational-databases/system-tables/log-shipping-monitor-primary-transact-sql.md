---
title: log_shipping_monitor_primary (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_primary
- log_shipping_monitor_primary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_primary system table
ms.assetid: 5f629a29-1a62-40e6-ae33-6f6b7dd09a36
author: stevestein
ms.author: sstein
ms.openlocfilehash: d39ea859f1fd2cc3064d8d8c71c91ba6324f162c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67989980"
---
# <a name="log_shipping_monitor_primary-transact-sql"></a>log_shipping_monitor_primary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Armazena um registro de monitor por banco de dados primário em cada configuração de envio de logs. Essa tabela é armazenada no banco de dados **msdb** .  
  
 As tabelas relacionadas ao histórico e monitoramento também são usadas no servidor primário e nos servidores secundários.   
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**primary_id**|**uniqueidentifier**|A ID do banco de dados primário para a configuração de envio de log.|  
|**primary_server**|**sysname**|Nome da instância primária do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] na configuração de envio de logs.|  
|**primary_database**|**sysname**|O nome do banco de dados primário na configuração de envio de log.|  
|**backup_threshold**|**int**|O número de minutos permitidos a decorrer entre operações de backup antes que um alerta seja gerado.|  
|**threshold_alert**|**int**|O alerta a ser emitido quando o limite do backup for excedido.|  
|**threshold_alert_enabled**|**bit**|Determina se os alertas de limite de backup foram habilitados. 1 = Habilitado.<br /><br /> 0 = Desabilitado.|  
|**last_backup_file**|**nvarchar (500)**|O caminho absoluto de backup de log de transações mais recente.|  
|**last_backup_date**|**datetime**|A hora e data da última operação de backup de log de transações no banco de dados primário.|  
|**last_backup_date_utc**|**datetime**|A hora e data da última operação de backup de log de transação no banco de dados primário, expressas no Tempo Universal Coordenado.|  
|**history_retention_period**|**int**|A quantidade de tempo, em minutos, que os registros do histórico do envio de log são mantidos para um determinado banco de dados primário antes de serem excluídos.|  
  
## <a name="remarks"></a>Comentários  
 Além de serem armazenados no servidor de monitor remoto, as informações relacionadas ao servidor primário são armazenadas no servidor primário em sua tabela de **log_shipping_monitor_primary** .  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [&#41;&#40;Transact-SQL de sp_add_log_shipping_primary_database](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_change_log_shipping_primary_database](../../relational-databases/system-stored-procedures/sp-change-log-shipping-primary-database-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_log_shipping_primary_database](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_log_shipping_primary_database](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_refresh_log_shipping_monitor](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_log_shipping_monitor_primary](../../relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-primary-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_log_shipping_alert_job](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-alert-job-transact-sql.md)   
 [Tabelas do sistema &#40;&#41;Transact-SQL](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
