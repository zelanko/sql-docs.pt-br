---
description: CREATE SERVER ROLE (Transact-SQL)
title: CREATE SERVER ROLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SERVER_ROLE_TSQL
- CREATE SERVER ROLE
- SERVER ROLE
- CREATE_SERVER_ROLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SERVER ROLE
- SERVER ROLE, CREATE
- CREATE SERVER ROLE statement
- ROLE
- user-defined server roles [SQL Server]
- roles, server
ms.assetid: 30c92f80-f7f6-4a84-ae89-16e69add0de6
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ac14d633e221e50fb821d92c0c1a0f61b2ce5efd
ms.sourcegitcommit: ac9feb0b10847b369b77f3c03f8200c86ee4f4e0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/16/2020
ms.locfileid: "90688714"
---
# <a name="create-server-role-transact-sql"></a>CREATE SERVER ROLE (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Cria uma função de servidor definida pelo usuário.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
CREATE SERVER ROLE role_name [ AUTHORIZATION server_principal ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *role_name*  
 É o nome da função de servidor a ser criada.  
  
 AUTHORIZATION *server_principal*  
 É o logon que possuirá a função de servidor. Se nenhum logon for especificado, a função de servidor será de propriedade do logon que executa CREATE SERVER ROLE.  
  
## <a name="remarks"></a>Comentários  
 As funções de servidor são protegíveis no nível do servidor. Depois de criar uma função de servidor, configure as permissões no nível de servidor da função por meio de GRANT, DENY e REVOKE. Para adicionar logons ou remover logons de uma função de servidor, use [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md). Para remover uma função de servidor, use [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md). Para obter mais informações, veja [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md).  
  
 É possível exibir as funções de servidor consultando as exibições do catálogo [sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md) e [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md).  
  
 As funções de servidor não podem receber permissão nos protegíveis do banco de dados. Para criar funções de banco de dados, veja [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md).  
  
 Para obter informações sobre como criar um sistema de permissões, veja [Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão CREATE SERVER ROLE ou associação na função de servidor fixa sysadmin.  
  
 Também exige IMPERSONATE no *server_principal* para logons, permissão ALTER para funções de servidor usadas como o *server_principal*ou associação em um grupo do Windows que é usado como o server_principal.  
  
 Isso disparará o evento Auditar Gerenciamento da Entidade de Segurança do Servidor com o tipo de objeto definido para a função de servidor e o tipo de evento a adicionar.  
  
 Ao usar a opção AUTHORIZATION para atribuir a propriedade de um função de servidor, as seguintes permissões também são necessárias:  
  
-   Para atribuir a propriedade de uma função de servidor a outro logon, a permissão IMPERSONATE é necessária naquele logon.  
  
-   Para atribuir a propriedade de uma função de servidor para outra, é necessária associação na função de servidor ou a permissão ALTER naquela função de servidor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-server-role-that-is-owned-by-a-login"></a>a. Criando uma função de servidor que é de propriedade de um logon  
 O exemplo a seguir cria a função de servidor `buyers` que é de propriedade do logon `BenMiller`.  
  
```sql  
USE master;  
CREATE SERVER ROLE buyers AUTHORIZATION BenMiller;  
GO  
```  
  
### <a name="b-creating-a-server-role-that-is-owned-by-a-fixed-server-role"></a>B. Criando uma função de servidor que é de propriedade de uma função de servidor fixa  
 O exemplo a seguir cria a função de servidor `auditors` que é de propriedade da função de servidor fixa `securityadmin`.  
  
```sql  
USE master;  
CREATE SERVER ROLE auditors AUTHORIZATION securityadmin;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [Guia de Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
  
