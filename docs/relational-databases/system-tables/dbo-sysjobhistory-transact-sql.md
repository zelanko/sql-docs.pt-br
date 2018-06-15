---
title: dbo.sysjobhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3ab9fbfb6a574f8f6c91ee15789c67cac204d5f3
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34334267"
---
# <a name="dbosysjobhistory-transact-sql"></a>dbo.sysjobhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém informações sobre a execução de trabalhos agendados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Essa tabela é armazenada no **msdb** banco de dados.  
  
> **Observação:** dados são atualizados somente depois que o jobstep for concluído.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**instance_id**|**Int**|Identificador exclusivo da linha.|  
|**job_id**|**uniqueidentifier**|ID do trabalho.|  
|**step_id**|**Int**|ID da etapa no trabalho.|  
|**step_name**|**sysname**|Nome da etapa.|  
|**sql_message_id**|**Int**|ID de qualquer mensagem de erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornada se o trabalho falhar.|  
|**sql_severity**|**Int**|Severidade de qualquer erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**message**|**nvarchar(4000)**|Texto, se houver, de um erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**run_status**|**Int**|O status da execução do trabalho:<br /><br /> **0** = falha<br /><br /> **1** = foi bem-sucedida<br /><br /> **2** = repetir<br /><br /> **3** = cancelada<br /><br /> **4** = em andamento|  
|**run_date**|**Int**|Data do início da execução do trabalho ou da etapa. Para um histórico Em andamento, esta é a data/hora em que o histórico foi gravado.|  
|**run_time**|**Int**|Hora do início do trabalho ou da etapa.|  
|**run_duration**|**Int**|Tempo decorrido na execução do trabalho ou da etapa no **HHMMSS** formato.|  
|**operator_id_emailed**|**Int**|ID do operador notificado quando o trabalho foi concluído.|  
|**operator_id_netsent**|**Int**|ID do operador notificado por uma mensagem quando o trabalho foi concluído.|  
|**operator_id_paged**|**Int**|ID do operador notificado por pager quando o trabalho foi concluído.|  
|**retries_attempted**|**Int**|Número de tentativas repetidas para o trabalho ou a etapa.|  
|**server**|**sysname**|Nome do servidor no qual o trabalho foi executado.|  
  
  ## <a name="example"></a>Exemplo
 O seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta converterá o **run_time** e **run_duration** colunas em um formato amigável mais.  Execute o script em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
 
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
