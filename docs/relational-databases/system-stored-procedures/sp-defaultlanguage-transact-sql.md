---
title: sp_defaultlanguage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_defaultlanguage
- sp_defaultlanguage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_defaultlanguage
ms.assetid: 908d01cc-e704-45d9-9e85-d2df6da3e6f5
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: a382ceab3491cfbcd1b8d6dad564f6d8826c2d13
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="spdefaultlanguage-transact-sql"></a>sp_defaultlanguage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera o idioma padrão para um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_defaultlanguage [ @loginame = ] 'login'   
     [ , [ @language = ] 'language' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@loginame =** ] **'***login***'**  
 É o nome de logon. *logon* é **sysname**, sem padrão. *logon* pode ser uma existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon ou um usuário ou grupo.  
  
 [  **@language =** ] **'***idioma***'**  
 É o idioma padrão do logon. *idioma* é **sysname**, com um padrão NULL. *idioma* deve ser um idioma válido no servidor. Se *idioma* não for especificado, *idioma* é definido como o idioma padrão do servidor; idioma padrão é definido pelo **sp_configure** variável de configuração **idioma padrão**. A alteração do idioma padrão de servidor não altera o idioma padrão para logons existentes.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_defaultlanguage** chama ALTER LOGIN, que oferece suporte a opções adicionais. Para obter informações sobre como alterar outros padrões de logon, consulte [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md).  
  
 Use a instrução SET LANGUAGE para alterar o idioma da sessão atual. Use o @@LANGUAGE função para mostrar a configuração de idioma atual.  
  
 Se o idioma padrão de um logon for removido do servidor, o logon adquirirá o idioma padrão do servidor. **sp_defaultlanguage** não pode ser executado em uma transação definida pelo usuário.  
  
 Informações sobre os idiomas instalados no servidor são visíveis no **sys. syslanguages** exibição do catálogo.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY LOGIN.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `ALTER LOGIN` ao alterar o idioma padrão do logon `Fathima` para árabe. Este é o método preferencial.  
  
```  
ALTER LOGIN Fathima WITH DEFAULT_LANGUAGE = Arabic;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [@@LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/functions/language-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [sys. syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
