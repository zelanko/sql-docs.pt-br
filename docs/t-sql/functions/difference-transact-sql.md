---
title: "DIFERENÇA (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 1868f902cf41eba9637138d7333ac908c72cb76e
ms.contentlocale: pt-br
ms.lasthandoff: 10/17/2017

---
# <a name="difference-transact-sql"></a>DIFFERENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna um valor de inteiro que indica a diferença entre os valores SOUNDEX de duas expressões de caractere.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DIFFERENCE ( character_expression , character_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 É um caractere alfanumérico [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de dados de caracteres. *character_expression* pode ser uma constante, variável ou coluna.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="remarks"></a>Comentários  
 O inteiro retornado é o número de caracteres nos valores SOUNDEX que são iguais. O valor de retorno varia de 0 a 4: 0 indica pouca ou nenhuma similaridade e 4 indica muita similaridade ou valores iguais.  
  
 DIFFERENCE e SOUNDEX diferenciam agrupamentos.  
  
## <a name="examples"></a>Exemplos  
 Na primeira parte do exemplo a seguir, os valores `SOUNDEX` de duas cadeias de caracteres muito similares são comparados. Para um agrupamento Latin1_General `DIFFERENCE` retorna um valor de `4`. Na segunda parte do exemplo a seguir, o `SOUNDEX` valores para duas cadeias de caracteres muito diferentes são comparadas e um agrupamento Latin1_General `DIFFERENCE` retorna um valor de `0`.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [SOUNDEX &#40; Transact-SQL &#41;](../../t-sql/functions/soundex-transact-sql.md)   
 [Funções de cadeia de caracteres &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


