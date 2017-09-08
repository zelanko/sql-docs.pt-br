---
title: '| (OR bit a bit) (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 01/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '|'
- '|_TSQL'
- Bitwise OR
- bitwise
- OR
dev_langs:
- TSQL
helpviewer_keywords:
- OR operator
- bitwise OR (|)
- '| (bitwise OR operator)'
ms.assetid: 86a3b87f-9688-4eaf-a552-29f1b01d880a
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 932b8cc8997a2faec55e56786a80e511fa9c273a
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="-bitwise-or-transact-sql"></a>| (OR bit a bit) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Executa uma operação OR lógica bit a bit entre dois valores inteiros especificados, conforme convertidos em expressões binárias dentro de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```   
expression | expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md) da categoria de tipo de dados inteiro, ou o **bit**, **binário**, ou **varbinary** tipos de dados. *expressão* é tratado como um número binário para a operação bit a bit.  
  
> [!NOTE]  
>  Apenas uma *expressão* pode ser do **binário** ou **varbinary** tipo de dados em uma operação bit a bit.  
  
## <a name="result-types"></a>Tipos de resultado  
 Retorna um **int** se os valores de entrada são **int**, um **smallint** se os valores de entrada são **smallint**, ou um **tinyint** se os valores de entrada são **tinyint**.  
  
## <a name="remarks"></a>Comentários  
 O operador bit a bit | executa um OR lógico bit a bit entre as duas expressões, usando cada bit correspondente para as duas expressões. Os bits no resultado serão definidos como 1 se um ou os dois bits (para o bit atual a ser resolvido) nas expressões de entrada tiverem o valor 1; se nenhum bit nas expressões de entrada for 1, o bit no resultado será definido como 0.  
  
 Se as expressões de esquerda e direita têm tipos de dados inteiros diferentes (por exemplo, à esquerda *expressão* é **smallint** e *expressão* é  **int**), o argumento do tipo de dados menor é convertido para o tipo de dados maior. Neste exemplo, o **smallint***expressão* é convertido em um **int**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma tabela com **int** dados tipos para mostrar os valores originais e coloca a tabela em uma linha.  
  
```tsql  
CREATE TABLE bitwise  
(   
 a_int_value int NOT NULL,  
b_int_value int NOT NULL  
);  
GO  
INSERT bitwise VALUES (170, 75);  
GO  
```  
  
 A consulta a seguir executa o OR bit a bit no **a_int_value** e **b_int_value** colunas.  
  
```  
SELECT a_int_value | b_int_value  
FROM bitwise;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-----------   
235           
  
(1 row(s) affected)  
```  
  
 A representação binária de 170 (**a_int_value** ou `A`, abaixo) é `0000 0000 1010 1010`. A representação binária de 75 (**b_int_value** ou `B`, abaixo) é `0000 0000 0100 1011`. A execução da operação OR bit a bit nesses dois valores produz o resultado binário `0000 0000 1110 1011`, que é o decimal 235.  
  
```  
(A | B)  
0000 0000 1010 1010  
0000 0000 0100 1011  
-------------------  
0000 0000 1110 1011  
```  
  
## <a name="see-also"></a>Consulte também  
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Operadores bit a bit &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [&#124; = &#40; OR bit a bit é igual a &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)   
 [Composta operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  



