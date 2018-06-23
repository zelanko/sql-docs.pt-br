---
title: 'Exemplo: especificando a diretiva ELEMENT e a codificação de entidade | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ELEMENT directive
- entity encoding [XML]
ms.assetid: 50cda5c1-7293-4080-93b3-872e3b8d484e
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 294ce0b9a064eabfac25b38d4dc171146e463111
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020654"
---
# <a name="example-specifying-the-element-directive-and-entity-encoding"></a>Exemplo: Especificando a diretiva ELEMENT e codificação de entidade
  Este exemplo ilustra a diferença entre as diretivas **ELEMENT** e **XML** . A entidade dos dados é definida pela diretiva **ELEMENT** , mas não pela diretiva **XML** . O elemento \<Summary> é atribuído como XML, `<Summary>This is summary description</Summary>`, na consulta.  
  
 Considere esta consulta:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        ProductModelID  as [ProductModel!1!ProdModelID],  
        Name            as [ProductModel!1!Name],  
        NULL            as [Summary!2!SummaryDescription!ELEMENT]  
FROM    Production.ProductModel  
WHERE   ProductModelID=19  
UNION ALL  
SELECT  2 as Tag,  
        1 as Parent,  
        ProductModelID,  
        NULL,  
       '<Summary>This is summary description</Summary>'  
FROM   Production.ProductModel  
WHERE  ProductModelID=19  
FOR XML EXPLICIT  
```  
  
 Este é o resultado. A entidade da descrição resumida é definida no resultado.  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
  <Summary>  
    <SummaryDescription><Summary>This is summary description</Summary></SummaryDescription>  
  </Summary>  
</ProductModel>  
```  
  
 Agora, se você especificar a diretiva **XML** no nome da coluna, `Summary!2!SummaryDescription!XML`, em vez da diretiva **ELEMENT** , receberá a descrição resumida sem definição de entidade.  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
  <Summary>  
    <SummaryDescription>  
      <Summary>This is summary description</Summary>  
    </SummaryDescription>  
  </Summary>  
</ProductModel>  
```  
  
 Em vez de atribuir um valor de XML estático, a consulta a seguir usa o método **query()** do tipo **xml** para recuperar a descrição resumida do modelo do produto da coluna CatalogDescription de tipo **xml** . Como se sabe que o resultado é de tipo **xml** , nenhuma definição de entidade é aplicada.  
  
```  
SELECT  1 as Tag,  
        0 as Parent,  
        ProductModelID  as [ProductModel!1!ProdModelID],  
        Name            as [ProductModel!1!Name],  
        NULL            as [Summary!2!SummaryDescription]  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not null  
UNION ALL  
SELECT  2 as Tag,  
        1 as Parent,  
        ProductModelID,  
        Name,  
       (SELECT CatalogDescription.query('  
            declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
          /pd:ProductDescription/pd:Summary'))  
FROM     Production.ProductModel  
WHERE    CatalogDescription is not null  
ORDER BY [ProductModel!1!ProdModelID],Tag  
FOR XML EXPLICIT  
```  
  
## <a name="see-also"></a>Consulte também  
 [Usar o modo EXPLICIT com FOR XML](use-explicit-mode-with-for-xml.md)  
  
  