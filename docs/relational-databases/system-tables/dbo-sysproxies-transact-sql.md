---
title: Proxies de dbo.sys(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysproxies_TSQL
- sysproxies_TSQL
- dbo.sysproxies
- sysproxies
dev_langs:
- TSQL
helpviewer_keywords:
- sysproxies system table
ms.assetid: a73da875-be22-45fc-b5e2-ea7ebd48e2d6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1e49698ae6692a06c141a4182df3c54cd4f61d43
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750302"
---
# <a name="dbosysproxies-transact-sql"></a>dbo.sysproxies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Define atributos de uma conta proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|ID da conta proxy.|  
|**name**|**sysname**|Nome da conta proxy.|  
|**credential_id**|**int**|ID da credencial que a conta proxy usa.|  
|**habilitado**|**tinyint**|Status da conta proxy:<br /><br /> **0** = desabilitado. **1** = habilitado.|  
|**ndescrição**|**nvarchar(512)**|Descrição que o usuário inseriu quando a conta proxy foi criada.|  
|**user_sid**|**varbinary (85)**|O Microsoft Windows *security_identifier* do usuário ou grupo associado à credencial de proxy.|  
|**credential_date_created**|**datetime**|Data e hora em que a credencial foi criada.|  
  
## <a name="remarks"></a>Comentários  
 Somente os membros da função de servidor fixa **sysadmin** podem acessar a tabela **sysproxies** .  
  
## <a name="see-also"></a>Consulte Também  
 [dbo.sysproxylogin &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxylogin-transact-sql.md)   
 [dbo.sysproxysubsystem &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.syssubsistemas &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-syssubsystems-transact-sql.md)  
  
  
