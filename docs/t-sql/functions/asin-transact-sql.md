---
description: ASIN (Transact-SQL)
title: ASIN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ASIN_TSQL
- ASIN
dev_langs:
- TSQL
helpviewer_keywords:
- ASIN function
- sine
- arcsine
ms.assetid: 6256dd7d-83d5-486e-a933-1d59afc7e417
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1133bbf52506fb7732e7a835e60242a4c2e929c7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484308"
---
# <a name="asin-transact-sql"></a>ASIN (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Uma função que retorna o ângulo, em radianos, cujo seno é a expressão **float** especificada. Isso também é chamado de **arco seno**.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
ASIN ( float_expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*float_expression*  
Uma [expressão](../../t-sql/language-elements/expressions-transact-sql.md) do tipo **float** ou de um tipo que pode ser convertido implicitamente em float. Somente um valor que varia de -1,00 a 1,00 é válido. Valores fora deste intervalo retornarão NULL e ASIN relatará um erro de domínio.
  
## <a name="return-types"></a>Tipos de retorno
**float**
  
## <a name="examples"></a>Exemplos  
Este exemplo usa uma expressão **float** e retorna o valor ASIN do ângulo especificado.
  
```sql
/* The first value will be -1.01. This fails because the value is   
outside the range.*/  
DECLARE @angle FLOAT  
SET @angle = -1.01  
SELECT 'The ASIN of the angle is: ' + CONVERT(VARCHAR, ASIN(@angle))  
GO  
  
-- The next value is -1.00.  
DECLARE @angle FLOAT  
SET @angle = -1.00  
SELECT 'The ASIN of the angle is: ' + CONVERT(VARCHAR, ASIN(@angle))  
GO  
  
-- The next value is 0.1472738.  
DECLARE @angle FLOAT  
SET @angle = 0.1472738  
SELECT 'The ASIN of the angle is: ' + CONVERT(VARCHAR, ASIN(@angle))  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-------------------------  
.Net SqlClient Data Provider: Msg 3622, Level 16, State 1, Line 3  
A domain error occurred.  
  
---------------------------------   
The ASIN of the angle is: -1.5708                          
  
(1 row(s) affected)  
  
----------------------------------   
The ASIN of the angle is: 0.147811                         
  
(1 row(s) affected)  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
Este exemplo retorna o arco seno de 1,00.
  
```sql
SELECT ASIN(1.00) AS asinCalc;  
```  
  
Este exemplo retorna um erro, pois solicita ao arco seno um valor fora do intervalo permitido.
  
```sql
SELECT ASIN(1.1472738) AS asinCalc;  
```  
  
## <a name="see-also"></a>Confira também
[CEILING &#40;Transact-SQL&#41;](../../t-sql/functions/ceiling-transact-sql.md)  
[Funções matemáticas &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[SET ARITHIGNORE &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithignore-transact-sql.md)  
[SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md)
  
  

