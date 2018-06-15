---
title: sp_help_category (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_category
- sp_help_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_category
ms.assetid: 8cad1dcc-b43e-43bd-bea0-cb0055c84169
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3e131d1152c3deb2debf78a59686365b85953530
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33254878"
---
# <a name="sphelpcategory-transact-sql"></a>sp_help_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fornece informações sobre as classes especificadas de trabalhos, alertas ou operadores.  
   
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_category [ [ @class = ] 'class' ]   
     [ , [ @type = ] 'type' ]   
     [ , [ @name = ] 'name' ]   
     [ , [ @suffix = ] suffix ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@class=**] **'***classe***'**  
 A classe sobre a qual as informações são solicitadas. *classe* é **varchar(8)**, com um valor padrão de **trabalho**. *classe* pode ser um destes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**JOB**|Fornece informações sobre uma categoria de trabalho.|  
|**ALERTA**|Fornece informações sobre uma categoria de alerta.|  
|**OPERADOR**|Fornece informações sobre uma categoria de operador.|  
  
 [  **@type=** ] **'***tipo***'**  
 O tipo de categoria para a qual as informações são solicitadas. *tipo* é **varchar(12)**, com um padrão NULL, e pode ser um destes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**LOCAL**|Categoria de trabalho local.|  
|**MULTI-SERVER**|Categoria de trabalho multisservidor.|  
|**NONE**|Categoria de uma classe diferente de **trabalho**.|  
  
 [ **@name=** ] **'***name***'**  
 O nome da categoria para a qual as informações são solicitadas. *nome* é **sysname**, com um padrão NULL.  
  
 [ **@suffix=** ] *suffix*  
 Especifica se o **category_type** coluna no conjunto de resultados é uma ID ou um nome. *sufixo* é **bit**, com um padrão de **0**. **1** mostra o **category_type** como um nome, e **0** mostra como uma ID.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Quando **@suffix** é **0**, **sp_help_category** retorna o conjunto de resultados a seguir:  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**category_id**|**Int**|ID da categoria|  
|**category_type**|**tinyint**|Tipo de categoria:<br /><br /> **1** = Local<br /><br /> **2** = multisservidor<br /><br /> **3** = nenhum|  
|**name**|**sysname**|Nome da categoria|  
  
 Quando **@suffix** é **1**, **sp_help_category** retorna o conjunto de resultados a seguir:  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**category_id**|**Int**|ID da categoria|  
|**category_type**|**sysname**|Tipo de categoria. Um dos **LOCAL**, **MULTISSERVIDOR**, ou **NONE**|  
|**name**|**sysname**|Nome da categoria|  
  
## <a name="remarks"></a>Remarks  
 **sp_help_category** deve ser executado a partir de **msdb** banco de dados.  
  
 Se nenhum parâmetro for especificado, o conjunto de resultados fornecerá informações sobre todas as categorias de trabalho.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-local-job-information"></a>A. Retornando informações do trabalho local  
 O exemplo a seguir retorna informações sobre trabalhos que são administrados localmente.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_category  
    @type = N'LOCAL' ;  
GO  
```  
  
### <a name="b-returning-alert-information"></a>B. Retornando informações de alerta  
 O exemplo a seguir retorna informações sobre a categoria de alerta Replication.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_category  
    @class = N'ALERT',  
    @name = N'Replication' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_add_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md)   
 [sp_delete_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [sp_update_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
