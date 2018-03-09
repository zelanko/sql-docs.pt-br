---
title: dbo.sysproxylogin (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.sysproxylogin_TSQL
- sysproxylogin_TSQL
- dbo.sysproxylogin
- sysproxylogin
dev_langs:
- TSQL
helpviewer_keywords:
- sysproxylogin system table
ms.assetid: 433d33cb-bdf2-47bb-af78-2a40b7c8dfce
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6235a99d6fa67fb00a84dbab315bd4f2355e37bc
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="dbosysproxylogin-transact-sql"></a>dbo.sysproxylogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registra quais logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão associados a cada conta proxy do SQL Server Agent. Essa tabela é armazenada no **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**Int**|ID da conta proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Esse valor corresponde do **proxy_id** coluna o **sysproxies** tabela.|  
|**sid**|**varbinary(85)**|Microsoft Windows *security_identifier* para o logon do SQL Server.|  
|**principal_id**|**Int**|ID do usuário ou grupo que têm permissão para usar a conta proxy de uma etapa de subsistema especificada.|  
|**flags**|**Int**|Tipo de logon:<br /><br /> **0** = usuário ou grupo, e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon.<br /><br /> **1**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] função de sistema fixa<br /><br /> **2** = **msdb** função de banco de dados|  
  
## <a name="remarks"></a>Remarks  
 Somente membros do **sysadmin** função de servidor fixa pode acessar essa tabela.  
  
## <a name="see-also"></a>Consulte também  
 [dbo.sysproxies &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)  
  
  
