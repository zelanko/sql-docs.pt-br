---
title: -= (Atribuição de subtração) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- -=
- -=_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- compound operators, -=
- assignment operators, -=
- augmented operators, -=
- -= (subtract equals)
- -= (subtraction assignment)
ms.assetid: 2a2056b5-1dfa-4ea8-8cfc-6331a2f94da9
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7914304b9951cf3e73674ae825ab41f5e508cf7b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="--subtraction-assignment-transact-sql"></a>-= (Atribuição de subtração) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Subtrai dois números e define um valor como o resultado da operação. Por exemplo, se uma variável @x for igual a 35, @x -= 2 usará o valor original de @x, subtrairá 2 desse valor e definirá @x com esse novo valor (33).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
expression -= expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É qualquer [expression](../../t-sql/language-elements/expressions-transact-sql.md) válida de qualquer um dos tipos de dados na categoria numérica, com exceção do tipo de dados **bit**.  
  
## <a name="result-types"></a>Tipos de resultado  
 Retorna o tipo de dados do argumento com a precedência mais alta. Para obter mais informações, veja [Precedência de tipo de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações, consulte [- &#40;Subtração&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/subtract-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Operadores compostos &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
