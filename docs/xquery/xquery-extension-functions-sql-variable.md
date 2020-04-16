---
title: sql:variável() Função (XQuery) | Microsoft Docs
description: Aprenda a usar a função XQuery Extension sql:variable() para expor uma variável que contém um valor relacional SQL dentro de uma expressão XQuery.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sql:variable() function
- sql:variable function
ms.assetid: 6e2e5063-c1cf-4b5a-b642-234921e3f4f7
author: rothja
ms.author: jroth
ms.openlocfilehash: 8241e15643eb4aa25912451ddfed94699954797f
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388600"
---
# <a name="xquery-extension-functions---sqlvariable"></a>Funções de Extensão XQuery – sql:variable()
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Expõe uma variável que contém um valor relacional SQL dentro de uma expressão XQuery.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sql:variable("variableName") as xdt:anyAtomicType?  
```  
  
## <a name="remarks"></a>Comentários  
 Como descrito no tópico [Binding Relational Dataal Inside XML](../t-sql/xml/binding-relational-data-inside-xml-data.md), você pode usar esta função quando você usa [métodos de tipo de dados XML](../t-sql/xml/xml-data-type-methods.md) para expor um valor relacional dentro do XQuery.  
  
 Por exemplo, o [método de consulta()](../t-sql/xml/query-method-xml-data-type.md) é usado para especificar uma consulta contra uma instância XML que é armazenada em uma variável ou coluna de tipo de dados **xml.** Às vezes, você pode também desejar que sua consulta utilize valores de uma variável ou de um parâmetro [!INCLUDE[tsql](../includes/tsql-md.md)], para unir dados relacionais e de XML. Para fazer isso, você usa a função **sql:variable.**  
  
 O valor SQL será mapeado para um valor xquery correspondente e seu tipo será um tipo de base XQuery que é equivalente ao tipo SQL correspondente.  
  
 Você só pode se referir a uma instância **xml** no contexto da expressão de origem de uma instrução de inserção XML-DML; caso contrário, você não pode se referir a valores que são do tipo **xml** ou um tipo de tempo de execução de linguagem comum (CLR) definido pelo usuário.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-the-sqlvariable-function-to-bring-a-transact-sql-variable-value-into-xml"></a>a. Usando uma função sql:variable() para levar um valor de variável Transact-SQL para o XML  
 O exemplo a seguir constrói uma instância XML composta do seguinte:  
  
-   Um valor (`ProductID`) de uma coluna não XML. A [função sql:column()](../xquery/xquery-extension-functions-sql-column.md) é usada para vincular esse valor no XML.  
  
-   Um valor (`ListPrice`) de uma coluna não XML em outra tabela. Novamente, `sql:column()` é usado para associar esse valor no XML.  
  
-   Um valor (`DiscountPrice`) de uma variável [!INCLUDE[tsql](../includes/tsql-md.md)]. O método `sql:variable()` é usado para associar esse valor ao XML.  
  
-   Um valor`ProductModelName`( ) de uma coluna do tipo **xml,** para tornar a consulta mais interessante.  
  
 Esta é a consulta:  
  
```sql
DECLARE @price money  
  
SET @price=2500.00  
SELECT ProductID, Production.ProductModel.ProductModelID,CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  
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
  
-   A `namespace` palavra-chave é usada para definir um prefixo namespace no [XQuery Prolog](../xquery/modules-and-prologs-xquery-prolog.md). Isso é feito porque o valor do atributo `ProductModelName` é recuperado na coluna de tipo `CatalogDescription xml`, que tem um esquema associado a ela.  
  
 Este é o resultado:  
  
```xml
<Product ProductID="771" ProductModelID="19"   
         ProductModelName="Mountain 100"   
         ListPrice="3399.99" DiscountPrice="2500" />  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de extensão xquery do servidor SQL](https://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)   
 [Compare XML digitado com XML não digitado](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [&#41;do servidor SQL de &#40;de dados XML](../relational-databases/xml/xml-data-sql-server.md)   
 [Criar instâncias de dados XML](../relational-databases/xml/create-instances-of-xml-data.md)   
 [Xml Data Type Methods](../t-sql/xml/xml-data-type-methods.md)   
 [Linguagem de modificação de dados XML &#40;XML DML&#41;](../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
