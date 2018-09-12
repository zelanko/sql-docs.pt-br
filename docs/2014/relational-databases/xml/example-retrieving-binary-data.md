---
title: 'Exemplo: recuperando dados binários | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, retrieving binary data example
ms.assetid: 5cea5d49-58ac-403a-a933-c4fd91de400b
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 32be7d9c93f7179cf7bc5e9a7d2de31b76b2a0b6
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43888662"
---
# <a name="example-retrieving-binary-data"></a>Exemplo: Recuperando dados binários
  A consulta a seguir retorna a fotografia do produto armazenada em uma coluna de tipo `varbinary(max)`. A opção `BINARY BASE64` é especificada na consulta para retornar os dados binários em formato codificado na base 64.  
  
## <a name="example"></a>Exemplo  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductPhotoID, ThumbNailPhoto  
FROM Production.ProductPhoto  
WHERE ProductPhotoID=1  
FOR XML RAW, BINARY BASE64 ;  
GO  
```  
  
 Este é o resultado:  
  
```  
<row ProductModelID="1" ThumbNailPhoto="base64 encoded binary data"/>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Usar modo RAW com FOR XML](use-raw-mode-with-for-xml.md)  
  
  
