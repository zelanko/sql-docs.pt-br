---
title: NOT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- NOT_TSQL
- NOT
dev_langs:
- TSQL
helpviewer_keywords:
- negating Boolean input
- NOT operator [Transact-SQL]
- expressions [SQL Server], negating
- reversing Boolean expression values
ms.assetid: dc07cc35-20f1-46e6-9995-2938390dc19a
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 4dfbc412c758bc234c670e3d1dd54d7dacabd6cd
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39459990"
---
# <a name="not-transact-sql"></a>NOT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Nega uma entrada booliana.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
[ NOT ] boolean_expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *boolean_expression*  
 É qualquer [expression](../../t-sql/language-elements/expressions-transact-sql.md) booliana válida.  
  
## <a name="result-types"></a>Tipos de resultado  
 **Booliano**  
  
## <a name="result-value"></a>Valor do resultado  
 NOT inverte o valor de qualquer expressão booliana.  
  
## <a name="remarks"></a>Remarks  
 Usar NOT nega uma expressão.  
  
 A tabela a seguir mostra os resultados ao comparar valores TRUE e FALSE que usam o operador NOT.  
  
||NOT|  
|------|---------|  
|**TRUE**|FALSE|  
|**FALSE**|TRUE|  
|**UNKNOWN**|UNKNOWN|  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir localiza todas as bicicletas coloridas prateadas que não têm um preço padrão acima de $ 400.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID, Name, Color, StandardCost  
FROM Production.Product  
WHERE ProductNumber LIKE 'BK-%' AND Color = 'Silver' AND NOT StandardCost > 400;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ProductID   Name                     Color         StandardCost
 ---------   -------------------      ------      ------------
 984         Mountain-500 Silver, 40  Silver        308.2179
 985         Mountain-500 Silver, 42  Silver        308.2179
 986         Mountain-500 Silver, 44  Silver        308.2179
 987         Mountain-500 Silver, 48  Silver        308.2179
 988         Mountain-500 Silver, 52  Silver        308.2179
 (6 row(s) affected)
 ```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir restringe os resultados a `SalesOrderNumber` para valores que começam com `SO6` e `ProductKeys` maior ou igual a 400.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductKey, CustomerKey, OrderDateKey, ShipDateKey  
FROM FactInternetSales  
WHERE SalesOrderNumber LIKE 'SO6%' AND NOT ProductKey < 400;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  


