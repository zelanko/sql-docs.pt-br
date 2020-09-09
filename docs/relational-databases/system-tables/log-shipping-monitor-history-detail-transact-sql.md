---
description: log_shipping_monitor_history_detail (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 515a2b38f10beca9c4797ce02d48387bfa662707
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544522"
---
# <a name="log_shipping_monitor_history_detail-transact-sql"></a>log_shipping_monitor_history_detail (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Armazena detalhes de histórico para trabalhos de envio de logs. Essa tabela é armazenada no banco de dados **msdb** .  
  
 As tabelas relacionadas ao histórico e monitoramento também são usadas no servidor primário e nos servidores secundários.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**agent_id**|**uniqueidentifier**|A ID primária para backup ou ID secundária para cópia ou restauração.|  
|**agent_type**|**tinyint**|O tipo de trabalho de envio de log.<br /><br /> 0 = Backup.<br /><br /> 1 = Cópia.<br /><br /> 2 = restaurar.|  
|**session_id**|**int**|A ID da sessão para o trabalho de backup/cópia/restauração.|  
|**database_name**|**sysname**|O nome do banco de dados associado a esse registro. Banco de dados primário para backup, banco de dados secundário para restauração ou vazio para cópia.|  
|**session_status**|**tinyint**|O status da sessão.<br /><br /> 0 = Iniciando.<br /><br /> 1 = Executando.<br /><br /> 2 = Sucesso.<br /><br /> 3 = Erro.<br /><br /> 4 = Aviso.|  
|**log_time**|**datetime**|A data e hora em que o registro foi criado.|  
|**log_time_utc**|**datetime**|A data e hora em que o registro foi criado, expressa em Tempo Universal Coordenado.|  
|**message**|**nvarchar(max)**|Texto de mensagem.|  
  
## <a name="remarks"></a>Comentários  
 Essa tabela contém detalhes de histórico para os agentes de envio de logs. Para identificar uma sessão de agente, use as colunas **agent_id**, **agent_type**e **session_id**. Para ver os detalhes do histórico da sessão do agente, classifique por **log_time**.  
  
 Além de serem armazenados no servidor de monitor remoto, as informações relacionadas ao servidor primário são armazenadas no servidor primário em sua tabela de **log_shipping_monitor_history_detail** , e as informações relacionadas a um servidor secundário também são armazenadas no servidor secundário em sua tabela de **log_shipping_monitor_history_detail** .  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [&#41;&#40;Transact-SQL de sp_delete_log_shipping_primary_database ](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_cleanup_log_shipping_history &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_refresh_log_shipping_monitor ](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_log_shipping_secondary_database ](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [Tabelas do sistema &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/system-tables-transact-sql.md)   
 [&#41;&#40;Transact-SQL de log_shipping_monitor_error_detail ](../../relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql.md)  
  
  
