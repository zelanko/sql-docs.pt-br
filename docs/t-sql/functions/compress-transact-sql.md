---
description: COMPRESS (Transact-SQL)
title: COMPRESS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- COMPRESS
- COMPRESS_TSQL
helpviewer_keywords:
- COMPRESS function
ms.assetid: c2bfe9b8-57a4-48b4-b028-e1a3ed5ece88
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 51cf2e37ae548383d7c02b3ba4028b9327857928
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468176"
---
# <a name="compress-transact-sql"></a>COMPRESS (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

Esta função compacta a expressão de entrada usando o algoritmo GZIP. A função retorna uma matriz de bytes do tipo **varbinary(max)**.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
COMPRESS ( expression )  
```  
  
## <a name="arguments"></a>Argumentos
*expressão*  
Um

* **binary(***n***)**
* **char(***n***)**
* **nchar(***n***)**
* **nvarchar(max)**
* **nvarchar(***n***)**
* **varbinary(max)**
* **varbinary(***n***)**
* **varchar(max)**

ou

* **varchar(***n***)**

expressão. Para saber mais, veja [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).
  
## <a name="return-types"></a>Tipos de retorno
**varbinary(max)** representa o conteúdo compactado da entrada.
  
## <a name="remarks"></a>Comentários  
Dados compactados não podem ser indexados.
  
A função `COMPRESS` compacta os dados de expressão de entrada. É necessário invocar essa função para cada seção de dados a ser compactada. Veja [Compactação de dados](../../relational-databases/data-compression/data-compression.md) para saber mais sobre a compactação de dados automática durante o armazenamento no nível de linha ou página.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-compress-data-during-the-table-insert"></a>a. Compactar dados durante a inserção de tabela  
O seguinte exemplo mostra como compactar dados inseridos em uma tabela:
  
```sql
INSERT INTO player (name, surname, info )  
VALUES (N'Ovidiu', N'Cracium',   
        COMPRESS(N'{"sport":"Tennis","age": 28,"rank":1,"points":15258, turn":17}'));  
  
INSERT INTO player (name, surname, info )  
VALUES (N'Michael', N'Raheem', compress(@info));  
```  
  
### <a name="b-archive-compressed-version-of-deleted-rows"></a>B. Arquivar a versão compactada de linhas excluídas  
Primeiro, essa instrução exclui registros antigos do player da tabela `player`. Para economizar espaço, em seguida, armazena os registros na tabela `inactivePlayer`, em um formato compactado.
  
```sql
DELETE FROM player  
OUTPUT deleted.id, deleted.name, deleted.surname, deleted.datemodifier, COMPRESS(deleted.info)   
INTO dbo.inactivePlayers
WHERE datemodified < @startOfYear; 
```  
  
## <a name="see-also"></a>Confira também
[Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
[DECOMPRESS &#40;Transact-SQL&#41;](../../t-sql/functions/decompress-transact-sql.md)
  
  
