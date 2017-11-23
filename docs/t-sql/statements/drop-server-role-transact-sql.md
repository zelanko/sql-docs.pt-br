---
title: "REMOVER a função de servidor (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP SERVER ROLE
- DROP_SERVER_ROLE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- SERVER ROLE, DROP
- DROP SERVER ROLE statement
ms.assetid: a2a1e6e6-e40c-4d6a-81be-d197b80bf226
caps.latest.revision: "13"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f76deca0b9f6247a004bfac6e6dfe9c995e896ed
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="drop-server-role-transact-sql"></a>DROP SERVER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-pdw-md.md)]

  Remove uma função de servidor definida pelo usuário.  
  
 Funções de servidor definidas pelo usuário são novas no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DROP SERVER ROLE role_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *nome_da_função*  
 Especifica a função de servidor definida pelo usuário a ser descartada do servidor.  
  
## <a name="remarks"></a>Comentários  
 As funções definidas pelo usuário que possuem protegíveis não podem ser descartadas do servidor. Para descartar uma função de servidor definida pelo usuário que possui protegíveis, é necessário primeiro transferir a propriedade dos protegíveis ou descartá-los.  
  
 As funções de servidor definidas pelo usuário que possuem membros não podem ser descartadas. Para descartar uma função de servidor definida pelo usuário que tem membros, primeiro você deve remover os membros da função usando [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
 A funções de servidor fixas não podem ser removidas.  
  
 Você pode exibir informações sobre associação de função consultando o [server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md) exibição do catálogo.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL na função de servidor ou a permissão ALTER ANY SERVER ROLE.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-to-drop-a-server-role"></a>A. Para remover uma função de servidor  
 O exemplo a seguir descarta a função de servidor `purchasing`.  
  
```  
DROP SERVER ROLE purchasing;  
GO  
```  
  
### <a name="b-to-view-role-membership"></a>B. Para exibir a associação de função  
 Para exibir a associação de função, use o **função de servidor (membros**) página [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou executar a consulta a seguir:  
  
```  
SELECT SRM.role_principal_id, SP.name AS Role_Name,   
SRM.member_principal_id, SP2.name  AS Member_Name  
FROM sys.server_role_members AS SRM  
JOIN sys.server_principals AS SP  
    ON SRM.Role_principal_id = SP.principal_id  
JOIN sys.server_principals AS SP2   
    ON SRM.member_principal_id = SP2.principal_id  
ORDER BY  SP.name,  SP2.name  
```  
  
### <a name="c-to-view-role-membership"></a>C. Para exibir a associação de função  
 Para determinar se uma função de servidor tem outra função de servidor, execute a consulta seguinte:  
  
```  
SELECT SP1.name AS RoleOwner, SP2.name AS Server_Role  
FROM sys.server_principals AS SP1  
JOIN sys.server_principals AS SP2  
    ON SP1.principal_id = SP2.owning_principal_id   
ORDER BY SP1.name ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [Criar função &#40; Transact-SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Remover função &#40; Transact-SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  
