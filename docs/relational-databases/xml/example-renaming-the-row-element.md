---
title: 'Exemplo: renomeando o elemento &lt;row&gt; | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, renaming <row> example
ms.assetid: b042292a-0b6e-40a3-b254-71c06e626706
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 275b1c6c138b11fa6330dc61fbfbfd2014a229c5
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68006804"
---
# <a name="example-renaming-the-ltrowgt-element"></a>Exemplo: renomeando o elemento &lt;row&gt;
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
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
 [Usar o modo RAW com FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  
