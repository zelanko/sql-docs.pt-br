---
title: 'Exemplo: Renomeando a &lt;linha&gt; elemento | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, renaming <row> example
ms.assetid: b042292a-0b6e-40a3-b254-71c06e626706
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01b835696c5e64182cffb72aea80d53b3c3bb776
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58532128"
---
# <a name="example-renaming-the-ltrowgt-element"></a>Exemplo: Renomeando a &lt;linha&gt; elemento
  Para cada linha no conjunto de resultados, o modo RAW gera um elemento `<row>`. Opcionalmente, é possível especificar outro nome para esse elemento especificando um argumento opcional para o modo RAW, conforme mostrado nesta consulta. A consulta retorna um elemento <`ProductModel`> para cada linha do conjunto de dados.  
  
## <a name="example"></a>Exemplo  
  
```  
SELECT ProductModelID, Name   
FROM Production.ProductModel  
WHERE ProductModelID=122  
FOR XML RAW ('ProductModel'), ELEMENTS  
GO  
```  
  
 Este é o resultado. Como a diretiva `ELEMENTS` é adicionada à consulta, o resultado é centrado em elemento.  
  
```  
<ProductModel>  
  <ProductModelID>122</ProductModelID>  
  <Name>All-Purpose Bike Stand</Name>  
</ProductModel>   
```  
  
## <a name="see-also"></a>Consulte também  
 [Usar modo RAW com FOR XML](use-raw-mode-with-for-xml.md)  
  
  
