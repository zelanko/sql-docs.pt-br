---
title: "FUNÇÃO DROP (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/28/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_FUNCTION_TSQL
- DROP FUNCTION
dev_langs:
- TSQL
helpviewer_keywords:
- user-defined functions [SQL Server], removing
- removing user-defined functions
- DROP FUNCTION statement
- dropping user-defined functions
- deleting user-defined functions
ms.assetid: ee5ad283-9e44-4109-902f-0ce12669ee11
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c0768b2a24a939bc2e646fb4cc7173762eae7679
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="drop-function-transact-sql"></a>DROP FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Remove uma ou mais funções definidas pelo usuário do banco de dados atual. Funções definidas pelo usuário são criadas usando [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md) e modificados usando [ALTER FUNCTION](../../t-sql/statements/alter-function-transact-sql.md).  
  
 A função DROP dá suporte a funções escalares definidas pelo usuário. Para obter mais informações, consulte [funções escalares definidas pelo usuário para OLTP na memória](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
 -- SQL Server, Azure SQL Database 

DROP FUNCTION [ IF EXISTS ] { [ schema_name. ] function_name } [ ,...n ]   
[;]
```

```  
 -- Azure SQL Data Warehouse, Parallel Data Warehouse 

DROP FUNCTION [ schema_name. ] function_name
[;] 
```  
   
  
## <a name="arguments"></a>Argumentos  
 *SE EXISTIR*    
 Condicionalmente descarta a função somente se ele já existe. Disponível a partir [!INCLUDE[ssnoversion_md](../../includes/ssnoversion_md.md)] 2016 e no [!INCLUDE[sssds_md](../../includes/sssds_md.md)].
  
 *schema_name*  
 É o nome do esquema ao qual a função definida pelo usuário pertence.  
  
 *nome_da_função*  
 É o nome da função ou funções definidas pelo usuário a serem removidas. A especificação do nome de esquema é opcional. Não é possível especificar o nome de servidor e de banco de dados.  
  
## <a name="remarks"></a>Comentários  
 DROP FUNCTION falhará se houver funções ou exibições [!INCLUDE[tsql](../../includes/tsql-md.md)] no banco de dados que referenciem essa função e forem criadas usando SCHEMABINDING, ou se houver colunas computadas, restrições CHECK ou DEFAULT que referenciem a função.  
  
 DROP FUNCTION falhará se houver colunas computadas que referenciem essa função e tenham sido indexadas.  
  
## <a name="permissions"></a>Permissões  
 Para executar DROP FUNCTION, no mínimo, um usuário deve ter permissão ALTER no esquema ao qual pertence a função definida pelo usuário ou permissão CONTROL na função.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-dropping-a-function"></a>A. Descartando uma função  
 O exemplo a seguir descarta o `fn_SalesByStore` função definida pelo usuário da `Sales` esquema o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] banco de dados de exemplo. Para criar esta função, consulte o exemplo B no [CREATE FUNCTION &#40; Transact-SQL &#41; ](../../t-sql/statements/create-function-transact-sql.md).  
  
```  
DROP FUNCTION Sales.fn_SalesByStore;  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-function-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [OBJECT_ID &#40; Transact-SQL &#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys. Parameters &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)  
  
  
