---
title: 'Exemplos: Usando OPENXML | Microsoft Docs'
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- ColPattern [XML in SQL Server]
- XML [SQL Server], mapping data
- OPENXML statement, about OPENXML statement
- overflow in XML document [SQL Server]
- mapping XML data [SQL Server]
- combining attribute-centric and element centric mapping
- unconsumed data
- attribute-centric mapping
- column patterns [XML in SQL Server]
- XML [SQL Server], overflow handling
- row patterns [XML in SQL Server]
- rowpattern [XML in SQL Server]
- flags parameter
- element-centric mapping [SQL Server]
- edge tables
ms.assetid: 689297f3-adb0-4d8d-bf62-cfda26210164
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4ea3ad1c2f7cb482888f0cd4d31a91f9975745b7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67943382"
---
# <a name="examples-using-openxml"></a>Exemplos: uso do OPENXML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Os exemplos neste tópico mostram como o OPENXML é usado para criar uma exibição de conjunto de linhas de um documento XML. Para obter informações sobre a sintaxe do OPENXML, veja [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md). Os exemplos mostram todos os aspectos do OPENXML, mas não especificam metapropriedades no OPENXML. Para obter mais informações sobre como especificar metapropriedades no OPENXML, veja [Especificar metapropriedades no OPENXML](../../relational-databases/xml/specify-metaproperties-in-openxml.md).  
  
## <a name="examples"></a>Exemplos  
 Ao recuperar dados, *rowpattern* é usado para identificar os nós no documento XML que determinam as linhas. Além disso, *rowpattern* é expressado na linguagem padrão XPath que é usada na implementação do MSXML XPath. Por exemplo, se o padrão terminar em um elemento ou atributo, uma linha será criada para cada elemento ou atributo selecionado por *rowpattern*.  
  
 O valor de *flags* fornece o mapeamento padrão. Se nenhum *ColPattern* for especificado no *SchemaDeclaration*, o mapeamento especificado em *flags* será assumido. O valor de *flags* será ignorado se *ColPattern* estiver especificado em *SchemaDeclaration*. O *ColPattern* especificado determina o mapeamento centrado em atributo ou centrado em elemento e também o comportamento para manipulação de dados não consumidos ou de estouro.  
  
### <a name="a-executing-a-simple-select-statement-with-openxml"></a>A. Executando uma instrução SELECT simples com OPENXML  
 O documento XML neste exemplo é composto dos elementos <`Customer`>, <`Order`>e <`OrderDetail`>. A instrução OPENXML recupera informações do cliente em um conjunto de linhas de duas colunas, **CustomerID** e **ContactName**, do documento XML.  
  
 Primeiro, o procedimento armazenado **sp_xml_preparedocument** é chamado para obter um identificador de documento. Esse identificador de documento é passado para o OPENXML.  
  
 A instrução OPENXML ilustra o seguinte:  
  
-   *rowpattern* (/ROOT/Customer) identifica os nós <`Customer`> a serem processados.  
  
-   O valor do parâmetro *flags* é definido como **1** e indica o mapeamento centrado em atributo. Como resultado, os atributos XML são mapeados para as colunas no conjunto de linhas definido em *SchemaDeclaration*.  
  
-   Em *SchemaDeclaration*, na cláusula WITH, os valores de *ColName* especificados correspondem aos nomes dos atributos XML correspondentes. Portanto o parâmetro *ColPattern* não é especificado em *SchemaDeclaration*.  
  
 Em seguida, a instrução SELECT recupera todas as colunas no conjunto de linhas fornecido pelo OPENXML.  
  
```  
DECLARE @DocHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
          OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
          OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @DocHandle OUTPUT, @XmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@DocHandle, '/ROOT/Customer',1)  
      WITH (CustomerID  varchar(10),  
            ContactName varchar(20))  
EXEC sp_xml_removedocument @DocHandle  
```  
  
 Este é o resultado:  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 Como os elementos <`Customer`> não têm nenhum subelemento, se a mesma instrução SELECT for executada com *flags* definido como **2** para indicar mapeamento centrado em elemento, os valores de **CustomerID** e **ContactName** dos dois clientes serão retornados como NULL.  
  
 O \@xmlDocument também podem ser do tipo **xml** ou do tipo **(n)varchar(max)** .  
  
 Se <`CustomerID`> e <`ContactName`> no documento XML forem subelementos, o mapeamento centrado em elemento recuperará os valores.  
  
