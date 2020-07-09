---
title: '&lt; (Menor que) (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- < (Less Than)
- <_TSQL
- Than
- Less
- <
- Less Than
dev_langs:
- TSQL
helpviewer_keywords:
- less than (<)
- < (less than operator)
ms.assetid: 54f50bdd-bb62-4593-9af9-4c49edecab75
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f370e3a5bdefb82f5971c8ffea2a065f2ccfb5a5
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86007307"
---
# <a name="lt-less-than-transact-sql"></a>&lt; (Menor que) (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Compara duas expressões (um operador de comparação). Ao comparar expressões não nulas, o resultado será TRUE se o operando da esquerda tiver um valor menor que o operando da direita; caso contrário, o resultado será FALSE. Se um ou ambos os operandos forem NULL, consulte o tópico [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
expression < expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md) válida. Ambas as expressões devem ter tipos de dados implicitamente conversíveis. A conversão depende das regras de [precedência de tipo de dados](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 **Booliano**  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using--in-a-simple-query"></a>a. Como usar < em uma consulta simples  
 O exemplo a seguir retorna todas as linhas da tabela `HumanResources.Department` contendo um valor `DepartmentID` que seja inferior ao valor 3.  
  
```  
-- Uses AdventureWorks  
  
SELECT DepartmentID, Name  
FROM HumanResources.Department  
WHERE DepartmentID < 3  
ORDER BY DepartmentID;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
DepartmentID Name  
------------ --------------------------------------------------  
1            Engineering  
2            Tool Design  
  
(2 row(s) affected)  
  
```  
  
### <a name="b-using--to-compare-two-variables"></a>B. Como usar < para comparar duas variáveis  
  
```  
DECLARE @a int = 45, @b int = 40;  
SELECT IIF ( @a < @b, 'TRUE', 'FALSE' ) AS Result;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------  
FALSE  
  
(1 row(s) affected)  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [IIF &#40;Transact-SQL&#41;](../../t-sql/functions/logical-functions-iif-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
