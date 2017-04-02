---
title: "Exemplo: Recuperando dados bin&#225;rios | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "modo RAW, exemplo de recuperação de dados binários"
ms.assetid: 5cea5d49-58ac-403a-a933-c4fd91de400b
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 11
---
# Exemplo: Recuperando dados bin&#225;rios
  A consulta a seguir retorna a foto do produto armazenada em uma coluna do tipo **varbinary(max)**. A opção `BINARY BASE64` é especificada na consulta para retornar os dados binários em formato codificado na base 64.  
  
## Exemplo  
  
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
  
## Consulte também  
 [Usar modo RAW com FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  