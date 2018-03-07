---
title: ^ (Bit a bit exclusivo) (Transact-SQL) | Microsoft Docs
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
- ^_TSQL
- Bitwise Exclusive OR
- Exclusive
- ^
- bitwise
- OR
dev_langs:
- TSQL
helpviewer_keywords:
- ^ (bitwise exclusive OR operator)
- OR operator
- exclusive OR mathematical operations
- bitwise exclusive OR (^)
ms.assetid: f38f0ad4-46d0-40ea-9851-0f928fda5293
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b5833bd94dd28f6c09b2f1c05d4a59a8a137ddad
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="-bitwise-exclusive-or-transact-sql"></a>^ (OR exclusivo bit a bit) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Executa uma operação OR exclusiva bit a bit entre dois valores inteiros.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
expression ^ expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer um dos tipos de dados da categoria de tipo de dados inteiro, ou o **bit**, ou o **binário** ou **varbinary** tipos de dados. *expressão* é tratado como um número binário para a operação bit a bit.  
  
> [!NOTE]  
>  Apenas uma *expressão* pode ser do **binário** ou **varbinary** tipo de dados em uma operação bit a bit.  
  
## <a name="result-types"></a>Tipos de resultado  
 **int** se os valores de entrada são **int**.  
  
 **smallint** se os valores de entrada são **smallint**.  
  
 **tinyint** se os valores de entrada são **tinyint**.  
  
## <a name="remarks"></a>Remarks  
 O  **^**  operador bit a bit executa um lógica OR exclusivo bit a bit entre as duas expressões, usando cada bit para ambas as expressões correspondente. Os bits no resultado são definidos como 1 se um dos dois bits  (mas não ambos) para o bit atual a ser resolvido nas expressões de entrada tiver o valor de 1. Se os dois bits forem 0 ou 1, o bit no resultado será limpo com o valor 0.  
  
 Se as expressões de esquerda e direita têm tipos de dados inteiros diferentes (por exemplo, à esquerda *expressão* é **smallint** e *expressão* é  **int**), o argumento do tipo de dados menor é convertido para o tipo de dados maior. Nesse caso, o **smallint * expressão* é convertido em um **int**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma tabela usando o **int** dados de tipo para armazenar os valores originais e insere os dois valores em uma linha.  
  
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
  
 A consulta a seguir executa o OR exclusivo bit a bit nas colunas `a_int_value` e `b_int_value`.  
  
```  
SELECT a_int_value ^ b_int_value  
FROM bitwise;  
GO  
```  
  
 Este é o conjunto de resultados:  
  
```  
-----------   
225           
  
(1 row(s) affected)  
```  
  
 A representação binária de 170 (`a_int_value` ou `A`) é `0000 0000 1010 1010`. A representação binária de 75 (`b_int_value` ou `B`) é `0000 0000 0100 1011`. A execução da operação OR exclusivo bit a bit nesses dois valores produz o resultado binário `0000 0000 1110 0001`, que é o decimal 225.  
  
```  
(A ^ B)     
         0000 0000 1010 1010  
         0000 0000 0100 1011  
         -------------------  
         0000 0000 1110 0001  
```  
  

  
## <a name="see-also"></a>Consulte também  
 [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Operadores bit a bit &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [^ = &#40; Bit a bit exclusivo ou atribuição &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)   
 [Composta operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  


