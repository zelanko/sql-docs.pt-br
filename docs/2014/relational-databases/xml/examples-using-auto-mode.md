---
title: 'Exemplos: Usando o modo AUTO | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, examples
ms.assetid: 11e8d0e4-df8a-46f8-aa21-9602d4f26cad
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 93a26764a7111a01b07d23c61bfbfb5c4a728e72
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63287804"
---
# <a name="examples-using-auto-mode"></a>Exemplos: uso do modo AUTO
  Os exemplos a seguir ilustram o uso do modo AUTO. Muitas dessas consultas são especificadas em relação a documentos XML de instruções da fabricação de bicicletas que são armazenados na coluna da tabela ProductModel no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] .  
  
## <a name="example-retrieving-customer-order-and-order-detail-information"></a>Exemplo: Recuperando informações de cliente, pedido e detalhes do pedido  
 Essa consulta recupera informações de cliente, pedido e detalhes do pedido de um cliente específico.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Cust.CustomerID,   
       OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       Detail.SalesOrderID, Detail.LineTotal, Detail.ProductID,   
       Product.Name,  
       Detail.OrderQty  
FROM Sales.Customer AS Cust  
INNER JOIN Sales.SalesOrderHeader AS OrderHeader   
    ON Cust.CustomerID = OrderHeader.CustomerID  
INNER JOIN Sales.SalesOrderDetail AS Detail  
    ON OrderHeader.SalesOrderID = Detail.SalesOrderID  
INNER JOIN Production.Product AS Product  
    ON Product.ProductID = Detail.ProductID  
WHERE Cust.CustomerID IN (29672, 29734)  
ORDER BY OrderHeader.CustomerID,  
         OrderHeader.SalesOrderID  
FOR XML AUTO;  
```  
  
 Como a consulta identifica alias das tabelas `Cust`, `OrderHeader`, `Detail`e `Product` , os elementos correspondentes são gerados pelo modo `AUTO` . Mais uma vez, a ordem em que as tabelas são identificadas pelas colunas especificadas na cláusula `SELECT` determina a hierarquia desses elementos.  
  
 Este é o resultado parcial.  
  
 `<Cust CustomerID="29672">`  
  
 `<OrderHeader CustomerID="29672" SalesOrderID="43660">`  
  
 `<Detail SalesOrderID="43660" LineTotal="874.794000" ProductID="758" OrderQty="1">`  
  
 `<Product Name="Road-450 Red, 52" />`  
  
 `</Detail>`  
  
 `<Detail SalesOrderID="43660" LineTotal="419.458900" ProductID="762" OrderQty="1">`  
  
 `<Product Name="Road-650 Red, 44" />`  
  
 `</Detail>`  
  
 `</OrderHeader>`  
  
 `<OrderHeader CustomerID="29672" SalesOrderID="47660">`  
  
 `<Detail SalesOrderID="47660" LineTotal="469.794000" ProductID="765" OrderQty="1">`  
  
 `<Product Name="Road-650 Black, 58" />`  
  
 `</Detail>`  
  
 `</OrderHeader>`  
  
 `<OrderHeader CustomerID="29672" SalesOrderID="49857">`  
  
 `<Detail SalesOrderID="49857" LineTotal="44.994000" ProductID="852" OrderQty="1">`  
  
 `<Product Name="Women's Tights, S" />`  
  
 `</Detail>`  
  
 `</OrderHeader>`  
  
 `...`  
  
 `</Cust>`  
  
## <a name="example-specifying-group-by-and-aggregate-functions"></a>Exemplo: Especificando GROUP BY e funções de agregação  
 A consulta a seguir retorna IDs de clientes individuais e o número de pedidos do cliente.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT C.CustomerID, COUNT(*) AS NoOfOrders  
FROM Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
On C.CustomerID = SOH.CustomerID  
GROUP BY C.CustomerID  
FOR XML AUTO;This is the partial result:  
```  
  
 `<I CustomerID="11000" NoOfOrders="3" />`  
  
 `<I CustomerID="11001" NoOfOrders="3" />`  
  
 `...`  
  
