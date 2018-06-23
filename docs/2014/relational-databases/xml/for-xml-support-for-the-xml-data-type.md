---
title: Suporte a FOR XML para o tipo de dados xml | Microsoft Docs
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
- user-defined functions [SQL Server], XML
- xml data type [SQL Server], FOR XML clause
ms.assetid: 365de07d-694c-4c8b-b671-8825be27f87c
caps.latest.revision: 24
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f33b889cb9bc409815c6fe8a0501de3bc1388e68
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36021098"
---
# <a name="for-xml-support-for-the-xml-data-type"></a>Suporte a FOR XML para o tipo de dados xml
  Se uma consulta FOR XML especificar uma coluna de `xml` tipo na cláusula SELECT, os valores de coluna serão mapeados como elementos no XML retornado, independentemente se você especificar a diretiva ELEMENTS. Qualquer declaração XML na coluna de tipo `xml` não é serializada.  
  
 Por exemplo, a consulta a seguir recupera informações de contato do cliente, tais como o `BusinessEntityID`, `FirstName`, e `LastName` colunas e os números de telefone do `AdditionalContactInfo` coluna `xml` tipo.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
') AS PhoneNumber  
FROM Person.Person  
WHERE AdditionalContactInfo.query('  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
')IS NOT NULL  
FOR XML AUTO, TYPE;  
```  
  
 Como a consulta não especifica a diretiva ELEMENTS, os valores de coluna são retornados como atributos, exceto para os valores de informações adicionais de contato recuperados do `xml` coluna de tipo. Esses são retornados como elementos.  
  
 Este é o resultado parcial:  
  
 `<Person.Person BusinessEntityID="291" FirstName="Gustavo" LastName="Achong">`  
  
 `<PhoneNumber>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1112</act:number>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1111</act:number>`  
  
 `</PhoneNumber>`  
  
 `</Person.Person>`  
  
 `<Person.Person BusinessEntityID="293" FirstName="Catherine" LastName="Abel">`  
  
 `<PhoneNumber>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-2222</act:number>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-1234</act:number>`  
  
 `</PhoneNumber>`  
  
```  
</Person.Person>  
...  
```  
  
 Se você especificar um alias para a coluna XML gerada pela XQuery, esse alias será usado para adicionar um elemento wrapper em torno do XML gerado pela XQuery. Por exemplo, a seguinte consulta especifica `MorePhoneNumbers` como um alias de coluna:  
  
```  
SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
') AS PhoneNumber  
FROM Person.Person  
WHERE AdditionalContactInfo.query('  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
')IS NOT NULL  
FOR XML AUTO, TYPE;  
```  
  
 O XML retornado pela XQuery é envolvido no elemento <`MorePhoneNumbers`>, conforme mostrado no seguinte resultado parcial:  
  
 `<Person.Person BusinessEntityID="291" FirstName="Gustavo" LastName="Achong">`  
  
 `<MorePhoneNumbers>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1112</act:number>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1111</act:number>`  
  
 `</MorePhoneNumbers>`  
  
 `</Person.Person>`  
  
 `<Person.Person BusinessEntityID="293" FirstName="Catherine" LastName="Abel">`  
  
 `<MorePhoneNumbers>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-2222</act:number>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-1234</act:number>`  
  
 `</MorePhoneNumbers>`  
  
```  
</Person.Person>  
...  
```  
  
 Se você especificar a diretiva ELEMENTS na consulta, BusinessEntityID, LastName e FirstName serão retornados como elementos no XML resultante.  
  
 O exemplo a seguir ilustra que a lógica de processamento de FOR XML não serializa nenhuma declaração XML nos dados XML de um `xml` coluna de tipo:  
  
```  
create table t(i int, x xml)  
go  
insert into t values(1, '<?xml version="1.0" encoding="UTF-8" ?>  
                             <Root SomeID="10" />')  
select i, x  
from   t  
for xml auto;  
```  
  
 Este é o resultado. No resultado, a declaração XML <`?xml version="1.0" encoding="UTF-8" ?`> não é serializada.  
  
```  
<root>  
  <t i="1">  
    <x>  
      <Root SomeID="10" />  
    </x>  
  </t>  
</root>  
```  
  
## <a name="returning-xml-from-a-user-defined-function"></a>Retornando XML de uma função definida pelo usuário  
 Consultas FOR XML podem ser usadas para retornar XML de uma função definida pelo usuário que retorna qualquer um dos seguintes itens:  
  
-   Uma tabela com uma única coluna de tipo `xml`  
  
-   Uma instância das `xml` tipo  
  
 Por exemplo, a seguinte função definida pelo usuário retorna uma tabela com uma única coluna de `xm`tipo:  
  
```  
USE AdventureWorks2012;  
GO  
CREATE FUNCTION dbo.MyUDF (@ProudctModelID int)  
RETURNS @T TABLE  
  (  
     ProductDescription xml  
  )  
AS  
BEGIN  
  INSERT @T  
     SELECT CatalogDescription.query('  
declare namespace PD="http://www.adventure-works.com/schemas/products/description";  
                    //PD:ProductDescription  ')  
     FROM Production.ProductModel  
     WHERE ProductModelID = @ProudctModelID  
  RETURN  
END;  
```  
  
 Você pode executar a função definida pelo usuário e consultar a tabela retornada por ela. Neste exemplo, o XML retornado pela consulta da tabela é atribuído a um `xml` variável de tipo.  
  
```  
declare @x xml;  
set @x = (SELECT * FROM MyUDF(19));  
select @x;  
```  
  
 Esse é outro exemplo de uma função definida pelo usuário. Essa função definida pelo usuário retorna uma instância do tipo `xml`. Neste exemplo, a função definida pelo usuário retorna uma instância XML com tipo, porque o namespace do esquema está especificado.  
  
```  
DROP FUNCTION dbo.MyUDF;  
GO  
CREATE FUNCTION MyUDF (@ProductModelID int)   
RETURNS xml ([Production].[ProductDescriptionSchemaCollection])  
AS  
BEGIN  
  declare @x xml  
  set @x =   ( SELECT CatalogDescription  
          FROM Production.ProductModel  
          WHERE ProductModelID = @ProductModelID )  
  return @x  
END;  
```  
  
 O XML retornado pela função definida pelo usuário pode ser atribuído a uma variável de tipo `xml` da seguinte maneira:  
  
```  
declare @x xml;  
SELECT @x= dbo.MyUDF4 (19) ;  
select @x;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Suporte a FOR XML para vários tipos de dados SQL Server](for-xml-support-for-various-sql-server-data-types.md)  
  
  