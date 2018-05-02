---
title: COMPRESS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 51324f00da71597a8a2dd37d8f0077c4b3bc8b55
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="compress-transact-sql"></a>COMPRESS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Compacta a expressão de entrada usando o algoritmo GZIP. O resultado da compactação é uma matriz de bytes do tipo **varbinary(max)**.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
COMPRESS ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
*expressão*  
É uma expressão **nvarchar(***n***)**, **nvarchar(max)**, **varchar(***n***)**, **varchar(max)**, **varbinary(***n***)**, **varbinary(max)**, **char(***n***)**, **nchar(***n***)** ou **binary(***n***)**. Para obter mais informações, veja [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).
  
## <a name="return-types"></a>Tipos de retorno
Retorna o tipo de dados **varbinary(max)** que representa o conteúdo compactado da entrada.
  
## <a name="remarks"></a>Remarks  
Dados compactados não podem ser indexados.
  
A função COMPRESS compacta os dados fornecidos como a expressão de entrada e deve ser invocada para cada seção de dados a ser compactada. Para obter a compactação automática no nível da linha ou da página durante o armazenamento, consulte [Compactação de dados](../../relational-databases/data-compression/data-compression.md).
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-compress-data-during-the-table-insert"></a>A. Compactar dados durante a inserção de tabela  
O seguinte exemplo mostra como compactar dados inseridos na tabela:
  
```sql
INSERT INTO player (name, surname, info )  
VALUES (N'Ovidiu', N'Cracium',   
        COMPRESS(N'{"sport":"Tennis","age": 28,"rank":1,"points":15258, turn":17}'));  
  
INSERT INTO player (name, surname, info )  
VALUES (N'Michael', N'Raheem', compress(@info));  
```  
  
### <a name="b-archive-compressed-version-of-deleted-rows"></a>B. Arquivar a versão compactada de linhas excluídas  
A instrução a seguir exclui registros antigos do player da tabela `player` e armazena os registros na tabela `inactivePlayer` em um formato compactado para economizar espaço.
  
```sql
DELETE player  
WHERE datemodified < @startOfYear  
OUTPUT id, name, surname datemodifier, COMPRESS(info)   
INTO dbo.inactivePlayers ;  
```  
  
## <a name="see-also"></a>Confira também
[Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
[DECOMPRESS &#40;Transact-SQL&#41;](../../t-sql/functions/decompress-transact-sql.md)
  
  
