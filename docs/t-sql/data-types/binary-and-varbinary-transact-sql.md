---
title: binary e varbinary (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f267da97eeb409be81bfcca71af602ebce1ffe1c
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86548732"
---
# <a name="binary-and-varbinary-transact-sql"></a>binary e varbinary (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Tipos de dados binários de comprimento fixo ou comprimento variável.
  
## <a name="arguments"></a>Argumentos

**binary** [ ( _n_ ) ] Dados binários de comprimento fixo com um tamanho de _n_ bytes, em que _n_ é um valor de 1 a 8.000. O tamanho do armazenamento é _n_ bytes.
  
**varbinary** [ ( _n_ | **max**) ] Dados binários de tamanho variável. _n_ pode ser um valor de 1 a 8.000. **max** indica que o tamanho de armazenamento máximo é de 2^31-1 bytes. O tamanho do armazenamento é o tamanho real dos dados inseridos + 2 bytes. Os dados inseridos podem ter 0 bytes de comprimento. O sinônimo ANSI SQL para **varbinary** é **binary varying**.
  
## <a name="remarks"></a>Comentários  
O tamanho padrão é 1 quando _n_ não é especificado em uma definição de dados ou instrução de declaração de variável. Quando _n_ não é especificado com a função CAST, o tamanho padrão é 30.

| Tipo de dados | Use quando... |
| --- | --- |
| **binary** | os tamanhos das entradas de dados de coluna forem consistentes.|
| **varbinary** | os tamanhos das entradas de dados de coluna variarem consideravelmente.|
| **varbinary(max)** | as entradas de dados de coluna excederem 8.000 bytes.|


## <a name="converting-binary-and-varbinary-data"></a>Convertendo dados binary e varbinary
Quando são convertidos dados de um tipo de dados String em um tipo de dados **binary** ou **varbinary** de tamanho diferente, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] preenche ou trunca os dados à direita. Esses tipos de dados de cadeia de caracteres são:

* **char** 
* **varchar**
* **nchar**
* **nvarchar**
* **binary**
* **varbinary**
* **text**
* **ntext**
* **imagem**

Quando outros tipos de dados são convertidos em **binary** ou **varbinary**, os dados são preenchidos ou truncados à esquerda. O preenchimento é realizado por meio de zeros hexadecimais.
  
A conversão de dados em tipos de dados **binary** e **varbinary** é útil se os dados **binary** são a maneira mais fácil de mover os dados. Em algum momento, você pode converter um tipo de valor em um valor binário de tamanho grande o suficiente e, em seguida, convertê-lo novamente. Essa conversão sempre resultará no mesmo valor se ambas as conversões estiverem acontecendo na mesma versão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A representação binária de um valor pode ser alterada de uma versão para outra do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
Você pode converter **int**, **smallint** e **tinyint** em **binary** ou **varbinary**. Se converter o valor **binary** de volta para um valor inteiro, esse valor será diferente do valor inteiro original se houver truncamento. Por exemplo, a instrução SELECT a seguir mostra que o valor inteiro `123456` é armazenado como um binário `0x0001e240`:
  
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
  
  
