---
title: Binary e varbinary (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 8/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- binary_TSQL
- varbinary_TSQL
- binary
- varbinary
dev_langs: TSQL
helpviewer_keywords:
- varbinary data type
- binary [SQL Server], about binary data type
ms.assetid: bcce65f9-10db-4b3e-bfaf-dfc06c6f820f
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4ad5bce3cacc0f892f7087df785da8cedcb4e932
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="binary-and-varbinary-transact-sql"></a>binary e varbinary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Tipos de dados binários de comprimento fixo ou comprimento variável.
  
## <a name="arguments"></a>Argumentos  
**binário** [(  *n*  )] dados binários de comprimento fixo com um comprimento de  *n*  bytes, onde  *n*  é um valor de 1 a 8.000. O tamanho de armazenamento é  *n*  bytes.
  
**varbinary** [(  *n*   |  **max**)] dados binários de comprimento variável. *n*pode ser um valor de 1 a 8.000. **Max** indica que o tamanho máximo de armazenamento é 2 ^ 31-1 bytes. O tamanho de armazenamento é o comprimento real dos dados inseridos + 2 bytes. Os dados inseridos podem ter 0 bytes de comprimento. O sinônimo ANSI SQL para **varbinary** é **binário variável**.
  
## <a name="remarks"></a>Comentários  
Quando  *n*  não for especificado em uma definição de dados ou uma instrução de declaração de variável, o comprimento padrão é 1. Quando  *n*  não é especificado com a função CAST, o comprimento padrão é 30.

| Tipo de dados | Use quando... |
| --- | --- |
| **binary** | os tamanhos das entradas de dados de coluna são consistentes.|
| **varbinary** | os tamanhos das entradas de dados de coluna variarem consideravelmente.|
| **varbinary(max)** | as entradas de dados de coluna excederem 8.000 bytes.|


## <a name="converting-binary-and-varbinary-data"></a>Convertendo dados binary e varbinary
Quando os dados são convertidos de um tipo de dados de cadeia de caracteres (**char**, **varchar**, **nchar**, **nvarchar**, **binário**, **varbinary**, **texto**, **ntext**, ou **imagem**) para um **binário** ou **varbinary** tipo de dados de comprimento diferente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] preenche ou trunca os dados à direita. Quando outros tipos de dados são convertidos em **binário** ou **varbinary**, os dados são preenchidos ou truncados à esquerda. O preenchimento é realizado por meio de zeros hexadecimais.
  
Conversão de dados para o **binário** e **varbinary** tipos de dados é útil se **binário** dados são a maneira mais fácil de mover os dados. Converter qualquer valor de qualquer tipo para um valor binário de grande suficiente tamanho e, em seguida, volta para o tipo, sempre resulta no mesmo valor se ambas as conversões estiverem acontecendo na mesma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A representação binária de um valor pode ser alterada de uma versão para outra do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
Você pode converter **int**, **smallint**, e **tinyint** para **binário** ou **varbinary**, mas se você converter o **binário** valor para um valor inteiro, esse valor será diferente do valor inteiro original se houver truncamento. Por exemplo, a instrução SELECT a seguir mostra que o valor inteiro `123456` normalmente é armazenado como um binário `0x0001e240`:
  
```sql
SELECT CAST( 123456 AS BINARY(4) );  
```  
  
No entanto, o seguinte `SELECT` instrução mostra que, se o **binário** destino é muito pequeno para conter o valor inteiro, os dígitos à esquerda serão silenciosamente truncados de forma que o mesmo número é armazenado como `0xe240`:
  
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
>  Conversões entre todos os dados de tipo e o **binário** não há garantia de tipos de dados para ser o mesmo entre versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Conversão de tipo de dados &#40; mecanismo de banco de dados &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
