---
title: Adicionar namespaces a consultas com WITH XMLNAMESPACES | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- ELEMENTS XSINIL directive
- adding namespaces
- XSINIL directive
- default namespaces
- queries [XML in SQL Server], WITH XMLNAMESPACES clause
- predefined namespaces [XML in SQL Server]
- FOR XML clause, WITH XMLNAMESPACES clause
- namespaces [XML in SQL Server]
- xml data type [SQL Server], WITH XMLNAMESPACES clause
- WITH XMLNAMESPACES clause
ms.assetid: 2189cb5e-4460-46c5-a254-20c833ebbfec
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c732b19c371a48e2bf165a3fe7d326fe8476e045
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47639334"
---
# <a name="add-namespaces-to-queries-with-with-xmlnamespaces"></a>Adicionar namespaces a consultas com WITH XMLNAMESPACES
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [WITH XMLNAMESPACES (Transact-SQL)](../../t-sql/xml/with-xmlnamespaces.md) fornece suporte a URI de namespace da seguinte maneira:  
  
-   Ele torna o mapeamento do prefixo do namespace para URI disponível ao [Construir consultas XML usando FOR XML](../../relational-databases/xml/for-xml-sql-server.md) .  
  
-   Ele torna o mapeamento do namespace para URI disponíveis para o contexto de namespace estático do Faz o namespace a URI que mapeia disponível para o contexto de namespace estático dos [Métodos de tipos de dados xml](../../t-sql/xml/xml-data-type-methods.md).  
  
## <a name="using-with-xmlnamespaces-in-the-for-xml-queries"></a>Usando WITH XMLNAMESPACES em consultas FOR XML  
 WITH XMLNAMESPACES permite incluir namespaces XML em consultas FOR XML. Por exemplo, considere a seguinte consulta FOR XML:  
  
```  
SELECT ProductID, Name, Color  
FROM   Production.Product  
WHERE  ProductID=316 or ProductID=317  
FOR XML RAW  
```  
  
 Este é o resultado:  
  
```  
<row ProductID="316" Name="Blade" />  
<row ProductID="317" Name="LL Crankarm" Color="Black" />  
  
```  
  
 Para adicionar namespaces ao XML construído pela consulta FOR XML, primeiro especifique os mapeamentos de prefixo de namespace para URI usando a cláusula WITH NAMESPACES. Em seguida, use os prefixos de namespace para especificar os nomes na consulta, conforme mostrado na seguinte consulta modificada. Observe que a cláusula WITH XMLNAMESPACES especifica o mapeamento de prefixo de namespace (`ns1`) para o URI (`uri`). Em seguida, o `ns1` é usado para especificar os nomes do atributo e do elemento a serem construídos pela consulta FOR XML.  
  
```  
WITH XMLNAMESPACES ('uri' as ns1)  
SELECT ProductID as 'ns1:ProductID',  
       Name      as 'ns1:Name',   
       Color     as 'ns1:Color'  
FROM Production.Product  
WHERE ProductID=316 or ProductID=317  
FOR XML RAW ('ns1:Prod'), ELEMENTS  
  
```  
  
 O resultado do XML inclui os prefixos de namespace:  
  
```  
<ns1:Prod xmlns:ns1="uri">  
  <ns1:ProductID>316</ns1:ProductID>  
  <ns1:Name>Blade</ns1:Name>  
</ns1:Prod>  
<ns1:Prod xmlns:ns1="uri">  
  <ns1:ProductID>317</ns1:ProductID>  
  <ns1:Name>LL Crankarm</ns1:Name>  
  <ns1:Color>Black</ns1:Color>  
</ns1:Prod>  
  
```  
  
 O seguinte se aplica à cláusula WITH XMLNAMESPACES:  
  
-   Ela tem suporte apenas nos modos RAW, AUTO e PATH de consultas FOR XML. Não há suporte para o modo EXPLICIT.  
  
-   Ela afeta apenas os prefixos de namespace de consultas FOR XML e os métodos de tipos de dados **xml** , mas não o analisador XML. Por exemplo, a consulta a seguir retorna um erro porque o documento XML não tem nenhuma declaração de namespace para o prefixo myNS:  
  
-   As diretivas de FOR XML, XMLSCHEMA e XMLDATA não podem ser usadas quando uma cláusula WITH XMLNAMESPACES está sendo usada.  
  
    ```  
    CREATE TABLE T (x xml)  
    go  
    WITH XMLNAMESPACES ('http://abc' as myNS )  
    INSERT INTO T VALUES('<myNS:root/>')  
    ```  
  
## <a name="using-the-xsinil-directive"></a>Usando a diretiva XSINIL  
 Não será possível definir o prefixo na cláusula WITH XMLNAMESPACES se você estiver usando a diretiva ELEMENTS XSINIL. Em vez disso, ela é adicionada automaticamente quando você usa ELEMENTS XSINIL. A consulta a seguir usa ELEMENTS XSINIL que gera XML centrado em elemento em que valores nulos são mapeados para elementos que têm o atributo **xsi:nil** definido como True.  
  
```  
WITH XMLNAMESPACES ('uri' as ns1)  
SELECT ProductID as 'ns1:ProductID',  
       Name      as 'ns1:Name',   
       Color     as 'ns1:Color'  
FROM Production.Product  
WHERE ProductID=316   
FOR XML RAW, ELEMENTS XSINIL  
```  
  
 Este é o resultado:  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:ns1="uri">  
  <ns1:ProductID>316</ns1:ProductID>  
  <ns1:Name>Blade</ns1:Name>  
  <ns1:Color xsi:nil="true" />  
