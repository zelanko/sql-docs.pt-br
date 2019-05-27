---
title: ~ (NOT bit a bit) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ~_TSQL
- bitwise
- NOT
- "~"
- Bitwise NOT
dev_langs:
- TSQL
helpviewer_keywords:
- NOT keyword
- bitwise NOT (~)
- ~ (bitwise NOT)
ms.assetid: 02da8016-f6c0-41ae-8d59-33eaa02bfc95
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5957410faa3bcc2870712e01857216c2ef526008
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65981323"
---
# <a name="-bitwise-not-transact-sql"></a>~ (NOT bit a bit) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Executa uma operação lógica NOT bit a bit em um valor inteiro.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
~ expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É qualquer [expression](../../t-sql/language-elements/expressions-transact-sql.md) válida de qualquer um dos tipos de dados da categoria de tipo de dados inteiro ou dos tipos de dados **bit**, **binary** ou **varbinary**. *expression* é tratada como um número binário para a operação bit a bit.  
  
> [!NOTE]  
>  Apenas uma *expression* pode ser do tipo de dados **binary** ou **varbinary** em uma operação bit a bit.  
  
## <a name="result-types"></a>Tipos de resultado  
 **int** se os valores de entrada são **int**.  
  
 **smallint** se os valores de entrada são **smallint**.  
  
 **tinyint** se os valores de entrada são **tinyint**.  
  
 **bit** se os valores de entrada são **bit**.  
  
## <a name="remarks"></a>Remarks  
 O operador bit a bit **~** executa uma expressão NOT lógica bit a bit para a *expression*, usando um bit por vez. Se *expression* tiver o valor 0, os bits no conjunto de resultados serão definidos como 1; caso contrário, o bit no resultado será limpo com o valor 0. Em outras palavras, uns são alterados para zeros e zeros são alterados para uns.  
  
> [!IMPORTANT]  
>  Ao executar qualquer tipo de operação bit a bit, o comprimento do armazenamento da expressão usada na operação bit a bit é importante. Recomenda-se usar esse mesmo número de bytes ao armazenar valores. Por exemplo, o armazenamento do valor decimal 5 como **tinyint**, **smallint** ou **int** produz um valor armazenado com diferentes números de bytes: **tinyint** armazena dados usando 1 byte; **smallint** armazena dados usando 2 bytes e **int** armazena dados usando 4 bytes. Portanto, a execução de uma operação bit a bit em um valor decimal **int** pode produzir resultados diferentes do que o uso de uma conversão binária ou hexadecimal direta, especialmente quando o operador **~** (expressão NOT bit a bit) é usado. A operação NOT bit a bit pode ocorrer em uma variável de um comprimento mais curto. Nesse caso, quando o comprimento mais curto for convertido em uma variável de tipo de dados mais longo, os bits nos 8 bits superiores podem não ser definidos com o valor esperado. Recomenda-se converter a variável de tipo de dados menor no tipo de dados maior e depois executar a operação NOT no resultado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma tabela usando o tipo de dados **int** para armazenar os valores e insere os dois valores em uma linha.  
  
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
  
 
## <a name="see-also"></a>Consulte Também  
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Operadores bit a bit &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  


