---
title: sp_revokelogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_revokelogin_TSQL
- sp_revokelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revokelogin
ms.assetid: cb1ab102-1ae0-4811-9144-9a8121ef2d7e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 95598885a80b1f697f5e1287e22c1048e737ba6b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67944729"
---
# <a name="sp_revokelogin-transact-sql"></a>sp_revokelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove as entradas de logon [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de para um usuário ou grupo do Windows criado usando CREATE login, **sp_grantlogin**ou **sp_denylogin**.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Em vez disso, use [drop login](../../t-sql/statements/drop-login-transact-sql.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_revokelogin [ @loginame= ] 'login'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @loginame = ] 'login'`É o nome do usuário ou grupo do Windows. o *logon* é **sysname**, sem padrão. o *logon* pode ser qualquer nome de usuário ou grupo existente do Windows no formato *nome*\\do computador*usuário ou domínio*\\*usuário*.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_revokelogin** desabilita conexões usando a conta especificada pelo parâmetro de *logon* . No entanto, os usuários do Windows que têm acesso a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] através da associação em um grupo do Windows ainda podem se conectar como o grupo após o acesso individual ter sido revogado. Da mesma forma, se o parâmetro de *logon* especificar o nome de um grupo do Windows, os membros desse grupo aos quais foi concedido acesso separado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à instância do ainda poderão se conectar.  
  
 Por exemplo, se o usuário do Windows **ADVWORKS\john** for membro do grupo do Windows **ADVWORKS\Admins**e **sp_revokelogin** revogar o acesso de `ADVWORKS\john`:  
  
```  
sp_revokelogin [ADVWORKS\john]  
```  
  
 O usuário **ADVWORKS\john** ainda poderá se conectar se **ADVWORKS\Admins** tiver recebido acesso a uma instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]do. Da mesma forma, se o grupo do Windows **ADVWORKS\Admins** tiver seu acesso revogado, mas o **ADVWORKS\john** tiver acesso concedido, o **ADVWORKS\john** ainda poderá se conectar.  
  
 Use **sp_denylogin** para impedir explicitamente que os usuários se conectem a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]uma instância do, independentemente de suas associações de grupo do Windows.  
  
 **sp_revokelogin** não pode ser executado em uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY LOGIN no servidor.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove as entradas de logon para o usuário do Windows `Corporate\MollyA`.  
  
```  
EXEC sp_revokelogin 'Corporate\MollyA';  
```  
  
 Ou  
  
```  
EXEC sp_revokelogin [Corporate\MollyA];  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DROP LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_denylogin](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_droplogin](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_grantlogin](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