## <a name="example-specifying-computed-columns-in-auto-mode"></a>Exemplo: Especificando colunas computadas no modo AUTO  
 Essa consulta retorna nomes de clientes individuais concatenados e informações de pedido. Porque a coluna computada é atribuída ao nível interno encontrado naquele ponto, o elemento <`SOH`> neste exemplo. Os nomes concatenados dos clientes são adicionados como atributos do elemento <`SOH`> no resultado.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT P.FirstName + ' ' + P.LastName AS Name,  
       SOH.SalesOrderID  
FROM Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
    ON  C.CustomerID = SOH.CustomerID  
INNER JOIN Person.Person AS P  
    ON P.BusinessEntityID = C.PersonID  
FOR XML AUTO;  
```  
  
 Este é o resultado parcial:  
  
```  
<SOH Name="Jon Yang" SalesOrderID="43793" />  
<SOH Name="Eugene Huang" SalesOrderID="43767" />  
```  
  
 Para recuperar os elementos <`IndividualCustomer`> que têm o atributo `Name` que contém cada informação de cabeçalho de pedidos de vendas como um subelemento, a consulta é reescrita usando uma subseleção. A seleção interna cria uma tabela `IndividualCustomer` temporária com a coluna computada que contém os nomes dos clientes individuais. Em seguida, essa tabela é unida à tabela `SalesOrderHeader` para obter o resultado.  
  
 Observe que a tabela `Sales.Customer` armazena informações do cliente individual, inclusive o valor de `PersonID` do cliente. Esse `PersonID` é usado para localizar o nome de contato da tabela `Person.Person` .  
  
```  
SELECT IndividualCustomer.Name, SOH.SalesOrderID  
FROM (SELECT FirstName+ ' '+LastName AS Name, C.PersonID, C.CustomerID  
      FROM Sales.Customer AS C, Person.Person AS P  
      WHERE C.PersonID = P.BusinessEntityID) AS IndividualCustomer  
LEFT OUTER JOIN  Sales.SalesOrderHeader AS SOH  
   ON IndividualCustomer.CustomerID = SOH.CustomerID  
