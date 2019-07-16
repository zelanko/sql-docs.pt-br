---
title: sp_addrolemember (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addrolemember_TSQL
- sp_addrolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addrolemember
ms.assetid: a583c087-bdb3-46d2-b9e5-3921b3e6d10b
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c9e0d3152c6d60faff4c1c42410374287bd7d111
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030908"
---
# <a name="spaddrolemember-transact-sql"></a>sp_addrolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Adiciona um usuário de banco de dados, uma função de banco de dados, o logon do Windows ou um grupo do Windows em uma função de banco de dados no banco de dados atual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [ALTER ROLE](../../t-sql/statements/alter-role-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```
sp_addrolemember [ @rolename = ] 'role', [ @membername = ] 'security_account'  

```    
  
## <a name="arguments"></a>Argumentos  
 [ @rolename=] '*função*'  
 É o nome da função de banco de dados no banco de dados atual. *função* é um **sysname**, sem padrão.  
  
 [ @membername= ] '*security_account*'  
 É a conta de segurança que está sendo adicionada à função. *security_account* é um **sysname**, sem padrão. *security_account* pode ser um usuário de banco de dados, função de banco de dados, logon do Windows ou grupo do Windows.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Um membro adicionado a uma função usando sp_addrolemember herda as permissões da função. Se o novo membro for uma entidade no nível do Windows sem um usuário de banco de dados correspondente, um usuário de banco de dados será criado, mas pode não ser totalmente mapeado para o logon. Sempre verifique se o logon existe e tem acesso ao banco de dados.  
  
 Uma função não pode ser incluída como um membro. Tais definições "circulares" não são válidas, mesmo quando a associação é implícita apenas indiretamente por uma ou mais associações intermediárias.  
  
 sp_addrolemember não pode adicionar uma função de banco de dados fixa, função de servidor fixa ou dbo a uma função.
  
 Use somente sp_addrolemember para adicionar um membro a uma função de banco de dados. Para adicionar um membro a uma função de servidor, use [sp_addsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 A adição de membros a funções de banco de dados flexíveis requer um dos seguintes:  
  
-   Associação na função de banco de dados fixa db_securityadmin ou db_owner.  
  
-   Associação na função proprietária da função.  
  
-   **ALTER ANY ROLE** permissão ou **ALTER** permissão na função.  
  
 A adição de membros a funções de banco de dados fixas requer associação na função de banco de dados fixa db_owner.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-adding-a-windows-login"></a>A. Adicionando um logon do Windows  
 O exemplo a seguir adiciona o logon do Windows `Contoso\Mary5` para o `AdventureWorks2012` banco de dados como usuário `Mary5`. O usuário `Mary5` então é adicionado à função `Production`.  
  
> [!NOTE]  
>  Como `Contoso\Mary5` é conhecido como o usuário de banco de dados `Mary5` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)], o nome de usuário `Mary5` deve ser especificado. A instrução falhará a menos que um logon `Contoso\Mary5` exista. Teste usando um logon de seu domínio.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE USER Mary5 FOR LOGIN [Contoso\Mary5] ;  
GO  
```  
  
### <a name="b-adding-a-database-user"></a>B. Adicionando um usuário de banco de dados  
 O exemplo a seguir adiciona o usuário de banco de dados `Mary5` à função de banco de dados `Production` no banco de dados atual.  
  
```  
EXEC sp_addrolemember 'Production', 'Mary5';  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-adding-a-windows-login"></a>C. Adicionando um logon do Windows  
 O exemplo a seguir adiciona o logon `LoginMary` para o `AdventureWorks2008R2` banco de dados como usuário `UserMary`. O usuário `UserMary` então é adicionado à função `Production`.  
  
> [!NOTE]  
>  Porque o logon `LoginMary` é conhecido como o usuário de banco de dados `UserMary` na [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] de banco de dados, o nome de usuário `UserMary` deve ser especificado. A instrução falhará a menos que um logon `Mary5` exista. Logons e usuários geralmente têm o mesmo nome. Este exemplo usa nomes diferentes para diferenciar as ações que afetam o logon versus o usuário.  
  
```  
-- Uses AdventureWorks  
  
CREATE USER UserMary FOR LOGIN LoginMary ;  
GO  
EXEC sp_addrolemember 'Production', 'UserMary'  
```  
  
### <a name="d-adding-a-database-user"></a>D. Adicionando um usuário de banco de dados  
 O exemplo a seguir adiciona o usuário de banco de dados `UserMary` à função de banco de dados `Production` no banco de dados atual.  
  
```  
EXEC sp_addrolemember 'Production', 'UserMary'  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_droprolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Funções de nível de banco de dados](../../relational-databases/security/authentication-access/database-level-roles.md)  
  
  
