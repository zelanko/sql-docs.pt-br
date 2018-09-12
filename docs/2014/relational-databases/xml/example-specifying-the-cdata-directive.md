---
title: 'Exemplo: especificando a diretiva CDATA | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- CDATA directive
ms.assetid: 949071e6-787f-480d-bb86-3ac16a027af1
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7384bd9bd0aa7196f71c4a1e50baff438e2d7325
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43889172"
---
# <a name="example-specifying-the-cdata-directive"></a>Exemplo: Especificando a diretiva CDATA
  Se a diretiva for definida como **CDATA**, os dados contidos não serão codificados como entidade, mas colocados na seção CDATA. Os atributos **CDATA** não devem ter nomes.  
  
 A seguinte consulta encapsula a descrição resumida do modelo do produto em uma seção CDATA.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        ProductModelID  as [ProductModel!1!ProdModelID],  
        Name            as [ProductModel!1!Name],  
        '<Summary>This is summary description</Summary>'     
            as [ProductModel!1!!CDATA] -- no attribute name so ELEMENT assumed  
FROM    Production.ProductModel  
WHERE   ProductModelID=19  
FOR XML EXPLICIT  
```  
  
 Este é o resultado:  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
   <![CDATA[<Summary>This is summary description</Summary>]]>  
</ProductModel>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Usar o modo EXPLICIT com FOR XML](use-explicit-mode-with-for-xml.md)  
  
  
