---
title: log_shipping_monitor_secondary (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_secondary_TSQL
- log_shipping_monitor_secondary
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_secondary system table
ms.assetid: afbe1bb7-89a7-4020-9408-0af64a043c2e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 838c810c28c03ae11237f449483789ed8dbbf740
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67989951"
---
# <a name="log_shipping_monitor_secondary-transact-sql"></a>log_shipping_monitor_secondary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Armazena um registro de monitor por banco de dados secundário em uma configuração de envio de logs. Essa tabela é armazenada no banco de dados **msdb** .  
  
 As tabelas relacionadas ao histórico e monitoramento também são usadas no servidor primário e nos servidores secundários.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**secondary_server**|**sysname**|O nome da instância secundária do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] na configuração de envio de logs.|  
|**secondary_database**|**sysname**|Nome do banco de dados secundário na configuração de envio de logs.|  
|**secondary_id**|**uniqueidentifier**|ID de servidor secundário na configuração de envio de logs.|  
|**primary_server**|**sysname**|Nome da instância primária do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] na configuração de envio de logs.|  
|**primary_database**|**sysname**|O nome do banco de dados primário na configuração de envio de log.|  
|**restore_threshold**|**int**|Número de minutos permitidos a decorrer entre operações de restauração antes que um alerta seja gerado.|  
|**threshold_alert**|**int**|Alerta a ser emitido quando o limite da restauração for excedido.|  
|**threshold_alert_enabled**|**bit**|Determina se os alertas de limite de restauração estão habilitados. 1 = Habilitado.<br /><br /> 0 = Desabilitado.|  
|**last_copied_file**|**nvarchar (500)**|O nome do último arquivo de backup copiado para o servidor secundário.|  
|**last_copied_date**|**datetime**|A hora e a data da última operação de cópia para o servidor secundário.|  
|**last_copied_date_utc**|**datetime**|Hora e data da última operação de cópia no servidor secundário, expressa em UTC (Coordinated Universal Time).|  
|**last_restored_file**|**nvarchar (500)**|Nome do último arquivo de backup restaurado no banco de dados secundário.|  
|**last_restored_date**|**datetime**|Hora e data da última operação de restauração no banco de dados secundário.|  
|**last_restored_date_utc**|**datetime**|Hora e data da última operação de restauração no banco de dados secundário, expressa em UTC (Coordinated Universal Time).|  
|**last_restored_latency**|**int**|Período em minutos decorrido entre o momento de criação do backup de log no primário e o momento em que ele foi restaurado no secundário.<br /><br /> O valor inicial é NULL.|  
|**history_retention_period**|**int**|O período em minutos em que os registros de histórico de envio de logs são retidos em um determinado banco de dados secundário antes de serem excluídos.|  
  
## <a name="remarks"></a>Comentários  
 Além de serem armazenados no servidor de monitor remoto, e as informações relacionadas a um servidor secundário também são armazenadas no servidor secundário em sua tabela de **log_shipping_monitor_secondary** .  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [&#41;&#40;Transact-SQL de sp_refresh_log_shipping_monitor](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_add_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_change_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-database-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_log_shipping_monitor_secondary](../../relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-secondary-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_refresh_log_shipping_monitor](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [Tabelas do sistema &#40;&#41;Transact-SQL](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
