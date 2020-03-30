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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 506f3f0e79501b16ea5455ab1ff4d4ee83a7abff
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68040213"
---
# <a name="binary_checksum--transact-sql"></a>BINARY_CHECKSUM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

Retorna o valor binário da soma de verificação calculado em uma linha de tabela ou em uma lista de expressões.
  
![Ícone de link do artigo](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do artigo") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
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
  
## <a name="remarks"></a>Comentários  
`BINARY_CHECKSUM(*)`, calculado em qualquer linha de uma tabela, retorna o mesmo valor contanto que a linha não seja modificada posteriormente. `BINARY_CHECKSUM` satisfaz as propriedades de uma função de hash: quando aplicado em quaisquer duas listas de expressões retorna o mesmo valor se os elementos correspondentes das duas listas tiverem o mesmo tipo e forem iguais quando comparados com o operador de igualdade (=). Para essa definição, dizemos que valores nulos, de um tipo especificado, são comparados como valores iguais. Se, pelo menos, um dos valores na lista de expressões for alterado, a soma de verificação da expressão também poderá ser alterada. Entretanto, essa alteração não é garantida e, para detectar se os valores foram alterados, recomendamos o uso de `BINARY_CHECKSUM` somente se o aplicativo pode tolerar uma alteração ausente ocasional. Caso contrário, considere a possibilidade de usar o `HASHBYTES`. Com um algoritmo de hash MD5 especificado, a probabilidade de que `HASHBYTES` retornará o mesmo resultado para duas entradas diferentes é muito menor que `BINARY_CHECKSUM`.
  
`BINARY_CHECKSUM` pode operar sobre uma lista de expressões e retorna o mesmo valor para uma lista especificada. `BINARY_CHECKSUM` aplicado sobre duas listas de expressões retorna o mesmo valor se os elementos correspondentes das duas listas tiverem o mesmo tipo e representação de byte. Nessa definição, os valores nulos de um tipo especificado são considerados como possuidores da mesma representação de byte.
  
`BINARY_CHECKSUM` e `CHECKSUM` são funções semelhantes. Elas podem ser usadas para calcular um valor de soma em uma lista de expressões e a ordem das expressões afeta o valor resultante. A ordem das colunas usada para `BINARY_CHECKSUM(*)` é a mesma especificada na definição de tabela ou exibição. Essa ordem inclui as colunas computadas.
  
`BINARY_CHECKSUM` e `CHECKSUM` retornam valores diferentes para os tipos de dados de cadeia de caracteres, em que a localidade pode fazer com que as cadeias de caracteres com uma representação diferente sejam comparadas como iguais. Os tipos de dados de cadeia de caracteres são  

* **char**  
* **nchar**  
* **nvarchar**  
* **varchar**  

ou  

* **sql_variant** (se o tipo base de **sql_variant** for um tipo de dados string).  
  
Por exemplo, as cadeias de caracteres "McCavity" e "Mccavity" têm diferentes valores `BINARY_CHECKSUM`. Por outro lado, para um servidor que não diferencia maiúsculas de minúsculas, `CHECKSUM` retorna os mesmos valores de soma de verificação para essas cadeias de caracteres. Você deve evitar a comparação dos valores de `CHECKSUM` com os valores de `BINARY_CHECKSUM`.
 
`BINARY_CHECKSUM` é compatível com qualquer comprimento do tipo **varbinary(max)** e até 255 caracteres do tipo **nvarchar(max)** .
  
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
[CHECKSUM_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-agg-transact-sql.md)  
[CHECKSUM &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)  
[HASHBYTES &#40;Transact-SQL&#41;](../../t-sql/functions/hashbytes-transact-sql.md)  
  
  
