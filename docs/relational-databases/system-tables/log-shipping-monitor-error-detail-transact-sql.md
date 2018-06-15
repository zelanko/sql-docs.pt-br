---
title: log_shipping_monitor_error_detail (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_error_detail_TSQL
- log_shipping_monitor_error_detail
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_error_detail system table
ms.assetid: 0c38a625-60d2-4ee2-bcf3-2ba367914220
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c7c41916a3ce32eacc974debb2a82e6c24a2c41a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33261595"
---
# <a name="logshippingmonitorerrordetail-transact-sql"></a>log_shipping_monitor_error_detail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Armazena detalhes de erros para trabalhos de envio de logs. Essa tabela é armazenada no **msdb** banco de dados.  
  
 As tabelas relacionadas ao histórico e monitoramento também são usadas no servidor primário e nos servidores secundários.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**uniqueidentifier**|A ID primária para backup ou ID secundária para cópia ou restauração.|  
|**agent_type**|**tinyint**|O tipo de trabalho de envio de log.<br /><br /> 0 = Backup.<br /><br /> 1 = Cópia.<br /><br /> 2 = restaurar.|  
|**session_id**|**Int**|A ID da sessão para o trabalho de backup/cópia/restauração.|  
|**database_name**|**sysname**|O nome do banco de dados associado com este registro de erro. Banco de dados primário para backup, banco de dados secundário para restauração ou vazio para cópia.|  
|**sequence_number**|**Int**|Um número incremental que indica a ordem correta das informações de erros que abrangem vários registros.|  
|**log_time**|**datetime**|A data e hora em que o registro foi criado.|  
|**log_time_utc**|**datetime**|A data e hora em que o registro foi criado, expressa em Tempo Universal Coordenado.|  
|**message**|**nvarchar**|Texto de mensagem.|  
|**origem**|**nvarchar**|A fonte da mensagem de erro ou do evento.|  
|**help_url**|**nvarchar**|A URL, se disponível, onde encontrar mais informações sobre o erro.|  
  
## <a name="remarks"></a>Remarks  
 Esta tabela contém detalhe de erro para os agentes de envio de logs. Cada erro é registrado como uma sequência de exceções. Pode haver vários erros (sequências) para cada sessão do agente.  
  
 Além de serem armazenadas no servidor monitor remoto, as informações relacionadas ao servidor primário são armazenadas no servidor primário em seu **log_shipping_monitor_error_detail** tabela e informações relacionadas a um servidor secundário também é armazenado no servidor secundário em seu **log_shipping_monitor_error_detail** tabela.  
  
 Para identificar uma sessão de agente, use colunas **agent_id**, **agent_type**, e **session_id**. Classificar por **log_time** para ver os erros na ordem em que eles foram registrados.  
  
## <a name="see-also"></a>Consulte também  
 [Sobre o envio de logs & #40; SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [log_shipping_monitor_history_detail &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql.md)   
 [sp_cleanup_log_shipping_history &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [sp_delete_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
