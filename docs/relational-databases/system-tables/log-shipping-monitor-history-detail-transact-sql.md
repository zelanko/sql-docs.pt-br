---
title: log_shipping_monitor_history_detail (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_history_detail_TSQL
- log_shipping_monitor_history_detail
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_history_detail system table
ms.assetid: 7080c888-323b-4206-a1ab-e6c51f9e2579
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f8968661442adabe4c04608ca5a5bb5362341c4b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47804104"
---
# <a name="logshippingmonitorhistorydetail-transact-sql"></a>log_shipping_monitor_history_detail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Armazena detalhes de histórico para trabalhos de envio de logs. Essa tabela é armazenada na **msdb** banco de dados.  
  
 As tabelas relacionadas ao histórico e monitoramento também são usadas no servidor primário e nos servidores secundários.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**uniqueidentifier**|A ID primária para backup ou ID secundária para cópia ou restauração.|  
|**agent_type**|**tinyint**|O tipo de trabalho de envio de log.<br /><br /> 0 = Backup.<br /><br /> 1 = Cópia.<br /><br /> 2 = restauração.|  
|**session_id**|**int**|A ID da sessão para o trabalho de backup/cópia/restauração.|  
|**database_name**|**sysname**|O nome do banco de dados associado a esse registro. Banco de dados primário para backup, banco de dados secundário para restauração ou vazio para cópia.|  
|**session_status**|**tinyint**|O status da sessão.<br /><br /> 0 = Iniciando.<br /><br /> 1 = Executando.<br /><br /> 2 = Sucesso.<br /><br /> 3 = Erro.<br /><br /> 4 = Aviso.|  
|**log_time**|**datetime**|A data e hora em que o registro foi criado.|  
|**log_time_utc**|**datetime**|A data e hora em que o registro foi criado, expressa em Tempo Universal Coordenado.|  
|**message**|**nvarchar(max)**|Texto de mensagem.|  
  
## <a name="remarks"></a>Comentários  
 Essa tabela contém detalhes de histórico para os agentes de envio de logs. Para identificar uma sessão de agente, use colunas **agent_id**, **agent_type**, e **session_id**. Para ver os detalhes de histórico para a sessão do agente, classificar por **log_time**.  
  
 Além de serem armazenadas no servidor monitor remoto, as informações relacionadas ao servidor primário são armazenadas no servidor primário em seu **log_shipping_monitor_history_detail** tabela e informações relacionadas para um secundário servidor também é armazenado no servidor secundário em sua **log_shipping_monitor_history_detail** tabela.  
  
## <a name="see-also"></a>Consulte também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_delete_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_cleanup_log_shipping_history &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)   
 [log_shipping_monitor_error_detail &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql.md)  
  
  
