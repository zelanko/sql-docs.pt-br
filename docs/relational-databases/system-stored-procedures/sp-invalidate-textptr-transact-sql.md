---
title: sp_invalidate_textptr (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_invalidate_textptr_TSQL
- sp_invalidate_textptr
dev_langs:
- TSQL
helpviewer_keywords:
- sp_invalidate_textptr
ms.assetid: dd9920e1-7064-4c05-93d8-9303103fa1d6
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 77b48427c017b543d73bf93e03a09fd7c4d50c78
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="spinvalidatetextptr-transact-sql"></a>sp_invalidate_textptr (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Invalida o ponteiro de texto em linha especificado ou todos os ponteiros de texto em linha, na transação. **sp_invalidate_textptr** pode ser usado apenas em ponteiros de texto na linha. Esses ponteiros são de tabelas que têm o **texto em linha** opção habilitada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_invalidate_textptr [ [ @TextPtrValue = ] textptr_value ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@TextPtrValue=** ] *textptr_value*  
 É o ponteiro de texto em linha a ser invalidado. *textptr_value* é **varbinary (**16**)**, com um padrão NULL. Se for NULL, **sp_invalidate_textptr** invalida todos os ponteiros de texto em linha na transação.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Remarks  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite um máximo de 1.024 ponteiros de texto em linha válidos ativos por transação, por banco de dados, no entanto, uma transação que inclui mais de um banco de dados pode ter 1.024 ponteiros de texto em linha em cada banco de dados. **sp_invalidate_textptr** pode ser usado para invalidar ponteiros de texto em linha e, portanto, liberar espaço para ponteiros de texto em linha adicionais.  
  
 Para obter mais informações sobre a opção text in row, consulte [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do mecanismo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_tableoption & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)   
 [TEXTPTR &#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)   
 [TEXTVALID &#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textvalid-transact-sql.md)  
  
  
