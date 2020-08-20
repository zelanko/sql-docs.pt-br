---
description: Captura de dados de alterações-sys. dm_cdc_log_scan_sessions
title: sys. dm_cdc_log_scan_sessions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f2e520a40c3f4b130d403ff30eae68b0b2c06b0a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460477"
---
# <a name="change-data-capture---sysdm_cdc_log_scan_sessions"></a>Captura de dados de alterações-sys. dm_cdc_log_scan_sessions
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada sessão de verificação de log no banco de dados atual. A última linha retornada representa a sessão atual. Você pode usar esta exibição para retornar informações de status sobre a sessão de exame de log atual ou informações agregadas sobre todas as sessões desde que a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi iniciada pela última vez.  
   
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|ID da sessão.<br /><br /> 0 = os dados retornados nesta linha são uma agregação de todas as sessões como a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que foi iniciada por último.|  
|**start_time**|**datetime**|A hora em que a sessão foi iniciada.<br /><br /> Quando **session_id** = 0, a hora da coleta de dados agregados foi iniciada.|  
|**end_time**|**datetime**|A hora em que a sessão foi encerrada.<br /><br /> NULL = a sessão está ativa.<br /><br /> Quando **session_id** = 0, a hora em que a última sessão terminou.|  
|**duration**|**bigint**|A duração da sessão em segundos.<br /><br /> 0 = a sessão não contém transações do Change Data Capture.<br /><br /> Quando **session_id** = 0, a soma da duração (em segundos) de todas as sessões com transações de captura de dados de alteração.|  
|**scan_phase**|**nvarchar(200)**|A fase atual da sessão. A seguir estão os possíveis valores e suas descrições:<br /><br /> 1: lendo a configuração<br />2: primeiro exame, criando tabela de hash<br />3: segunda verificação<br />4: segunda verificação<br />5: segunda verificação<br />6: controle de versão do esquema<br />7: última verificação<br />8: concluído<br /><br /> Quando **session_id** = 0, esse valor é sempre "Aggregate".|  
|**error_count**|**int**|Número de erros encontrados.<br /><br /> Quando **session_id** = 0, o número total de erros em todas as sessões.|  
|**start_lsn**|**nvarchar (23)**|Iniciando LSN para a sessão.<br /><br /> Quando **session_id** = 0, o LSN inicial para a última sessão.|  
|**current_lsn**|**nvarchar (23)**|LSN atual sendo verificado.<br /><br /> Quando **session_id** = 0, o LSN atual é 0.|  
|**end_lsn**|**nvarchar (23)**|Encerrando LSN para a sessão.<br /><br /> NULL = a sessão está ativa.<br /><br /> Quando **session_id** = 0, o LSN final para a última sessão.|  
|**tran_count**|**bigint**|Número de transações do Change Data Capture processadas. Esse contador é populado na fase 2.<br /><br /> Quando **session_id** = 0, o número de transações processadas em todas as sessões.|  
|**last_commit_lsn**|**nvarchar (23)**|LSN do último registro de log de confirmação processado.<br /><br /> Quando **session_id** = 0, o LSN do último registro de log de confirmação para qualquer sessão.|  
|**last_commit_time**|**datetime**|Hora em que o último registro de log de confirmação foi processado.<br /><br /> Quando **session_id** = 0, a hora em que o último registro de log de confirmação de qualquer sessão.|  
|**log_record_count**|**bigint**|Número de registros de log verificados.<br /><br /> Quando **session_id** = 0, o número de registros verificados para todas as sessões.|  
|**schema_change_count**|**int**|Número de operações de linguagem de definição de dados (DDL) detectados. Este contador é populado na fase 6.<br /><br /> Quando **session_id** = 0, o número de operações DDL processadas em todas as sessões.|  
|**command_count**|**bigint**|Número de comandos processados.<br /><br /> Quando **session_id** = 0, o número de comandos processados em todas as sessões.|  
|**first_begin_cdc_lsn**|**nvarchar (23)**|Primeiro LSN que contém transações do Change Data Capture.<br /><br /> Quando **session_id** = 0, o primeiro LSN que continha transações de captura de dados de alteração.|  
|**last_commit_cdc_lsn**|**nvarchar (23)**|LSN do último registro de log de confirmação que contém transações do Change Data Capture.<br /><br /> Quando **session_id** = 0, o LSN do último registro de log de confirmação para qualquer sessão que contiver transações de captura de dados de alteração|  
|**last_commit_cdc_time**|**datetime**|Horário em que o último registro de log de confirmação foi processado que contém transações do Change Data Capture.<br /><br /> Quando **session_id** = 0, a hora em que o último registro de log de confirmação de qualquer sessão que continha transações de captura de dados de alteração.|  
|**MOLAP**|**int**|A diferença, em segundos, entre **end_time** e **last_commit_cdc_time** na sessão. Este contador é populado no final da fase 7.<br /><br /> Quando **session_id** = 0, o último valor de latência diferente de zero gravado por uma sessão.|  
|**empty_scan_count**|**int**|Número de sessões sucessivas que não contém nenhuma transação do Change Data Capture.|  
|**failed_sessions_count**|**int**|Número de sessões que falharam.|  
  
## <a name="remarks"></a>Comentários  
 Os valores nesta exibição de gerenciamento dinâmico são redefinidos sempre que a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciada.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE para consultar a exibição de gerenciamento dinâmico **Sys. dm_cdc_log_scan_sessions** . Para obter mais informações sobre permissões em exibições de gerenciamento dinâmico, consulte [funções e exibições de gerenciamento dinâmico &#40;&#41;Transact-SQL ](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações da sessão mais atual.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT session_id, start_time, end_time, duration, scan_phase,  
    error_count, start_lsn, current_lsn, end_lsn, tran_count,  
    last_commit_lsn, last_commit_time, log_record_count, schema_change_count,  
    command_count, first_begin_cdc_lsn, last_commit_cdc_lsn,   
    last_commit_cdc_time, latency, empty_scan_count, failed_sessions_count  
FROM sys.dm_cdc_log_scan_sessions  
WHERE session_id = (SELECT MAX(b.session_id) FROM sys.dm_cdc_log_scan_sessions AS b);  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys. dm_cdc_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-errors.md)  
  
  

