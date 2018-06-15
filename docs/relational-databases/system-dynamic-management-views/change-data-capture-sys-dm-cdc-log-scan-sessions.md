---
title: sys.dm_cdc_log_scan_sessions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_cdc_log_scan_sessions
- dm_cdc_log_scan_sessions_TSQL
- sys.dm_cdc_log_scan_sessions_TSQL
- sys.dm_cdc_log_scan_sessions
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], log scan reporting
- sys.dm_cdc_log_scan_sessions dynamic management view
ms.assetid: d337e9d0-78b1-4a07-8820-2027d0b9f87c
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 74a99cc08a030327c4f0b70f11c64f6c2a952dec
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34465992"
---
# <a name="change-data-capture---sysdmcdclogscansessions"></a>Change Data Capture - cdc_log_scan_sessions
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada sessão de verificação de log no banco de dados atual. A última linha retornada representa a sessão atual. Você pode usar esta exibição para retornar informações de status sobre a sessão de exame de log atual ou informações agregadas sobre todas as sessões desde que a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi iniciada pela última vez.  
   
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**Int**|ID da sessão.<br /><br /> 0 = os dados retornados nesta linha são uma agregação de todas as sessões como a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que foi iniciada por último.|  
|**start_time**|**datetime**|A hora em que a sessão foi iniciada.<br /><br /> Quando **session_id** = 0, a hora de início da coleta de dados agregados.|  
|**end_time**|**datetime**|A hora em que a sessão foi encerrada.<br /><br /> NULL = a sessão está ativa.<br /><br /> Quando **session_id** = 0, a hora a última sessão foi encerrada.|  
|**duration**|**bigint**|A duração da sessão em segundos.<br /><br /> 0 = a sessão não contém transações do Change Data Capture.<br /><br /> Quando **session_id** = 0, a soma da duração (em segundos) de todas as sessões com transações do change data capture.|  
|**scan_phase**|**nvarchar(200)**|A fase atual da sessão. Estes são os valores possíveis e suas descrições:<br /><br /> 1: configuração de leitura<br />2: verificação primeiro, a criação de tabela de hash<br />3: verificar segundo<br />4: verificação de segundo<br />5: verificar segundo<br />6: controle de versão de esquema<br />7: da última verificação<br />8: concluído<br /><br /> Quando **session_id** = 0, esse valor é sempre "Aggregate".|  
|**error_count**|**Int**|Número de erros encontrados.<br /><br /> Quando **session_id** = 0, o número total de erros em todas as sessões.|  
|**start_lsn**|**nvarchar(23)**|Iniciando LSN para a sessão.<br /><br /> Quando **session_id** = 0, o LSN inicial para a última sessão.|  
|**current_lsn**|**nvarchar(23)**|LSN atual sendo verificado.<br /><br /> Quando **session_id** = 0, o LSN atual é 0.|  
|**end_lsn**|**nvarchar(23)**|Encerrando LSN para a sessão.<br /><br /> NULL = a sessão está ativa.<br /><br /> Quando **session_id** = 0, o LSN final da última sessão.|  
|**tran_count**|**bigint**|Número de transações do Change Data Capture processadas. Este contador é populado na fase 2.<br /><br /> Quando **session_id** = 0, o número de transações processadas em todas as sessões.|  
|**last_commit_lsn**|**nvarchar(23)**|LSN do último registro de log de confirmação processado.<br /><br /> Quando **session_id** = 0, o último registro de log de confirmação LSN para qualquer sessão.|  
|**last_commit_time**|**datetime**|Hora em que o último registro de log de confirmação foi processado.<br /><br /> Quando **session_id** = 0, a hora em que a confirmação do último registro de log para qualquer sessão.|  
|**log_record_count**|**bigint**|Número de registros de log verificados.<br /><br /> Quando **session_id** = 0, o número de registros verificados para todas as sessões.|  
|**schema_change_count**|**Int**|Número de operações de linguagem de definição de dados (DDL) detectados. Este contador é populado na fase 6.<br /><br /> Quando **session_id** = 0, o número de operações DDL processadas em todas as sessões.|  
|**command_count**|**bigint**|Número de comandos processados.<br /><br /> Quando **session_id** = 0, o número de comandos processados em todas as sessões.|  
|**first_begin_cdc_lsn**|**nvarchar(23)**|Primeiro LSN que contém transações do Change Data Capture.<br /><br /> Quando **session_id** = 0, o primeiro LSN que contém transações do change data capture.|  
|**last_commit_cdc_lsn**|**nvarchar(23)**|LSN do último registro de log de confirmação que contém transações do Change Data Capture.<br /><br /> Quando **session_id** = 0, o último registro de log de confirmação LSN para qualquer sessão que continha transações do change data capture|  
|**last_commit_cdc_time**|**datetime**|Horário em que o último registro de log de confirmação foi processado que contém transações do Change Data Capture.<br /><br /> Quando **session_id** = 0, a hora em que o último log de confirmação registro para qualquer sessão que continha transações do change data capture.|  
|**Latência**|**Int**|A diferença, em segundos, entre **end_time** e **last_commit_cdc_time** na sessão. Este contador é populado no final da fase 7.<br /><br /> Quando **session_id** = 0, o último valor de latência diferente de zero registrado por uma sessão.|  
|**empty_scan_count**|**Int**|Número de sessões sucessivas que não contém nenhuma transação do Change Data Capture.|  
|**failed_sessions_count**|**Int**|Número de sessões que falharam.|  
  
## <a name="remarks"></a>Remarks  
 Os valores nesta exibição de gerenciamento dinâmico são redefinidos sempre que a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciada.  
  
## <a name="permissions"></a>Permissões  
 Requer permissão VIEW DATABASE STATE para consultar o **cdc_log_scan_sessions** exibição de gerenciamento dinâmico. Para obter mais informações sobre permissões sobre exibições de gerenciamento dinâmico, consulte [funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações da sessão mais atual.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT session_id, start_time, end_time, duration, scan_phase  
    error_count, start_lsn, current_lsn, end_lsn, tran_count  
    last_commit_lsn, last_commit_time, log_record_count, schema_change_count  
    command_count, first_begin_cdc_lsn, last_commit_cdc_lsn,   
    last_commit_cdc_time, latency, empty_scan_count, failed_sessions_count  
FROM sys.dm_cdc_log_scan_sessions  
WHERE session_id = (SELECT MAX(b.session_id) FROM sys.dm_cdc_log_scan_sessions AS b);  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.dm_cdc_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-errors.md)  
  
  