```  
DECLARE @XmlDocumentHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer>  
   <CustomerID>VINET</CustomerID>  
   <ContactName>Paul Henriot</ContactName>  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5" OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer>     
   <CustomerID>LILAS</CustomerID>  
   <ContactName>Carlos Gonzlez</ContactName>  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3" OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @XmlDocumentHandle OUTPUT, @XmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT    *  
FROM      OPENXML (@XmlDocumentHandle, '/ROOT/Customer',2)  
           WITH (CustomerID  varchar(10),  
                 ContactName varchar(20))  
EXEC sp_xml_removedocument @XmlDocumentHandle  
```  
  
 Este é o resultado:  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 Observe que o identificador de documento retornado por **sp_xml_preparedocument** é válido durante o lote e não durante a sessão.  
  
### <a name="b-specifying-colpattern-for-mapping-between-rowset-columns-and-the-xml-attributes-and-elements"></a>B. Especificando ColPattern para mapeamento entre colunas do conjunto de linhas e os elementos e atributos XML  
 Este exemplo mostra como o padrão Xpath é especificado no parâmetro *ColPattern* opcional para fornecer mapeamento entre colunas do conjunto de linhas e os elementos e atributos XML.  
  
 O documento XML neste exemplo é composto dos elementos <`Customer`>, <`Order`>e <`OrderDetail`>. A instrução OPENXML recupera informações do cliente e do pedido como um conjunto de linhas (**CustomerID**, **OrderDate**, **ProdID** e **Qty**) do documento XML.  
  
 Primeiro, o procedimento armazenado **sp_xml_preparedocument** é chamado para obter um identificador de documento. Esse identificador de documento é passado para o OPENXML.  
  
 A instrução OPENXML ilustra o seguinte:  
  
-   *rowpattern* (/ROOT/Customer/Order/OrderDetail) identifica os nós <`OrderDetail`> a serem processados.  
  
 Para fins ilustrativos, o valor do parâmetro *flags* está definido como **2** e indica mapeamento centrado em elemento. No entanto o mapeamento especificado em *ColPattern* substitui esse mapeamento. Quer dizer, o padrão XPath especificado em *ColPattern* mapeia as colunas do conjunto de linhas para atributos. Isso resulta em mapeamento centrado em atributo.  
  
 Em *SchemaDeclaration*, cláusula WITH, *ColPattern* também é especificado com os parâmetros *ColName* e *ColType* . O *ColPattern* opcional é o padrão XPath especificado e indica o seguinte:  
  
-   As colunas **OrderID**, **CustomerID** e **OrderDate** no conjunto de linhas são mapeadas para os atributos do pai dos nós identificados por *rowpattern*, e *rowpattern* identifica os nós <`OrderDetail`>. Portanto as colunas **CustomerID** e **OrderDate** são mapeadas para os atributos **CustomerID** e **OrderDate** do elemento <`Order`>.  
  
-   As colunas **ProdID** e **Qty** do conjunto de linhas são mapeadas para os atributos **ProductID** e **Quantity** dos nós identificados em *rowpattern*.  
  
 Em seguida, a instrução SELECT recupera todas as colunas no conjunto de linhas fornecido pelo OPENXML.  
  
```  
DECLARE @XmlDocumentHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
           OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
           OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @XmlDocumentHandle OUTPUT, @XmlDocument  
-- Execute a SELECT stmt using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@XmlDocumentHandle, '/ROOT/Customer/Order/OrderDetail',2)  
WITH (OrderID     int         '../@OrderID',  
      CustomerID  varchar(10) '../@CustomerID',  
      OrderDate   datetime    '../@OrderDate',  
      ProdID      int         '@ProductID',  
      Qty         int         '@Quantity')  
EXEC sp_xml_removedocument @XmlDocumentHandle  
```  
  
 Este é o resultado:  
  
