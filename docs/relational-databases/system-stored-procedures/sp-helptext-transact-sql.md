---
title: sp_helptext (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helptext
- sp_helptext_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helptext
ms.assetid: 24135456-05f0-427c-884b-93cf38dd47a8
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3cc2628e0c689f41ff954ae9e0d916f79e65c06b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sphelptext-transact-sql"></a>sp_helptext (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Exibe a definição de uma regra definida pelo usuário, um procedimento armazenado, padrão, não criptografado [!INCLUDE[tsql](../../includes/tsql-md.md)], uma função [!INCLUDE[tsql](../../includes/tsql-md.md)] definida pelo usuário, um gatilho, uma coluna computada, uma restrição CHECK, uma exibição ou um objeto de sistema como um procedimento armazenado de sistema.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helptext [ @objname = ] 'name' [ , [ @columnname = ] computed_column_name ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@objname =** ] **'***nome***'**  
 É o nome qualificado ou não qualificado de um objeto de escopo de esquema definido pelo usuário. Somente serão requeridas aspas se um objeto qualificado for especificado. Se um nome completamente qualificado, incluindo um nome de banco de dados, for fornecido, o nome do banco de dados deverá ser o nome do banco de dados atual. O objeto deve estar no banco de dados atual. *nome* é **nvarchar(776)**, sem padrão.  
  
 [  **@columnname =** ] **'***computed_column_name***'**  
 É o nome da coluna computada para a qual exibir informações de definição. A tabela que contém a coluna deve ser especificada como *nome*. *nome da coluna* é **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**Texto**|**nvarchar(255)**|Definição do objeto|  
  
## <a name="remarks"></a>Remarks  
 sp_helptext exibe a definição que é usada para criar um objeto em linhas múltiplas. Cada linha contém 255 caracteres da definição [!INCLUDE[tsql](../../includes/tsql-md.md)]. A definição reside no **definição** coluna o [sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) exibição do catálogo.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** . Definições de objeto de sistema são publicamente visíveis. A definição de objetos de usuário é visível ao proprietário do objeto e aos que possuírem qualquer uma das seguintes permissões: ALTER, CONTROL, TAKE OWNERSHIP ou VIEW DEFINITION.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-displaying-the-definition-of-a-trigger"></a>A. Exibindo a definição de um gatilho  
 O exemplo a seguir exibe a definição do gatilho `dEmployee` no [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]banco de dados.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helptext 'HumanResources.dEmployee';  
GO  
```  
  
### <a name="b-displaying-the-definition-of-a-computed-column"></a>B. Exibindo a definição de uma coluna computada  
 O exemplo a seguir exibe a definição da coluna computada `TotalDue` na tabela `SalesOrderHeader` do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
sp_helptext @objname = N'AdventureWorks2012.Sales.SalesOrderHeader', @columnname = TotalDue ;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Text`  
  
 `---------------------------------------------------------------------`  
  
 `(isnull(([SubTotal]+[TaxAmt])+[Freight],(0)))`  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do mecanismo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
