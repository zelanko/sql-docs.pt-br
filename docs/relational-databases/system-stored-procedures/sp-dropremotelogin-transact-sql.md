---
title: sp_dropremotelogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropremotelogin
- sp_dropremotelogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropremotelogin
ms.assetid: 9f097652-a286-40b2-be73-568d77ada698
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: c316f48f3e590fcba419e125f8e327b25ee1ede6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933828"
---
# <a name="sp_dropremotelogin-transact-sql"></a>sp_dropremotelogin (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove um logon remoto mapeado para um logon local usado ao executar procedimentos armazenados remotos em um servidor local que executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]Em vez disso, use servidores vinculados e procedimentos armazenados de servidor vinculado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_dropremotelogin [ @remoteserver = ] 'remoteserver'   
     [ , [ @loginame = ] 'login' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @remoteserver = ] 'remoteserver'`É o nome do servidor remoto mapeado para o logon remoto que deve ser removido. o *servidor_remoto* é **sysname**, sem padrão. o *servidor_remoto* já deve existir.  
  
`[ @loginame = ] 'login'`É o nome de logon opcional no servidor local que está associado ao servidor remoto. *logon* é **sysname**, com um padrão de NULL. o *logon* já deve existir se especificado.  
  
`[ @remotename = ] 'remote_name'`É o nome opcional do logon remoto que é mapeado para *logon* ao fazer logon do servidor remoto. *remote_name* é **sysname**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Se apenas o *servidor_remoto* for especificado, todos os logons remotos desse servidor remoto serão removidos do servidor local. Se o *logon* também for especificado, todos os logons remotos do *servidor_remoto* mapeados para esse logon local específico serão removidos do servidor local. Se *remote_name* também for especificado, somente o logon remoto desse usuário remoto do *servidor_remoto* será removido do servidor local.  
  
 Para adicionar usuários do servidor local, use **sp_addlogin**. Para remover usuários do servidor local, use **sp_droplogin**.  
  
 Logons remotos são necessários apenas quando você usa versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 7.0 e versões subsequentes usam logons de servidor vinculado. Use **sp_addlinkedsrvlogin** e **sp_droplinkedsrvlogin** para adicionar e remover logons de servidor vinculado.  
  
 **sp_dropremotelogin** não pode ser executado em uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer associação nas funções de servidor fixas **sysadmin** ou **securityadmin** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-dropping-all-remote-logins-for-a-remote-server"></a>a. Descartando todos os logons remotos para um servidor remoto  
 O exemplo a seguir remove a entrada para o servidor remoto `ACCOUNTS` e, portanto, remove todos os mapeamentos entre logons no servidor local e logons remotos no servidor remoto.  
  
```sql
EXEC sp_dropremotelogin 'ACCOUNTS';  
```  
  
### <a name="b-dropping-a-login-mapping"></a>B. Descartando um mapeamento de logon  
 O exemplo a seguir remove a entrada para o mapeamento de logons remotos do servidor remoto `ACCOUNTS` do logon local `Albert`.  
  
```sql
EXEC sp_dropremotelogin 'ACCOUNTS', 'Albert';  
```  
  
### <a name="c-dropping-a-remote-user"></a>C. Descartando um usuário remoto  
 O exemplo a seguir remove o logon para o logon remoto `Chris` no servidor remoto `ACCOUNTS` que foi mapeado para o logon local `salesmgr`.  
  
```sql
EXEC sp_dropremotelogin 'ACCOUNTS', 'salesmgr', 'Chris';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addlinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addremotelogin](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addserver](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_droplinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_droplogin](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpremotelogin](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
