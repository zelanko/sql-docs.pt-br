---
title: Método value() (tipo de dados xml) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
manager: craigg
ms.openlocfilehash: edd094a6c887c390f7a37dbd0ac3ca7950b49d02
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36253158"
---
# <a name="value-method-xml-data-type"></a>Método de valor() (Tipo de dados xml)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Executa uma XQuery em relação ao XML e retorna um valor de tipo SQL. Este método retorna um valor escalar.  
  
 Este método é usado, em geral, para extrair um valor de uma instância de XML armazenada em uma coluna de tipo, um parâmetro ou uma variável **xml**. Dessa forma, você pode especificar consultas SELECT que combinam ou comparam dados de XML com dados em colunas não XML.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
value (XQuery, SQLType)  
```  
  
## <a name="arguments"></a>Argumentos  
 *XQuery*  
 É a expressão *XQuery*, uma literal de cadeia de caracteres, que recupera dados dentro da instância de XML. A XQuery deve retornar no máximo um valor. Caso contrário, um erro é retornado.  
  
 *SQLType*  
 É o tipo SQL preferido, uma literal de cadeia de caracteres, a ser retornado. O tipo de retorno desse método corresponde ao parâmetro *SQLType*. *SQLType* não pode ser um tipo de dados **xml**, um tipo CLR (Common Language Runtime) definido pelo usuário, um tipo de dados **image**, **text**, **ntext** ou **sql_variant**. *SQLType* pode ser um tipo de dados SQL definido pelo usuário.  
  
 O método **value()** usa o operador [!INCLUDE[tsql](../../includes/tsql-md.md)] CONVERT implicitamente e tenta converter o resultado da expressão XQuery, a representação serializada de cadeia de caracteres, do tipo XSD para o tipo SQL correspondente especificado pela conversão de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para obter mais informações sobre regras de conversão de tipo para CONVERT, consulte [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
> [!NOTE]  
>  Por motivos de desempenho, em vez de usar o método **value()** em um predicado para comparação com um valor relacional, use **exist()** com **sql:column()**. Isso é demonstrado no exemplo D a seguir.  
  
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
  
 Embora exista apenas um atributo `ProductID` na instância XML, as regras de digitação estática exigem que você especifique explicitamente que a expressão de caminho retorne um singleton. Portanto, o `[1]` adicional é especificado ao término da expressão de caminho. Para obter mais informações sobre a tipagem estática, consulte [XQuery e tipagem estática](../../xquery/xquery-and-static-typing.md).  
  
### <a name="b-using-the-value-method-to-retrieve-a-value-from-an-xml-type-column"></a>B. Usando o método de value() para recuperar um valor de uma coluna de tipo xml  
 A consulta a seguir é especificada em uma coluna de tipo **xml** (`CatalogDescription`) no banco de dados `AdventureWorks`. A consulta recupera valores de atributo `ProductModelID` de cada instância de XML armazenada na coluna.  
  
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
 O exemplo a seguir demonstra o uso do método `value()` e do [método exist()](../../t-sql/xml/exist-method-xml-data-type.md) do tipo de dados **xml**. O método `value()` é usado para recuperar valores de atributo `ProductModelID` do XML. O método `exist()` na cláusula`WHERE` é usado para filtrar as linhas da tabela.  
  
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
  
-   A coluna `CatalogDescription` é uma coluna XML com tipo. Isso significa que ela possui uma coleção de esquema associada ao mesmo. No [Prólogo do XQuery](../../xquery/modules-and-prologs-xquery-prolog.md), a declaração de namespace é usada para definir o prefixo que é usado posteriormente no corpo da consulta.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar namespaces a consultas com WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Comparar XML digitado com XML não digitado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [Métodos de tipos de dados xml](../../t-sql/xml/xml-data-type-methods.md)   
 [XML DML &#40;linguagem de manipulação de dados XML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