ORDER BY IndividualCustomer.CustomerID, SOH.CustomerIDFOR XML AUTO;  
```  
  
 Este é o resultado parcial:  
  
 `<IndividualCustomer Name="Jon Yang">`  
  
 `<SOH SalesOrderID="43793" />`  
  
 `<SOH SalesOrderID="51522" />`  
  
 `<SOH SalesOrderID="57418" />`  
  
 `</IndividualCustomer>`  
  
 `...`  
  
 `...`  
  
## <a name="example-returning-binary-data"></a>Exemplo: Retornando dados binários  
 Esta consulta retorna uma fotografia do produto a partir da tabela `ProductPhoto` . `ThumbNailPhoto` é uma coluna `varbinary(max)` na tabela `ProductPhoto`. Por padrão, o modo `AUTO` retorna para os dados binários uma referência que é uma URL relativa à raiz virtual do banco de dados onde a consulta é executada. O atributo de chave `ProductPhotoID` deve ser especificado para identificar a imagem. Para recuperar uma referência de imagem, conforme ilustrado neste exemplo, a chave primária da tabela também deve ser especificada na cláusula `SELECT` para identificar uma linha exclusivamente.  
  
```  
SELECT ProductPhotoID, ThumbNailPhoto  
FROM   Production.ProductPhoto   
WHERE ProductPhotoID=70  
FOR XML AUTO;  
```  
  
 Esse é o resultado:  
  
 `-- result`  
  
 `<Production.ProductPhoto`  
  
 `ProductPhotoID="70"`  
  
 `ThumbNailPhoto= "dbobject/Production.ProductPhoto[@ProductPhotoID='70']/@ThumbNailPhoto" />`  
  
 A mesma consulta é executada com a opção `BINARY BASE64` . A consulta retorna os dados binários em formato codificado na base64.  
  
```  
SELECT ProductPhotoID, ThumbNailPhoto  
FROM   Production.ProductPhoto   
WHERE ProductPhotoID=70  
FOR XML AUTO, BINARY BASE64;  
```  
  
 Esse é o resultado:  
  
 `-- result`  
  
 `<Production.ProductPhoto ProductPhotoID="70" ThumbNailPhoto="Base64 encoded photo" />`  
  
 Por padrão, quando o modo AUTO é usado para recuperar dados binários, em vez dos dados binários, é retornada uma referência a uma URL relativa à raiz virtual do banco de dados onde a consulta foi executada. Isso acontecerá se a opção BINARY BASE64 não estiver especificada.  
  
 Quando o modo AUTO retorna uma referência de URL aos dados binários em bancos de dados que não diferenciam maiúsculas de minúsculas, a consulta é executada quando um nome de tabela ou coluna especificado na consulta não corresponde ao nome da tabela ou coluna do banco de dados. Porém, as maiúsculas e minúsculas retornadas na referência não são consistentes. Por exemplo:   
  
```  
SELECT ProductPhotoID, ThumbnailPhoto  
FROM   Production.ProductPhoto   
WHERE  ProductPhotoID=70  
FOR XML AUTO;  
```  
  
 Esse é o resultado:  
  
 `<Production.PRODUCTPHOTO`  
  
 `PRODUCTPHOTOID="70"`  
  
 `THUMBNAILPHOTO= "dbobject/Production.PRODUCTPHOTO[@ProductPhotoID='70']/@ThumbNailPhoto" />`  
  
 Isso pode ser um problema, principalmente quando são executadas consultas de dbobject em um banco de dados que diferencia maiúsculas e minúsculas. Para evitar isso, as maiúsculas e minúsculas do nome da tabela ou coluna especificado nas consultas devem corresponder às maiúsculas e minúsculas do nome da tabela ou coluna do banco de dados.  
  
## <a name="example-understanding-the-encoding"></a>Exemplo: Entendendo a codificação  
 Este exemplo mostra as várias codificações que ocorrem no resultado.  
  
 Crie esta tabela:  
  
```  
CREATE TABLE [Special Chars] (Col1 char(1) primary key, [Col#&2] varbinary(50));  
```  
  
 Adicione os seguintes dados à tabela:  
  
```  
INSERT INTO [Special Chars] VALUES ('&', 0x20), ('#', 0x20);  
```  
  
 Esta consulta retorna os dados da tabela. O modo FOR XML AUTO é especificado. São retornados dados binários como uma referência.  
  
```  
SELECT * FROM [Special Chars] FOR XML AUTO;  
```  
  
 Esse é o resultado:  
  
 `<Special_x0020_Chars`  
  
 `Col1="#"`  
  
 `Col_x0023__x0026_2="dbobject/Special_x0020_Chars[@Col1='#']/@Col_x0023__x0026_2"`  
  
 `/>`  
  
 `<Special_x0020_Chars`  
  
 `Col1="&"`  
  
 `Col_x0023__x0026_2="dbobject/Special_x0020_Chars[@Col1='&']/@Col_x0023__x0026_2"`  
  
 `/>`  
  
 Este é o processo para codificar caracteres especiais no resultado:  
  
-   No resultado da consulta, os caracteres especiais XML e URL nos nomes dos elementos e atributos que são retornados são codificados usando o valor hexadecimal do caractere Unicode correspondente. No resultado anterior, os <`Special Chars`> do nome do elemento são retornados como <`Special_x0020_Chars`>. O nome do atributo <`Col#&2`> é retornado como <`Col_x0023__x0026_2`>. Os caracteres especiais de XML e URL são codificados.  
  
-   Se os valores dos elementos ou do atributo contiverem qualquer uma das cinco entidades de caracteres XML padrão (', "", \<, > e &), esses caracteres XML especiais serão sempre codificados usando a codificação de caracteres XML. No resultado anterior, o valor `&` no valor do atributo <`Col1`> é codificado como `&`. Entretanto, o caractere # permanece #, porque é um caractere XML válido e não um caractere XML especial.  
  
-   Se os valores dos elementos e atributos contiverem qualquer caractere especial da URL com significado especial na URL, eles serão codificados apenas no valor da URL DBOBJECT e apenas quando o caractere especial fizer parte de um nome de tabela ou coluna. No resultado, o caractere `#` que faz parte do nome da tabela `Col#&2` é codificado como `_x0023_ in the DBOJBECT URL`.  
  
## <a name="see-also"></a>Consulte também  
 [Usar o modo AUTO com FOR XML](use-auto-mode-with-for-xml.md)  
  
  
