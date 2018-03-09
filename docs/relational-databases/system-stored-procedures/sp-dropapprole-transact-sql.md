---
title: sp_dropapprole (Transact-SQL) | Microsoft Docs
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
- sp_dropapprole_TSQL
- sp_dropapprole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropapprole
ms.assetid: ea1aefe6-8f7d-46e9-a3cb-7b037b393e73
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 51581dbebaeb9e1ad39b4cc2792d9b628324d3e1
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="spdropapprole-transact-sql"></a>sp_dropapprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove uma função de aplicativo do banco de dados atual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use [DROP APPLICATION ROLE](../../t-sql/statements/drop-application-role-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropapprole [@rolename = ] 'role'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@rolename =** ] **'***função***'**  
 É a função de aplicativo a ser removida. *função* é um **sysname**, sem padrão. *função* deve existir no banco de dados atual.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_dropapprole** só pode ser usado para remover funções de aplicativo. Se uma função possuir algum item protegível, a função não poderá ser descartada. Antes de descartar uma função de aplicativo que possui itens protegíveis, é necessário transferir a propriedade dos itens protegíveis primeiro ou descartá-los.  
  
 **sp_dropapprole** não pode ser executado em uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY APPLICATION ROLE no banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove a função de aplicativo `SalesApp` do banco de dados atual.  
  
```  
EXEC sp_dropapprole 'SalesApp';  
```  
  
## <a name="see-also"></a>Consulte também  
 [Segurança armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addapprole &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addapprole-transact-sql.md)   
 [Remover função de aplicativo &#40; Transact-SQL &#41;](../../t-sql/statements/drop-application-role-transact-sql.md)   
 [sp_changeobjectowner &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changeobjectowner-transact-sql.md)   
 [sp_setapprole &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
