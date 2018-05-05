---
title: dbo.systaskids (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
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
- systaskids_TSQL
- dbo.systaskids
- systaskids
- dbo.systaskids_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- systaskids system table
ms.assetid: 45c56d89-4160-4d84-80bf-a7a05488792d
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7770d270d229bb27554a4d0d64905e80901dc15f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="dbosystaskids-transact-sql"></a>dbo.systaskids (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém um mapeamento das tarefas criadas em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para trabalhos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] na versão atual. Essa tabela é armazenada no **msdb** banco de dados.  
  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**task_id**|**Int**|ID da tarefa|  
|**job_id**|**uniqueidentifier**|ID do trabalho para o qual a tarefa está mapeada|  
  
  
