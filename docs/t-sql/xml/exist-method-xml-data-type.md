---
title: exist () Method (xml Data Type) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- exist() method
- exist method
ms.assetid: a55b75e0-0a17-4787-a525-9b095410f7af
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0e152abc34c459d82f451c5ded02d30f5fb76b23
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="exist-method-xml-data-type"></a>Método exista() (Tipo de dados xml)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna um **bit** que representa uma das seguintes condições:  
  
-   1, representando Verdadeiro, se a expressão XQuery em uma consulta retornar um resultado nonempty. Quer dizer, retorna no mínimo um nó XML.  
  
-   0, representando Falso, se retornar um resultado vazio.  
  
-   NULO se o **xml** instância de tipo de dados no qual a consulta foi executada contiver NULL.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
exist (XQuery)   
```  
  
## <a name="arguments"></a>Argumentos  
 XQuery  
 É uma expressão XQuery, uma cadeia de caracteres literal.  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]  
>  O **exist ()** método retorna 1 para a expressão XQuery que retorna um resultado não vazio. Se você especificar o **verdadeiro ()** ou **False ()** funções dentro de **exist ()** método, o **exist ()** método retornará 1, porque o funções **verdadeiro ()** e **False ()** retornar booliano True e False, respectivamente. Quer dizer, elas retornam um resultado nonempty. Portanto, **exist ()** retornará 1 (verdadeiro), conforme mostrado no exemplo a seguir:  
  
```  
declare @x xml;  
set @x='';  
select @x.exist('true()');   
```  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir mostram como especificar o **exist ()** método.  
  
### <a name="example-specifying-the-exist-method-against-an-xml-type-variable"></a>Exemplo: Especificando o método exist() em uma variável de tipo xml  
 No exemplo a seguir, @x é um **xml** variável de tipo (xml não tipado) e @f é uma variável de tipo de inteiro que armazena o valor retornado pelo **exist ()** método. O **exist ()** método retornará verdadeiro (1) se o valor de data armazenado na instância XML é `2002-01-01`.  
  
```  
declare @x xml;  
declare @f bit;  
set @x = '<root Somedate = "2002-01-01Z"/>';  
set @f = @x.exist('/root[(@Somedate cast as xs:date?) eq xs:date("2002-01-01Z")]');  
select @f;  
```  
  
 Comparando as datas no **exist ()** método, observe o seguinte:  
  
-   O código `cast as xs:date?` é usado para converter o valor **xs: Date** tipo para fins de comparação.  
  
-   O valor de  **@Somedate**  atributo é digitado. Comparando esse valor, ela será convertida implicitamente para o tipo do lado direito da comparação, o **xs: Date** tipo.  
  
-   Em vez de **convertida como xs:date()**, você pode usar o **xs:date()** função de construtor. Para obter mais informações, consulte [funções de construtor &#40; XQuery &#41; ](../../xquery/constructor-functions-xquery.md).  
  
 O exemplo a seguir é semelhante ao anterior, com a exceção de que tem um elemento <`Somedate`>.  
  
```  
DECLARE @x xml;  
DECLARE @f bit;  
SET @x = '<Somedate>2002-01-01Z</Somedate>';  
SET @f = @x.exist('/Somedate[(text()[1] cast as xs:date ?) = xs:date("2002-01-01Z") ]')  
SELECT @f;  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   O **Text ()** método retorna um nó de texto que contém o valor não digitado `2002-01-01`. (O tipo XQuery é **XDT: untypedatomic**.) É necessário converter explicitamente esse valor digitado de **x** para **xsd: Date**, porque a conversão implícita não é suportada nesse caso.  
  
### <a name="example-specifying-the-exist-method-against-a-typed-xml-variable"></a>Exemplo: Especificando o método exist() em uma variável xml digitada  
 O exemplo a seguir ilustra o uso do **exist ()** método em relação a um **xml** variável de tipo. É uma variável XML digitada, porque especifica o nome de coleção de namespace do esquema, `ManuInstructionsSchemaCollection`.  
  
 No exemplo, um documento é atribuído primeiro a esta variável de instruções de fabricação e, em seguida, o **exist ()** método é usado para localizar se o documento inclui um <`Location`> elemento cujo **LocationID**  valor de atributo é 50.  
  
 O **exist ()** método especificado em relação a @x variável retorna 1 (verdadeiro) se as instruções de fabricação documento inclui um <`Location`> elemento que tem `LocationID=50`. Caso contrário, o método retornará 0 (Falso).  
  
```  
DECLARE @x xml (Production.ManuInstructionsSchemaCollection);  
SELECT @x=Instructions  
FROM Production.ProductModel  
WHERE ProductModelID=67;  
--SELECT @x  
DECLARE @f int;  
SET @f = @x.exist(' declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
    /AWMI:root/AWMI:Location[@LocationID=50]  
');  
SELECT @f;  
```  
  
### <a name="example-specifying-the-exist-method-against-an-xml-type-column"></a>Exemplo: Especificando o método exist() em uma coluna de tipo xml  
 A consulta a seguir recupera as IDs de modelos de produtos cujas descrições no catálogo não incluem as especificações, o elemento <`Specifications`>:  
  
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
     /pd:ProductDescription[not(pd:Specifications)]'  
    ) = 1;  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A cláusula WHERE seleciona somente as linhas do **ProductDescription** table que satisfazem a condição especificada em relação a **CatalogDescription xml** coluna de tipo.  
  
-   O **exist ()** método na cláusula WHERE retornará 1 (verdadeiro) se o XML não incluir nenhum <`Specifications`> elemento. Observe o uso do [not () function (XQuery)](../../xquery/functions-on-boolean-values-not-function.md).  
  
-   O [função SQL: Column (XQuery)](../../xquery/xquery-extension-functions-sql-column.md) função é usada para exibir o valor de uma coluna não XML.  
  
-   Essa consulta retorna um conjunto de linhas vazias.  
  
 A consulta especifica **Query ()** e **exist ()** métodos de tipo de dados xml e esses dois métodos declaram os mesmos namespaces no prólogo da consulta. Nesse caso, é possível usar WITH XMLNAMESPACES para declarar o prefixo e usá-lo na consulta.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
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
  
## <a name="see-also"></a>Consulte também  
 [Adicionar namespaces a consultas com WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Comparar XML digitado com XML não digitado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [Métodos de tipos de dados xml](../../t-sql/xml/xml-data-type-methods.md)   
 [Linguagem de modificação de dados XML &#40; XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  

