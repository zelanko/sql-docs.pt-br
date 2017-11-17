---
title: COMPACTAR (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- COMPRESS
- COMPRESS_TSQL
helpviewer_keywords:
- COMPRESS function
ms.assetid: c2bfe9b8-57a4-48b4-b028-e1a3ed5ece88
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c30cb5f351d9a84beec608483380edb94b8c7844
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="compress-transact-sql"></a>COMPACTAR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Compacta a expressão de entrada usando o algoritmo GZIP. O resultado da compactação é a matriz de bytes de tipo **varbinary (max)**.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
COMPRESS ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
*expressão*  
É um **nvarchar (***n***)**, **nvarchar (max)**, **varchar (**  *n*  **)**, **varchar (max)**, **varbinary (**  *n*  **)**, **varbinary (max)**, **char (***n***)**, **(nchar**   *n*  **)**, ou **binário (***n***)** expressão. Para obter mais informações, veja [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).
  
## <a name="return-types"></a>Tipos de retorno
Retorna o tipo de dados de **varbinary (max)** que representa o conteúdo compactado de entrada.
  
## <a name="remarks"></a>Comentários  
Dados compactados não podem ser indexados.
  
A função COMPRESS compacta os dados fornecidos como expressão de entrada e deve ser chamada para cada seção de dados deve ser compactado. Para a compactação no nível de linha ou de página automática durante o armazenamento, consulte [compactação de dados](../../relational-databases/data-compression/data-compression.md).
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-compress-data-during-the-table-insert"></a>A. Compactar dados durante a inserção de tabela  
O exemplo a seguir mostra como compactar dados inseridos na tabela:
  
```sql
INSERT INTO player (name, surname, info )  
VALUES (N'Ovidiu', N'Cracium',   
        COMPRESS(N'{"sport":"Tennis","age": 28,"rank":1,"points":15258, turn":17}'));  
  
INSERT INTO player (name, surname, info )  
VALUES (N'Michael', N'Raheem', compress(@info));  
```  
  
### <a name="b-archive-compressed-version-of-deleted-rows"></a>B. Versão compactada do arquivo morto de linhas excluídas  
A instrução a seguir exclui registros antigos do player do `player` de tabela e armazena os registros a `inactivePlayer` tabela em um formato compactado para economizar espaço.
  
```sql
DELETE player  
WHERE datemodified < @startOfYear  
OUTPUT id, name, surname datemodifier, COMPRESS(info)   
INTO dbo.inactivePlayers ;  
```  
  
## <a name="see-also"></a>Consulte também
[Funções de cadeia de caracteres &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
[Descompactar &#40; Transact-SQL &#41;](../../t-sql/functions/decompress-transact-sql.md)
  
  

