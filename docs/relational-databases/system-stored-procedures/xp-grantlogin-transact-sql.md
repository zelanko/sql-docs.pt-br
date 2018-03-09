---
title: xp_grantlogin (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- xp_grantlogin
- xp_grantlogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_grantlogin
ms.assetid: c851c1ab-3b29-4b99-9902-78c2665a844b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eb35af7a2de8fae7d227ea146d2578a73e5c6c28
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="xpgrantlogin-transact-sql"></a>xp_grantlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Concede a um grupo ou usuário do Windows acesso ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
xp_grantlogin {[@loginame = ] 'login'} [,[@logintype = ] 'logintype']  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@loginame =** ] **'***login***'**  
 É o nome do usuário ou grupo do Windows a ser adicionado. O usuário ou grupo deve ser qualificado com um nome de domínio do Windows no formato *domínio*\\*usuário*. *logon* é **sysname**, sem padrão.  
  
 [  **@logintype =** ] **'***logintype***'**  
 É o nível de segurança do logon que está recebendo o acesso. *logintype* é **varchar(5)**, com um padrão NULL. Somente **administrador** pode ser especificado. Se **admin** for especificado, *login* é concedido acesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e adicionado como um membro do **sysadmin** função de servidor fixa.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **xp_grantlogin** é agora um sistema armazenados procedimento em vez de um procedimento armazenado estendido. **xp_grantlogin** chamadas **sp_grantlogin** e **sp_addsrvrolemember**.  
  
## <a name="permissions"></a>Permissões  
 Requer a participação no **securityadmin** função de servidor fixa. Ao alterar o *logintype*, requer a participação no **sysadmin** função de servidor fixa.  
  
## <a name="see-also"></a>Consulte também  
 [sp_denylogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Estendidos gerais procedimentos armazenados &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_enumgroups &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/xp-enumgroups-transact-sql.md)   
 [XP_LOGINCONFIG &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [xp_logininfo &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)   
 [sp_revokelogin &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)  
  
  
