---
title: "-= (Atribuição de subtração) (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- -=
- -=_TSQL
dev_langs: TSQL
helpviewer_keywords:
- compound operators, -=
- assignment operators, -=
- augmented operators, -=
- -= (subtract equals)
- -= (subtraction assignment)
ms.assetid: 2a2056b5-1dfa-4ea8-8cfc-6331a2f94da9
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e42283367d3035ce4d7fcaecb4f7c96bcb7fed68
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="--subtraction-assignment-transact-sql"></a>-= (Subtraction Assignment) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Subtrai dois números e define um valor como o resultado da operação. Por exemplo, se uma variável @x é igual a 35, então @x -= 2 assumirá o valor original de @x, subtrairá 2 e define @x para esse novo valor (33).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
expression -= expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer um dos dados de tipos da categoria numérica, exceto o **bit** tipo de dados.  
  
## <a name="result-types"></a>Tipos de resultado  
 Retorna o tipo de dados do argumento com a precedência mais alta. Para obter mais informações, veja [Precedência de tipo de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações, consulte [-&#40; Subtração &#41; &#40; Transact-SQL &#41; ](../../t-sql/language-elements/subtract-transact-sql.md).  
  
## <a name="see-also"></a>Consulte também  
 [Composta operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
