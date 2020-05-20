---
title: sp_delete_category (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_category_TSQL
- sp_delete_category
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_category
ms.assetid: 63ea7d0d-a567-456e-a778-bee99e21d16c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2e150318d4c334c67c51f6cf47c127793a25edb2
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831244"
---
# <a name="sp_delete_category-transact-sql"></a>sp_delete_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove a categoria especificada de trabalhos, alertas ou operadores do servidor atual.  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_delete_category [ @class = ] 'class' , [ @name = ] 'name'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @class = ] 'class'`A classe da categoria. a *classe* é **varchar (8)**, sem padrão, e deve ter um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**TRABALHO**|Exclui uma categoria de trabalho.|  
|**ALERTA**|Exclui uma categoria de alerta.|  
|**OPERADOR**|Exclui uma categoria de operador.|  
  
`[ @name = ] 'name'`O nome da categoria a ser removida. o *nome* é **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 **sp_delete_category** deve ser executado do banco de dados **msdb** .  
  
 A exclusão de uma categoria recategoriza quaisquer trabalhos, alertas ou operadores nessa categoria para a categoria padrão da classe.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir exclui a categoria de trabalho denominada `AdminJobs`.  
  
```  
USE msdb ;  
GO   
  
EXEC dbo.sp_delete_category  
    @name = N'AdminJobs',  
    @class = N'JOB' ;  
GO   
```  
  
## <a name="see-also"></a>Confira também  
 [&#41;&#40;Transact-SQL de sp_add_category](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_category](../../relational-databases/system-stored-procedures/sp-help-category-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_update_category](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
