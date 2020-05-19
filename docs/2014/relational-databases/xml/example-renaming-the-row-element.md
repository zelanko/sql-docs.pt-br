---
title: 'Exemplo: renomeando o elemento &lt;row&gt; | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, renaming <row> example
ms.assetid: b042292a-0b6e-40a3-b254-71c06e626706
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3780bb0f35c65003f7a5bdb126ca7597786758a9
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716902"
---
# <a name="example-renaming-the-ltrowgt-element"></a>Exemplo: renomeando o elemento &lt;row&gt;
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
  
## <a name="see-also"></a>Consulte Também  
 [Usar o modo RAW com FOR XML](use-raw-mode-with-for-xml.md)  
  
  
