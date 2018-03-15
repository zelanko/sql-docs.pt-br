---
title: '&amp; (AND bit a bit) (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 01/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- bitwise
- '&'
- '&_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- AND, bitwise AND
- '& (bitwise AND)'
- bitwise AND (&)
ms.assetid: 20275755-4fa7-47b1-a9be-ac85606d63b0
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 094c127434f2339a4a3e977c4455ca6ce904ab01
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="amp-bitwise-and-transact-sql"></a>&amp; (AND bit a bit) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Executa uma operação lógica AND bit a bit entre dois valores inteiros.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
expression & expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É qualquer [expression](../../t-sql/language-elements/expressions-transact-sql.md) válida de um dos tipos de dados da categoria de tipo de dados inteiro ou os tipos de dados **bit**, **binary** ou **varbinary**. *expression* é tratada como um número binário para a operação bit a bit.  
  
> [!NOTE]  
>  Em uma operação bit a bit, apenas uma *expression* pode ser do tipo de dados **binary** ou **varbinary**.  
  
## <a name="result-types"></a>Tipos de resultado  
 **int** se os valores de entrada são **int**.  
  
 **smallint** se os valores de entrada são **smallint**.  
  
 **tinyint** se os valores de entrada são **tinyint** ou **bit**.  
  
## <a name="remarks"></a>Remarks  
 O operador bit a bit **&** executa uma expressão AND lógica bit a bit entre as duas expressões, usando cada bit correspondente para as duas expressões. Os bits no resultado são definidos como 1 se e somente se os dois bits (para o bit atual a ser resolvido) nas expressões de entrada tiverem um valor de 1; caso contrário, o bit no resultado será definido como 0.  
  
 Se as expressões à esquerda e à direita tiverem tipos de dados inteiros diferentes (por exemplo, a *expression* à esquerda é **smallint** e a *expression* à direita é **int**), o argumento do tipo de dados menor será convertido no tipo de dados maior. Nesse caso, a **smallint***expression* é convertida em um **int**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma tabela usando o tipo de dados **int** para armazenar os valores e insere dois valores em uma linha.  
  
```  
CREATE TABLE bitwise  
(   
a_int_value int NOT NULL,  
b_int_value int NOT NULL  
);  
GO  
INSERT bitwise VALUES (170, 75);  
GO  
```  
  
 Esta consulta executa o AND bit a bit nas colunas `a_int_value` e `b_int_value`.  
  
```  
SELECT a_int_value & b_int_value  
FROM bitwise;  
GO  
```  
  
 Este é o conjunto de resultados:  
  
```  
-----------   
10            
  
(1 row(s) affected)  
```  
  
 A representação binária de 170 (`a_int_value` ou `A`) é `0000 0000 1010 1010`. A representação binária de 75 (`b_int_value` ou `B`) é `0000 0000 0100 1011`. A execução da operação AND bit a bit nesses dois valores produz o resultado binário `0000 0000 0000 1010`, que é o decimal 10.  
  
```  
(A & B)  
0000 0000 1010 1010  
0000 0000 0100 1011  
-------------------  
0000 0000 0000 1010  
```  
  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Operadores bit a bit &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [&= &#40;Atribuição de AND bit a bit&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)   
 [Operadores compostos &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  


