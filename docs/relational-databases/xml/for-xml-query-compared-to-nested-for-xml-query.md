---
title: Consulta XML FOR comparada com consulta XML FOR aninhada | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR XML query
- queries [XML in SQL Server], comparing query types
ms.assetid: 19225b4a-ee3f-47cf-8bcc-52699eeda32c
caps.latest.revision: "11"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 26e2fb52bc52ff9f00fb70f20385533104cb8924
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="for-xml-query-compared-to-nested-for-xml-query"></a>Consulta FOR XML comparada com consulta FOR XML aninhada
  Este tópico compara uma consulta FOR XML de nível único com uma consulta FOR XML aninhada. Um dos benefícios do uso de consultas FOR XML aninhadas é que é possível especificar uma combinação de XML centrado em atributo e em elemento para resultados da consulta. O exemplo demonstra isso.  
  
## <a name="example"></a>Exemplo  
 A consulta `SELECT` a seguir recupera informações de categoria e subcategoria de produtos no banco de dados do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Não há FOR XML aninhado na consulta.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT   ProductCategory.ProductCategoryID,   
         ProductCategory.Name as CategoryName,  
         ProductSubCategory.ProductSubCategoryID,   
         ProductSubCategory.Name  
FROM     Production.ProductCategory, Production.ProductSubCategory  
WHERE    ProductCategory.ProductCategoryID = ProductSubCategory.ProductCategoryID  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
GO  
```  
  
 Este é o resultado parcial:  
  
```  
<ProductCategory ProductCategoryID="1" CategoryName="Bike">  
  <ProductSubCategory ProductSubCategoryID="1" Name="Mountain Bike"/>  
  <ProductSubCategory ProductSubCategoryID="2" Name="Road Bike"/>  
  <ProductSubCategory ProductSubCategoryID="3" Name="Touring Bike"/>  
</ProductCategory>  
...  
```  
  
 Se você especificar a política `ELEMENTS` na consulta, receberá um resultado centrado em elemento, conforme mostrado no seguinte fragmento de resultado:  
  
```  
<ProductCategory>  
  <ProductCategoryID>1</ProductCategoryID>  
  <CategoryName>Bike</CategoryName>  
  <ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <Name>Mountain Bike</Name>  
  </ProductSubCategory>  
  <ProductSubCategory>  
     ...  
  </ProductSubCategory>  
</ProductCategory>  
```  
  
 Em seguida, suponha que você queira gerar uma hierarquia XML que seja uma combinação de XML centrado em atributo e em elemento, conforme mostrado neste fragmento:  
  
```  
<ProductCategory ProductCategoryID="1" CategoryName="Bike">  
  <ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <SubCategoryName>Mountain Bike</SubCategoryName></ProductSubCategory>  
  <ProductSubCategory>  
     ...  
  <ProductSubCategory>  
     ...  
</ProductCategory>  
```  
  
 No fragmento anterior, as informações da categoria de produtos como ID e nome da categoria são atributos. No entanto as informações de subcategoria são centradas em elemento. Para construir o elemento <`ProductCategory`>, você pode escrever uma consulta `FOR XML` conforme mostrado a seguir:  
  
```  
SELECT ProductCategoryID, Name as CategoryName  
FROM Production.ProductCategory ProdCat  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
```  
  
 Este é o resultado:  
  
```  
< ProdCat ProductCategoryID="1" CategoryName="Bikes" />  
< ProdCat ProductCategoryID="2" CategoryName="Components" />  
< ProdCat ProductCategoryID="3" CategoryName="Clothing" />  
< ProdCat ProductCategoryID="4" CategoryName="Accessories" />  
```  
  
 Para construir os elementos <`ProductSubCategory`> aninhados no XML desejado, adicione uma consulta `FOR XML` aninhada, conforme mostrado a seguir:  
  
```  
SELECT ProductCategoryID, Name as CategoryName,  
       (SELECT ProductSubCategoryID, Name SubCategoryName  
        FROM   Production.ProductSubCategory  
        WHERE ProductSubCategory.ProductCategoryID =   
              ProductCategory.ProductCategoryID  
        FOR XML AUTO, TYPE, ELEMENTS  
       )  
