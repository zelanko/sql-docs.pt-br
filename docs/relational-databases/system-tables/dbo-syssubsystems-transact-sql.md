---
title: dbo. syssubsystems (Transact-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ff13af62635273773551ded6df3175bc80157a45
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82806437"
---
# <a name="dbosyssubsystems-transact-sql"></a>dbo.syssubsystems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém informações sobre todos os subsistemas proxy disponíveis do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. A tabela **syssubsystems** é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|ID do subsistema.|  
|**subsistema**|**nvarchar(40)**|Nome do subsistema.|  
|**description_id**|**int**|ID da mensagem da linha na exibição do catálogo **Sys. messages** que contém a descrição do subsistema.|  
|**subsystem_dll**|**nvarchar (255)**|Local da DLL do subsistema.|  
|**agent_exe**|**nvarchar (255)**|Caminho completo do executável que usa o subsistema.|  
|**start_entry_point**|**nvarchar(30)**|Função que é chamada quando o subsistema é inicializado.|  
|**event_entry_point**|**nvarchar(30)**|Função que é chamada quando uma etapa do subsistema é executada.|  
|**stop_entry_point**|**nvarchar(30)**|Função que é chamada quando a execução de um subsistema é finalizada.|  
|**max_worker_threads**|**int**|Número máximo de etapas simultâneas para um determinado subsistema.|  
  
## <a name="remarks"></a>Comentários  
 Somente os membros da função de servidor fixa **sysadmin** podem acessar essa tabela.  
  
## <a name="see-also"></a>Consulte Também  
 [dbo. sysproxysubsystem &#40;&#41;Transact-SQL](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo. sysproxies &#40;&#41;Transact-SQL](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)  
  
  
