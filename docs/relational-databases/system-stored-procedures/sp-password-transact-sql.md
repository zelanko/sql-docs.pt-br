---
title: sp_password (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_password
- sp_password_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_password
ms.assetid: 0ecbec81-e637-44a9-a61e-11bf060ef084
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f65a56aaca4e2ede491f41cb6c2aca84dc1c988e
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899299"
---
# <a name="sp_password-transact-sql"></a>sp_password (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Adiciona ou altera uma senha para um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Em vez disso, use [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_password [ [ @old = ] 'old_password' , ]  
     { [ @new =] 'new_password' }  
     [ , [ @loginame = ] 'login' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @old = ] 'old_password'`É a senha antiga. *old_password* é **sysname**, com um padrão de NULL.  
  
`[ @new = ] 'new_password'`É a nova senha. *new_password* é **sysname**, sem padrão. *old_password* deverá ser especificado se os parâmetros nomeados não forem usados.  
  
> [!IMPORTANT]  
>  Não use uma senha NULL. Use uma senha forte. Para saber mais, confira [Strong Passwords](../../relational-databases/security/strong-passwords.md).  
  
`[ @loginame = ] 'login'`É o nome do logon afetado pela alteração de senha. *login* é **sysname**, com um padrão de NULL. o *logon* já deve existir e pode ser especificado somente por membros das funções de servidor fixas **sysadmin** ou **securityadmin** .  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_password** chama ALTER login. Esta instrução oferece suporte a opções adicionais. Para obter informações sobre como alterar senhas, consulte [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md).  
  
 **sp_password** não pode ser executado em uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY LOGIN. Requer ainda a permissão CONTROL SERVER para redefinir uma senha sem fornecer a senha antiga ou se o logon que estiver sendo alterado tiver permissão CONTROL SERVER.  
  
 Um diretor pode alterar sua própria senha.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-the-password-of-a-login-without-knowing-the-old-password"></a>a. Alterando a senha de um logon sem saber a senha antiga  
 O exemplo seguinte mostra como usar `ALTER LOGIN` para alterar a senha para o logon `Victoria` para `B3r1000d#2-36`. Este é o método preferencial. O usuário que está executando este comando deve ter permissão CONTROL SERVER.  
  
```  
ALTER LOGIN Victoria WITH PASSWORD = 'B3r1000d#2-36';  
GO  
```  
  
### <a name="b-changing-a-password"></a>B. Alterando uma senha  
 O exemplo seguinte mostra como usar `ALTER LOGIN` para alterar a senha para o logon `Victoria` de `B3r1000d#2-36` para `V1cteAmanti55imE`. Este é o método preferencial. O usuário `Victoria` pode executar este comando sem permissões adicionais. Outros usuários requerem permissão ALTER ANY LOGIN.  
  
```  
ALTER LOGIN Victoria WITH   
     PASSWORD = 'V1cteAmanti55imE'   
     OLD_PASSWORD = 'B3r1000d#2-36';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [CRIAR logon &#40;&#41;Transact-SQL](../../t-sql/statements/create-login-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addlogin](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_adduser](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_grantlogin](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_revokelogin](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