FROM Production.ProductCategory  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A consulta `FOR XML` interna recupera informações de subcategoria de produtos. A diretiva `ELEMENTS` é adicionada ao `FOR XML` interno para gerar XML centrado em elemento que é adicionado ao XML gerado pela consulta externa. Por padrão, a consulta externa gera XML centrado em atributo.  
  
-   Na consulta interna, a diretiva `TYPE` é especificada de forma que o resultado seja do tipo **xml** . Se `TYPE` não for especificado, o resultado será retornado como tipo **nvarchar(max)** e os dados XML serão retornados como entidades.  
  
-   A consulta externa também especifica a diretiva `TYPE` . Portanto o resultado dessa consulta é retornado ao cliente como tipo **xml** .  
  
 Este é o resultado parcial:  
  
```  
<ProductCategory ProductCategoryID="1" CategoryName="Bike">  
  <ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <SubCategoryName>Mountain Bike</SubCategoryName></ProductSubCategory>  
  <ProductSubCategory>  
     ...  
  <ProductSubCategory>  
     ...  
</ProductCategory>  
```  
  
 A consulta a seguir é apenas uma extensão da consulta anterior. Ela mostra a hierarquia completa de produtos no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Isso inclui o seguinte:  
  
-   Categorias de produtos  
  
-   Subcategorias de produtos em cada categoria  
  
-   Modelos de produtos em cada subcategoria  
  
-   Produtos em cada modelo  
  
 A consulta a seguir pode ser útil para entender o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
```  
SELECT ProductCategoryID, Name as CategoryName,  
       (SELECT ProductSubCategoryID, Name SubCategoryName,  
               (SELECT ProductModel.ProductModelID,   
                       ProductModel.Name as ModelName,  
                       (SELECT ProductID, Name as ProductName, Color  
                        FROM   Production.Product  
                        WHERE  Product.ProductModelID =   
                               ProductModel.ProductModelID  
                        FOR XML AUTO, TYPE)  
                FROM   (SELECT distinct ProductModel.ProductModelID,   
                               ProductModel.Name  
                        FROM   Production.ProductModel,   
                               Production.Product  
                        WHERE  ProductModel.ProductModelID =   
                               Product.ProductModelID  
                        AND    Product.ProductSubCategoryID =   
                               ProductSubCategory.ProductSubCategoryID)   
                                  ProductModel  
                FOR XML AUTO, type  
               )  
        FROM Production.ProductSubCategory  
        WHERE ProductSubCategory.ProductCategoryID =   
              ProductCategory.ProductCategoryID  
        FOR XML AUTO, TYPE, ELEMENTS  
       )  
FROM Production.ProductCategory  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
```  
  
 Este é o resultado parcial:  
  
```  
<Production.ProductCategory ProductCategoryID="1" CategoryName="Bikes">  
  <Production.ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <SubCategoryName>Mountain Bikes</SubCategoryName>  
    <ProductModel ProductModelID="19" ModelName="Mountain-100">  
      <Production.Product ProductID="771"   
                ProductName="Mountain-100 Silver, 38" Color="Silver" />  
      <Production.Product ProductID="772"   
                ProductName="Mountain-100 Silver, 42" Color="Silver" />  
      <Production.Product ProductID="773"   
                ProductName="Mountain-100 Silver, 44" Color="Silver" />  
        …  
    </ProductModel>  
     …  
```  
  
 Se você remover a diretiva `ELEMENTS` da consulta `FOR XML` aninhada que gera subcategorias de produtos, todo o resultado será centrado em atributo. Em seguida, você pode escrever esta consulta sem aninhamento. A adição de resultados de `ELEMENTS` em um XML que é parcialmente centrado em atributo e em elemento. Esse resultado não pode ser gerado por uma consulta FOR XML de nível único.  
  
## <a name="see-also"></a>Consulte também  
 [Usar consultas FOR XML aninhadas](../../relational-databases/xml/use-nested-for-xml-queries.md)  
  
  
