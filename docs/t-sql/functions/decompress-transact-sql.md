---
title: DECOMPRESS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/30/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DECOMPRESS
- DECOMPRESS_TSQL
helpviewer_keywords:
- DECOMPRESS function
ms.assetid: 738d56be-3870-4774-b112-3dce27becc11
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2d2b965d3177be06b46bb51b8f5238f5a4b21dee
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="decompress-transact-sql"></a>DECOMPRESS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Descompacte a expressão de entrada usando o algoritmo GZIP. O resultado da compactação é uma matriz de bytes (tipo VARBINARY(MAX)).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DECOMPRESS ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É um **varbinary(***n***)**, **varbinary(max)** ou **binary(***n***)**. Para obter mais informações, veja [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna o tipo de dados **varbinary(max)**. O argumento de entrada é descompactado com o algoritmo ZIP. O usuário deve converter explicitamente o resultado para um tipo de destino, se necessário.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-decompress-data-at-query-time"></a>A. Descompactar os dados no momento da consulta  
 O seguinte exemplo mostra como mostrar dados compactados em uma tabela:  
  
```  
SELECT _id, name, surname, datemodified,  
             CAST(DECOMPRESS(info) AS NVARCHAR(MAX)) AS info  
FROM player;  
```  
  
### <a name="b-display-compressed-data-using-computed-column"></a>B. Exibir dados compactados usando uma coluna computada  
 O seguinte exemplo mostra como criar uma tabela para armazenar dados descompactados:  
  
```  
CREATE TABLE (  
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
  
  
