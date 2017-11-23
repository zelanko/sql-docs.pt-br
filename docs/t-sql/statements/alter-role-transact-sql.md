---
title: "FUNÇÃO ALTER (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_ROLE_TSQL
- ALTER ROLE
dev_langs: TSQL
helpviewer_keywords:
- modifying database roles
- ALTER ROLE statement
- renaming database roles
- database roles [SQL Server], modifying
- names [SQL Server], database roles
ms.assetid: e1e83caa-17cc-4871-b2db-2711339fb64f
caps.latest.revision: "64"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a568c327c48b346491fae7d8b72d0e27bf5b5fea
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="alter-role-transact-sql"></a>ALTER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Adiciona ou remove membros de uma função de banco de dados ou altera o nome de uma função de banco de dados definido pelo usuário.  
  
> [!NOTE]  
>  Para alterar as funções em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use [sp_addrolemember &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) e [sp_droprolemember &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md).  
  
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
 *nome_da_função*  
 **Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com o 2008)  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 Especifica a função de banco de dados para alterar.  
  
 Adicionar membro *database_principal*l  
 **Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com o 2012)  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 Especifica para adicionar o banco de dados principal para a associação de uma função de banco de dados.  
  
-   *database_principal* é um usuário de banco de dados ou uma função de banco de dados definido pelo usuário.  
  
-   *database_principal* não pode ser uma função de banco de dados fixa ou uma entidade de servidor.  
  
Remover membro *database_principal*  
 **Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com o 2012)  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 Especifica para remover um banco de dados principal da associação de uma função de banco de dados.  
  
-   *database_principal* é um usuário de banco de dados ou uma função de banco de dados definido pelo usuário.  
  
-   *database_principal* não pode ser uma função de banco de dados fixa ou uma entidade de servidor.  
  
COM nome = *novo_nome*  
 **Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com o 2008)  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 Especifica para alterar o nome de uma função de banco de dados definido pelo usuário. O novo nome não deve existir no banco de dados.  
  
 A alteração do nome de uma função de banco de dados não altera o número da ID, o proprietário ou as permissões da função.  
  
## <a name="permissions"></a>Permissões  
 Para executar esse comando, é necessário um ou mais dessas permissões ou associações:  
  
-   **ALTER** permissão na função  
-   **ALTER ANY ROLE** no banco de dados  
-   Associação de **db_securityadmin** função de banco de dados fixa  
  
Além disso, para alterar a associação em uma função de banco de dados fixa, você precisa:  
  
-   Associação de **db_owner** função de banco de dados fixa  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Não é possível alterar o nome de uma função de banco de dados fixa.  
  
## <a name="metadata"></a>Metadados  
 Essas exibições do sistema contêm informações sobre as funções de banco de dados e objetos de banco de dados.  
  
-   [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)  
  
-   [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-change-the-name-of-a-database-role"></a>A. Alterar o nome de uma função de banco de dados  
 **Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com o 2008)  [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
 O exemplo a seguir altera o nome da função `buyers` para `purchasing`. [!INCLUDE[AdWorks-example](../../includes/adworks-example-md.md)]  
  
```tsql  
ALTER ROLE buyers WITH NAME = purchasing;  
```  
  
### <a name="b-add-or-remove-role-members"></a>B. Adicionar ou remover membros da função  
 **Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com o 2012)  [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
 Este exemplo cria uma função de banco de dados denominada `Sales`. Ele adiciona um usuário de banco de dados chamado Barry para a associação e, em seguida, mostra como remover o membro Barry. [!INCLUDE[AdWorks-example](../../includes/adworks-example-md.md)]  
  
```tsql  
CREATE ROLE Sales;  
ALTER ROLE Sales ADD MEMBER Barry;  
ALTER ROLE Sales DROP MEMBER Barry;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Criar função &#40; Transact-SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Remover função &#40; Transact-SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  
