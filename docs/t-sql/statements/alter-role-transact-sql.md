---
title: ALTER ROLE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_ROLE_TSQL
- ALTER ROLE
dev_langs:
- TSQL
helpviewer_keywords:
- modifying database roles
- ALTER ROLE statement
- renaming database roles
- database roles [SQL Server], modifying
- names [SQL Server], database roles
ms.assetid: e1e83caa-17cc-4871-b2db-2711339fb64f
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 897e8017965e71f345a93550e9af0c138d80b3b7
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="alter-role-transact-sql"></a>ALTER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Adiciona membros a uma função de banco de dados ou remove membros dela, ou altera o nome de uma função de banco de dados definida pelo usuário.  
  
> [!NOTE]  
>  Para alterar as funções no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) e [sp_droprolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server (starting with 2012) and Azure SQL Database  
  
ALTER ROLE  role_name  
{  
       ADD MEMBER database_principal  
    |  DROP MEMBER database_principal  
    |  WITH NAME = new_name  
}  
[;]  
```  
  
 
```  
-- Syntax for SQL Server 2008 only  
  
-- Change the name of a user-defined database role  
ALTER ROLE role_name   
    WITH NAME = new_name  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *role_name*  
 **APLICA-SE A:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando pelo 2008), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 Especifica a função de banco de dados a ser alterada.  
  
 ADD MEMBER *database_principal*l  
 **APLICA-SE A:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando pelo 2012), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 Especifica para adicionar a entidade de segurança do banco de dados à associação de uma função de banco de dados.  
  
-   *database_principal* é um usuário ou uma função de banco de dados definida pelo usuário.  
  
-   *database_principal* não pode ser uma função de banco de dados fixa ou uma entidade de segurança do servidor.  
  
DROP MEMBER *database_principal*  
 **APLICA-SE A:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando pelo 2012), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 Especifica para remover uma entidade de segurança do banco de dados da associação a uma função de banco de dados.  
  
-   *database_principal* é um usuário ou uma função de banco de dados definida pelo usuário.  
  
-   *database_principal* não pode ser uma função de banco de dados fixa ou uma entidade de segurança do servidor.  
  
WITH NAME = *new_name*  
 **APLICA-SE A:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando pelo 2008), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 Especifica para alterar o nome de uma função de banco de dados definida pelo usuário. O novo nome ainda não deve existir no banco de dados.  
  
 A alteração do nome de uma função de banco de dados não altera o número da ID, o proprietário ou as permissões da função.  
  
## <a name="permissions"></a>Permissões  
 Para executar esse comando, é necessário ter uma ou mais destas permissões ou associações:  
  
-   Permissão **ALTER** na função  
-   Permissão **ALTER ANY ROLE** no banco de dados  
-   Associação à função de banco de dados fixa **db_securityadmin**  
  
Além disso, para alterar a associação em uma função de banco de dados fixa, você precisa:  
  
-   Associação à função de banco de dados fixa **db_owner**  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Não é possível alterar o nome de uma função de banco de dados fixa.  
  
## <a name="metadata"></a>Metadados  
 Essas exibições do sistema contêm informações sobre as funções do banco de dados e entidades de segurança do banco de dados.  
  
-   [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)  
  
-   [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-change-the-name-of-a-database-role"></a>A. Alterar o nome de uma função de banco de dados  
 **APLICA-SE A:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando pelo 2008), [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
 O exemplo a seguir altera o nome da função `buyers` para `purchasing`. [!INCLUDE[AdWorks-example](../../includes/adworks-example-md.md)]  
  
```sql  
ALTER ROLE buyers WITH NAME = purchasing;  
```  
  
### <a name="b-add-or-remove-role-members"></a>B. Adicionar ou remover membros da função  
 **APLICA-SE A:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando pelo 2012), [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
 Esse exemplo cria uma função de banco de dados chamada `Sales`. Ele adiciona um usuário de banco de dados chamado Carlos à associação e, em seguida, mostra como remover o membro Carlos. [!INCLUDE[AdWorks-example](../../includes/adworks-example-md.md)]  
  
```sql  
CREATE ROLE Sales;  
ALTER ROLE Sales ADD MEMBER Barry;  
ALTER ROLE Sales DROP MEMBER Barry;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [DROP ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  
