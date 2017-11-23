---
title: dbo.syssessions (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.syssessions_TSQL
- dbo.syssessions
- syssessions_TSQL
- syssessions
dev_langs: TSQL
helpviewer_keywords: syssessions system table
ms.assetid: 187819b6-c7f4-4a26-b74c-0a89e96695cf
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 140d81eef1b0f6b745e5f889b7889c265820405c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="dbosyssessions-transact-sql"></a>dbo.syssessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Sempre que é iniciado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent cria uma nova sessão. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent usa sessões para preservar o status de trabalhos quando serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é reinicializado ou para inesperadamente. Cada linha do **syssessions** tabela contém informações sobre uma sessão. Use o **sysjobactivity** tabela para exibir o estado do trabalho no final de cada sessão.  
  
 Essa tabela é armazenada no **msdb** banco de dados.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|ID de uma sessão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|  
|**agent_start_date**|**datetime**|Data e hora em que o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent foi iniciado para essa sessão.|  
  
## <a name="remarks"></a>Comentários  
 Somente os usuários que são membros do **sysadmin** função de servidor fixa pode acessar essa tabela.  
  
## <a name="see-also"></a>Consulte também  
 [dbo.sysjobactivity &#40; Transact-SQL &#41;](../../relational-databases/system-tables/dbo-sysjobactivity-transact-sql.md)  
  
  
