---
title: "Soma de verificação (Transact-SQL) | Microsoft Docs"
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
- CHECKSUM_TSQL
- CHECKSUM
dev_langs:
- TSQL
helpviewer_keywords:
- hash indexes
- CHECKSUM function
- checksum values
ms.assetid: e26d3339-845c-49c2-9d89-243376874c13
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0379260c517f546bf00c5e757f6a3069f574f102
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="checksum-transact-sql"></a>CHECKSUM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

Retorna o valor da soma de verificação calculado em uma linha de uma tabela ou em uma lista de expressões. CHECKSUM foi desenvolvido para ser usado na criação de índices de hash.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CHECKSUM ( * | expression [ ,...n ] )  
```  
  
## <a name="arguments"></a>Argumentos  
\*  
Especifica que o cálculo é feito em todas as colunas da tabela. CHECKSUM retorna um erro se alguma coluna for do tipo de dados não comparável. Tipos de dados não comparáveis são **texto**, **ntext**, **imagem**, XML, e **cursor**e também **sql_variant**com qualquer um dos tipos anteriores como seu tipo base.
  
*expressão*  
É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer tipo, exceto um tipo de dados não comparáveis.
  
## <a name="return-types"></a>Tipos de retorno
 **int**  
  
## <a name="remarks"></a>Comentários  
CHECKSUM calcula um valor de hash, chamado de soma de verificação, em sua lista de argumentos. O valor de hash deve ser usado na criação de índices de hash. Se os argumentos de CHECKSUM forem colunas e um índice for criado no valor de CHECKSUM calculado, o resultado será um índice de hash. Isso pode ser usado para pesquisas de igualdade em colunas.
  
CHECKSUM satisfaz as propriedades de uma função de hash: CHECKSUM aplicado em quaisquer duas listas de expressões retorna o mesmo valor se os elementos correspondentes das duas listas tiverem o mesmo tipo e forem iguais quando comparados com o operador de igualdade (=). Para essa definição, os valores nulos de um tipo especificado são considerados para serem comparados como iguais. Se um dos valores da lista de expressão for alterado, em geral, a soma de verificação da lista também será alterada. Entretanto, há uma pequena chance de que a soma de verificação não seja alterada. Por esse motivo, não recomendamos o uso de CHECKSUM para detectar se os valores foram alterados, a não ser que o aplicativo ofereça suporte, ocasionalmente, para a ausência de uma alteração. Considere o uso de [HashBytes](../../t-sql/functions/hashbytes-transact-sql.md) em vez disso. Quando um algoritmo de hash MD5 é especificado, a probabilidade de HashBytes retornar o mesmo resultado para duas entradas diferentes é muito maior que o do retorno de CHECKSUM.
  
A ordem das expressões afeta o valor resultante de CHECKSUM. A ordem das colunas usada com CHECKSUM(*) é a mesma especificada na definição da tabela ou exibição. Isso inclui as colunas computadas.
  
O valor de CHECKSUM é dependente do agrupamento. O mesmo valor armazenado com um agrupamento diferente retornará um valor de CHECKSUM diferente.
  
## <a name="examples"></a>Exemplos  
Os exemplos a seguir mostram como usar `CHECKSUM` para criar índices de hash. O índice de hash é criado adicionando-se uma coluna de soma de verificação calculada à tabela que está sendo indexada e, em seguida, criando um índice na coluna de soma de verificação.
  
```sql
-- Create a checksum index.  
SET ARITHABORT ON;  
USE AdventureWorks2012;   
GO  
ALTER TABLE Production.Product  
ADD cs_Pname AS CHECKSUM(Name);  
GO  
CREATE INDEX Pname_index ON Production.Product (cs_Pname);  
GO  
```  
  
O índice de soma de verificação pode ser usado como um índice de hash, especialmente para melhorar a velocidade de indexação quando a coluna a ser indexada é uma coluna de caracteres longa. O índice de soma de verificação pode ser usado para pesquisas de igualdade.
  
```sql
/*Use the index in a SELECT query. Add a second search   
condition to catch stray cases where checksums match,   
but the values are not the same.*/  
SELECT *   
FROM Production.Product  
WHERE CHECKSUM(N'Bearing Ball') = cs_Pname  
AND Name = N'Bearing Ball';  
GO  
```  
  
A criação do índice na coluna computada materializa a coluna de soma de verificação e todas as alterações no valor de `ProductName` serão propagados na coluna de soma de verificação. Opcionalmente, um índice pode ser criado diretamente na coluna indexada. No entanto, se os valores de chave forem longos, um índice normal provavelmente não será executado, assim como um índice de soma de verificação.
  
## <a name="see-also"></a>Consulte também
[CHECKSUM_AGG &#40; Transact-SQL &#41;](../../t-sql/functions/checksum-agg-transact-sql.md)  
[HASHBYTES &#40; Transact-SQL &#41;](../../t-sql/functions/hashbytes-transact-sql.md)  
[BINARY_CHECKSUM &#40; Transact-SQL &#41;](../../t-sql/functions/binary-checksum-transact-sql.md)
  
  

