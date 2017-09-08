---
title: "(tipo de dados xml) do método Query () | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- query method
- query() method
ms.assetid: f48f6f7b-219f-463a-bf36-bc10f21afaeb
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: db0f9b1ffc4c6ca13084942144e13d64765d7019
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="query-method-xml-data-type"></a>Método consulta() (Tipo de dados xml)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Especifica um XQuery em relação uma instância do **xml** tipo de dados. O resultado é de **xml** tipo. O método retorna uma instância de XML sem-tipo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
query ('XQuery')  
```  
  
## <a name="arguments"></a>Argumentos  
 XQuery  
 É uma cadeia de caracteres, uma expressão XQuery, que consulta nós XML, como elementos e atributos, em uma instância XML.  
  
## <a name="examples"></a>Exemplos  
 Esta seção fornece exemplos de como usar o método Query () a **xml** tipo de dados.  
  
### <a name="a-using-the-query-method-against-an-xml-type-variable"></a>A. Usando o método query() em relação a uma variável de tipo xml  
 O exemplo a seguir declara uma variável  **@myDoc**  de **xml** digite e atribui uma instância XML a ela. O **Query ()** método é usado para especificar um XQuery em relação o documentos.  
  
 A consulta recupera o elemento filho <`Features`> do elemento <`ProductDescription`>:  
  
```  
declare @myDoc xml  
set @myDoc = '<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>  
</ProductDescription>  
</Root>'  
SELECT @myDoc.query('/Root/ProductDescription/Features')  
```  
  
 Este é o resultado:  
  
```  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>        
```  
  
### <a name="b-using-the-query-method-against-an-xml-type-column"></a>B. Usando o método query() em relação a uma coluna do tipo XML  
 No exemplo a seguir, o **Query ()** método é usado para especificar um XQuery em relação a **CatalogDescription** coluna de **xml** digite o  **AdventureWorks** banco de dados:  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
<Product ProductModelID="{ /PD:ProductDescription[1]/@ProductModelID }" />  
') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A coluna CatalogDescription é uma **xml** coluna. Isso significa que ela possui uma coleção de esquema associada. No [prólogo do XQuery](../../xquery/modules-and-prologs-xquery-prolog.md), o **namespace** palavra-chave é usada para definir o prefixo que será usado posteriormente no corpo da consulta.  
  
-   O **Query ()** método constrói o XML, um <`Product`> elemento que tem um **ProductModelID** atributo, no qual o **ProductModelID** é o valor do atributo recuperados do banco de dados. Para obter mais informações sobre a construção de XML, consulte [construção XML &#40; XQuery &#41; ](../../xquery/xml-construction-xquery.md).  
  
-   O [método exist () (tipo de dados XML)](../../t-sql/xml/exist-method-xml-data-type.md) na cláusula WHERE é usada para localizar somente as linhas que contém o <`Warranty`> elemento no XML. Novamente, o **namespace** palavra-chave é usada para definir dois prefixos de namespace.  
  
 Este é o resultado parcial:  
  
```  
<Product ProductModelID="19"/>   
<Product ProductModelID="23"/>   
...  
```  
  
 Observe que os métodos query() e exist() devem declarar o prefixo PD. Nesses casos, você pode usar WITH XMLNAMESPACES para definir primeiro os prefixos e usá-los na consulta.  
  
```  
WITH XMLNAMESPACES (  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD,  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
SELECT CatalogDescription.query('  
<Product ProductModelID="{ /PD:ProductDescription[1]/@ProductModelID }" />  
') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar namespaces a consultas com WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Comparar XML digitado com XML não digitado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [Métodos de tipos de dados xml](../../t-sql/xml/xml-data-type-methods.md)   
 [Linguagem de modificação de dados XML &#40; XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  

