---
title: '*= (Atribuição de multiplicação) (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '*=_TSQL'
- '*='
dev_langs:
- TSQL
helpviewer_keywords:
- compound operators, *=
- assignment operators, *=
- augmented operators, *=
- '*= (multiply equals)'
- '*= (multiplication assignment)'
ms.assetid: 816ff5dc-9a40-4c07-8351-39c194dbc079
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c6ad2f4cd1c650831415eb4fea8182eaf5fb81fe
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68122086"
---
# <a name="-multiplication-assignment-transact-sql"></a>*= (Atribuição de multiplicação) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Multiplica dois números e define um valor como o resultado da operação. Por exemplo, se uma variável @x for igual a 35, @x *= 2 usará o valor original de @x, multiplicará esse valor por 2 e definirá @x com esse novo valor (70).  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
expression *= expression  
```  
  
## <a name="arguments"></a>Argumentos  
_expressão_  
É qualquer [expression](../../t-sql/language-elements/expressions-transact-sql.md) válida de tipo de dados, exceto o tipo de dados **bit**, na categoria numérica.  
  
## <a name="result-types"></a>Tipos de resultado  
Retorna o tipo de dados do argumento com a precedência mais alta. Para obter mais informações, veja [Precedência de tipo de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="remarks"></a>Comentários  
Para obter mais informações, consulte [&#42; &#40;Multiplicação&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/multiply-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
[Operadores compostos &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
[Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
[Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
