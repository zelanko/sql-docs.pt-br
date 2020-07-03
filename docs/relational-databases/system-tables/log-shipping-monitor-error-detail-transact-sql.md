---
title: log_shipping_monitor_error_detail (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_error_detail_TSQL
- log_shipping_monitor_error_detail
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_error_detail system table
ms.assetid: 0c38a625-60d2-4ee2-bcf3-2ba367914220
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1abbc89dcd085d65f2b44aab54d731f17184b9a7
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890185"
---
# <a name="log_shipping_monitor_error_detail-transact-sql"></a>log_shipping_monitor_error_detail (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Armazena detalhes de erros para trabalhos de envio de logs. Essa tabela é armazenada no banco de dados **msdb** .  
  
 As tabelas relacionadas ao histórico e monitoramento também são usadas no servidor primário e nos servidores secundários.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**agent_id**|**uniqueidentifier**|A ID primária para backup ou ID secundária para cópia ou restauração.|  
|**agent_type**|**tinyint**|O tipo de trabalho de envio de log.<br /><br /> 0 = Backup.<br /><br /> 1 = Cópia.<br /><br /> 2 = restaurar.|  
|**session_id**|**int**|A ID da sessão para o trabalho de backup/cópia/restauração.|  
|**database_name**|**sysname**|O nome do banco de dados associado com este registro de erro. Banco de dados primário para backup, banco de dados secundário para restauração ou vazio para cópia.|  
|**sequence_number**|**int**|Um número incremental que indica a ordem correta das informações de erros que abrangem vários registros.|  
|**log_time**|**datetime**|A data e hora em que o registro foi criado.|  
|**log_time_utc**|**datetime**|A data e hora em que o registro foi criado, expressa em Tempo Universal Coordenado.|  
|**message**|**nvarchar**|Texto de mensagem.|  
|**source**|**nvarchar**|A fonte da mensagem de erro ou do evento.|  
|**help_url**|**nvarchar**|A URL, se disponível, onde encontrar mais informações sobre o erro.|  
  
## <a name="remarks"></a>Comentários  
 Esta tabela contém detalhe de erro para os agentes de envio de logs. Cada erro é registrado como uma sequência de exceções. Pode haver vários erros (sequências) para cada sessão do agente.  
  
 Além de serem armazenados no servidor de monitor remoto, as informações relacionadas ao servidor primário são armazenadas no servidor primário em sua tabela de **log_shipping_monitor_error_detail** , e as informações relacionadas a um servidor secundário também são armazenadas no servidor secundário em sua tabela de **log_shipping_monitor_error_detail** .  
  
 Para identificar uma sessão de agente, use as colunas **agent_id**, **agent_type**e **session_id**. Classifique por **log_time** para ver os erros na ordem em que foram registrados.  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [&#41;&#40;Transact-SQL de log_shipping_monitor_history_detail](../../relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql.md)   
 [sp_cleanup_log_shipping_history &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_log_shipping_primary_database](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_refresh_log_shipping_monitor](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
