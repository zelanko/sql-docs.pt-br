---
title: dbo.syssubsystems (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dbo.syssubsystems
- syssubsystems
- syssubsystems_TSQL
- dbo.syssubsystems_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syssubsystems system table
ms.assetid: 114b3d55-1ad6-4777-b868-8ef0c86ba596
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: abe7c8fa687a5868bae73b9590ea39a30fc90ee2
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33254826"
---
# <a name="dbosyssubsystems-transact-sql"></a>dbo.syssubsystems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém informações sobre todos os subsistemas proxy disponíveis do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. O **syssubsystems** tabela é armazenada no **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**Int**|ID do subsistema.|  
|**subsystem**|**nvarchar(40)**|Nome do subsistema.|  
|**description_id**|**Int**|ID da linha de mensagem a **messages** exibição do catálogo que contém a descrição do subsistema.|  
|**subsystem_dll**|**nvarchar(255)**|Local da DLL do subsistema.|  
|**agent_exe**|**nvarchar(255)**|Caminho completo do executável que usa o subsistema.|  
|**start_entry_point**|**nvarchar(30)**|Função que é chamada quando o subsistema é inicializado.|  
|**event_entry_point**|**nvarchar(30)**|Função que é chamada quando uma etapa do subsistema é executada.|  
|**stop_entry_point**|**nvarchar(30)**|Função que é chamada quando a execução de um subsistema é finalizada.|  
|**max_worker_threads**|**Int**|Número máximo de etapas simultâneas para um determinado subsistema.|  
  
## <a name="remarks"></a>Remarks  
 Somente membros do **sysadmin** função de servidor fixa pode acessar essa tabela.  
  
## <a name="see-also"></a>Consulte também  
 [dbo.sysproxysubsystem &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.sysproxies &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)   
 [sys. messages &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)  
  
  
