---
title: dbo. no sysjobhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/24/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysjobhistory_TSQL
- dbo.sysjobhistory
- sysjobhistory
- sysjobhistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobhistory system table
ms.assetid: 1b1fcdbb-2af2-45e6-bf3f-e8279432ce13
author: stevestein
ms.author: sstein
ms.openlocfilehash: cc488958513f4a84ac776ff26f1fe2c867f8fa74
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "76761830"
---
# <a name="dbosysjobhistory-transact-sql"></a>dbo.sysjobhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Contém informações sobre a execução de trabalhos agendados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.
  
> [!NOTE]
> Na maioria dos casos, os dados são atualizados somente depois que a etapa de trabalho é concluída e a tabela *normalmente não contém* registros para etapas de trabalho que estão em andamento no momento, mas, em alguns casos, os processos subjacentes fornecem informações sobre etapas de trabalho em andamento.

Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|Identificador exclusivo da linha.|  
|**job_id**|**uniqueidentifier**|ID do trabalho.|  
|**step_id**|**int**|ID da etapa no trabalho.|  
|**step_name**|**sysname**|Nome da etapa.|  
|**sql_message_id**|**int**|ID de qualquer mensagem de erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornada se o trabalho falhar.|  
|**sql_severity**|**int**|Severidade de qualquer erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Mensagem**|**nvarchar(4000)**|Texto, se houver, de um erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**run_status**|**int**|O status da execução do trabalho:<br /><br /> **0** = falha<br /><br /> **1** = com êxito<br /><br /> **2** = repetir<br /><br /> **3** = cancelado<br /><br />**4** = em andamento|  
|**run_date**|**int**|Data do início da execução do trabalho ou da etapa. Para um histórico Em andamento, esta é a data/hora em que o histórico foi gravado.|  
|**run_time**|**int**|Hora em que o trabalho ou a etapa foi iniciado no formato **HHMMSS** .|  
|**run_duration**|**int**|Tempo decorrido na execução do trabalho ou etapa no formato **HHMMSS** .|  
|**operator_id_emailed**|**int**|ID do operador notificado quando o trabalho foi concluído.|  
|**operator_id_netsent**|**int**|ID do operador notificado por uma mensagem quando o trabalho foi concluído.|  
|**operator_id_paged**|**int**|ID do operador notificado por pager quando o trabalho foi concluído.|  
|**retries_attempted**|**int**|Número de tentativas repetidas para o trabalho ou a etapa.|  
|**servidor**|**sysname**|Nome do servidor no qual o trabalho foi executado.|  
  
  ## <a name="example"></a>Exemplo
 A consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir converterá as colunas **run_time** e **run_duration** em um formato mais amigável.  Execute o script em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
 
 ```sql
 SET NOCOUNT ON;
 
 SELECT sj.name,
        sh.run_date,
        sh.step_name,
        STUFF(STUFF(RIGHT(REPLICATE('0', 6) +  CAST(sh.run_time as varchar(6)), 6), 3, 0, ':'), 6, 0, ':') 'run_time',
        STUFF(STUFF(STUFF(RIGHT(REPLICATE('0', 8) + CAST(sh.run_duration as varchar(8)), 8), 3, 0, ':'), 6, 0, ':'), 9, 0, ':') 'run_duration (DD:HH:MM:SS)  '
FROM msdb.dbo.sysjobs sj
JOIN msdb.dbo.sysjobhistory sh
ON sj.job_id = sh.job_id
```
