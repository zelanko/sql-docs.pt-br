---
title: sp_delete_operator (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_operator
- sp_delete_operator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_operator
ms.assetid: ff6c2c4b-e9fe-4d0c-bbc2-a2ddcc1acb95
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 27656c693409387eb65dea75800142255648a864
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833340"
---
# <a name="sp_delete_operator-transact-sql"></a>sp_delete_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove um operador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_delete_operator [ @name = ] 'name'   
     [ , [ @reassign_to_operator = ] 'reassign_operator' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name = ] 'name'`O nome do operador a ser excluído. o *nome* é **sysname**, sem padrão.  
  
`[ @reassign_to_operator = ] 'reassign_operator'`O nome de um operador para o qual os alertas do operador especificado podem ser reatribuídos. *reassign_operator* é **sysname**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Quando um operador é removido, todas as notificações associadas a ele também são eliminadas.  
  
## <a name="permissions"></a>Permissões  
 Os membros da função de servidor fixa **sysadmin** podem executar **sp_delete_operator**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo seguinte exclui o operador `François Ajenstat`.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_operator @name = 'François Ajenstat' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_add_operator](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_operator](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_update_operator](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