```  
OrderID CustomerID        OrderDate          ProdID    Qty  
-------------------------------------------------------------  
10248    VINET     1996-07-04 00:00:00.000     11       12  
10248    VINET     1996-07-04 00:00:00.000     42       10  
10283    LILAS     1996-08-16 00:00:00.000     72        3  
```  
  
 O padrão XPath especificado como *ColPattern* também pode ser especificado para mapear os elementos XML para as colunas do conjunto de linhas. Isso resulta em mapeamento centrado em elemento. No exemplo seguinte, o documento XML <`CustomerID`> e <`OrderDate`> são subelementos do elemento <`Orders`>. Como *ColPattern* substitui o mapeamento especificado no parâmetro *flags* , o parâmetro *flags* não é especificado no OPENXML.  
  
```  
DECLARE @docHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order EmployeeID="5" >  
      <OrderID>10248</OrderID>  
      <CustomerID>VINET</CustomerID>  
      <OrderDate>1996-07-04T00:00:00</OrderDate>  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order  EmployeeID="3" >  
      <OrderID>10283</OrderID>  
      <CustomerID>LILAS</CustomerID>  
      <OrderDate>1996-08-16T00:00:00</OrderDate>  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @XmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer/Order/OrderDetail')  
WITH (CustomerID  varchar(10)   '../CustomerID',  
      OrderDate   datetime      '../OrderDate',  
      ProdID      int           '@ProductID',  
      Qty         int           '@Quantity')  
EXEC sp_xml_removedocument @docHandle  
```  
  
### <a name="c-combining-attribute-centric-and-element-centric-mapping"></a>C. Combinando o mapeamento centrado em elemento e centrado em atributo  
 Neste exemplo, o parâmetro *flags* está definido como **3** e indica que o mapeamento centrado em atributo e o mapeamento centrado em elemento serão aplicados. Nesse caso, o mapeamento centrado em atributo é aplicado primeiro e, em seguida, o mapeamento centrado em elemento é aplicado a todas as colunas que ainda não foram tratadas.  
  
```  
DECLARE @docHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument =N'<ROOT>  
<Customer CustomerID="VINET"  >  
     <ContactName>Paul Henriot</ContactName>  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
          OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" >   
     <ContactName>Carlos Gonzlez</ContactName>  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
          OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @XmlDocument  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer',3)  
      WITH (CustomerID  varchar(10),  
            ContactName varchar(20))  
EXEC sp_xml_removedocument @docHandle  
```  
  
 Este será o resultado  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 O mapeamento centrado em atributo é aplicado para **CustomerID**. Não há nenhum atributo **ContactName** no elemento <`Customer`>. Portanto o mapeamento centrado em elemento é aplicado.  
  
### <a name="d-specifying-the-text-xpath-function-as-colpattern"></a>D. Especificando a função text() XPath como ColPattern  
 O documento XML neste exemplo é composto dos elementos <`Customer`> e <`Order`>. A instrução OPENXML recupera um conjunto de linhas composto do atributo **oid** do elemento <`Order`>, a ID do pai do nó identificado por *rowpattern* e a cadeia de caracteres do valor de folha do conteúdo do elemento.  
  
 Primeiro, o procedimento armazenado **sp_xml_preparedocument** é chamado para obter um identificador de documento. Esse identificador de documento é passado para o OPENXML.  
  
 A instrução OPENXML ilustra o seguinte:  
  
-   *rowpattern* (/root/Customer/Order) identifica os nós <`Order`> a serem processados.  
  
-   O valor do parâmetro *flags* é definido como **1** e indica o mapeamento centrado em atributo. Como resultado, os atributos XML são mapeados para as colunas do conjunto de linhas definidas em *SchemaDeclaration*.  
  
-   Em *SchemaDeclaration* na cláusula WITH, os nomes das colunas do conjunto de linhas **oid** e **amount** coincidem com os nomes dos atributos XML correspondentes. Portanto o parâmetro *ColPattern* não é especificado. Para a coluna **comment** do conjunto de linhas, a função XPath, **text()** , é especificada como *ColPattern*. Isso substitui o mapeamento centrado em atributo especificado em *flags*, e a coluna contém a cadeia de caracteres do valor de folha do conteúdo do elemento.  
  
 Em seguida, a instrução SELECT recupera todas as colunas no conjunto de linhas fornecido pelo OPENXML.  
  
