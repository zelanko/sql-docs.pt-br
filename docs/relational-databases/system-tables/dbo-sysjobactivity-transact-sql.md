---
title: dbo.sysjobactivity (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c42bdaf9a9905e7ccd945bee2132242fa6e79f13
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="dbosysjobactivity-transact-sql"></a>dbo.sysjobactivity (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registra a atividade e o status do trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  Essa tabela é armazenada no **msdb** banco de dados.
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**Int**|ID da sessão armazenada no **syssessions** tabela o **msdb** banco de dados.|  
|**job_id**|**uniqueidentifier**|Identificação do trabalho.|  
|**run_requested_date**|**datetime**|Data e hora em que foi solicitada a execução do trabalho.|  
|**run_requested_source**|**sysname(nvarchar(128))**|Quem solicitou a execução do trabalho.<br /><br /> **1** = SOURCE_SCHEDULER<br /><br /> **2** = SOURCE_ALERTER<br /><br /> **3** = SOURCE_BOOT<br /><br /> **4** = SOURCE_USER<br /><br /> **6** = SOURCE_ON_IDLE_SCHEDULE|  
|**queued_date**|**datetime**|Data e hora em que o trabalho entrou na fila. Se o trabalho for executado diretamente, essa coluna será NULL.|  
|**start_execution_date**|**datetime**|Data e hora para as quais a execução do trabalho foi programada.|  
|**last_executed_step_id**|**Int**|Identificação da última etapa de trabalho executada.|  
|**last_executed_step_**<br /><br /> **date**|**datetime**|Data e hora em que começou a execução da última etapa do trabalho.|  
|**stop_execution_date**|**datetime**|Data e hora em que a execução do trabalho terminou.|  
|**job_history_id**|**Int**|Usado para identificar uma linha de **sysjobhistory** tabela.|  
|**next_scheduled_run_date**|**datetime**|Próxima data e hora em que o trabalho é agendado para execução.|  

## <a name="example"></a>Exemplo
Este exemplo retorna o status de tempo de execução de todos os trabalhos do SQL Server Agent.  Execute o [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
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
  
## <a name="see-also"></a>Consulte também  
 [dbo.sysjobhistory &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysjobhistory-transact-sql.md)  
  
  
