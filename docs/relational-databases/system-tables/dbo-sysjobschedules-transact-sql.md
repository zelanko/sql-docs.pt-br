---
title: dbo.sysjobschedules (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysjobschedules
- dbo.sysjobschedules
- dbo.sysjobschedules_TSQL
- sysjobschedules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobschedules system table
ms.assetid: ccdafec7-2a9b-4356-bffb-1caa3a12db59
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 272a950b77f541172b3c76ce4b5d597b9e908dee
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="dbosysjobschedules-transact-sql"></a>dbo.sysjobschedules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém informações de agenda dos trabalhos a serem executados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Essa tabela é armazenada no **msdb** banco de dados.  
  
> **Observação:** o **sysjobschedules** tabela atualiza cada 20 minutos, o que pode afetar os valores retornados pelo **sp_help_jobschedule** procedimento armazenado.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**Int**|ID da agenda.|  
|**job_id**|**uniqueidentifier**|Identificação do trabalho.|  
|**next_run_date**|**Int**|Data e hora para as quais está programada a próxima execução do trabalho. A data é formatada como AAAAMMDD.|  
|**next_run_time**|**Int**|Hora em que o trabalho é agendado para execução. A hora é formatada como HHMMSS e usa um relógio de 24 horas.|  
  
## <a name="see-also"></a>Consulte também  
 [dbo.sysschedules &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
  
  
