---
title: dbo.syssubsystems (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3f06182f06e92ff581dd02c072b63fc10962921a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069081"
---
# <a name="dbosyssubsystems-transact-sql"></a>dbo.syssubsystems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém informações sobre todos os subsistemas proxy disponíveis do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. O **syssubsystems** tabela é armazenada na **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|ID do subsistema.|  
|**subsystem**|**nvarchar(40)**|Nome do subsistema.|  
|**description_id**|**int**|ID da linha da mensagem a **sys. messages** exibição do catálogo que contém a descrição do subsistema.|  
|**subsystem_dll**|**nvarchar(255)**|Local da DLL do subsistema.|  
|**agent_exe**|**nvarchar(255)**|Caminho completo do executável que usa o subsistema.|  
|**start_entry_point**|**nvarchar(30)**|Função que é chamada quando o subsistema é inicializado.|  
|**event_entry_point**|**nvarchar(30)**|Função que é chamada quando uma etapa do subsistema é executada.|  
|**stop_entry_point**|**nvarchar(30)**|Função que é chamada quando a execução de um subsistema é finalizada.|  
|**max_worker_threads**|**int**|Número máximo de etapas simultâneas para um determinado subsistema.|  
  
## <a name="remarks"></a>Comentários  
 Somente os membros dos **sysadmin** função de servidor fixa pode acessar essa tabela.  
  
## <a name="see-also"></a>Consulte também  
 [dbo.sysproxysubsystem &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.sysproxies &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)   
 [sys. messages &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)  
  
  
