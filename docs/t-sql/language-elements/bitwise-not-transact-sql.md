---
title: ~ (NOT bit a bit) (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/10/2017
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
- ~_TSQL
- bitwise
- NOT
- ~
- Bitwise NOT
dev_langs: TSQL
helpviewer_keywords:
- NOT keyword
- bitwise NOT (~)
- ~ (bitwise NOT)
ms.assetid: 02da8016-f6c0-41ae-8d59-33eaa02bfc95
caps.latest.revision: "42"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5bd0f8234088fbb358740d5c9b4e753d9ecaa11d
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="-bitwise-not-transact-sql"></a>~ (NOT bit a bit) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Executa uma operação lógica NOT bit a bit em um valor inteiro.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
~ expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer um dos tipos de dados da categoria de tipo de dados inteiro, o **bit**, ou o **binário** ou **varbinary** dados tipos. *expressão* é tratado como um número binário para a operação bit a bit.  
  
> [!NOTE]  
>  Apenas uma *expressão* pode ser do **binário** ou **varbinary** tipo de dados em uma operação bit a bit.  
  
## <a name="result-types"></a>Tipos de resultado  
 **int** se os valores de entrada são **int**.  
  
 **smallint** se os valores de entrada são **smallint**.  
  
 **tinyint** se os valores de entrada são **tinyint**.  
  
 **bit** se os valores de entrada são **bit**.  
  
## <a name="remarks"></a>Remarks  
 O  **~**  operador bit a bit executa um NOT lógico bit a bit para o *expressão*, obtendo cada bit por vez. Se *expressão* tem um valor de 0, os bits no conjunto de resultados são definidos como 1; caso contrário, o bit no resultado será alterado para um valor de 0. Em outras palavras, uns são alterados para zeros e zeros são alterados para uns.  
  
> [!IMPORTANT]  
>  Ao executar qualquer tipo de operação bit a bit, o comprimento do armazenamento da expressão usada na operação bit a bit é importante. Recomenda-se usar esse mesmo número de bytes ao armazenar valores. Por exemplo, armazenar o valor decimal 5 como um **tinyint**, **smallint**, ou **int** produz um valor armazenado com diferentes números de bytes: **tinyint** armazena dados usando 1 byte; **smallint** armazena dados usando 2 bytes, e **int** armazena dados que usa 4 bytes. Portanto, executar uma operação bit a bit em uma **int** valor decimal pode produzir resultados diferentes daqueles usando uma conversão binária ou hexadecimal direta, especialmente quando o  **~**  ( NOT bit a bit) é usado. A operação NOT bit a bit pode ocorrer em uma variável de um comprimento mais curto. Nesse caso, quando o comprimento mais curto for convertido em uma variável de tipo de dados mais longo, os bits nos 8 bits superiores podem não ser definidos com o valor esperado. Recomenda-se converter a variável de tipo de dados menor no tipo de dados maior e depois executar a operação NOT no resultado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma tabela usando o **int** tipo para armazenar os valores de dados e insere os dois valores em uma linha.  
  
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
  
 A consulta a seguir executa o NOT bit a bit nas colunas `a_int_value` e `b_int_value`.  
  
```  
SELECT ~ a_int_value, ~ b_int_value  
FROM bitwise;  
```  
  
 Este é o conjunto de resultados:  
  
```  
--- ---   
-171  -76   
  
(1 row(s) affected)  
```  
  
 A representação binária de 170 (`a_int_value` ou `A`) é `0000 0000 1010 1010`. A execução da operação NOT bit a bit nesse valor produz o resultado binário `1111 1111 0101 0101`, que é o decimal -171. A representação binária de 75 é `0000 0000 0100 1011`. A execução da operação NOT bit a bit produz `1111 1111 1011 0100`, que é o decimal -76.  
  
```  
 (~A)     
         0000 0000 1010 1010  
         -------------------  
         1111 1111 0101 0101  
(~B)     
         0000 0000 0100 1011  
         -------------------  
         1111 1111 1011 0100  
```  
  
 
## <a name="see-also"></a>Consulte também  
 [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Operadores bit a bit &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  


