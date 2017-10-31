---
title: BINARY_CHECKSUM (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BINARY_CHECKSUM
- BINARY_CHECKSUM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- BINARY_CHECKSUM function
- binary [SQL Server], checksum values
ms.assetid: 07fece4d-58e3-446e-a3b5-92fe24d2d1fb
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b84847f3efe7224c6fa0ad945b03f3afbc1381b9
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="binarychecksum--transact-sql"></a>BINARY_CHECKSUM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

Retorna o valor binário da soma de verificação calculado em uma linha de tabela ou em uma lista de expressões.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
BINARY_CHECKSUM ( * | expression [ ,...n ] )   
```  
  
## <a name="arguments"></a>Argumentos  
*\**  
Especifica que o cálculo é feito em todas as colunas da tabela. BINARY_CHECKSUM ignora colunas de tipos de dados não comparáveis em sua computação. Tipos de dados não comparáveis incluem **texto**, **ntext**, **imagem**, **cursor**, **xml**, e não comparáveis tipos common language runtime (CLR) definidos pelo usuário.
  
*expressão*  
É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer tipo. BINARY_CHECKSUM ignora expressões de tipos de dados não comparáveis em sua computação.
  
## <a name="remarks"></a>Comentários  
BINARY_CHECKSUM(*), calculado em qualquer linha de uma tabela, retorna o mesmo valor enquanto a linha não for modificada subsequentemente. BINARY_CHECKSUM satisfaz as propriedades de uma função de hash: BINARY_CHECKSUM aplicado em quaisquer duas listas de expressões retorna o mesmo valor se os elementos correspondentes das duas listas tiverem o mesmo tipo e forem iguais quando comparados com o operador de igualdade (=). Para essa definição, os valores nulos de um tipo especificado são considerados para serem comparados como iguais. Se um dos valores da lista de expressão for alterado, em geral, a soma de verificação da lista também será alterada. Entretanto, há uma pequena chance de que a soma de verificação não seja alterada. Por esse motivo, é recomendável não usar BINARY_CHECKSUM para detectar se os valores foram alterados, a menos que seu aplicativo pode tolerar ausente, ocasionalmente, uma alteração. Considere o uso de HashBytes. Quando um algoritmo de hash MD5 é especificado, a probabilidade de HashBytes retornar o mesmo resultado para duas entradas diferentes é muito menor que BINARY_CHECKSUM.
  
BINARY_CHECKSUM pode ser aplicado sobre uma lista de expressões e retorna o mesmo valor para uma lista especificada. BINARY_CHECKSUM aplicado sobre duas listas de expressões retorna o mesmo valor se os elementos correspondentes das duas listas tiverem o mesmo tipo e representação de byte. Nessa definição, os valores nulos de um tipo especificado são considerados como possuidores da mesma representação de byte.
  
BINARY_CHECKSUM e CHECKSUM são funções semelhantes: Elas podem ser usadas para calcular um valor de soma em uma lista de expressões e a ordem das expressões afeta o valor resultante. A ordem de colunas usada em BINARY_CHECKSUM(*) é a ordem de colunas especificada na tabela ou definição de exibição. Esses incluem colunas computadas.
  
CHECKSUM e BINARY_CHECKSUM retornam valores diferentes para os tipos de dados de cadeia de caracteres, em que o local pode fazer com que as cadeias de caracteres com representação diferente sejam iguais. Os tipos de dados de cadeia de caracteres são **char**, **varchar**, **nchar**, **nvarchar**, ou **sql_variant** (se a tipo de base de **sql_variant** é um tipo de dados de cadeia de caracteres). Por exemplo, os valores de BINARY_CHECKSUM para as cadeias de caracteres "McCavity" e "Mccavity" são diferentes. Em contraste, em um servidor que não faz distinção entre maiúsculas e minúsculas, CHECKSUM retorna os mesmos valores de soma para essas cadeias de caracteres. Os valores de CHECKSUM não devem ser comparados com valores de BINARY_CHECKSUM.
 
BINARY_CHECKSUM oferece suporte a até 8.000 caracteres do tipo **varbinary (max)** e até 255 caracteres de tipo **nvarchar (max)**.
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir usa `BINARY_CHECKSUM` para detectar alterações em uma linha da tabela.
  
```sql
USE AdventureWorks2012;  
GO  
CREATE TABLE myTable (column1 int, column2 varchar(256));  
GO  
INSERT INTO myTable VALUES (1, 'test');  
GO  
SELECT BINARY_CHECKSUM(*) from myTable;  
GO  
UPDATE myTable set column2 = 'TEST';  
GO  
SELECT BINARY_CHECKSUM(*) from myTable;  
GO  
```  
  
## <a name="see-also"></a>Consulte também
[Funções de agregação &#40; Transact-SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[Soma de verificação &#40; Transact-SQL &#41;](../../t-sql/functions/checksum-transact-sql.md)  
[CHECKSUM_AGG &#40; Transact-SQL &#41;](../../t-sql/functions/checksum-agg-transact-sql.md)
  
  

