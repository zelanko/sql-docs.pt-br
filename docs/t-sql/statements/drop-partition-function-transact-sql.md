---
title: "REMOVER a função de partição (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP PARTITION FUNCTION
- DROP_PARTITION_FUNCTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting partition functions
- DROP PARTITION FUNCTION statement
- partition functions [SQL Server], removing
- dropping partition functions
- removing partition functions
ms.assetid: a4bb055a-a538-4db9-a6fb-550d1eabfa18
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 127a240e1619200f758e528acc363a733d33da53
ms.sourcegitcommit: 50e54dda407f362262b86941f68b7d80516db7fb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/06/2017
---
# <a name="drop-partition-function-transact-sql"></a>DROP PARTITION FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Remove uma função de partição do banco de dados atual. As funções de partição são criadas usando CREATE PARTITION FUNCTION e modificadas usando ALTER PARTITION FUNCTION.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP PARTITION FUNCTION partition_function_name [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *partition_function_name*  
 É o nome da função de partição que será descartada.  
  
## <a name="remarks"></a>Comentários  
 Uma função de partição pode ser descartada somente se não houver nenhum esquema de partição usando a função de partição atualmente. Se houver esquemas de partição usando a função de partição, DROP PARTITION FUNCTION retornará um erro.  
  
## <a name="permissions"></a>Permissões  
 Qualquer uma das permissões a seguir pode ser usada para executar DROP PARTITION FUNCTION:  
  
-   Permissão ALTER ANY DATASPACE. Essa permissão tem como padrão os membros da função de servidor fixa **sysadmin** e das funções de banco de dados fixas **db_owner** e **db_ddladmin** .  
  
-   A permissão CONTROL ou ALTER no banco de dados no qual a função de partição foi criada.  
  
-   A permissão CONTROL SERVER ou ALTER ANY DATABASE no servidor do banco de dados no qual a função de partição foi criada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir supõe que a função de partição `myRangePF` foi criada no banco de dados atual.  
  
```  
DROP PARTITION FUNCTION myRangePF;  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [ALTER PARTITION FUNCTION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [partition_functions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [partition_parameters &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)   
 [sys.partition_range_values &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)   
 [sys. Partitions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
