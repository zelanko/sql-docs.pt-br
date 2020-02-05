---
title: DIFFERENCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DIFFERENCE
- DIFFERENCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DIFFERENCE function
- comparing SOUNDEX values
- SOUNDEX values
ms.assetid: c58ca25d-d6ea-48fa-93bb-c9374b0b2a2b
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fe01e0d9465495cbf4943ba7867ebf262a1f3dd1
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68135926"
---
# <a name="difference-transact-sql"></a>DIFFERENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Esta função retorna um valor inteiro que mede a diferença entre os valores [SOUNDEX()](./soundex-transact-sql.md) de duas expressões de caractere distintas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DIFFERENCE ( character_expression , character_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
*character_expression*  
Uma [expressão](../../t-sql/language-elements/expressions-transact-sql.md) alfanumérica de dados de caractere. *character_expression* pode ser uma constante, variável ou coluna.  
  
## <a name="return-types"></a>Tipos de retorno  
**int**  
 
## <a name="remarks"></a>Comentários  
`DIFFERENCE` compara dois diferentes valores `SOUNDEX` e retorna um valor inteiro. Esse valor mede o grau de correspondência entre os valores de `SOUNDEX`, em uma escala de 0 a 4. Um valor de 0 indica pouca ou nenhuma semelhança entre os valores SOUNDEX; 4 indica valores SOUNDEX com forte semelhança ou até mesmo idênticos, apresentando correspondência total.  
  
`DIFFERENCE` e `SOUNDEX` têm sensibilidade de ordenação.  
  
## <a name="examples"></a>Exemplos  
A primeira parte deste exemplo compara os valores `SOUNDEX` de duas cadeias de caracteres muito similares. Para uma ordenação Latin1_General, `DIFFERENCE` retorna um valor `4`. A segunda parte do exemplo compara os valores `SOUNDEX` de duas cadeias de caracteres muito diferentes e, para uma ordenação Latin1_General, `DIFFERENCE` retorna um valor `0`.  
  
```  
-- Returns a DIFFERENCE value of 4, the least possible difference.  
SELECT SOUNDEX('Green'), SOUNDEX('Greene'), DIFFERENCE('Green','Greene');  
GO  
-- Returns a DIFFERENCE value of 0, the highest possible difference.  
SELECT SOUNDEX('Blotchet-Halls'), SOUNDEX('Greene'), DIFFERENCE('Blotchet-Halls', 'Greene');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----- ----- -----------   
G650  G650  4             
  
(1 row(s) affected)  
  
----- ----- -----------   
B432  G650  0             
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [SOUNDEX &#40;Transact-SQL&#41;](../../t-sql/functions/soundex-transact-sql.md)   
 [Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