</row>  
```  
  
## <a name="specifying-default-namespaces"></a>Especificando namespaces padrão  
 Em vez de declarar um prefixo de namespace, é possível declarar um namespace padrão usando uma palavra-chave DEFAULT. Na consulta FOR XML, ele associará o namespace padrão a nós XML no XML resultante. No exemplo a seguir, WITH XMLNAMESPACES define dois prefixos de namespace que são definidos junto com um namespace padrão.  
  
```  
WITH XMLNAMESPACES ('uri1' as ns1,   
                    'uri2' as ns2,  
                    DEFAULT 'uri2')  
SELECT ProductID,   
      Name,  
      Color  
FROM Production.Product   
WHERE ProductID=316 or ProductID=317  
FOR XML RAW ('ns1:Product'), ROOT('ns2:root'), ELEMENTS  
```  
  
 A consulta FOR XML gera XML centrado em elemento. Observe que a consulta usa os dois prefixos de namespace na nomeação de nós. Na cláusula SELECT, ProductID, Name e Color não especificam um nome com qualquer prefixo. Portanto os elementos correspondentes no XML resultante pertencem ao namespace padrão.  
  
```  
<ns2:root xmlns="uri2" xmlns:ns2="uri2" xmlns:ns1="uri1">  
  <ns1:Product>  
    <ProductID>316</ProductID>  
    <Name>Blade</Name>  
  </ns1:Product>  
  <ns1:Product>  
    <ProductID>317</ProductID>  
    <Name>LL Crankarm</Name>  
    <Color>Black</Color>  
  </ns1:Product>  
</ns2:root>  
```  
  
 A consulta a seguir é semelhante à anterior, exceto que o modo FOR XML AUTO é especificado.  
  
```  
WITH XMLNAMESPACES ('uri1' as ns1,  'uri2' as ns2,DEFAULT 'uri2')  
SELECT ProductID,   
      Name,  
      Color  
FROM Production.Product as "ns1:Product"  
WHERE ProductID=316 or ProductID=317  
FOR XML AUTO, ROOT('ns2:root'), ELEMENTS  
```  
  
## <a name="using-predefined-namespaces"></a>Usando namespaces predefinidos  
 Quando namespaces predefinidos são usados, exceto pelo namespace xml e o namespace xsi quando ELEMENTS XSINIL é usado, você deve especificar explicitamente a associação do namespace usando WITH XMLNAMESPACES. A consulta a seguir define explicitamente o prefixo de namespace para associação de URI para o namespace predefinido (`urn:schemas-microsoft-com:xml-sql`).  
  
```  
WITH XMLNAMESPACES ('urn:schemas-microsoft-com:xml-sql' as sql)  
SELECT 'SELECT * FROM Customers FOR XML AUTO, ROOT("a")' AS "sql:query"  
FOR XML PATH('sql:root')  
```  
  
 Este é o resultado. Usuários de SQLXML estão familiarizados com esse modelo de XML. Para obter mais informações, consulte [Conceitos de programação do SQLXML 4.0](../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md).  
  
```  
<sql:root xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>SELECT * FROM Customers FOR XML AUTO, ROOT("a")</sql:query>  
</sql:root>  
```  
  
 Apenas o prefixo de namespace xml pode ser usado sem defini-lo explicitamente em WITH XMLNAMESPACES, conforme mostrado na consulta de modo PATH a seguir. Além disso, se o prefixo for declarado, ele deverá ser associado ao namespace http://www.w3.org/XML/1998/namespace. Os nomes especificados na cláusula SELECT fazem referência ao prefixo de namespace xml que não é definido explicitamente usando WITH XMLNAMESPACES.  
  
```  
SELECT 'en'    as "English/@xml:lang",  
       'food'  as "English",  
       'ger'   as "German/@xml:lang",  
       'Essen' as "German"  
FOR XML PATH ('Translation')  
go  
```  
  
 Os atributos @xml:lang usam o namespace de XML predefinido. Como o XML versão 1.0 não requer a declaração explícita da associação do namespace xml, o resultado não incluirá uma declaração explícita da associação de namespace.  
  
 Este é o resultado:  
  
```  
<Translation>  
  <English xml:lang="en">food</English>  
  <German xml:lang="ger">Essen</German>  
</Translation>  
```  
  
## <a name="using-with-xmlnamespaces-with-the-xml-data-type-methods"></a>Usando WITH XMLNAMESPACES com métodos de tipos de dados xml  
 Os [Métodos de tipos de dados xml](../../t-sql/xml/xml-data-type-methods.md) especificados em uma consulta SELECT, ou em UPDATE quando o método for **modify()** , todos precisam repetir a declaração de namespace em seu prólogo. Isto pode ser demorado. Por exemplo, a consulta a seguir recupera IDs de modelos de produtos cujas descrições no catálogo não incluem especificação. Isto é, o elemento <`Specifications`> existe.  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
    declare namespace  pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /pd:ProductDescription[(pd:Specifications)]'  
    ) = 1  
```  
  
 Na consulta anterior, os métodos **query()** e **exist()** declaram o mesmo namespace em seus prólogos. Por exemplo:  
  
```  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
```  
  
 Alternativamente, você pode declarar WITH XMLNAMESPACES primeiro e usar os prefixos de namespace na consulta. Nesse caso, os métodos **query()** e **exist()** não precisam incluir declarações de namespace em seus prólogos.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' as pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[(pd:Specifications)]'  
    ) = 1  
Go  
```  
  
 Observe que uma declaração explícita no prólogo de XQuery substitui o prefixo de namespace e o namespace do elemento padrão definidos na cláusula WITH.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos de tipos de dados xml](../../t-sql/xml/xml-data-type-methods.md)   
 [Referência de linguagem XQuery &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)   
 [WITH XMLNAMESPACES &#40;Transact-SQL&#41;](../../t-sql/xml/with-xmlnamespaces.md)   
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
