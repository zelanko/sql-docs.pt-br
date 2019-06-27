---
title: dbo.sysjobhistory (Transact-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 809e8c80ec1734c24f6930b4042b5e1a84356597
ms.sourcegitcommit: 65ceea905030582f8d89e75e97758abf3b1f0bd6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2019
ms.locfileid: "67400111"
---
# <a name="dbosysjobhistory-transact-sql"></a>dbo.sysjobhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Contém informações sobre a execução de trabalhos agendados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.
  
> [!NOTE]
> Na maioria dos casos os dados são atualizados somente depois que a etapa de trabalho for concluído e a tabela normalmente não contém registros para etapas de trabalho que estão atualmente em andamento, mas, em alguns casos, processos subjacentes *fazer* fornecem informações sobre em etapas de trabalho de progresso.

Essa tabela é armazenada na **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|Identificador exclusivo da linha.|  
|**job_id**|**uniqueidentifier**|ID do trabalho.|  
|**step_id**|**int**|ID da etapa no trabalho.|  
|**step_name**|**sysname**|Nome da etapa.|  
|**sql_message_id**|**int**|ID de qualquer mensagem de erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornada se o trabalho falhar.|  
|**sql_severity**|**int**|Severidade de qualquer erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**message**|**nvarchar(4000)**|Texto, se houver, de um erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**run_status**|**int**|O status da execução do trabalho:<br /><br /> **0** = falha<br /><br /> **1** = foi bem-sucedida<br /><br /> **2** = repetir<br /><br /> **3** = cancelada<br /><br />**4** = em andamento|  
|**run_date**|**int**|Data do início da execução do trabalho ou da etapa. Para um histórico Em andamento, esta é a data/hora em que o histórico foi gravado.|  
|**run_time**|**int**|Hora do início do trabalho ou da etapa.|  
|**run_duration**|**int**|Tempo decorrido na execução do trabalho ou da etapa **HHMMSS** formato.|  
|**operator_id_emailed**|**int**|ID do operador notificado quando o trabalho foi concluído.|  
|**operator_id_netsent**|**int**|ID do operador notificado por uma mensagem quando o trabalho foi concluído.|  
|**operator_id_paged**|**int**|ID do operador notificado por pager quando o trabalho foi concluído.|  
|**retries_attempted**|**int**|Número de tentativas repetidas para o trabalho ou a etapa.|  
|**server**|**sysname**|Nome do servidor no qual o trabalho foi executado.|  
  
  ## <a name="example"></a>Exemplo
 O seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta converterá o **run_time** e **run_duration** colunas em um formato amigável de usuário mais.  Execute o script em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
 
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
