---
title: Formar XML com consultas FOR XML aninhadas | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML query
- queries [XML in SQL Server], nested FOR XML
- XML [SQL Server], FOR XML queries
ms.assetid: 8dc42c05-16e8-4b7b-a5d3-550b55acae26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f62b355f2363434767b42b34130faa8722e966fb
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2019
ms.locfileid: "54256291"
---
# <a name="shape-xml-with-nested-for-xml-queries"></a>Formar XML com consultas FOR XML aninhadas
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  O exemplo a seguir consulta a tabela `Production.Product` para recuperar os valores de `ListPrice` e `StandardCost` de um produto específico. Para tornar a consulta interessante, os dois preços são retornados em um elemento <`Price`> e cada elemento <`Price`> tem um atributo `PriceType`.  
  
## <a name="example"></a>Exemplo  
 Esta é a forma esperada do XML:  
  
```  
<xsd:schema xmlns:schema="urn:schemas-microsoft-com:sql:SqlRowSet2" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet2" elementFormDefault="qualified">  
  <xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="https://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />  
  <xsd:element name="Production.Product" type="xsd:anyType" />  
</xsd:schema>  
<Production.Product xmlns="urn:schemas-microsoft-com:sql:SqlRowSet2" ProductID="520">  
  <Price xmlns="" PriceType="ListPrice">133.34</Price>  
  <Price xmlns="" PriceType="StandardCost">98.77</Price>  
</Production.Product>  
```  
  
 Esta é a consulta FOR XML aninhada:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Product.ProductID,   
          (SELECT 'ListPrice' as PriceType,   
                   CAST(CAST(ListPrice as NVARCHAR(40)) as XML)   
           FROM    Production.Product Price   
           WHERE   Price.ProductID=Product.ProductID   
           FOR XML AUTO, TYPE),  
          (SELECT  'StandardCost' as PriceType,   
                   CAST(CAST(StandardCost as NVARCHAR(40)) as XML)   
           FROM    Production.Product Price   
           WHERE   Price.ProductID=Product.ProductID   
           FOR XML AUTO, TYPE)  
FROM Production.Product  
WHERE ProductID=520  
for XML AUTO, TYPE, XMLSCHEMA  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A instrução SELECT externa constrói o elemento <`Product`> que tem um atributo **ProductID** e dois elementos filho <`Price`>.  
  
-   A instrução SELECT interna constrói dois elementos <`Price`>, cada um com um atributo **PriceType** e XML que retorna o preço do produto.  
  
-   A diretiva XMLSCHEMA na instrução SELECT externa gera o esquema XSD embutido que descreve a forma do XML resultante.  
  
 Para tornar a consulta interessante, é possível escrever a consulta FOR XML e, em seguida, escrever uma XQuery em relação ao resultado para reformatar o XML, conforme mostrado na seguinte consulta:  
  
```  
SELECT ProductID,   
 ( SELECT p2.ListPrice, p2.StandardCost  
   FROM Production.Product p2   
   WHERE Product.ProductID = p2.ProductID  
   FOR XML AUTO, ELEMENTS XSINIL, type ).query('  
                                   for $p in /p2/*  
                                   return   
                                    <Price PriceType = "{local-name($p)}">  
                                     { data($p) }  
                                    </Price>  
                                  ')  
FROM Production.Product  
WHERE ProductID = 520  
FOR XML AUTO, TYPE  
```  
  
 O exemplo anterior usa o método **query()** do tipo de dados **xml** para consultar o XML retornado pela consulta FOR XML interna e construir o resultado esperado.  
  
 Este é o resultado:  
  
```  
<Production.Product ProductID="520">  
  <Price PriceType="ListPrice">133.3400</Price>  
  <Price PriceType="StandardCost">98.7700</Price>  
</Production.Product>  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usar consultas FOR XML aninhadas](../../relational-databases/xml/use-nested-for-xml-queries.md)  
  
  
