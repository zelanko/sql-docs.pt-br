---
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
ms.openlocfilehash: 13d57b4c36d238cb8e6893ff912e7052ba2e079f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890383"
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
  
  
