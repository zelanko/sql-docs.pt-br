---
description: dbo.sysjobactivity (Transact-SQL)
title: dbo.sysjobactivity (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysjobactivity_TSQL
- dbo.sysjobactivity
- sysjobactivity
- sysjobactivity_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobactivity system table
ms.assetid: fd17cac9-5d1f-4b44-b2dc-ee9346d8bf1e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: dd0fb9ae28d2101b02feb17bc5b2eacbfcb476a7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551101"
---
# <a name="dbosysjobactivity-transact-sql"></a>dbo.sysjobactivity (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Registra a atividade e o status do trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  Essa tabela é armazenada no banco de dados **msdb** .
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|ID da sessão armazenada na tabela **syssessions** no banco de dados **msdb** .|  
|**job_id**|**uniqueidentifier**|Identificação do trabalho.|  
|**run_requested_date**|**datetime**|Data e hora em que foi solicitada a execução do trabalho.|  
|**run_requested_source**|**sysname(nvarchar(128))**|Quem solicitou a execução do trabalho.<br /><br /> **1** = SOURCE_SCHEDULER<br /><br /> **2** = SOURCE_ALERTER<br /><br /> **3** = SOURCE_BOOT<br /><br /> **4** = SOURCE_USER<br /><br /> **6** = SOURCE_ON_IDLE_SCHEDULE|  
|**queued_date**|**datetime**|Data e hora em que o trabalho entrou na fila. Se o trabalho for executado diretamente, essa coluna será NULL.|  
|**start_execution_date**|**datetime**|Data e hora para as quais a execução do trabalho foi programada.|  
|**last_executed_step_id**|**int**|Identificação da última etapa de trabalho executada.|  
|**last_executed_step_**<br /><br /> **date**|**datetime**|Data e hora em que começou a execução da última etapa do trabalho.|  
|**stop_execution_date**|**datetime**|Data e hora em que a execução do trabalho terminou.|  
|**job_history_id**|**int**|Usado para identificar uma linha na tabela **no sysjobhistory** .|  
|**next_scheduled_run_date**|**datetime**|Próxima data e hora em que o trabalho está agendado para ser executado.|  

## <a name="example"></a>Exemplo
Este exemplo retornará o status de tempo de execução para todos os trabalhos de SQL Server Agent.  Execute o [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
```sql
SELECT sj.Name, 
    CASE
        WHEN sja.start_execution_date IS NULL THEN 'Not running'
        WHEN sja.start_execution_date IS NOT NULL AND sja.stop_execution_date IS NULL THEN 'Running'
        WHEN sja.start_execution_date IS NOT NULL AND sja.stop_execution_date IS NOT NULL THEN 'Not running'
    END AS 'RunStatus'
FROM msdb.dbo.sysjobs sj
JOIN msdb.dbo.sysjobactivity sja
ON sj.job_id = sja.job_id
WHERE session_id = (
    SELECT MAX(session_id) FROM msdb.dbo.sysjobactivity); 
```
  
## <a name="see-also"></a>Consulte Também  
 [dbo.sysjobhistory &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysjobhistory-transact-sql.md)  
  
  
