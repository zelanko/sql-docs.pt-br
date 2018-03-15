---
title: CREATE ROLE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE ROLE
- DATABASE ROLE
- ROLE_TSQL
- DATABASE_ROLE_TSQL
- CREATE_ROLE_TSQL
- CREATE DATABASE ROLE
- ROLE
- CREATE_DATABASE_ROLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database roles [SQL Server], creating
- CREATE DATABASE ROLE statement
- roles [SQL Server], creating
- CREATE ROLE statement
ms.assetid: b0cd54ad-e81d-4d71-acec-8a6d7261ca08
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: cccfc9f6f9810d8f674ea32858e08683160b2ef1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="create-role-transact-sql"></a>CREATE ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Cria uma nova função de banco de dados no banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
CREATE ROLE role_name [ AUTHORIZATION owner_name ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *role_name*  
 É o nome da função a ser criada.  
  
 AUTHORIZATION *owner_name*  
 É o usuário de banco de dados ou função que terá a propriedade da nova função. Se nenhum usuário for especificado, a função será de propriedade do usuário que executar CREATE ROLE.  
  
## <a name="remarks"></a>Remarks  
 As funções são protegíveis no nível de banco de dados. Depois de criar uma função, configure as permissões em nível de banco de dados da função usando GRANT, DENY e REVOKE. Para adicionar membros a uma função de banco de dados, use [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md). Para obter mais informações, veja [Funções em nível de banco de dados](../../relational-databases/security/authentication-access/database-level-roles.md).  
  
 As funções de banco de dados são visíveis nas exibições do catálogo sys.database_role_members e sys.database_principals.  
  
 Para obter informações sobre como criar um sistema de permissões, veja [Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão **CREATE ROLE** no banco de dados, ou a associação na função de banco de dados fixa **db_securityadmin**. Ao usar a opção de **AUTHORIZATION**, as seguintes permissões também são necessárias:  
  
-   Para atribuir a propriedade de uma função a outro usuário, requer permissão IMPERSONATE naquele usuário.  
  
-   Para atribuir a propriedade de uma função para outra, requer associação na função de destinatário ou a permissão ALTER nessa função.  
  
-   Para atribuir a propriedade de uma função a uma função de aplicativo é necessária a permissão ALTER na função de aplicativo.  
  
## <a name="examples"></a>Exemplos  
Os seguintes exemplos usam todos o banco de dados AdventureWorks.   

### <a name="a-creating-a-database-role-that-is-owned-by-a-database-user"></a>A. Criando uma função de banco de dados pertencente a um usuário de banco de dados  
 O exemplo a seguir cria a função de banco de dados `buyers` que pertence ao usuário `BenMiller`.  
  
```  
CREATE ROLE buyers AUTHORIZATION BenMiller;  
GO  
```  
  
### <a name="b-creating-a-database-role-that-is-owned-by-a-fixed-database-role"></a>B. Criando uma função de banco de dados pertencente a uma função de banco de dados fixa  
 O exemplo a seguir cria a função de banco de dados `auditors` que é de propriedade da função de banco de dados fixa `db_securityadmin`.  
  
```  
CREATE ROLE auditors AUTHORIZATION db_securityadmin;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [DROP ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [Guia de Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
  


