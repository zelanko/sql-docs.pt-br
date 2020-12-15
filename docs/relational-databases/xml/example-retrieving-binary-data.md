---
title: 'Exemplo: Recuperando dados binários | Microsoft Docs'
description: Veja um exemplo de uma consulta SQL que recupera dados binários usando as opções RAW e BINARY BASE64 com a cláusula XML FOR.
ms.custom: ''
ms.date: 04/03/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, retrieving binary data example
ms.assetid: 5cea5d49-58ac-403a-a933-c4fd91de400b
author: RothJa
ms.author: jroth
ms.openlocfilehash: fedec9e351b9c8910db0bee51c1e2c5dc8569655
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97402973"
---
# <a name="example-retrieving-binary-data"></a>Exemplo: Recuperando dados binários

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

A consulta a seguir retorna a foto do produto armazenada em uma coluna do tipo **varbinary(max)** . A opção `BINARY BASE64` é especificada na consulta para retornar os dados binários em formato codificado na base 64.

## <a name="example"></a>Exemplo

```sql
USE AdventureWorks2012;
GO
SELECT ProductPhotoID, ThumbNailPhoto
FROM Production.ProductPhoto
WHERE ProductPhotoID=1
FOR XML RAW, BINARY BASE64 ;
GO
```

Espere o seguinte resultado:

```console
<row ProductModelID="1" ThumbNailPhoto="base64 encoded binary data"/>
```

## <a name="see-also"></a>Consulte Também

[Usar o modo RAW com FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)
