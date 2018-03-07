---
title: "ALTERAR a função de servidor (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 09/06/2016
ms.prod: sql-non-specified
ms.prod_service: pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_SERVER_ROLE_TSQL
- ALTER SERVER ROLE
dev_langs:
- TSQL
helpviewer_keywords:
- SERVER ROLE, ALTER
- ALTER SERVER ROLE statement
ms.assetid: 7a4db7bb-c442-4e12-9a8a-114da5bc7710
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7ce5b5223f5c755c89cb3e105ceb6517087d699f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="alter-server-role-transact-sql"></a>ALTER SERVER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-pdw-md.md)]

Altera a associação de uma função de servidor ou altera nome de uma função de servidor definida pelo usuário. As funções de servidor fixas não podem ser renomeadas.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server  
  
ALTER SERVER ROLE server_role_name   
{  
    [ ADD MEMBER server_principal ]  
  | [ DROP MEMBER server_principal ]  
  | [ WITH NAME = new_server_role_name ]  
} [ ; ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
ALTER SERVER ROLE  server_role_name  ADD MEMBER login;  
  
ALTER SERVER ROLE  server_role_name  DROP MEMBER login;  
```  
  
## <a name="arguments"></a>Argumentos  
*server_role_name*  
É o nome da função de servidor a ser alterada.  
  
Adicionar membro *server_principal*  
Adiciona a entidade de segurança do servidor especificado à função de servidor. *server_principal* pode ser um logon ou uma função de servidor definida pelo usuário. *server_principal* não pode ser uma função de servidor fixa, uma função de banco de dados ou sa.  
  
Remover membro *server_principal*  
Remove a entidade de segurança de servidor especificada da função de servidor. *server_principal* pode ser um logon ou uma função de servidor definida pelo usuário. *server_principal* não pode ser uma função de servidor fixa, uma função de banco de dados ou sa.  
  
COM o nome  **=**  *new_server_role_name*  
Especifica o novo nome da função de servidor definida pelo usuário. Esse nome ainda não pode existir no servidor.  
  
## <a name="remarks"></a>Comentários  
A alteração do nome de uma função de servidor definida pelo usuário não altera o número da ID, o proprietário ou as permissões da função.  
  
Para alterar a associação de função, `ALTER SERVER ROLE` substitui sp_addsrvrolemember e sp_dropsrvrolemember. Esses procedimentos armazenados foram preteridos.  
  
É possível exibir as funções de servidor por meio de consulta das exibições do catálogo `sys.server_role_members` e `sys.server_principals`.  
  
Para alterar o proprietário de uma função de servidor definida pelo usuário, use [ALTER AUTHORIZATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
Requer `ALTER ANY SERVER ROLE` permissão no servidor para alterar o nome de uma função de servidor definida pelo usuário.  
  
**Funções de servidor fixas**  
  
Para adicionar um membro a uma função de servidor fixa, você deve ser membro dessa função de servidor fixa ou da função de servidor fixa `sysadmin`.  
  
> [!NOTE]  
>  O `CONTROL SERVER` e `ALTER ANY SERVER ROLE` permissões não forem suficientes para executar `ALTER SERVER ROLE` para uma função de servidor fixa, e `ALTER` permissão não pode ser concedida em uma função de servidor fixa.  
  
**Funções de servidor definidas pelo usuário**  
  
Para adicionar um membro a uma função de servidor definida pelo usuário, você deve ser um membro do `sysadmin` função de servidor fixa ou tem `CONTROL SERVER` ou `ALTER ANY SERVER ROLE` permissão. Ou você deve ter `ALTER` permissão nessa função.  
  
> [!NOTE]  
>  Ao contrário das funções de servidor fixas, os membros de uma função de servidor definida pelo usuário não têm permissão inerentemente para adicionar membros àquela mesma função.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-the-name-of-a-server-role"></a>A. Alterando o nome de uma função de servidor  
O exemplo seguinte cria uma função de servidor chamada `Product` e, em seguida, altera o nome da função de servidor para `Production`.  
  
```  
CREATE SERVER ROLE Product ;  
ALTER SERVER ROLE Product WITH NAME = Production ;  
GO  
```  
  
### <a name="b-adding-a-domain-account-to-a-server-role"></a>B. Adicionando uma conta de domínio a uma função de servidor.  
O exemplo a seguir adiciona uma conta de domínio chamada `adventure-works\roberto0` à função de servidor definida pelo usuário chamada `Production`.  
  
```  
ALTER SERVER ROLE Production ADD MEMBER [adventure-works\roberto0] ;  
```  
  
### <a name="c-adding-a-sql-server-login-to-a-server-role"></a>C. Adicionando um logon do SQL Server a uma função de servidor  
O exemplo a seguir adiciona uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon denominado `Ted` para o `diskadmin` função de servidor fixa.  
  
```  
ALTER SERVER ROLE diskadmin ADD MEMBER Ted ;  
GO  
```  
  
### <a name="d-removing-a-domain-account-from-a-server-role"></a>D. Removendo uma conta de domínio de uma função de servidor  
O exemplo a seguir remove uma conta de domínio chamada `adventure-works\roberto0` da função de servidor definida pelo usuário chamada `Production`.  
  
```  
ALTER SERVER ROLE Production DROP MEMBER [adventure-works\roberto0] ;  
```  
  
### <a name="e-removing-a-sql-server-login-from-a-server-role"></a>E. Removendo um logon do SQL Server de uma função de servidor  
O exemplo a seguir remove o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login `Ted` do `diskadmin` função de servidor fixa.  
  
```  
ALTER SERVER ROLE Production DROP MEMBER Ted ;  
GO  
```  
  
### <a name="f-granting-a-login-the-permission-to-add-logins-to-a-user-defined-server-role"></a>F. Concedendo a um logon a permissão para adicionar logons a uma função de servidor definida pelo usuário  
O exemplo a seguir permite que `Ted` adicione outros logons à função de servidor definida pelo usuário chamada `Production`.  
  
```  
GRANT ALTER ON SERVER ROLE::Production TO Ted ;  
GO  
```  
  
### <a name="g-to-view-role-membership"></a>G. Para exibir a associação de função  
Para exibir a associação de função, use o **a função de servidor (membros)** página [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou executar a consulta a seguir:  
  
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
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Exemplos:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="h-basic-syntax"></a>H. Sintaxe básica  
O exemplo a seguir adiciona o logon `Anna` para o `LargeRC` função de servidor.  
  
```  
ALTER SERVER ROLE LargeRC ADD MEMBER Anna;  
```  
  
### <a name="i-remove-a-login-from-a-resource-class"></a>I. Remova um logon de uma classe de recurso.  
O exemplo a seguir remove a associação de Anna no `LargeRC` função de servidor.  
  
```  
ALTER SERVER ROLE LargeRC DROP MEMBER Anna;  
```  
  
## <a name="see-also"></a>Consulte também  
[Criar função de servidor &#40; Transact-SQL &#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
[Remover função de servidor &#40; Transact-SQL &#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
[Criar função &#40; Transact-SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
[ALTER ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md)   
[Remover função &#40; Transact-SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
[Segurança armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
[Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
[Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
[server_role_members &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)   
[sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
