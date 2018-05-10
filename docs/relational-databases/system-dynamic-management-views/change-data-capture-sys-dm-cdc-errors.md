---
title: sys.dm_cdc_errors (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_cdc_errors_TSQL
- dm_cdc_errors
- sys.dm_cdc_errors
- sys.dm_cdc_errors_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cdc_errors dynamic management view
- change data capture [SQL Server], error reporting
ms.assetid: 898f2d76-9e63-45ef-94da-8034e86004ab
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2b12ebd0edae5efc061ce49ed7d2986f6710c775
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
---
# <a name="change-data-capture---sysdmcdcerrors"></a>Change Data Capture - sys.DM cdc_errors
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada erro encontrado durante a sessão de verificação de log do Change Data Capture.  
 
 
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**Int**|ID da sessão.<br /><br /> 0 = o erro não ocorreu em uma sessão de verificação de log.|  
|**phase_number**|**Int**|Número que indica a fase em que a sessão estava no momento em que o erro ocorreu. Para obter uma descrição de cada fase, consulte [cdc_log_scan_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md).|  
|**entry_time**|**datetime**|A data e hora em que o erro foi registrado. Esse valor corresponde ao carimbo de data/hora no log de erros do SQL.|  
|**error_number**|**Int**|A identificação da mensagem de erro.|  
|**error_severity**|**Int**|O nível de severidade da mensagem, entre 1 e 25.|  
|**error_state**|**Int**|Número de estado do erro.|  
|**error_message**|**nvarchar(1024)**|Texto da mensagem do erro.|  
|**start_lsn**|**nvarchar(23)**|Valor LSN de início das linhas sendo processadas quando o erro ocorreu.<br /><br /> 0 = o erro não ocorreu em uma sessão de verificação de log.|  
|**begin_lsn**|**nvarchar(23)**|Valor LSN de início da transação sendo processada quando o erro ocorreu.<br /><br /> 0 = o erro não ocorreu em uma sessão de verificação de log.|  
|**sequence_value**|**nvarchar(23)**|Valor LSN das linhas sendo processadas quando o erro ocorreu.<br /><br /> 0 = o erro não ocorreu em uma sessão de verificação de log.|  
  
## <a name="remarks"></a>Remarks  
 **sys.DM cdc_errors** contém informações de erro para 32 sessões anteriores.  
  
## <a name="permissions"></a>Permissões  
 Requer permissão VIEW DATABASE STATE para consultar o **sys.DM cdc_errors** exibição de gerenciamento dinâmico. Para obter mais informações sobre permissões sobre exibições de gerenciamento dinâmico, consulte [funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="see-also"></a>Consulte também  
 [sys.dm_cdc_log_scan_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md)   
 [sys.dm_repl_traninfo &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-repl-traninfo-transact-sql.md)  
  
  

