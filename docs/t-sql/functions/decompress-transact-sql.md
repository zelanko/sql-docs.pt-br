---
description: DECOMPRESS (Transact-SQL)
title: DECOMPRESS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECOMPRESS
- DECOMPRESS_TSQL
helpviewer_keywords:
- DECOMPRESS function
ms.assetid: 738d56be-3870-4774-b112-3dce27becc11
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9d6851056673a896e1b07a26ee5d50142272a31a
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91116424"
---
# <a name="decompress-transact-sql"></a>DECOMPRESS (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

Esta função descompactará um valor de expressão de entrada usando o algoritmo GZIP. `DECOMPRESS` retornará uma matriz de bytes (tipo VARBINARY(MAX)).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
DECOMPRESS ( expression )  
```  
  
## <a name="arguments"></a>Argumentos
 *expressão*  
Um valor **varbinary(** _n_ **)** , **varbinary(max)** ou **binary(** _n_ **)** . Para saber mais, veja [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="return-types"></a>Tipos de retorno  
Um valor de tipo de dados **varbinary (max)**. `DECOMPRESS` usará o algoritmo ZIP para descompactar o argumento de entrada. O usuário deve converter explicitamente o resultado em um tipo de destino, se necessário.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-decompress-data-at-query-time"></a>a. Descompactar os dados no momento da consulta  
Este exemplo mostra como retornar dados de tabela compactados:  
  
```sql  
SELECT _id, name, surname, datemodified,  
             CAST(DECOMPRESS(info) AS NVARCHAR(MAX)) AS info  
FROM player;  
```  
  
### <a name="b-display-compressed-data-using-computed-column"></a>B. Exibir dados compactados usando uma coluna computada  
Este exemplo mostra como criar uma tabela para armazenar dados descompactados:  
  
```sql  
CREATE TABLE example_table (  
    _id INT PRIMARY KEY IDENTITY,  
    name NVARCHAR(max),  
    surname NVARCHAR(max),  
    info VARBINARY(max),  
    info_json as CAST(DECOMPRESS(info) as NVARCHAR(max))  
);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [COMPRESS &#40;Transact-SQL&#41;](../../t-sql/functions/compress-transact-sql.md)  
  
  