```  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
--sample XML document  
SET @xmlDocument =N'<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very satisfied  
      </Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue   
             white red">  
            <Urgency>Important</Urgency>  
            Happy Customer.  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/root/Customer/Order', 1)  
     WITH (oid     char(5),   
           amount  float,   
           comment ntext 'text()')  
EXEC sp_xml_removedocument @docHandle  
```  
  
 Este é o resultado:  
  
```  
oid   amount        comment  
----- -----------   -----------------------------  
O1    3.5           NULL  
O2    13.4          Customer was very satisfied  
O3    100.0         Happy Customer.  
O4    10000.0       NULL  
```  
  
### <a name="e-specifying-tablename-in-the-with-clause"></a>E. Especificando TableName na cláusula WITH  
 Este exemplo especifica *TableName* na cláusula WITH em vez de *SchemaDeclaration*. Isso será útil se você tiver uma tabela que tem a estrutura desejada e nenhum padrão de coluna, parâmetro *ColPattern* , é necessário.  
  
 O documento XML neste exemplo é composto dos elementos <`Customer`> e <`Order`>. A instrução OPENXML recupera informações de pedido em um conjunto de linhas de três colunas (**oid**, **date** e **amount**) do documento XML.  
  
 Primeiro, o procedimento armazenado **sp_xml_preparedocument** é chamado para obter um identificador de documento. Esse identificador de documento é passado para o OPENXML.  
  
 A instrução OPENXML ilustra o seguinte:  
  
-   *rowpattern* (/root/Customer/Order) identifica os nós <`Order`> a serem processados.  
  
-   Não há nenhum *SchemaDeclaration* na cláusula WITH. Em vez disso, um nome de tabela é especificado. Portanto o esquema da tabela é usado como o esquema do conjunto de linhas.  
  
-   O valor do parâmetro *flags* é definido como **1** e indica o mapeamento centrado em atributo. Portanto os atributos dos elementos identificados por *rowpattern*são mapeados para as colunas do conjunto de linhas com o mesmo nome.  
  
 Em seguida, a instrução SELECT recupera todas as colunas no conjunto de linhas fornecido pelo OPENXML.  
  
```  
-- Create a test table. This table schema is used by OPENXML as the  
-- rowset schema.  
CREATE TABLE T1(oid char(5), date datetime, amount float)  
GO  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
-- Sample XML document  
SET @xmlDocument =N'<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very   
             satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue   
             white red">  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>'  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/root/Customer/Order', 1)  
     WITH T1  
EXEC sp_xml_removedocument @docHandle  
```  
  
 Este é o resultado:  
  
```  
oid   date                        amount  
----- --------------------------- ----------  
O1    1996-01-20 00:00:00.000     3.5  
O2    1997-04-30 00:00:00.000     13.4  
O3    1999-07-14 00:00:00.000     100.0  
O4    1996-01-20 00:00:00.000     10000.0  
```  
  
### <a name="f-obtaining-the-result-in-an-edge-table-format"></a>F. Obtendo o resultado em um formato de tabela de borda  
 Neste exemplo, a cláusula WITH não é especificada na instrução OPENXML. Como resultado, o conjunto de linhas gerado por OPENXML tem um formato de tabela de borda. A instrução SELECT retorna todas as colunas da tabela de borda.  
  
 O documento XML de exemplo é composto dos elementos <`Customer`>, <`Order`> e <`OrderDetail`>.  
  
 Primeiro, o procedimento armazenado **sp_xml_preparedocument** é chamado para obter um identificador de documento. Esse identificador de documento é passado para o OPENXML.  
  
 A instrução OPENXML ilustra o seguinte:  
  
-   *rowpattern* (/ROOT/Customer) identifica os nós <`Customer`> a serem processados.  
  
-   A cláusula WITH não é fornecida. Portanto o OPENXML retorna o conjunto de linhas em um formato de tabela de borda.  
  
 Em seguida, a instrução SELECT retorna todas as colunas da tabela de borda.  
  
