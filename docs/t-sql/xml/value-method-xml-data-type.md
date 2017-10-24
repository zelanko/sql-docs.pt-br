---
title: "(tipo de dados xml) do método Value () | Microsoft Docs"
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
- value method
- value() method
ms.assetid: 298a7361-dc9a-4902-9b1e-49a093cd831d
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3b2cd81e4b96ce5c38a816c50728d794390bb383
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="value-method-xml-data-type"></a>Método de valor() (Tipo de dados xml)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Executa uma XQuery em relação ao XML e retorna um valor de tipo SQL. Este método retorna um valor escalar.  
  
 Você normalmente usa esse método para extrair um valor de uma instância XML armazenada em um **xml** coluna de tipo, parâmetro ou variável. Dessa forma, você pode especificar consultas SELECT que combinam ou comparam dados de XML com dados em colunas não XML.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
value (XQuery, SQLType)  
```  
  
## <a name="arguments"></a>Argumentos  
 *XQuery*  
 É o *XQuery* expressão, uma cadeia de caracteres literal, que recupera dados dentro da instância XML. A XQuery deve retornar no máximo um valor. Caso contrário, um erro é retornado.  
  
 *SQLType*  
 É o tipo SQL preferido, uma literal de cadeia de caracteres, a ser retornado. O tipo de retorno desse método corresponde a *SQLType* parâmetro. *SQLType* não pode ser um **xml** tipo de dados, um tipo common language runtime (CLR) definidos pelo usuário, **imagem**, **texto**, **ntext**, ou **sql_variant** tipo de dados. *SQLType* pode ser um SQL, o tipo de dados definido pelo usuário.  
  
 O **Value ()** método usa o [!INCLUDE[tsql](../../includes/tsql-md.md)] operador CONVERT implicitamente e tenta converter o resultado da expressão XQuery, a representação de cadeia de caracteres serializada, do tipo XSD para o tipo SQL correspondente especificado por [!INCLUDE[tsql](../../includes/tsql-md.md)] conversão. Para obter mais informações sobre regras de conversão de tipo para CONVERT, consulte [CAST e CONVERT &#40; Transact-SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
> [!NOTE]  
>  Por motivos de desempenho, em vez de usar o **Value ()** método em um predicado para comparar com um valor relacional, use **exist ()** com **SQL: Column**. Isso é demonstrado no exemplo D a seguir.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-the-value-method-against-an-xml-type-variable"></a>A. Usando o método de valor() em relação a uma variável de tipo xml  
 No exemplo a seguir, uma instância XML é armazenada em uma variável de tipo `xml`. O método `value()` recupera o valor de atributo `ProductID` do XML. O valor é então atribuído a uma variável `int`.  
  
```  
DECLARE @myDoc xml  
DECLARE @ProdID int  
SET @myDoc = '<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>  
</ProductDescription>  
</Root>'  
  
SET @ProdID =  @myDoc.value('(/Root/ProductDescription/@ProductID)[1]', 'int' )  
SELECT @ProdID  
```  
  
 O valor 1 é retornado como resultado.  
  
 Embora exista apenas um atributo `ProductID` na instância XML, as regras de digitação estática exigem que você especifique explicitamente que a expressão de caminho retorne um singleton. Portanto, o `[1]` adicional é especificado ao término da expressão de caminho. Para obter mais informações sobre digitação estática, consulte [XQuery e digitação estática](../../xquery/xquery-and-static-typing.md).  
  
### <a name="b-using-the-value-method-to-retrieve-a-value-from-an-xml-type-column"></a>B. Usando o método de value() para recuperar um valor de uma coluna de tipo xml  
 A consulta a seguir é especificada em uma **xml** coluna de tipo (`CatalogDescription`) no `AdventureWorks` banco de dados. A consulta recupera valores de atributo `ProductModelID` de cada instância de XML armazenada na coluna.  
  
```  
SELECT CatalogDescription.value('             
    declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";             
       (/PD:ProductDescription/@ProductModelID)[1]', 'int') AS Result             
FROM Production.ProductModel             
WHERE CatalogDescription IS NOT NULL             
ORDER BY Result desc             
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A palavra-chave `namespace` é usada para definir um prefixo de namespace.  
  
-   De acordo com as exigências de digitação estática, `[1]` é adicionado no final da expressão de caminho no método `value()` a fim de indicar explicitamente que a expressão de caminho retorna um singleton.  
  
 Este é o resultado parcial:  
  
```  
-----------  
35           
34           
...  
```  
  
### <a name="c-using-the-value-and-exist-methods-to-retrieve-values-from-an-xml-type-column"></a>C. Usando os métodos valor() e exist() para recuperar valores de uma coluna tipo xml  
 O exemplo a seguir demonstra o uso de `value()` método e o [método exist ()](../../t-sql/xml/exist-method-xml-data-type.md) do **xml** tipo de dados. O método `value()` é usado para recuperar valores de atributo `ProductModelID` do XML. O método `exist()` na cláusula`WHERE` é usado para filtrar as linhas da tabela.  
  
 A consulta recupera IDs de modelo de produto de instâncias XML que incluem informações de garantia (o elemento <`Warranty`>) como um dos recursos. A condição na cláusula `WHERE` usa o método `exist()` para recuperar apenas as linhas que satisfazem esta condição.  
  
```  
SELECT CatalogDescription.value('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
           (/PD:ProductDescription/@ProductModelID)[1] ', 'int') as Result  
FROM  Production.ProductModel  
WHERE CatalogDescription.exist('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A coluna `CatalogDescription` é uma coluna XML com tipo. Isso significa que ela possui uma coleção de esquema associada ao mesmo. No [prólogo do XQuery](../../xquery/modules-and-prologs-xquery-prolog.md), a declaração de namespace é usada para definir o prefixo que é usado posteriormente no corpo da consulta.  
  
-   Se o método `exist()` retorna um `1` (True), isso indica que a instância XML inclui o elemento filho <`Warranty`> como um dos recursos.  
  
-   O método `value()` na cláusula `SELECT` recupera os valores de atributo `ProductModelID` como inteiros.  
  
 Este é o resultado parcial:  
  
```  
Result       
-----------  
19           
23           
...  
```  
  
### <a name="d-using-the-exist-method-instead-of-the-value-method"></a>D. Usando o método exist() em vez do método value()  
 Por motivos de desempenho, em vez de usar o método `value()` em um predicado para comparar com um valor relacional, use `exist()` com `sql:column()`. Por exemplo:  
  
```  
CREATE TABLE T (c1 int, c2 varchar(10), c3 xml)  
GO  
  
SELECT c1, c2, c3   
FROM T  
WHERE c3.value( '/root[1]/@a', 'integer') = c1  
GO  
```  
  
 Isso pode ser gravado da seguinte maneira:  
  
```  
SELECT c1, c2, c3   
FROM T  
WHERE c3.exist( '/root[@a=sql:column("c1")]') = 1  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar namespaces a consultas com WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Comparar XML digitado com XML não digitado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [Métodos de tipos de dados xml](../../t-sql/xml/xml-data-type-methods.md)   
 [Linguagem de modificação de dados XML &#40; XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  

