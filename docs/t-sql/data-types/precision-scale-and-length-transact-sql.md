---
title: "Precisão, escala e comprimento (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], length
- data types [SQL Server], scale
- precision [SQL Server], data types
- lengths [SQL Server], data types
- number of digits
- scale [SQL Server]
- scale [SQL Server], data types
- data types [SQL Server], precision
ms.assetid: fbc9ad2c-0d3b-4e98-8fdd-4d912328e40a
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 557d7a5c45e9cc5a0839dfb4a1fdb0d08c2bf83f
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="precision-scale-and-length-transact-sql"></a>Precisão, escala e comprimento (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

A precisão é o número de dígitos em um número. A escala é o número de dígitos à direita da casa decimal em um número. Por exemplo, o número 123,45 tem uma precisão de 5 e uma escala de 2.
  
Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a precisão máxima padrão de **numérico** e **decimal** tipos de dados é 38. Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o máximo padrão é 28.
  
O comprimento de um tipo de dados numérico é o número de bytes usado para armazenar o número. Comprimento de uma cadeia de caracteres ou tipo de dados de Unicode é o número de caracteres. O comprimento de **binário**, **varbinary**, e **imagem** tipos de dados é o número de bytes. Por exemplo, um **int** tipo de dados pode conter 10 dígitos, é armazenado em 4 bytes e não aceita casas decimais. O **int** tipo de dados tem uma precisão de 10, um comprimento de 4 e uma escala de 0.
  
Quando dois **char**, **varchar**, **binário**, ou **varbinary** expressões são concatenadas, o comprimento da expressão resultante é a a soma dos comprimentos das duas expressões de origem ou 8.000 caracteres, o que for menor.
  
Quando dois **nchar** ou **nvarchar** expressões são concatenadas, o comprimento da expressão resultante é a soma dos comprimentos das duas expressões de origem ou 4.000 caracteres, o que for menor.
  
Quando duas expressões com o mesmo tipo de dados mas com comprimentos diferentes são comparados usando UNION, EXCEPT ou INTERSECT, o comprimento resultante é o comprimento máximo das duas expressões.
  
A precisão e escala dos tipos de dados numéricos além **decimal** corrigidos. Se um operador aritmético tiver duas expressões do mesmo tipo, o resultado terá o mesmo tipo de dados com precisão e escala definidas para esse tipo. Se um operador aritmético tiver duas expressões com tipos de dados numéricos diferentes, a regras de precedência do tipo de dados definirão os tipos de dados do resultado. O resultado terá a precisão e a escala definidas para seu tipo de dados.
  
A tabela a seguir define como a precisão e a escala do resultado são calculadas quando o resultado de uma operação é do tipo **decimal**. O resultado é **decimal** quando uma das seguintes opções for verdadeira:
-   As duas expressões são **decimal**.  
-   Uma expressão é **decimal** e a outra é um tipo de dados com uma precedência inferior à **decimal**.  
  
As expressões de operandos são indicadas como expressão e1, com precisão p1 e escala s1, e expressão e2, com precisão p2 e escala s2. A precisão e escala de qualquer expressão que não seja **decimal** é a precisão e escala definidas para o tipo de dados da expressão.
  
|Operação|Precisão de resultado|Escala de resultado*|  
|---|---|---|
|e1 + e2|máx(s1, s2) + máx(p1-s1, p2-s2) + 1|máx(s1, s2)|  
|e1 - e2|máx(s1, s2) + máx(p1-s1, p2-s2) + 1|máx(s1, s2)|  
|e1 * e2|p1 + p2 + 1|s1 + s2|  
|e1 / e2|p1 - s1 + s2 + máx(6, s1 + p2 + 1)|máx(6, s1 + p2 + 1)|  
|E1 {UNION &#124; EXCETO &#124; E2 INTERSECT}|máx(s1, s2) + máx(p1-s1, p2-s2)|máx(s1, s2)|  
|e1 % e2|mín(p1-s1, p2 -s2) + máx( s1,s2 )|máx(s1, s2)|  
  
\*A precisão de resultado e a escala tem um máximo absoluto de 38. Quando a precisão de resultado for maior que 38, é reduzido a 38 e a escala correspondente será reduzida para impedir que a parte de um resultado sendo truncado. Em alguns casos, como multiplicação ou divisão, fator de escala não será reduzido para manter a precisão decimal, embora o erro de estouro pode ser gerado.

Em operações de adição e subtração precisamos `max(p1 – s1, p2 – s2)` locais para armazenar parte integrante do número decimal. Se não houver espaço suficiente para armazená-los ou seja, `max(p1 – s1, p2 – s2) < min(38, precision) – scale`, a escala será reduzida para fornecer espaço suficiente para parte integral. Escala resultante é `MIN(precision, 38) - max(p1 – s1, p2 – s2)`, portanto, a parte fracionária pode ser arredondada para se ajustar à escala resultante.

Em operações de multiplicação e divisão precisamos `precision - scale` locais para armazenar a parte integral do resultado. A escala pode ser reduzida usando as seguintes regras:
1.  A escala resultante é reduzida ao `min(scale, 38 – (precision-scale))` se a parte integral é menor que 32, porque ele não pode ser maior que `38 – (precision-scale)`. Nesse caso o resultado pode ser arredondado.
1. A escala não será alterada se for inferior a 6 e se a parte integral é maior do que 32. Nesse caso, o erro de estouro pode ser gerado se ela não couber em decimal (38, escala) 
1. A escala será definida para 6 se for maior que 6 e se a parte integral é maior do que 32. Nesse caso, seriam reduzidos parte integrante e escala e o tipo resultante é decimal(38,6). Resultado pode ser arredondado até 6 decimais ou erro de estouro será lançado se parte integral não cabe dentro 32 dígitos.

## <a name="examples"></a>Exemplos
A expressão a seguir retorna o resultado `0.00000090000000000` sem arredondamento, pois os resultados podem ser ajustadas no `decimal(38,17)`:
```sql
select cast(0.0000009000 as decimal(30,20)) * cast(1.0000000000 as decimal(30,20)) [decimal 38,17]
```
Nesse caso, a precisão é 61 e escala é 40.
Parte integrante (escala de precisão = 21) é menor que 32, portanto esse for o caso (1) nas regras de multiplicação e escala é calculada como `min(scale, 38 – (precision-scale)) = min(40, 38 – (61-40)) = 17`. Tipo de resultado é `decimal(38,17)`.

A expressão a seguir retorna o resultado `0.000001` para caber na `decimal(38,6)`:
```sql
select cast(0.0000009000 as decimal(30,10)) * cast(1.0000000000 as decimal(30,10)) [decimal(38, 6)]
```
Nesse caso, a precisão é 61 e escala é 20.
Escala é maior que a parte integral e 6 (`precision-scale = 41`) é maior do que 32. Esse é o caso (3) nas regras de multiplicação e tipo de resultado é `decimal(38,6)`.

## <a name="see-also"></a>Consulte também
[Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  

