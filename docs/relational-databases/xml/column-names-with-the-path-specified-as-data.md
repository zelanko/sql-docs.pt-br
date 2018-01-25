---
title: Nomes de coluna com o caminho especificado como data() | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: names [SQL Server], columns with
ms.assetid: 0b738e44-6108-4417-a9a4-abeb7680d899
caps.latest.revision: "10"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e97d1a5fc6a121dab9411deedfb5bea494513abb
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="column-names-with-the-path-specified-as-data"></a>Nomes de colunas com o caminho especificado como data()
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] Se o caminho especificado como nome da coluna for "data()", o valor será tratado com um valor atômico no XML gerado. Um caractere de espaço será adicionado ao XML se o próximo item na serialização também for um valor atômico. Isso é útil quando você está criando elemento de tipo lista e valores de atributos. A consulta a seguir recupera a ID e o nome do modelo do produto e a lista de produtos naquele modelo do produto.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID       AS "@ProductModelID",  
       Name                 AS "@ProductModelName",  
      (SELECT ProductID AS "data()"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
      FOR XML PATH (''))    AS "@ProductIDs"  
FROM  Production.ProductModel  
WHERE ProductModelID= 7   
FOR XML PATH('ProductModelData');  
```  
  
 O SELECT aninhado recupera uma lista de IDs de produtos. Ele especifica "data()" como o nome da coluna para IDs de produtos. Como o modo PATH especifica uma cadeia de caracteres vazia para o nome do elemento de linha, não há nenhum elemento de linha gerado. Em vez disso, os valores são retornados conforme são atribuídos a um atributo ProductIDs do elemento de linha <`ProductModelData`> do SELECT pai. Este é o resultado:  
  
 `<ProductModelData ProductModelID="7"`  
  
 `ProductModelName="HL Touring Frame"`  
  
 `ProductIDs="885 887 888 889 890 891 892 893" />`  
  
## <a name="see-also"></a>Consulte Também  
 [Usar o modo PATH com FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
