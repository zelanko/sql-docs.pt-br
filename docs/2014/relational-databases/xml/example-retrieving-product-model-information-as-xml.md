---
title: 'Exemplo: recuperando informações de modelo de produto como XML | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, retrieving XML information example
ms.assetid: 3828b4ca-3ab2-444f-9c58-8be6e7f064a6
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8cc5eb38cf23b82f61d48941fbf828ff494f3049
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716825"
---
# <a name="example-retrieving-product-model-information-as-xml"></a>Exemplo: Recuperando informações de modelo de produto como XML
  A consulta a seguir retorna informações sobre modelos de produtos. `RAW` O modo é especificado na cláusula `FOR XML` .  
  
## <a name="example"></a>Exemplo  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML RAW;  
GO  
```  
  
 Este é o resultado parcial:  
  
 `<row ProductModelID="122" Name="All-Purpose Bike Stand" />`  
  
 `<row ProductModelID="119" Name="Bike Wash" />`  
  
 É possível recuperar XML centrado em elemento especificando a política `ELEMENTS` .  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML RAW, ELEMENTS;  
GO  
```  
  
 Este é o resultado:  
  
```  
<row>  
  <ProductModelID>122</ProductModelID>  
  <Name>All-Purpose Bike Stand</Name>  
</row>  
<row>  
  <ProductModelID>119</ProductModelID>  
  <Name>Bike Wash</Name>  
</row>  
```  
  
 Opcionalmente, é possível especificar a política `TYPE` para recuperar os resultados como tipo `xml`. A política `TYPE` não altera o conteúdo dos resultados. Apenas o tipo de dados dos resultados é afetado.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML RAW, TYPE ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usar o modo RAW com FOR XML](use-raw-mode-with-for-xml.md)  
  
  
