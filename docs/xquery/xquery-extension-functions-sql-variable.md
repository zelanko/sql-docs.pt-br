---
title: 'SQL: função Variable () (XQuery) | Microsoft Docs'
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
ms.openlocfilehash: 56a8c53a22fefec7fbda4c2ac7476ae46d664199
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67946003"
---
# <a name="xquery-extension-functions---sqlvariable"></a>Funções de Extensão XQuery – sql:variable()
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Expõe uma variável que contém um valor relacional SQL dentro de uma expressão XQuery.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sql:variable("variableName") as xdt:anyAtomicType?  
```  
  
## <a name="remarks"></a>Comentários  
 Conforme descrito no tópico [associando dados relacionais dentro de XML](../t-sql/xml/binding-relational-data-inside-xml-data.md), você pode usar essa função ao usar [métodos de tipo de dados XML](../t-sql/xml/xml-data-type-methods.md) para expor um valor relacional dentro do XQuery.  
  
 Por exemplo, o [método Query ()](../t-sql/xml/query-method-xml-data-type.md) é usado para especificar uma consulta em relação a uma instância XML que é armazenada em uma variável ou coluna de tipo de dados **XML** . Às vezes, você pode também desejar que sua consulta utilize valores de uma variável ou de um parâmetro [!INCLUDE[tsql](../includes/tsql-md.md)], para unir dados relacionais e de XML. Para fazer isso, use a função **SQL: variable** .  
  
 O valor SQL será mapeado para um valor XQuery correspondente e seu tipo será um tipo base XQuery equivalente ao tipo SQL correspondente.  
  
 Você só pode fazer referência a uma instância **XML** no contexto da expressão de origem de uma instrução XML-DML insert; caso contrário, não será possível se referir a valores do tipo **XML** ou um tipo definido pelo usuário Common Language Runtime (CLR).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-the-sqlvariable-function-to-bring-a-transact-sql-variable-value-into-xml"></a>a. Usando uma função sql:variable() para levar um valor de variável Transact-SQL para o XML  
 O exemplo a seguir constrói uma instância XML composta do seguinte:  
  
-   Um valor (`ProductID`) de uma coluna não XML. A [função SQL: Column ()](../xquery/xquery-extension-functions-sql-column.md) é usada para associar esse valor no XML.  
  
-   Um valor (`ListPrice`) de uma coluna não XML em outra tabela. Novamente, `sql:column()` é usado para associar esse valor no XML.  
  
-   Um valor (`DiscountPrice`) de uma variável [!INCLUDE[tsql](../includes/tsql-md.md)]. O método `sql:variable()` é usado para associar esse valor ao XML.  
  
-   Um valor (`ProductModelName`) de uma coluna de tipo **XML** , para tornar a consulta mais interessante.  
  
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
  
-   A `namespace` palavra-chave é usada para definir um prefixo de namespace no [prólogo XQuery](../xquery/modules-and-prologs-xquery-prolog.md). Isso é feito porque o valor do atributo `ProductModelName` é recuperado na coluna de tipo `CatalogDescription xml`, que tem um esquema associado a ela.  
  
 Este é o resultado:  
  
```xml
<Product ProductID="771" ProductModelID="19"   
         ProductModelName="Mountain 100"   
         ListPrice="3399.99" DiscountPrice="2500" />  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de extensão SQL Server XQuery](https://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)   
 [Comparar XML digitado com XML não digitado](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Dados XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Criar instâncias de dados XML](../relational-databases/xml/create-instances-of-xml-data.md)   
 [Métodos de tipos de dados xml](../t-sql/xml/xml-data-type-methods.md)   
 [XML DML &#40;linguagem de manipulação de dados XML &#41;](../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
