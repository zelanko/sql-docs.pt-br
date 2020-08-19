---
description: ntext, text e image (Transact-SQL)
title: ntext, text e image (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ntext_TSQL
- ntext
dev_langs:
- TSQL
helpviewer_keywords:
- text data type, about text data type
- text [SQL Server], data types
- ntext data type
- ntext data type, about ntext data type
- image data type, about image data type
ms.assetid: b0d8769c-7598-4f97-8162-ace5f182b5bc
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b7b067831ca56d3dc5797aa68e4810a7e9969946
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459949"
---
# <a name="ntext-text-and-image-transact-sql"></a>ntext, text e image (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Tipos de dados fixos e de comprimento variável para armazenar dados binários e de caracteres não Unicode e Unicode grandes. Dados Unicode usam o conjunto de caracteres UNICODE UCS-2.
  
>**IMPORTANTE:**  Os tipos de dados **ntext**, **text** e **image** serão removidos em uma versão futura do SQL Server. Evite usar esses tipos de dados em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que os utilizam atualmente. Em vez disso, use [nvarchar(max)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), [varchar(max)](../../t-sql/data-types/char-and-varchar-transact-sql.md)e [varbinary(max)](../../t-sql/data-types/binary-and-varbinary-transact-sql.md) .  
  
## <a name="arguments"></a>Argumentos
**ntext**  
Dados Unicode de comprimento variável com um comprimento máximo de cadeia de caracteres de 2^30 - 1 (1.073.741.823) bytes. O tamanho de armazenamento, em bytes, é duas vezes o comprimento da cadeia de caracteres inserido. O sinônimo ISO de **ntext** é **national text**.
  
**text**  
Dados não Unicode de comprimento variável na página de código do servidor e com um comprimento máximo de cadeia de caracteres de 2^31-1 (2.147.483.647). Quando a página de código de servidor usar caracteres de dois bytes, o armazenamento ainda será de 2.147.483.647 bytes. Dependendo da cadeia de caracteres, o tamanho do armazenamento pode ser menor que 2.147.483.647 bytes.
  
**imagem**  
Dados binários do comprimento variável de 0 a 2^31-1 (2.147.483.647) bytes.
  
## <a name="remarks"></a>Comentários  
As funções e instruções a seguir podem ser usadas com os dados **ntext**, **text** ou **image**.
  
|Funções|Instruções|  
|---|---|
|[DATALENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/datalength-transact-sql.md)|[READTEXT &#40;Transact-SQL&#41;](../../t-sql/queries/readtext-transact-sql.md)|  
|[PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)|[SET TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/statements/set-textsize-transact-sql.md)|  
|[SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)|[UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)|  
|[TEXTPTR &#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)|[WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)|  
|[TEXTVALID &#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textvalid-transact-sql.md)||  
  
## <a name="see-also"></a>Confira também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Conversão de tipo de dados &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)

