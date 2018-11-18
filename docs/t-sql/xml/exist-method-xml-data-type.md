---
title: Método exist() (tipo de dados xml) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- exist() method
- exist method
ms.assetid: a55b75e0-0a17-4787-a525-9b095410f7af
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 83b029554b8a85f11c477063a818bd90a4019740
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51698544"
---
# <a name="exist-method-xml-data-type"></a>Método exista() (Tipo de dados xml)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna um **bit** que representa uma das seguintes condições:  
  
-   1, representando Verdadeiro, se a expressão XQuery em uma consulta retornar um resultado nonempty. Quer dizer, retorna no mínimo um nó XML.  
  
-   0, representando Falso, se retornar um resultado vazio.  
  
-   NULL se a instância de tipo de dados **xml** na qual a consulta foi executada contiver NULL.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
exist (XQuery)   
```  
  
## <a name="arguments"></a>Argumentos  
 XQuery  
 É uma expressão XQuery, uma cadeia de caracteres literal.  
  
## <a name="remarks"></a>Remarks  
  
> [!NOTE]  
>  O método **exist()** retorna 1 para a expressão XQuery que retorna um resultado não vazio. Se você especificar as funções **true()** ou **false()** no método **exist()**, o método **exist()** retornará 1, porque as funções **true()** e **false()** retornam Boolean True e False, respectivamente. Quer dizer, elas retornam um resultado nonempty. Portanto, **exist()** retornará 1 (True), conforme mostrado no seguinte exemplo:  
  
```  
declare @x xml;  
set @x='';  
select @x.exist('true()');   
```  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir mostram como especificar o método **exist()**.  
  
### <a name="example-specifying-the-exist-method-against-an-xml-type-variable"></a>Exemplo: Especificando o método exist() em uma variável de tipo xml  
 No exemplo a seguir, @xé uma variável de tipo **xml** (xml não tipado) e @f é uma variável de tipo inteiro que armazena o valor retornado pelo método **exist()**. O método **exist()** retorna True (1) se o valor de data armazenado na instância de XML é `2002-01-01`.  
  
```  
declare @x xml;  
declare @f bit;  
set @x = '<root Somedate = "2002-01-01Z"/>';  
set @f = @x.exist('/root[(@Somedate cast as xs:date?) eq xs:date("2002-01-01Z")]');  
select @f;  
```  
  
 Comparando as datas no método **exist()**, observe o seguinte:  
  
-   O código `cast as xs:date?` é usado para converter o valor no tipo **xs:date** para fins de comparação.  
  
-   O valor do atributo **@Somedate** é não tipado. Comparando esse valor, ele é implicitamente convertido no tipo do lado direito da comparação, o tipo **xs:date**.  
  
-   Em vez de **cast as xs:date()**, use a função de construtor **xs:date()**. Para obter mais informações, consulte [Funções de construtor &#40;XQuery&#41;](../../xquery/constructor-functions-xquery.md).  
  
 O exemplo a seguir é semelhante ao anterior, com a exceção de que tem um elemento <`Somedate`>.  
  
```  
DECLARE @x xml;  
DECLARE @f bit;  
SET @x = '<Somedate>2002-01-01Z</Somedate>';  
SET @f = @x.exist('/Somedate[(text()[1] cast as xs:date ?) = xs:date("2002-01-01Z") ]')  
SELECT @f;  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   O método **text()** retorna um nó de texto que contém o valor não tipado `2002-01-01`. (O tipo XQuery é **xdt:untypedAtomic**.) É necessário converter explicitamente esse valor tipado de **x** para **xsd:date**, porque a conversão implícita não é compatível, nesse caso.  
  
### <a name="example-specifying-the-exist-method-against-a-typed-xml-variable"></a>Exemplo: Especificando o método exist() em uma variável xml digitada  
 O exemplo a seguir ilustra o uso do método **exist()** em uma variável do tipo **xml**. É uma variável XML digitada, porque especifica o nome de coleção de namespace do esquema, `ManuInstructionsSchemaCollection`.  
  
 No exemplo, um documento de instruções de fabricação é atribuído primeiro a essa variável e, em seguida, o método **exist()** é usado para descobrir se o documento inclui um elemento <`Location`> cujo valor do atributo **LocationID** é 50.  
  
 O método **exist()** especificado na variável @x retornará 1 (Verdadeiro) se o documento de instruções de fabricação inclui um elemento <`Location`> que tem `LocationID=50`. Caso contrário, o método retornará 0 (Falso).  
  
```  
DECLARE @x xml (Production.ManuInstructionsSchemaCollection);  
SELECT @x=Instructions  
FROM Production.ProductModel  
WHERE ProductModelID=67;  
--SELECT @x  
DECLARE @f int;  
SET @f = @x.exist(' declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
    /AWMI:root/AWMI:Location[@LocationID=50]  
');  
SELECT @f;  
```  
  
### <a name="example-specifying-the-exist-method-against-an-xml-type-column"></a>Exemplo: Especificando o método exist() em uma coluna de tipo xml  
 A consulta a seguir recupera as IDs de modelos de produtos cujas descrições no catálogo não incluem as especificações, o elemento <`Specifications`>:  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
    declare namespace  pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /pd:ProductDescription[not(pd:Specifications)]'  
    ) = 1;  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A cláusula WHERE seleciona somente as linhas da tabela **ProductDescription** que atendem à condição especificada na coluna do tipo **CatalogDescription xml**.  
  
-   O método **exist()** na cláusula WHERE retorna 1 (Verdadeiro) se o XML não inclui nenhum elemento <`Specifications`>. Observe o uso da [função not() (XQuery)](../../xquery/functions-on-boolean-values-not-function.md).  
  
-   A função [sql:column() (XQuery)](../../xquery/xquery-extension-functions-sql-column.md) é usada para obter o valor de uma coluna não XML.  
  
-   Essa consulta retorna um conjunto de linhas vazias.  
  
 A consulta especifica os métodos **query()** e **exist()** do tipo de dados xml e os dois métodos declaram os mesmos namespaces no prólogo da consulta. Nesse caso, é possível usar WITH XMLNAMESPACES para declarar o prefixo e usá-lo na consulta.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[not(pd:Specifications)]'  
    ) = 1;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar namespaces a consultas com WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Comparar XML digitado com XML não digitado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [Métodos de tipos de dados xml](../../t-sql/xml/xml-data-type-methods.md)   
 [XML DML &#40;linguagem de manipulação de dados XML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