```  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
SET @xmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5" OrderDate=  
           "1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3" OrderDate=  
           "1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer')  
  
EXEC sp_xml_removedocument @docHandle  
```  
  
 O resultado é retornado como uma tabela de borda. É possível escrever consultas em relação à tabela de borda para obter informações. Por exemplo:  
  
-   A consulta a seguir retorna o número de nós **Customer** no documento. Como a cláusula WITH não é especificada, o OPENXML retorna uma tabela de borda. A instrução SELECT consulta a tabela de borda.  
  
    ```  
    SELECT count(*)  
    FROM OPENXML(@docHandle, '/')  
    WHERE localname = 'Customer'  
    ```  
  
-   A consulta a seguir retorna os nomes locais de nós XML do tipo do elemento.  
  
    ```  
    SELECT distinct localname   
    FROM OPENXML(@docHandle, '/')   
    WHERE nodetype = 1   
    ORDER BY localname  
    ```  
  
### <a name="g-specifying-rowpattern-ending-with-an-attribute"></a>G. Especificando rowpattern terminando com um atributo  
 O documento XML neste exemplo é composto dos elementos <`Customer`>, <`Order`>e <`OrderDetail`>. A instrução OPENXML recupera informações sobre os detalhes do pedido em um conjunto de linhas de três colunas (**ProductID**, **Quantity** e **OrderID**) do documento XML.  
  
 Primeiro, o **sp_xml_preparedocument** é chamado para obter um identificador de documento. Esse identificador de documento é passado para o OPENXML.  
  
 A instrução OPENXML ilustra o seguinte:  
  
-   *rowpattern* (/ROOT/Customer/Order/OrderDetail/\@ProductID) termina com um atributo XML, **ProductID**. No conjunto de linhas resultante, uma linha é criada para cada nó de atributo selecionado no documento XML.  
  
-   Neste exemplo, o parâmetro *flags* não é especificado. Em vez disso, os mapeamentos são especificados pelo parâmetro *ColPattern* .  
  
 Em *SchemaDeclaration* na cláusula WITH, *ColPattern* também é especificado com os parâmetros *ColName* e *ColType* . O *ColPattern* opcional é o padrão XPath especificado para indicar o seguinte:  
  
-   O padrão XPath ( **.** ) especificado como *ColPattern* para a coluna **ProdID** no conjunto de linhas identifica o nó de contexto, o nó atual. De acordo com o *rowpattern* especificado, ele é o atributo **ProductID** do elemento <`OrderDetail`>.  
  
-   O *ColPattern*, **../\@Quantity**, especificado para a coluna **Qty** no conjunto de linhas identifica o atributo **Quantity** do pai, <`OrderDetail`>, nó do nó de contexto, \<ProductID>.  
  
-   De maneira semelhante, o *ColPattern*, **../../\@OrderID**, especificado para a coluna **OID** no conjunto de linhas identifica o atributo **OrderID** do pai, <`Order`>, do nó pai do nó de contexto. O nó pai é <`OrderDetail`>, e o nó de contexto é <`ProductID`>.  
  
 Em seguida, a instrução SELECT recupera todas as colunas no conjunto de linhas fornecido pelo OPENXML.  
  
```  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
--Sample XML document  
SET @xmlDocument =N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5" OrderDate=  
           "1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3" OrderDate=  
           "1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer/Order/OrderDetail/@ProductID')  
       WITH ( ProdID  int '.',  
              Qty     int '../@Quantity',  
              OID     int '../../@OrderID')  
EXEC sp_xml_removedocument @docHandle  
```  
  
 Este é o resultado:  
  
```  
ProdID      Qty         OID  
----------- ----------- -------   
11          12          10248  
42          10          10248  
72          3           10283  
```  
  
### <a name="h-specifying-an-xml-document-that-has-multiple-text-nodes"></a>H. Especificando um documento XML que tem vários nós de texto  
 Se você tiver vários nós de texto em um documento XML, uma instrução SELECT com um *ColPattern*, **text()** , retornará apenas o primeiro nó de texto, em vez de todos eles. Por exemplo:  
  
