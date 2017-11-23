---
title: sp_droplogin (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_droplogin
- sp_droplogin_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_droplogin
ms.assetid: e58684d1-c394-48de-906e-da6ee91100c3
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f1dffca95e1623b8177359e5f327ddd7df774e28
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spdroplogin-transact-sql"></a>sp_droplogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso impede o acesso a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com esse nome de logon.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md) em vez disso.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_droplogin [ @loginame = ] 'login'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@loginame =** ] **'***login***'**  
 É o logon a ser removido. *logon* é **sysname**, sem padrão. *logon* já deve existir no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_droplogin** chama DROP LOGIN.  
  
 **sp_droplogin** não pode ser executado em uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY LOGIN no servidor.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `DROP LOGIN` para remover o logon `Victoria` de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este é o método preferencial.  
  
```  
DROP LOGIN Victoria;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Segurança armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Remover logon &#40; Transact-SQL &#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
