---
title: sp_adduser (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_adduser
- sp_adduser_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_adduser
ms.assetid: 61a40eb4-573f-460c-9164-bd1bbfaf8b25
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 5c917889a4ed435e59e7d165841234b80390dc7e
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85875411"
---
# <a name="sp_adduser-transact-sql"></a>sp_adduser (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Adiciona um novo usuário ao banco de dados atual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Em vez disso, use [Create User](../../t-sql/statements/create-user-transact-sql.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_adduser [ @loginame = ] 'login'   
    [ , [ @name_in_db = ] 'user' ]   
    [ , [ @grpname = ] 'role' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @loginame = ] 'login'`É o nome do logon [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do logon do Windows. o *logon* é um **sysname**, sem padrão. o *logon* deve ser um logon existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um logon do Windows.  
  
`[ @name_in_db = ] 'user'`É o nome do novo usuário de banco de dados. o *usuário* é um **sysname**, com um padrão de NULL. Se o *usuário* não for especificado, o nome do novo usuário do banco de dados será padronizado como o nome de *logon* . A especificação de *User* dá ao novo usuário um nome no banco de dados diferente do nome de logon no nível do servidor.  
  
`[ @grpname = ] 'role'`É a função de banco de dados da qual o novo usuário se torna um membro. *role* é **sysname**, com um padrão de NULL. a *função* deve ser uma função de banco de dados válida no banco de dados atual.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_adduser** também criará um esquema com o nome do usuário.  
  
 Depois que um usuário for adicionado, use as instruções GRANT, DENY e REVOKE para definir as permissões que controlam as atividades executadas pelo usuário.  
  
 Use **Sys. server_principals** para exibir uma lista de nomes de logon válidos.  
  
 Use **sp_helprole** para exibir uma lista de nomes de função válidos. Quando você especifica uma função, o usuário automaticamente ganha as permissões definidas para ela. Se uma função não for especificada, o usuário Obtém as permissões concedidas à função **pública** padrão. Para adicionar um usuário a uma função, deve ser fornecido um valor para o *nome de usuário* . (o*nome de usuário* pode ser o mesmo que *login_id*.)  
  
 O **convidado** do usuário já existe em todos os bancos de dados. Adicionar o usuário **convidado** habilitará esse usuário, se ele tiver sido desabilitado anteriormente. Por padrão, o **convidado** do usuário é desabilitado em novos bancos de dados.  
  
 **sp_adduser** não pode ser executado dentro de uma transação definida pelo usuário.  
  
 Você não pode adicionar um usuário **convidado** porque já existe um usuário **convidado** dentro de cada banco de dados. Para habilitar o usuário **convidado** , Conceda permissão Connect de **convidado** , conforme mostrado:  
  
```  
GRANT CONNECT TO guest;  
GO  
```  
  
## <a name="permissions"></a>Permissões  
 Requer propriedade do banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-adding-a-database-user"></a>a. Adicionando um usuário de banco de dados  
 O exemplo a seguir adicionar o usuário de banco de dados `Vidur` à função existente `Recruiting` no banco de dados atual, usando o logon existente `Vidur` do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
EXEC sp_adduser 'Vidur', 'Vidur', 'Recruiting';  
```  
  
### <a name="b-adding-a-database-user-with-the-same-login-id"></a>B. Adicionando um usuário de banco de dados com a mesma ID de logon  
 O exemplo a seguir adiciona o usuário `Arvind` ao banco de dados atual para o logon `Arvind` do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este usuário pertence à função **pública** padrão.  
  
```  
EXEC sp_adduser 'Arvind';  
```  
  
### <a name="c-adding-a-database-user-with-a-different-name-than-its-server-level-login"></a>C. Adicionando um usuário de banco de dados com um nome diferente de seu logon em nível de servidor  
 O exemplo a seguir adiciona o logon `BjornR` do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao banco de dados atual que possui um nome de usuário `Bjorn`, e adiciona o usuário de banco de dados `Bjorn` à função de banco de dados `Production`.  
  
```  
EXEC sp_adduser 'BjornR', 'Bjorn', 'Production';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sys. server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addrole](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [CRIAR usuário &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropuser](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_grantdbaccess](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_grantlogin](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
