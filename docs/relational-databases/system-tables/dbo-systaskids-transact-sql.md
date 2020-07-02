---
title: dbo.systaskids (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 729df88407b71234fedc64d88ccaa1bc00a46fd0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750210"
---
# <a name="dbosystaskids-transact-sql"></a>dbo.systaskids (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Contém um mapeamento das tarefas criadas em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para trabalhos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] na versão atual. Essa tabela é armazenada no banco de dados **msdb** .  
  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**task_id**|**int**|ID da tarefa|  
|**job_id**|**uniqueidentifier**|ID do trabalho para o qual a tarefa está mapeada|  
  
  
