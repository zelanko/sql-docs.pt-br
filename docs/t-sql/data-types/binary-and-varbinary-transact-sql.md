---
title: binary e varbinary (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 8/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- binary_TSQL
- varbinary_TSQL
- binary
- varbinary
dev_langs:
- TSQL
helpviewer_keywords:
- varbinary data type
- binary [SQL Server], about binary data type
ms.assetid: bcce65f9-10db-4b3e-bfaf-dfc06c6f820f
caps.latest.revision: 27
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: eb67f7bbfe21b1e213e5ef166b54f91ae4b3513c
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39454990"
---
# <a name="binary-and-varbinary-transact-sql"></a>binary e varbinary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Tipos de dados binários de comprimento fixo ou comprimento variável.
  
## <a name="arguments"></a>Argumentos  
**binary** [ ( *n* ) ] Dados binários de comprimento fixo com um tamanho de *n* bytes, em que *n* é um valor de 1 a 8.000. O tamanho do armazenamento é *n* bytes.
  
**varbinary** [ ( *n* | **max**) ] Dados binários de tamanho variável. *n* pode ser um valor de 1 a 8.000. **max** indica que o tamanho de armazenamento máximo é de 2^31-1 bytes. O tamanho do armazenamento é o tamanho real dos dados inseridos + 2 bytes. Os dados inseridos podem ter 0 bytes de comprimento. O sinônimo ANSI SQL para **varbinary** é **binary varying**.
  
## <a name="remarks"></a>Remarks  
Quando *n* não é especificado em uma definição de dados ou instrução de declaração de variável, o tamanho padrão é 1. Quando *n* não é especificado com a função CAST, o tamanho padrão é 30.

| Tipo de dados | Use quando... |
| --- | --- |
| **binary** | os tamanhos das entradas de dados de coluna forem consistentes.|
| **varbinary** | os tamanhos das entradas de dados de coluna variarem consideravelmente.|
| **varbinary(max)** | as entradas de dados de coluna excederem 8.000 bytes.|


## <a name="converting-binary-and-varbinary-data"></a>Convertendo dados binary e varbinary
Quando os dados são convertidos de um tipo de dados de cadeia de caracteres (**char**, **varchar**, **nchar**, **nvarchar**, **binary**, **varbinary**, **text**, **ntext** ou **image**) em um tipo de dados **binary** ou **varbinary** de tamanho diferente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] preenche ou trunca os dados à direita. Quando outros tipos de dados são convertidos em **binary** ou **varbinary**, os dados são preenchidos ou truncados à esquerda. O preenchimento é realizado por meio de zeros hexadecimais.
  
A conversão de dados em tipos de dados **binary** e **varbinary** é útil se os dados **binary** são a maneira mais fácil de mover os dados. A conversão de qualquer valor de qualquer tipo em um valor binário de tamanho grande o suficiente e, em seguida, novamente no tipo, sempre resulta no mesmo valor se ambas as conversões ocorrem na mesma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A representação binária de um valor pode ser alterada de uma versão para outra do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
Você pode converter **int**, **smallint** e **tinyint** em **binary** ou **varbinary**, mas se você converter o valor **binary** de volta para um valor inteiro, esse valor será diferente do valor inteiro original, caso tenha ocorrido truncamento. Por exemplo, a instrução SELECT a seguir mostra que o valor inteiro `123456` normalmente é armazenado como um binário `0x0001e240`:
  
```sql
SELECT CAST( 123456 AS BINARY(4) );  
```  
  
Entretanto, a seguinte instrução `SELECT` mostra que se o destino **binary** for muito pequeno para manter o valor inteiro, os dígitos à esquerda serão silenciosamente truncados, de forma que o mesmo número seja armazenado como `0xe240`:
  
```sql
SELECT CAST( 123456 AS BINARY(2) );  
```  
  
O lote seguinte mostra que esse truncamento silencioso pode afetar operações aritméticas sem gerar um erro:
  
```sql
DECLARE @BinaryVariable2 BINARY(2);  
  
SET @BinaryVariable2 = 123456;  
SET @BinaryVariable2 = @BinaryVariable2 + 1;  
  
SELECT CAST( @BinaryVariable2 AS INT);  
GO  
```  
  
O resultado final é `57921`, não `123457`.
  
> [!NOTE]  
>  As conversões entre qualquer tipo de dados e os tipos de dados **binary** não têm garantia de serem as mesmas entre as versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Confira também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Conversão de tipo de dados &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
