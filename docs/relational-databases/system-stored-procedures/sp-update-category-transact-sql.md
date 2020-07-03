---
title: sp_update_category (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_category
- sp_update_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_category
ms.assetid: 098b926a-b078-4122-a5e1-3ef54b979dd4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3c738d918c43764048cd0c67ade2fccc9be961c7
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891351"
---
# <a name="sp_update_category-transact-sql"></a>sp_update_category (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Altera o nome de uma categoria.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_update_category  
     [@class =] 'class' ,   
     [@name =] 'old_name' ,  
     [@new_name =] 'new_name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @class = ] 'class'`A classe da categoria a ser atualizada. a *classe*é **varchar (8)**, sem padrão, e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**ALERTA**|Atualiza uma categoria de alerta.|  
|**TRABALHO**|Atualiza uma categoria de trabalho.|  
|**OPERADOR**|Atualiza uma categoria de operador.|  
  
`[ @name = ] 'old_name'`O nome atual da categoria. *old_name*é **sysname**, sem padrão.  
  
`[ @new_name = ] 'new_name'`O novo nome da categoria. *new_name*é **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_update_category** deve ser executado do banco de dados **msdb** .  
  
## <a name="permissions"></a>Permissões  
 Para executar esse procedimento armazenado, os usuários devem receber a função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir renomeia uma categoria de trabalho de `AdminJobs` para `Administrative Jobs`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_category  
  @class = N'JOB',  
  @name = N'AdminJobs',  
  @new_name = N'Administrative Jobs' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_add_category](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_category](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_category](../../relational-databases/system-stored-procedures/sp-help-category-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
