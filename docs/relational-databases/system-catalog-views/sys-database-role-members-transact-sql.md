---
title: database_role_members (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/31/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.database_role_members_TSQL
- sys.database_role_members
- database_role_members_TSQL
- database_role_members
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_role_members catalog view
ms.assetid: ed1b019d-ca48-4db3-85df-cf6d2db591cf
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: abe12465ae80a9373475a0158cdacc663b8f00fa
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sysdatabaserolemembers-transact-sql"></a>sys.database_role_members (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma linha para cada membro de cada função de banco de dados.  Usuários de banco de dados, funções de aplicativo e outras funções de banco de dados podem ser membros de uma função de banco de dados. Para adicionar membros a uma função, use o [ALTER ROLE](../../t-sql/statements/alter-role-transact-sql.md) instrução com o `ADD MEMBER` opção. Associar [database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) para retornar os nomes do `principal_id` valores.
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**role_principal_id**|**int**|ID do banco de dados principal da função.|  
|**member_principal_id**|**int**|ID do banco de dados principal do membro.|  
  
## <a name="permissions"></a>Permissões  
 Qualquer usuário pode exibir a própria associação de função. Para exibir a outra função associações requer a participação no `db_securityadmin` função de banco de dados fixa ou `VIEW DEFINITION` no banco de dados.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="example"></a>Exemplo  
 A consulta a seguir retorna os membros das funções de banco de dados.  
  
```  
SELECT DP1.name AS DatabaseRoleName,   
   isnull (DP2.name, 'No members') AS DatabaseUserName   
 FROM sys.database_role_members AS DRM  
 RIGHT OUTER JOIN sys.database_principals AS DP1  
   ON DRM.role_principal_id = DP1.principal_id  
 LEFT OUTER JOIN sys.database_principals AS DP2  
   ON DRM.member_principal_id = DP2.principal_id  
WHERE DP1.type = 'R'
ORDER BY DP1.name;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
[FUNÇÃO ALTER (Transact-SQLL)](../../t-sql/statements/alter-role-transact-sql.md)      
[server_role_members (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)   
  


