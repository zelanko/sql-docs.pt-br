---
title: sp_defaultlanguage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_defaultlanguage
- sp_defaultlanguage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_defaultlanguage
ms.assetid: 908d01cc-e704-45d9-9e85-d2df6da3e6f5
author: stevestein
ms.author: sstein
ms.openlocfilehash: af2402ce4f1e49ee572a9d271497c2798d679070
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68120087"
---
# <a name="sp_defaultlanguage-transact-sql"></a>sp_defaultlanguage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera o idioma padrão para um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Em vez disso, use [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_defaultlanguage [ @loginame = ] 'login'   
     [ , [ @language = ] 'language' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @loginame = ] 'login'`É o nome de logon. o *logon* é **sysname**, sem padrão. o *logon* pode ser um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon existente ou um usuário ou grupo do Windows.  
  
`[ @language = ] 'language'`É o idioma padrão do logon. o *idioma* é **sysname**, com um padrão de NULL. o *idioma* deve ser um idioma válido no servidor. Se o *idioma* não for especificado, o *idioma* será definido como o idioma padrão do servidor; o idioma padrão é definido pelo **idioma padrão**da variável de configuração **sp_configure** . A alteração do idioma padrão de servidor não altera o idioma padrão para logons existentes.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_defaultlanguage** chama ALTER login, que dá suporte a opções adicionais. Para obter informações sobre como alterar outros padrões de logon, consulte [ALTER login &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md).  
  
 Use a instrução SET LANGUAGE para alterar o idioma da sessão atual. Use a função@LANGUAGE @ para mostrar a configuração de idioma atual.  
  
 Se o idioma padrão de um logon for removido do servidor, o logon adquirirá o idioma padrão do servidor. **sp_defaultlanguage** não pode ser executado em uma transação definida pelo usuário.  
  
 As informações sobre os idiomas instalados no servidor estão visíveis na exibição do catálogo **Sys. syslanguages** .  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY LOGIN.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `ALTER LOGIN` ao alterar o idioma padrão do logon `Fathima` para árabe. Este é o método preferencial.  
  
```  
ALTER LOGIN Fathima WITH DEFAULT_LANGUAGE = Arabic;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [@@LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/functions/language-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [sys. syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
