---
title: Precisão, escala e comprimento (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: bf6c6caf1162c3b2257ffea9c051fa7634250fd2
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52507258"
---
# <a name="precision-scale-and-length-transact-sql"></a>Precisão, escala e comprimento (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

A precisão é o número de dígitos em um número. A escala é o número de dígitos à direita da casa decimal em um número. Por exemplo, o número 123,45 tem uma precisão de 5 e uma escala de 2.
  
Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a precisão máxima padrão dos tipos de dados **numeric** e **decimal** é 38. Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o máximo padrão é 28.
  
O comprimento de um tipo de dados numérico é o número de bytes usado para armazenar o número. Comprimento de uma cadeia de caracteres ou tipo de dados de Unicode é o número de caracteres. O comprimento para os tipos de dados **binary**, **varbinary** e **image** é o número de bytes. Por exemplo, um tipo de dados **int** pode conter 10 dígitos, é armazenado em 4 bytes e não aceita casas decimais. O tipo de dados **int** tem uma precisão de 10, um comprimento de 4 e uma escala de 0.
  
Quando duas expressões **char**, **varchar**, **binary** ou **varbinary** forem concatenadas, o comprimento da expressão resultante será a soma dos comprimentos das duas expressões de origem ou 8.000 caracteres, o que for menor.
  
Quando duas expressões **char** ou **varchar** forem concatenadas, o comprimento da expressão resultante será a soma dos comprimentos das duas expressões de origem ou 4.000 caracteres, o que for menor.
  
Quando duas expressões com o mesmo tipo de dados mas com comprimentos diferentes são comparados usando UNION, EXCEPT ou INTERSECT, o comprimento resultante é o comprimento máximo das duas expressões.
  
A precisão e a escala dos tipos de dados numéricos além de **decimal** são fixos. Se um operador aritmético tiver duas expressões do mesmo tipo, o resultado terá o mesmo tipo de dados com precisão e escala definidas para esse tipo. Se um operador aritmético tiver duas expressões com tipos de dados numéricos diferentes, a regras de precedência do tipo de dados definirão os tipos de dados do resultado. O resultado terá a precisão e a escala definidas para seu tipo de dados.
  
A tabela a seguir define como a precisão e a escala do resultado são calculadas quando o resultado de uma operação é do tipo **decimal**. O resultado é **decimal** quando uma das seguintes condições é verdadeira:
-   As duas expressões são do tipo **decimal**.  
-   Uma expressão é **decimal** e a outra é um tipo de dados com uma precedência inferior a **decimal**.  
  
As expressões de operandos são indicadas como expressão e1, com precisão p1 e escala s1, e expressão e2, com precisão p2 e escala s2. A precisão e a escala de qualquer expressão que não seja **decimal** serão aquelas definidas para o tipo de dados da expressão.
  
|Operação|Precisão de resultado|Escala de resultado*|  
|---|---|---|
|e1 + e2|máx(s1, s2) + máx(p1-s1, p2-s2) + 1|máx(s1, s2)|  
|e1 - e2|máx(s1, s2) + máx(p1-s1, p2-s2) + 1|máx(s1, s2)|  
|e1 * e2|p1 + p2 + 1|s1 + s2|  
|e1 / e2|p1 - s1 + s2 + máx(6, s1 + p2 + 1)|máx(6, s1 + p2 + 1)|  
|e1 { UNION &#124; EXCEPT &#124; INTERSECT } e2|máx(s1, s2) + máx(p1-s1, p2-s2)|máx(s1, s2)|  
|e1 % e2|mín(p1-s1, p2 -s2) + máx( s1,s2 )|máx(s1, s2)|  
  
\* A precisão e a escala de resultado têm um máximo absoluto de 38. Se a precisão de resultado for maior que 38, ela será reduzida a 38, e a escala correspondente será reduzida para tentar evitar que alguma parte do resultado seja truncada. Em alguns casos, como multiplicação ou divisão, o fator de escala não será reduzido para manter a precisão decimal, embora o erro de estouro possa ser gerado.

Em operações de adição e subtração, precisamos de `max(p1 - s1, p2 - s2)` casas para armazenar parte integral do número decimal. Se não houver espaço suficiente para armazená-los ou seja, `max(p1 - s1, p2 - s2) < min(38, precision) - scale`, a escala será reduzida para fornecer espaço suficiente para a parte integral. A escala resultante será `MIN(precision, 38) - max(p1 - s1, p2 - s2)`, portanto, a parte fracionária poderá ser arredondada para se ajustar à escala resultante.

Em operações de multiplicação e divisão, precisamos de `precision - scale` casa para armazenar a parte integral do resultado. A escala pode ser reduzida usando as seguintes regras:
1.  A escala resultante será reduzida a `min(scale, 38 - (precision-scale))` se a parte integral for menor que 32, pois ela não pode ser maior que `38 - (precision-scale)`. Nesse caso, o resultado pode ser arredondado.
1. A escala não será alterada se for inferior a 6 e se a parte integral for maior do que 32. Nesse caso, o erro de estouro poderá ser gerado se ela não couber em decimal(38, scale) 
1. A escala será definida como 6 se for maior do que 6 e se a parte integral for maior do que 32. Nesse caso, tanto a parte integral quanto a escala seriam reduzidas e o tipo resultante seria decimal (38,6). O resultado pode ser arredondado para até 6 decimais ou um erro de estouro será gerado se parte integral não couber dentro 32 dígitos.

## <a name="examples"></a>Exemplos
A expressão a seguir retorna o resultado `0.00000090000000000` sem arredondamento, pois os resultados cabe em `decimal(38,17)`:
```sql
select cast(0.0000009000 as decimal(30,20)) * cast(1.0000000000 as decimal(30,20)) [decimal 38,17]
```
Neste caso, a precisão é de 61 e escala é de 40.
Aparte integral (escala de precisão = 21) é menor que 32, portanto, isso é caso (1) nas regras de multiplicação e a escala é calculada como `min(scale, 38 - (precision-scale)) = min(40, 38 - (61-40)) = 17`. O tipo de resultado é `decimal(38,17)`.

A expressão a seguir retorna o resultado `0.000001` para caber em `decimal(38,6)`:
```sql
select cast(0.0000009000 as decimal(30,10)) * cast(1.0000000000 as decimal(30,10)) [decimal(38, 6)]
```
Neste caso, a precisão é de 61 e escala é de 20.
A escala é maior do que 6 e a parte integral (`precision-scale = 41`) é maior do que 32. Isso é caso (3) nas regras de multiplicação e tipo de resultado é `decimal(38,6)`.

## <a name="see-also"></a>Confira também
[Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