```  
DECLARE @h int  
EXEC sp_xml_preparedocument @h OUTPUT,  
         N'<root xmlns:a="urn:1">  
           <a:Elem abar="asdf">  
             T<a>a</a>U  
           </a:Elem>  
         </root>',  
         '<ns xmlns:b="urn:1" />'  
  
SELECT * FROM openxml(@h, '/root/b:Elem')  
      WITH (Col1 varchar(20) 'text()')  
EXEC sp_xml_removedocument @h  
```  
  
 A instrução SELECT retorna **T** como o resultado, e não **TaU**.  
  
### <a name="i-specifying-the-xml-data-type-in-the-with-clause"></a>I. Especificando o tipo de dados xml na cláusula WITH  
 Na cláusula WITH, um padrão de coluna que é mapeado para a coluna de tipo de dados **xml** , com tipo ou sem-tipo, deve retornar uma sequência vazia ou uma sequência de elementos, instruções de processamento, nós de texto e comentários. Os dados são convertidos em um tipo de dados **xml** .  
  
 No exemplo a seguir, a declaração de esquema de tabela na cláusula WITH inclui colunas de tipo **xml** .  
  
```  
DECLARE @h int  
DECLARE @x xml  
set @x = '<Root>  
  <row id="1"><lname>Duffy</lname>  
   <Address>  
            <Street>111 Maple</Street>  
            <City>Seattle</City>  
   </Address>  
  </row>  
  <row id="2"><lname>Wang</lname>  
   <Address>  
            <Street>222 Pine</Street>  
            <City>Bothell</City>  
   </Address>  
  </row>  
</Root>'  
  
EXEC sp_xml_preparedocument @h output, @x  
SELECT *  
FROM   OPENXML (@h, '/Root/row', 10)  
      WITH (id int '@id',  
  
            lname    varchar(30),  
            xmlname  xml 'lname',  
            OverFlow xml '@mp:xmltext')  
EXEC sp_xml_removedocument @h  
```  
  
 Especificamente, você está passando uma variável de tipo **xml** (\@x) para a função **sp_xml_preparedocument()** .  
  
 Este é o resultado:  
  
```  
id  lname   xmlname                   OverFlow  
--- ------- ------------------------------ -------------------------------  
1   Duffy   <lname>Duffy</lname>  <row><Address>  
                                   <Street>111 Maple</Street>  
                                   <City>Seattle</City>  
                                  </Address></row>  
2   Wang    <lname>Wang</lname>   <row><Address>  
                                    <Street>222 Pine</Street>  
                                    <City>Bothell</City>  
                                   </Address></row>  
```  
  
 Observe o seguinte no resultado:  
  
-   Para a coluna **lname** de tipo **varchar(30)** , o valor é recuperado do elemento <`lname`> correspondente.  
  
-   Para a coluna **xmlname** de tipo **xml** , o mesmo elemento de nome é retornado como seu valor.  
  
-   O sinalizador é definido como 10. O 10 significa 2 + 8, em que 2 indica mapeamento centrado em elemento e 8 indica que apenas os dados XML não consumidos devem ser adicionados à coluna OverFlow definida na cláusula WITH. Se você definir o sinalizador como 2, todo o documento XML será copiado para a coluna OverFlow especificada na cláusula WITH.  
  
-   Caso a coluna da cláusula WITH seja uma coluna XML com tipo e a instância XML não seja confirmada para o esquema, será retornado um erro.  
  
### <a name="j-retrieving-individual-values-from-multivalued-attributes"></a>J. Recuperando valores individuais de atributos com vários valores  
 Um documento XML pode ter atributos com vários valores. Por exemplo, o atributo **IDREFS** pode ter vários valores. Em um documento XML, valores de atributos com vários valores são especificados como uma cadeia de caracteres, com os valores separados por um espaço. No documento XML a seguir, o atributo **attends** do elemento \<Student> e o atributo **attendedBy** de \<Class> têm vários valores. A recuperação de valores individuais de um atributo XML de vários valores e o armazenamento de cada valor em uma linha separada no banco de dados requer trabalho adicional. Este exemplo mostra o processo.  
  
 Este documento XML de exemplo é composto dos seguintes elementos:  
  
