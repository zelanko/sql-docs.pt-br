---
title: sp_denylogin (Transact-SQL) | Microsoft Docs
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
- sp_denylogin_TSQL
- sp_denylogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_denylogin
ms.assetid: db80f152-e8af-4303-95b6-3a3a7b664374
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9c6059041564e3c97c683595ca2baa9d60619147
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="spdenylogin-transact-sql"></a>sp_denylogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Impede que um usuário ou grupo do Windows se conecte a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_denylogin [ @loginame = ] 'login'   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@loginame =** ] **'***login* **'**  
 É o nome de um usuário ou grupo do Windows. *logon* é **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_denylogin** nega a permissão CONNECT SQL para a entidade de segurança de nível de servidor mapeada para o usuário do Windows especificado ou o grupo do Windows. Se o principal do servidor não existir, será criado. O novo principal será visível no [sys. server_principals &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) exibição do catálogo.  
  
 **sp_denylogin** não pode ser executado em uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como usar **sp_denylogin** para impedir que o usuário do Windows `CORPORATE\GeorgeV` de se conectar ao servidor.  
  
```  
EXEC sp_denylogin 'CORPORATE\GeorgeV';  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Segurança armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
