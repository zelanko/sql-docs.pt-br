---
title: sp_password (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_password
- sp_password_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_password
ms.assetid: 0ecbec81-e637-44a9-a61e-11bf060ef084
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7aadc50a6a57a7880fa8aed9ad498d713090c009
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sppassword-transact-sql"></a>sp_password (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona ou altera uma senha para um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_password [ [ @old = ] 'old_password' , ]  
     { [ @new =] 'new_password' }  
     [ , [ @loginame = ] 'login' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@old=** ] **'***old_password***'**  
 É a senha antiga. *old_password* é **sysname**, com um padrão NULL.  
  
 [  **@new=** ] **'***nova_senha***'**  
 É a nova senha. *nova_senha* é **sysname**, sem padrão. *old_password* deve ser especificado se os parâmetros nomeados não são usados.  
  
> [!IMPORTANT]  
>  Não use uma senha NULL. Use uma senha forte. Para saber mais, confira [Strong Passwords](../../relational-databases/security/strong-passwords.md).  
  
 [  **@loginame=** ] **'***login***'**  
 É o nome de logon afetado pela mudança de senha. *login* é **sysname**, com um padrão de NULL. *logon* já deve existir e pode ser especificado somente por membros do **sysadmin** ou **securityadmin** funções de servidor fixas.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_password** chama ALTER LOGIN. Esta instrução oferece suporte a opções adicionais. Para obter informações sobre como alterar as senhas, consulte [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md).  
  
 **sp_password** não pode ser executado em uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY LOGIN. Requer ainda a permissão CONTROL SERVER para redefinir uma senha sem fornecer a senha antiga ou se o logon que estiver sendo alterado tiver permissão CONTROL SERVER.  
  
 Um diretor pode alterar sua própria senha.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-the-password-of-a-login-without-knowing-the-old-password"></a>A. Alterando a senha de um logon sem saber a senha antiga  
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
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