-   \<Student>  
  
     Os atributos **id** (ID do estudante), **name**e **attends** . O atributo **attends** é um atributo com vários valores.  
  
-   \<Class>  
  
     Os atributos **id** (ID da aula), **name**e **attendedBy** . O atributo **attendedBy** é um atributo com vários valores.  
  
 O atributo **attends** em \<Student> e o atributo **attendedBy** em \<Class> representam uma relação **m:n** entre as tabelas Student e Class. Um estudante pode assistir muitas aulas e uma aula pode ter muitos estudantes.  
  
 Suponha que você queira fragmentar esse documento e salvá-lo no banco de dados, conforme mostrado a seguir:  
  
-   Salve os dados de \<Student> na tabela Students.  
  
-   Salve os dados de \<Class> na tabela Courses.  
  
-   Salve os dados da relação **m:n** , entre Student e Class, na tabela CourseAttendence. Trabalho adicional é necessário para extrair os valores. Para recuperar essas informações e armazená-las na tabela, use estes procedimentos armazenados:  
  
    -   **Insert_Idrefs_Values**  
  
         Insere os valores de ID do curso e ID do estudante na tabela CourseAttendence.  
  
    -   **Extract_idrefs_values**  
  
         Extrai as IDs de estudantes individuais de cada elemento \<Course>. Uma tabela de borda é usada para recuperar esses valores.  
  
 Estas são as etapas:  
  
```  
-- Create these tables:  
DROP TABLE CourseAttendance  
DROP TABLE Students  
DROP TABLE Courses  
GO  
CREATE TABLE Students(  
                id   varchar(5) primary key,  
                name varchar(30)  
                )  
GO  
CREATE TABLE Courses(  
               id       varchar(5) primary key,  
               name     varchar(30),  
               taughtBy varchar(5)  
)  
GO  
CREATE TABLE CourseAttendance(  
             id         varchar(5) references Courses(id),  
             attendedBy varchar(5) references Students(id),  
             constraint CourseAttendance_PK primary key (id, attendedBy)  
)  
go  
-- Create these stored procedures:  
DROP PROCEDURE f_idrefs  
GO  
CREATE PROCEDURE f_idrefs  
    @t      varchar(500),  
    @idtab  varchar(50),  
    @id     varchar(5)  
AS  
DECLARE @sp int  
DECLARE @att varchar(5)  
SET @sp = 0  
WHILE (LEN(@t) > 0)  
BEGIN   
    SET @sp = CHARINDEX(' ', @t+ ' ')  
    SET @att = LEFT(@t, @sp-1)  
    EXEC('INSERT INTO '+@idtab+' VALUES ('''+@id+''', '''+@att+''')')  
    SET @t = SUBSTRING(@t+ ' ', @sp+1, LEN(@t)+1-@sp)  
END  
Go  
  
DROP PROCEDURE fill_idrefs  
GO  
CREATE PROCEDURE fill_idrefs   
    @xmldoc     int,  
    @xpath      varchar(100),  
    @from       varchar(50),  
    @to         varchar(50),  
    @idtable    varchar(100)  
AS  
DECLARE @t varchar(500)  
DECLARE @id varchar(5)  
  
/* Temporary Edge table */  
SELECT *   
INTO #TempEdge   
FROM OPENXML(@xmldoc, @xpath)  
  
DECLARE fillidrefs_cursor CURSOR FOR  
    SELECT CAST(iv.text AS nvarchar(200)) AS id,  
           CAST(av.text AS nvarchar(4000)) AS refs  
    FROM   #TempEdge c, #TempEdge i,  
           #TempEdge iv, #TempEdge a, #TempEdge av  
    WHERE  c.id = i.parentid  
    AND    UPPER(i.localname) = UPPER(@from)  
    AND    i.id = iv.parentid  
    AND    c.id = a.parentid  
    AND    UPPER(a.localname) = UPPER(@to)  
    AND    a.id = av.parentid  
  
OPEN fillidrefs_cursor  
FETCH NEXT FROM fillidrefs_cursor INTO @id, @t  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
    IF (@@FETCH_STATUS <> -2)  
    BEGIN  
        execute f_idrefs @t, @idtable, @id  
    END  
    FETCH NEXT FROM fillidrefs_cursor INTO @id, @t  
END  
CLOSE fillidrefs_cursor  
DEALLOCATE fillidrefs_cursor  
Go  
-- This is the sample document that is shredded and the data is stored in the preceding tables.  
DECLARE @h int  
EXECUTE sp_xml_preparedocument @h OUTPUT, N'<Data>  
  <Student id = "s1" name = "Student1"  attends = "c1 c3 c6"  />  
  <Student id = "s2" name = "Student2"  attends = "c2 c4" />  
  <Student id = "s3" name = "Student3"  attends = "c2 c4 c6" />  
  <Student id = "s4" name = "Student4"  attends = "c1 c3 c5" />  
  <Student id = "s5" name = "Student5"  attends = "c1 c3 c5 c6" />  
  <Student id = "s6" name = "Student6" />  
  
  <Class id = "c1" name = "Intro to Programming"   
         attendedBy = "s1 s4 s5" />  
  <Class id = "c2" name = "Databases"   
         attendedBy = "s2 s3" />  
  <Class id = "c3" name = "Operating Systems"   
         attendedBy = "s1 s4 s5" />  
  <Class id = "c4" name = "Networks" attendedBy = "s2 s3" />  
  <Class id = "c5" name = "Algorithms and Graphs"   
         attendedBy =  "s4 s5"/>  
  <Class id = "c6" name = "Power and Pragmatism"   
         attendedBy = "s1 s3 s5" />  
</Data>'  
  
INSERT INTO Students SELECT * FROM OPENXML(@h, '//Student') WITH Students  
  
INSERT INTO Courses SELECT * FROM OPENXML(@h, '//Class') WITH Courses  
/* Using the edge table */  
EXECUTE fill_idrefs @h, '//Class', 'id', 'attendedby', 'CourseAttendance'  
  
SELECT * FROM Students  
SELECT * FROM Courses  
SELECT * FROM CourseAttendance  
  
EXECUTE sp_xml_removedocument @h  
```  
  
