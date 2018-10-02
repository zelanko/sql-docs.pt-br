---
title: BINARY_CHECKSUM (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 392e21cdf50dc537e5bf6cdfcadf18771e66aad7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47759684"
---
# <a name="binarychecksum--transact-sql"></a>BINARY_CHECKSUM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

Retorna o valor binário da soma de verificação calculado em uma linha de tabela ou em uma lista de expressões.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
BINARY_CHECKSUM ( * | expression [ ,...n ] )   
```  
  
## <a name="arguments"></a>Argumentos  
*\**  
Especifica que a computação abrange todas as colunas da tabela. BINARY_CHECKSUM ignora colunas de tipos de dados não comparáveis em sua computação. Tipos de dados não comparáveis incluem  
* **cursor**  
* **imagem**  
* **ntext**  
* **text**  
* **xml**  

e tipos CLR (Common Language Runtime) definidos pelo usuário não comparáveis.
  
*expressão*  
Uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer tipo. BINARY_CHECKSUM ignora expressões de tipos de dados não comparáveis em sua computação.

## <a name="return-types"></a>Tipos de retorno  
 **int**
  
## <a name="remarks"></a>Remarks  
BINARY_CHECKSUM(*), calculado em qualquer linha de uma tabela, retorna o mesmo valor enquanto a linha não for modificada subsequentemente. BINARY_CHECKSUM atende às propriedades de uma função de hash: BINARY_CHECKSUM, aplicado a duas listas de expressões quaisquer, retorna o mesmo valor se os elementos correspondentes das duas listas têm o mesmo tipo e são iguais, quando comparados usando o operador de igualdade (=). Para essa definição, dizemos que valores nulos, de um tipo especificado, são comparados como valores iguais. Se, pelo menos, um dos valores na lista de expressões for alterado, a soma de verificação da expressão também poderá ser alterada. No entanto, isso não é garantido. Portanto, para detectar se os valores foram alterados, recomendamos o uso de BINARY_CHECKSUM somente se o aplicativo puder tolerar uma alteração ausente ocasional. Caso contrário, considere o uso de HashBytes. Com um algoritmo de hash MD5 especificado, a probabilidade de que HashBytes retornará o mesmo resultado para duas entradas diferentes é muito menor em comparação com BINARY_CHECKSUM.
  
BINARY_CHECKSUM pode operar sobre uma lista de expressões e retorna o mesmo valor para uma lista especificada. BINARY_CHECKSUM aplicado sobre duas listas de expressões retorna o mesmo valor se os elementos correspondentes das duas listas tiverem o mesmo tipo e representação de byte. Nessa definição, os valores nulos de um tipo especificado são considerados como possuidores da mesma representação de byte.
  
BINARY_CHECKSUM e CHECKSUM são funções semelhantes: Elas podem ser usadas para calcular um valor de soma em uma lista de expressões e a ordem das expressões afeta o valor resultante. A ordem de colunas usada em BINARY_CHECKSUM(*) é a ordem de colunas especificada na tabela ou definição de exibição. Isso inclui as colunas computadas.
  
BINARY_CHECKSUM e CHECKSUM retornam valores diferentes para os tipos de dados de cadeia de caracteres, em que a localidade pode fazer com que as cadeias de caracteres com uma representação diferente sejam comparadas como iguais. Os tipos de dados de cadeia de caracteres são  

* **char**  
* **nchar**  
* **nvarchar**  
* **varchar**  

ou em  

* **sql_variant** (se o tipo base de **sql_variant** for um tipo de dados string).  
  
Por exemplo, as cadeias de caracteres "McCavity" e "Mccavity" têm diferentes valores BINARY_CHECKSUM. Por outro lado, para um servidor que não diferencia maiúsculas de minúsculas, CHECKSUM retorna os mesmos valores de soma de verificação para essas cadeias de caracteres. Você deve evitar a comparação de valores de soma CHECKSUM com valores de BINARY_CHECKSUM.
 
BINARY_CHECKSUM é compatível com até 8.000 caracteres do tipo **varbinary(max)** e até 255 caracteres do tipo **nvarchar(max)**.
  
## <a name="examples"></a>Exemplos  
Este exemplo usa `BINARY_CHECKSUM` para detectar as alterações em uma linha da tabela.
  
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
  
## <a name="see-also"></a>Confira também
[Funções de agregação &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[CHECKSUM &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)  
[CHECKSUM_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-agg-transact-sql.md)
  
  
