---
description: sp_add_category (Transact-SQL)
title: sp_add_category (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_category
- sp_add_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_category
ms.assetid: 6cca32cd-d941-4378-aed6-a7c90cb7520a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 845801380e1047dc9c44bf597a5fbea21e9d8dc4
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753702"
---
# <a name="sp_add_category-transact-sql"></a>sp_add_category (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  Adiciona a categoria especificada de trabalhos, alertas ou operadores ao servidor. Para obter um método alternativo, consulte [criar categoria de trabalho usando SQL Server Management Studio](../../ssms/agent/create-a-job-category.md).
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
 > [!IMPORTANT]  
 > No momento, na [Instância Gerenciada de SQL do Azure](/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira detalhes nas [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_add_category   
     [ [ @class = ] 'class', ]   
     [ [ @type = ] 'type', ]   
     { [ @name = ] 'name' }  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @class = ] 'class'` A classe da categoria a ser adicionada. a *classe* é **varchar (8)** com um valor padrão de trabalho e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|JOB|Adiciona uma categoria de trabalho.|  
|ALERT|Adiciona uma categoria de alerta.|  
|OPERATOR|Adiciona uma categoria de operador.|  
  
`[ @type = ] 'type'` O tipo de categoria a ser adicionado. o *tipo* é **varchar (12)**, com um valor padrão de **local**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|LOCAL|Uma categoria de trabalho local.|  
|VÁRIOS SERVIDORES|Uma categoria de trabalho multisservidor.|  
|Nenhuma|Uma categoria para uma classe que não seja trabalho **.**|  
  
`[ @name = ] 'name'` O nome da categoria a ser adicionada. O nome deve ser exclusivo na classe especificada. o *nome* é **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 **sp_add_category** deve ser executado do banco de dados **msdb** .  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_add_category**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma categoria de trabalho local denominada `AdminJobs`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_category  
    @class=N'JOB',  
    @type=N'LOCAL',  
    @name=N'AdminJobs' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_delete_category ](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_category ](../../relational-databases/system-stored-procedures/sp-help-category-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_update_category ](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [ Trabalhos dedbo.sys&#40;&#41;de Transact-SQL ](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md)   
 [dbo.sysjobservers &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysjobservers-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
