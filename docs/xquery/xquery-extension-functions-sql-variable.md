---
title: 'SQL: Variable Function (XQuery) | Microsoft Docs'
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sql:variable() function
- sql:variable function
ms.assetid: 6e2e5063-c1cf-4b5a-b642-234921e3f4f7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 938560986eeaae29ee1d0a2b37f1b2bcceec5b53
ms.sourcegitcommit: 08b3de02475314c07a82a88c77926d226098e23f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49119763"
---
# <a name="xquery-extension-functions---sqlvariable"></a>Funções de Extensão XQuery – sql:variable()
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Expõe uma variável que contém um valor relacional SQL dentro de uma expressão XQuery.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sql:variable("variableName") as xdt:anyAtomicType?  
```  
  
## <a name="remarks"></a>Comentários  
 Conforme descrito no tópico [associando dados relacionais dentro do XML](../t-sql/xml/binding-relational-data-inside-xml-data.md), você pode usar essa função quando você usa [métodos de tipo de dados XML](../t-sql/xml/xml-data-type-methods.md) para expor um valor relacional dentro do XQuery.  
  
 Por exemplo, o [método Query ()](../t-sql/xml/query-method-xml-data-type.md) é usado para especificar uma consulta em relação a uma instância XML que é armazenada em um **xml** variável ou coluna de tipo de dados. Às vezes, você pode também desejar que sua consulta utilize valores de uma variável ou de um parâmetro [!INCLUDE[tsql](../includes/tsql-md.md)], para unir dados relacionais e de XML. Para fazer isso, você deve usar o **SQL: Variable** função.  
  
 O valor SQL será mapeado para um valor correspondente XQuery e seu tipo será um tipo base XQuery equivalente ao tipo SQL correspondente.  
  
 Você só pode se referir a um **xml** instância no contexto da expressão de origem de um XML-DML insert instrução; caso contrário, você não pode se referir aos valores que são do tipo **xml** ou um common language runtime (CLR) tipo definido pelo usuário.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-the-sqlvariable-function-to-bring-a-transact-sql-variable-value-into-xml"></a>A. Usando uma função sql:variable() para levar um valor de variável Transact-SQL para o XML  
 O exemplo a seguir constrói uma instância XML composta do seguinte:  
  
-   Um valor (`ProductID`) de uma coluna não XML. O [função SQL: Column](../xquery/xquery-extension-functions-sql-column.md) é usado para associar esse valor no XML.  
  
-   Um valor (`ListPrice`) de uma coluna não XML em outra tabela. Novamente, `sql:column()` é usado para associar esse valor no XML.  
  
-   Um valor (`DiscountPrice`) de uma variável [!INCLUDE[tsql](../includes/tsql-md.md)]. O método `sql:variable()` é usado para associar esse valor ao XML.  
  
-   Um valor (`ProductModelName`) de um **xml** coluna de tipo, para tornar a consulta mais interessante.  
  
 Esta é a consulta:  
  
```sql
DECLARE @price money  
  
SET @price=2500.00  
SELECT ProductID, Production.ProductModel.ProductModelID,CatalogDescription.query('  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  
       <Product   
           ProductID="{ sql:column("Production.Product.ProductID") }"  
           ProductModelID= "{ sql:column("Production.Product.ProductModelID") }"  
           ProductModelName="{/pd:ProductDescription[1]/@ProductModelName }"  
           ListPrice="{ sql:column("Production.Product.ListPrice") }"  
           DiscountPrice="{ sql:variable("@price") }"  
        />')   
FROM Production.Product   
JOIN Production.ProductModel  
ON Production.Product.ProductModelID = Production.ProductModel.ProductModelID  
WHERE ProductID=771  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   O XQuery dentro do método `query()` constrói o XML.  
  
-   O `namespace` palavra-chave é usada para definir um prefixo de namespace na [prólogo do XQuery](../xquery/modules-and-prologs-xquery-prolog.md). Isso é feito porque o valor do atributo `ProductModelName` é recuperado na coluna de tipo `CatalogDescription xml`, que tem um esquema associado a ela.  
  
 Este é o resultado:  
  
```xml
<Product ProductID="771" ProductModelID="19"   
         ProductModelName="Mountain 100"   
         ListPrice="3399.99" DiscountPrice="2500" />  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções de extensão XQuery do SQL Server](http://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)   
 [Comparar XML digitado com XML não digitado](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Dados XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Criar instâncias de dados XML](../relational-databases/xml/create-instances-of-xml-data.md)   
 [Métodos de tipos de dados xml](../t-sql/xml/xml-data-type-methods.md)   
 [XML DML &#40;linguagem de manipulação de dados XML &#41;](../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
