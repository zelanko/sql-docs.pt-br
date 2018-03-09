---
title: server_role_members (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- server_role_members
- sys.server_role_members_TSQL
- server_role_members_TSQL
- sys.server_role_members
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_role_members catalog view
ms.assetid: efa20414-2c6b-45a2-a7a9-60110a24da18
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: dd26b9ea6419e17df0e318fbffeaeee958c0c501
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sysserverrolemembers-transact-sql"></a>sys.server_role_members (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Retorna uma linha para cada membro de cada função de servidor fixa e definida pelo usuário.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**role_principal_id**|**int**|ID do principal do servidor da função.|  
|**member_principal_id**|**int**|ID do principal do servidor do membro.|  
  
 Para adicionar ou remover membros da função de servidor, use o [ALTER SERVER ROLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-server-role-transact-sql.md)instrução.  
  
## <a name="permissions"></a>Permissões  
 Os logons podem exibir a própria associação de função de servidor e também o principal_id dos membros das funções de servidor fixas. Para exibir todas as associação de função de servidor requer o **VIEW DEFINITION ON SERVER ROLE** permissão ou associação no **securityadmin** função de servidor fixa.  
  
 Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna os nomes e as IDs das funções e de seus membros.  
  
```  
SELECT sys.server_role_members.role_principal_id, role.name AS RoleName,   
    sys.server_role_members.member_principal_id, member.name AS MemberName  
FROM sys.server_role_members  
JOIN sys.server_principals AS role  
    ON sys.server_role_members.role_principal_id = role.principal_id  
JOIN sys.server_principals AS member  
    ON sys.server_role_members.member_principal_id = member.principal_id;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Funções de nível de servidor](../../relational-databases/security/authentication-access/server-level-roles.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
