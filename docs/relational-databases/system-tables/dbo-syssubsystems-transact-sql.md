---
description: dbo.syssubsystems (Transact-SQL)
title: Subsistemas dbo.sys(Transact-SQL) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4124ca1df5ef49984cb8e614ece4e37461ef1974
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538324"
---
# <a name="dbosyssubsystems-transact-sql"></a>dbo.syssubsystems (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém informações sobre todos os subsistemas proxy disponíveis do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. A tabela **syssubsystems** é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|ID do subsistema.|  
|**subsistema**|**nvarchar(40)**|Nome do subsistema.|  
|**description_id**|**int**|ID da mensagem da linha na exibição do catálogo **Sys. messages** que contém a descrição do subsistema.|  
|**subsystem_dll**|**nvarchar(255)**|Local da DLL do subsistema.|  
|**agent_exe**|**nvarchar(255)**|Caminho completo do executável que usa o subsistema.|  
|**start_entry_point**|**nvarchar(30)**|Função que é chamada quando o subsistema é inicializado.|  
|**event_entry_point**|**nvarchar(30)**|Função que é chamada quando uma etapa do subsistema é executada.|  
|**stop_entry_point**|**nvarchar(30)**|Função que é chamada quando a execução de um subsistema é finalizada.|  
|**max_worker_threads**|**int**|Número máximo de etapas simultâneas para um determinado subsistema.|  
  
## <a name="remarks"></a>Comentários  
 Somente os membros da função de servidor fixa **sysadmin** podem acessar essa tabela.  
  
## <a name="see-also"></a>Consulte Também  
 [dbo.sysproxysubsystem &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.sysproxies &#40;&#41;de Transact-SQL ](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)  
  
  