### <a name="k-retrieving-binary-from-base64-encoded-data-in-xml"></a>K. Recuperando binários de dados codificados na base64 no XML  
 Dados Binários são frequentemente incluídos no XML usando codificação na base64. Quando você fragmenta esse XML usando OPENXML, você recebe os dados codificados na base64. Este exemplo mostra como é possível converter o dados codificados na base64 novamente em binários.  
  
-   Crie uma tabela com dados binários de exemplo.  
  
-   Use uma consulta FOR XML e a opção BINARY BASE64 para construir XML que tenha dados binários codificados como base64.  
  
-   Fragmente o XML usando OPENXML. Os dados retornados por OPENXML serão codificados na base64. Em seguida, chame a função .value para convertê-los novamente em binários.  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 varbinary(100))  
go  
-- Insert sample binary data  
INSERT T VALUES(1, 0x1234567890)   
go  
 -- Create test XML document that has base64 encoded binary data (use FOR XML query and specify BINARY BASE64 option)  
SELECT * FROM T  
FOR XML AUTO, BINARY BASE64  
go  
-- result  
-- <T Col1="1" Col2="EjRWeJA="/>  
  
-- Now shredd the sample XML using OPENXML.   
-- Call the .value function to convert   
-- the base64 encoded data returned by OPENXML to binary.  
DECLARE @h int ;  
EXEC sp_xml_preparedocument @h OUTPUT, '<T Col1="1" Col2="EjRWeJA="/>' ;  
SELECT Col1,   
CAST('<binary>' + Col2 + '</binary>' AS XML).value('.', 'varbinary(max)') AS BinaryCol   
FROM openxml(@h, '/T')   
WITH (Col1 integer, Col2 varchar(max)) ;  
EXEC sp_xml_removedocument @h ;  
GO  
```  
  
 Este é o resultado. Os dados binários retornados são os dados binários originais na tabela T.  
  
```  
Col1        BinaryCol  
----------- ---------------------  
1           0x1234567890  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sp_xml_preparedocument &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql.md)   
 [sp_xml_removedocument &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql.md)   
 [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md)   
 [OPENXML &#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
  
  
