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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933828"
---
# <a name="spdropremotelogin-transact-sql"></a>sp_dropremotelogin (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove um logon remoto mapeado para um logon local usado ao executar procedimentos armazenados remotos em um servidor local que executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Em vez disso, use servidores vinculados e procedimentos armazenados do servidor vinculado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_dropremotelogin [ @remoteserver = ] 'remoteserver'   
     [ , [ @loginame = ] 'login' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @remoteserver = ] 'remoteserver'` É o nome do servidor remoto mapeado para o logon remoto a ser removido. *remoteserver* está **sysname**, sem padrão. *remoteserver* já deve existir.  
  
`[ @loginame = ] 'login'` É o nome de logon opcional no servidor local que está associado com o servidor remoto. *login* é **sysname**, com um padrão de NULL. *logon* já deve existir se especificado.  
  
`[ @remotename = ] 'remote_name'` É o nome opcional do logon remoto mapeado para *login* durante o logon do servidor remoto. *remote_name* está **sysname**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Se apenas *remoteserver* for especificado, todos os logons remotos para o servidor remoto são removidos do servidor local. Se *login* também for especificados, remotos todos os logons do *remoteserver* logon local mapeado para específicos que são removidos do servidor local. Se *remote_name* também for especificado, somente o logon remoto para o usuário remoto do *remoteserver* é removido do servidor local.  
  
 Para adicionar os usuários do servidor local, use **sp_addlogin**. Para remover os usuários do servidor local, use **sp_droplogin**.  
  
 Logons remotos são necessários apenas quando você usa versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 7.0 e versões subsequentes usam logons de servidor vinculado. Use **sp_addlinkedsrvlogin** e **sp_droplinkedsrvlogin** para adicionar e remover logons de servidor vinculado.  
  
 **sp_dropremotelogin** não pode ser executado em uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na **sysadmin** ou **securityadmin** funções de servidor fixas.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-dropping-all-remote-logins-for-a-remote-server"></a>A. Descartando todos os logons remotos para um servidor remoto  
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
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_addremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)   
 [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [sp_droplogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_helpremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
