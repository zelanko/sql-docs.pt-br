---
title: "Tipo de dados precedência (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- precedence [SQL Server]
- data types [SQL Server], converting
- data types [SQL Server], precedence
- converting data types [SQL Server], precedence
- precedence [SQL Server], data types
ms.assetid: f4c804ab-ed3f-43b1-a024-c9ac6944b66b
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9f39337e00dfdbcd4a6bb01a00093a61f46a79fa
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="data-type-precedence-transact-sql"></a>Precedência de tipo de dados (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Quando um operador combinar duas expressões com tipos de dados diferentes, as regras de precedência do tipo de dados especificam que o mesmo, com a precedência mais baixa, será convertido para o tipo de dado de maior precedência. Se a conversão não for uma conversão implícita com suporte, um erro será retornado. Quando ambas as expressões de operando tiverem o mesmo tipo de dados, o resultado da operação terá aquele tipo de dados.
  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa a seguinte ordem de precedência para tipos de dados:
  
1.  UDT (tipos de dados definidos pelo usuário) (maior)  
1.  **sql_variant**  
1.  **xml**  
1.  **datetimeoffset**  
1.  **datetime2**  
1.  **datetime**  
1.  **smalldatetime**  
1.  **date**  
1. **time**  
1. **float**  
1. **real**  
1. **decimal**  
1. **money**  
1. **smallmoney**  
1. **bigint**  
1. **int**  
1. **smallint**  
1. **tinyint**  
1. **bit**  
1. **ntext**  
1. **texto**  
1. **imagem**  
1. **timestamp**  
1. **uniqueidentifier**  
1. **nvarchar** (incluindo **nvarchar (max)** )  
1. **nchar**  
1. **varchar** (incluindo **varchar (max)** )  
1. **char**  
1. **varbinary** (incluindo **varbinary (max)** )  
1. **binário** (menor)  
  
## <a name="see-also"></a>Consulte também
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

