---
title: dbo.sysjobservers (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sysjobservers
- sysjobservers_TSQL
- dbo.sysjobservers
- dbo.sysjobservers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobservers system table
ms.assetid: 9abcc20f-a421-4591-affb-62674d04575e
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 60a5062226e97be3e7c3a38086f0e88dbf9fb023
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="dbosysjobservers-transact-sql"></a>dbo.sysjobservers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Armazena a associação ou relação de um trabalho específico com um ou mais servidores de destino. Esta tabela está armazenada no banco de dados msdb.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|job_id|**uniqueidentifier**|Número de identificação do trabalho.|  
|server_id|**Int**|Número de identificação do servidor.|  
|last_run_outcome|**tinyint**|Resultado da última execução do trabalho:<br /><br /> **0** = Fail<br /><br /> **1** = êxito<br /><br /> **3** = Cancelar|  
|mensagem last_outcome_|**nvarchar(1024)**|Mensagem associada, se houver, à coluna last_run_outcome.|  
|last_run_date|**Int**|Data em que o trabalho foi executado pela última vez.|  
|last_run_time|**Int**|Hora em que o trabalho foi executado pela última vez.|  
|last_run_duration|**Int**|Duração pela qual o trabalho foi executado, em horas, minutos e segundos. Computado usando a fórmula: (*horas*\*10000) + (*minutos*\*100) + *segundos*.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas do SQL Server Agent &#40; Transact-SQL &#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
  
  
