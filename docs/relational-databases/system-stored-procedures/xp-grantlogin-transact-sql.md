---
title: xp_grantlogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_grantlogin
- xp_grantlogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_grantlogin
ms.assetid: c851c1ab-3b29-4b99-9902-78c2665a844b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 957bbdc43c0f0adf3a545fee76e9f69df130d8f9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68116666"
---
# <a name="xp_grantlogin-transact-sql"></a>xp_grantlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Concede a um grupo ou usuário do Windows acesso ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Em vez disso, use [Create login](../../t-sql/statements/create-login-transact-sql.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
xp_grantlogin {[@loginame = ] 'login'} [,[@logintype = ] 'logintype']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @loginame = ] 'login'`É o nome do usuário ou grupo do Windows a ser adicionado. O usuário ou grupo do Windows deve ser qualificado com um nome de domínio do Windows no formato *domínio*\\*usuário*. o *logon* é **sysname**, sem padrão.  
  
`[ @logintype = ] 'logintype'`É o nível de segurança do logon com acesso concedido. *LoginType* é **varchar (5)**, com um padrão de NULL. Somente o **administrador** pode ser especificado. Se **admin** for especificado, o *logon* terá acesso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]concedido e adicionado como membro da função de servidor fixa **sysadmin** .  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **xp_grantlogin** agora é um procedimento armazenado do sistema em vez de um procedimento armazenado estendido. **xp_grantlogin** chama **sp_grantlogin** e **sp_addsrvrolemember**.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função de servidor fixa **securityadmin** . Ao alterar o *LoginType*, o requer a associação na função de servidor fixa **sysadmin** .  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_denylogin](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_grantlogin](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados estendidos gerais &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de xp_enumgroups](../../relational-databases/system-stored-procedures/xp-enumgroups-transact-sql.md)   
 [&#41;&#40;Transact-SQL de xp_loginconfig](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [&#41;&#40;Transact-SQL de xp_logininfo](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_revokelogin](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)  
  
  
