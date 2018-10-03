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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 28a1b42780b57fb5807e0ff8f900bfe7b1fc7559
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47670454"
---
# <a name="spdeletecategory-transact-sql"></a>sp_delete_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove a categoria especificada de trabalhos, alertas ou operadores do servidor atual.  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_delete_category [ @class = ] 'class' , [ @name = ] 'name'   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@class =**] **'***classe***'**  
 A classe da categoria. *classe* está **varchar(8)**, sem padrão e deve ter um destes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**JOB**|Exclui uma categoria de trabalho.|  
|**ALERTA**|Exclui uma categoria de alerta.|  
|**OPERADOR**|Exclui uma categoria de operador.|  
  
 [  **@name =**] **'***nome***'**  
 O nome da categoria a ser removida. *nome da* está **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentários  
 **sp_delete_category** deve ser executado a partir de **msdb** banco de dados.  
  
 A exclusão de uma categoria recategoriza quaisquer trabalhos, alertas ou operadores nessa categoria para a categoria padrão da classe.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa pode executar esse procedimento.  
  
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
 [sp_add_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md)   
 [sp_help_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-category-transact-sql.md)   
 [sp_update_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
