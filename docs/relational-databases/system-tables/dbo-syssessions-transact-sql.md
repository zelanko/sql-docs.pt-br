---
title: dbo. syssessions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/30/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.syssessions_TSQL
- dbo.syssessions
- syssessions_TSQL
- syssessions
dev_langs:
- TSQL
helpviewer_keywords:
- syssessions system table
ms.assetid: 187819b6-c7f4-4a26-b74c-0a89e96695cf
author: stevestein
ms.author: sstein
ms.openlocfilehash: 566445a3680dc54382a7e3e66bf77dbcbddca2e8
ms.sourcegitcommit: 4933934fad9f3c3e16406952ed964fbd362ee086
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75548291"
---
# <a name="dbosyssessions-transact-sql"></a>dbo.syssessions (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Sempre que é iniciado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent cria uma nova sessão. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent usa sessões para preservar o status de trabalhos quando serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é reinicializado ou para inesperadamente. Cada linha da tabela **syssessions** contém informações sobre uma sessão. Use a tabela **sysjobactivity** para exibir o estado do trabalho no final de cada sessão.  
  
 Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**session_id**|**inteiro**|ID de uma sessão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Esse session_id não é o SPID da sessão, mas sim um valor de identidade nessa tabela do sistema.|  
|**agent_start_date**|**horário**|Data e hora em que o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent foi iniciado para essa sessão.|  
  
## <a name="remarks"></a>Comentários  
 Somente os usuários que são membros da função de servidor fixa **sysadmin** podem acessar essa tabela.  
  
## <a name="see-also"></a>Consulte Também  
 [dbo. sysjobactivity &#40;&#41;Transact-SQL](../../relational-databases/system-tables/dbo-sysjobactivity-transact-sql.md)  
  
  
