---
description: xp_grantlogin (Transact-SQL)
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
ms.openlocfilehash: 185532cdcade18b6902fe1c3e8d1c8ab3eb568b7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419260"
---
# <a name="xp_grantlogin-transact-sql"></a>xp_grantlogin (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Concede a um grupo ou usuário do Windows acesso ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use [Create login](../../t-sql/statements/create-login-transact-sql.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
xp_grantlogin {[@loginame = ] 'login'} [,[@logintype = ] 'logintype']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @loginame = ] 'login'` É o nome do usuário ou grupo do Windows a ser adicionado. O usuário ou grupo do Windows deve ser qualificado com um nome de domínio do Windows no formato *domínio* \\ *usuário*. o *logon* é **sysname**, sem padrão.  
  
`[ @logintype = ] 'logintype'` É o nível de segurança do logon com acesso concedido. *LoginType* é **varchar (5)**, com um padrão de NULL. Somente o **administrador** pode ser especificado. Se **admin** for especificado, o *logon* terá acesso concedido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e adicionado como membro da função de servidor fixa **sysadmin** .  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **xp_grantlogin** agora é um procedimento armazenado do sistema em vez de um procedimento armazenado estendido. **xp_grantlogin** chama **sp_grantlogin** e **sp_addsrvrolemember**.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função de servidor fixa **securityadmin** . Ao alterar o *LoginType*, o requer a associação na função de servidor fixa **sysadmin** .  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_denylogin ](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_grantlogin ](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados estendidos gerais &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de xp_enumgroups ](../../relational-databases/system-stored-procedures/xp-enumgroups-transact-sql.md)   
 [&#41;&#40;Transact-SQL de xp_loginconfig ](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [&#41;&#40;Transact-SQL de xp_logininfo ](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)  
  
  
