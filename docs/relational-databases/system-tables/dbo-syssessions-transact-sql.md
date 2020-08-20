---
description: dbo.syssessions (Transact-SQL)
title: Sessões de dbo.sys(Transact-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 72fa9a3d55b3ed783fcbfc7c230676e7fe653eea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473275"
---
# <a name="dbosyssessions-transact-sql"></a>dbo.syssessions (Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Sempre que é iniciado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent cria uma nova sessão. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent usa sessões para preservar o status de trabalhos quando serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é reinicializado ou para inesperadamente. Cada linha da tabela **syssessions** contém informações sobre uma sessão. Use a tabela **sysjobactivity** para exibir o estado do trabalho no final de cada sessão.  
  
 Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|ID de uma sessão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Esse session_id não é o SPID da sessão, mas sim um valor de identidade nessa tabela do sistema.|  
|**agent_start_date**|**datetime**|Data e hora em que o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent foi iniciado para essa sessão.|  
  
## <a name="remarks"></a>Comentários  
 Somente os usuários que são membros da função de servidor fixa **sysadmin** podem acessar essa tabela.  
  
## <a name="see-also"></a>Consulte Também  
 [dbo.sysjobactivity &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysjobactivity-transact-sql.md)  
  
  
