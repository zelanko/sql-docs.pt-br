---
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
ms.openlocfilehash: d4fcf2cf0eb10bc7312923c887314b36e04b369d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85682652"
---
# <a name="decompress-transact-sql"></a>DECOMPRESS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

Esta função descompactará um valor de expressão de entrada usando o algoritmo GZIP. `DECOMPRESS` retornará uma matriz de bytes (tipo VARBINARY(MAX)).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DECOMPRESS ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
Um valor **varbinary(** _n_ **)** , **varbinary(max)** ou **binary(** _n_ **)** . Para saber mais, veja [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="return-types"></a>Tipos de retorno  
Um valor de tipo de dados **varbinary (max)** . `DECOMPRESS` usará o algoritmo ZIP para descompactar o argumento de entrada. O usuário deve converter explicitamente o resultado em um tipo de destino, se necessário.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-decompress-data-at-query-time"></a>a. Descompactar os dados no momento da consulta  
Este exemplo mostra como retornar dados de tabela compactados:  
  
```  
SELECT _id, name, surname, datemodified,  
             CAST(DECOMPRESS(info) AS NVARCHAR(MAX)) AS info  
FROM player;  
```  
  
### <a name="b-display-compressed-data-using-computed-column"></a>B. Exibir dados compactados usando uma coluna computada  
Este exemplo mostra como criar uma tabela para armazenar dados descompactados:  
  
```  
CREATE TABLE example_table (  
    _id int primary key identity,  
    name nvarchar(max),  
    surname nvarchar(max),  
    info varbinary(max),  
    info_json as CAST(decompress(info) as nvarchar(max))  
);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [COMPRESS &#40;Transact-SQL&#41;](../../t-sql/functions/compress-transact-sql.md)  
  
  
