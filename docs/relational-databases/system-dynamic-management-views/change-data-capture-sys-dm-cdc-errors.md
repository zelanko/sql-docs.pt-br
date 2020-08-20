---
description: Captura de dados de alterações-sys. dm_cdc_errors
title: sys. dm_cdc_errors (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b34623ac9b7732faff5b1f29e6a154dddf79dd78
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482021"
---
# <a name="change-data-capture---sysdm_cdc_errors"></a>Captura de dados de alterações-sys. dm_cdc_errors
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada erro encontrado durante a sessão de verificação de log do Change Data Capture.  
 
 
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|ID da sessão.<br /><br /> 0 = o erro não ocorreu em uma sessão de verificação de log.|  
|**phase_number**|**int**|Número que indica a fase em que a sessão estava no momento em que o erro ocorreu. Para obter uma descrição de cada fase, consulte [Sys. dm_cdc_log_scan_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md).|  
|**entry_time**|**datetime**|A data e hora em que o erro foi registrado. Esse valor corresponde ao carimbo de data/hora no log de erros do SQL.|  
|**error_number**|**int**|A identificação da mensagem de erro.|  
|**error_severity**|**int**|O nível de severidade da mensagem, entre 1 e 25.|  
|**error_state**|**int**|Número de estado do erro.|  
|**error_message**|**nvarchar(1024)**|Texto da mensagem do erro.|  
|**start_lsn**|**nvarchar (23)**|Valor LSN de início das linhas sendo processadas quando o erro ocorreu.<br /><br /> 0 = o erro não ocorreu em uma sessão de verificação de log.|  
|**begin_lsn**|**nvarchar (23)**|Valor LSN de início da transação sendo processada quando o erro ocorreu.<br /><br /> 0 = o erro não ocorreu em uma sessão de verificação de log.|  
|**sequence_value**|**nvarchar (23)**|Valor LSN das linhas sendo processadas quando o erro ocorreu.<br /><br /> 0 = o erro não ocorreu em uma sessão de verificação de log.|  
  
## <a name="remarks"></a>Comentários  
 **Sys. dm_cdc_errors** contém informações de erro para as sessões 32 anteriores.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE para consultar a exibição de gerenciamento dinâmico **Sys. dm_cdc_errors** . Para obter mais informações sobre permissões em exibições de gerenciamento dinâmico, consulte [funções e exibições de gerenciamento dinâmico &#40;&#41;Transact-SQL ](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="see-also"></a>Consulte Também  
 [sys. dm_cdc_log_scan_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md)   
 [sys. dm_repl_traninfo &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-repl-traninfo-transact-sql.md)  
  
  

