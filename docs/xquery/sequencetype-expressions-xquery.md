---
title: Expressões SequenceType (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- SequenceType expressions
- instance of operator [XQuery]
- expressions [XQuery], SequenceType
- cast as operator
ms.assetid: ad3573da-d820-4d1c-81c4-a83c4640ce22
author: rothja
ms.author: jroth
ms.openlocfilehash: e7c3cdf33b0765ba50e5553f3bc31fd5c69312e0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67946288"
---
# <a name="sequencetype-expressions-xquery"></a>Expressões SequenceType (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  No XQuery, um valor é sempre uma sequência. O tipo do valor é referido como um tipo de sequência. O tipo de sequência pode ser usado em uma **instância da** expressão XQuery. A sintaxe SequenceType descrita na especificação XQuery é usada quando você precisar consultar um tipo em uma expressão XQuery.  
  
 O nome do tipo atômico também pode ser usado na expressão **Cast** as XQuery. No [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], a **instância do** e o **cast como** expressões XQuery em SequenceTypes têm suporte parcial.  
  
## <a name="instance-of-operator"></a>Operador instance of  
 A **instância do** operador pode ser usada para determinar o tipo dinâmico ou de tempo de execução do valor da expressão especificada. Por exemplo:  
  
```  
  
Expression instance of SequenceType[Occurrence indicator]  
```  
  
 Observe que o `instance of` operador, o `Occurrence indicator`, especifica a cardinalidade, o número de itens na sequência resultante. Se não estiver especificada, supõe-se que a cardinalidade seja 1. No [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], há suporte apenas para o indicador de ocorrência de ponto de interrogação (**?)** . O **?** o indicador de ocorrência `Expression` indica que o pode retornar zero ou um item. Se o **?** o indicador de ocorrência é `instance of` especificado, retorna true `Expression` quando o tipo corresponde `SequenceType`ao especificado, independentemente `Expression` de retornar um singleton ou uma sequência vazia.  
  
 Se o **?** o indicador de ocorrência não foi `sequence of` especificado, retorna true somente `Expression` quando o tipo `Type` corresponde ao `Expression` especificado e retorna um singleton.  
  
 **Observação** Não há suporte para**+** os indicadores de ocorrência símbolo de adição () e asterisco (**&#42;**) no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Os exemplos a seguir ilustram o uso da**instância do** operador XQuery.  
  
### <a name="example-a"></a>Exemplo A  
 O exemplo a seguir cria uma variável de tipo **XML** e especifica uma consulta em relação a ela. A expressão de consulta especifica um operador `instance of` para determinar se o tipo dinâmico do valor retornado pelo primeiro operando corresponde ao tipo especificado no segundo operando.  
  
 A consulta a seguir retorna true, porque o valor 125 é uma instância do tipo especificado, **xs: integer**:  
  
```  
declare @x xml  
set @x=''  
select @x.query('125 instance of xs:integer')  
go  
```  
  
 A consulta a seguir retorna True, pois o valor retornado pela expressão, /a [1], no primeiro operando é um elemento:  
  
```  
declare @x xml  
set @x='<a>1</a>'  
select @x.query('/a[1] instance of element()')  
go  
```  
  
 Da mesma forma, `instance of` retorna True na consulta a seguir, pois o tipo de valor da expressão na primeira expressão é um atributo:  
  
```  
declare @x xml  
set @x='<a attr1="x">1</a>'  
select @x.query('/a[1]/@attr1 instance of attribute()')  
go  
```  
  
 No exemplo a seguir, a expressão, `data(/a[1]`, retorna um valor atômico que é digitado como xdt:untypedAtomic. Portanto, o `instance of` retorna True.  
  
```  
declare @x xml  
set @x='<a>1</a>'  
select @x.query('data(/a[1]) instance of xdt:untypedAtomic')  
go  
```  
  
 Na consulta a seguir, a expressão, `data(/a[1]/@attrA`, retorna um valor atômico não digitado. Portanto, o `instance of` retorna True.  
  
```  
declare @x xml  
set @x='<a attrA="X">1</a>'  
select @x.query('data(/a[1]/@attrA) instance of xdt:untypedAtomic')  
go  
```  
  
### <a name="example-b"></a>Exemplo B  
 Neste exemplo, você está consultando uma coluna XML digitada no banco de dados de exemplo da AdventureWorks. A coleção de esquemas XML associada com a coluna que está sendo consultada fornece as informações digitadas.  
  
 Na expressão, **Data ()** retorna o valor tipado do atributo ProductModelID cujo tipo é xs: String de acordo com o esquema associado à coluna. Portanto, o `instance of` retorna True.  
  
```  
SELECT CatalogDescription.query('  
   declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
   data(/PD:ProductDescription[1]/@ProductModelID) instance of xs:string  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 Para obter mais informações, consulte [Comparar XML digitado com XML não digitado](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
 A expressão a seguir `instance of` consulta usetheBoolean para determinar se o atributo LocationID é do tipo xs: Integer:  
  
```  
SELECT Instructions.query('  
   declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   /AWMI:root[1]/AWMI:Location[1]/@LocationID instance of attribute(LocationID,xs:integer)  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 A consulta a seguir é especificada em relação à coluna XML CatalogDescription digitada. A coleção de esquemas XML associada com essa coluna fornece as informações digitadas.  
  
 A consulta usa o teste `element(ElementName, ElementType?)` na expressão `instance of` para verificar se o `/PD:ProductDescription[1]` retorna um nó de elemento de um nome e tipo específicos.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /PD:ProductDescription[1] instance of element(PD:ProductDescription, PD:ProductDescription?)  
    ') as Result  
FROM  Production.ProductModel  
where ProductModelID=19  
```  
  
 A consulta retorna True.  
  
### <a name="example-c"></a>Exemplo C  
 Ao usar tipos de união, a expressão `instance of` no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tem uma limitação: especificamente, quando o tipo de um elemento ou atributo for um tipo de união, `instance of` pode não determinar o tipo exato. Por conseguinte, uma consulta retornará False, a menos que os tipos atômicos usados em SequenceType sejam o pai mais elevado do tipo real da expressão na hierarquia simpleType. Ou seja, os tipos atômicos especificados em SequenceType devem ser um filho direto de anySimpleType. Para obter informações sobre a hierarquia de tipos, consulte [regras de conversão de tipo em XQuery](../xquery/type-casting-rules-in-xquery.md).  
  
 O próximo exemplo de consulta executa o seguinte:  
  
-   Crie uma coleção de esquemas XML com um tipo de união, como um inteiro ou tipo de cadeia de caracteres, definido nele.  
  
-   Declare uma variável **XML** com tipo usando a coleção de esquema XML.  
  
-   Atribua uma instância XML de amostra à variável.  
  
-   Consulte a variável para ilustrar o comportamento `instance of` ao lidar com um tipo de união.  
  
 Esta é a consulta:  
  
```  
CREATE XML SCHEMA COLLECTION MyTestSchema AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns" xmlns:ns="http://ns">  
<simpleType name="MyUnionType">  
<union memberTypes="integer string"/>  
</simpleType>  
<element name="TestElement" type="ns:MyUnionType"/>  
</schema>'  
Go  
```  
  
 A consulta a seguir retorna False, pois o SequenceType especificado na expressão `instance of` não é o pai mais alto do tipo real da expressão especificada. Ou seja, o valor do <`TestElement`> é um tipo inteiro. O pai mais alto é xs:decimal. Porém, não é especificado como o segundo operando ao operador `instance of`.  
  
```  
SET QUOTED_IDENTIFIER ON  
DECLARE @var XML(MyTestSchema)  
  
SET @var = '<TestElement xmlns="http://ns">123</TestElement>'  
  
SELECT @var.query('declare namespace ns="http://ns"   
   data(/ns:TestElement[1]) instance of xs:integer')  
go  
```  
  
 Como o pai mais alto de xs:integer é xs:decimal, a consulta retornará True se você modificar a consulta e especificar xs:decimal como SequenceType na consulta.  
  
```  
SET QUOTED_IDENTIFIER ON  
DECLARE @var XML(MyTestSchema)  
SET @var = '<TestElement xmlns="http://ns">123</TestElement>'  
SELECT @var.query('declare namespace ns="http://ns"     
   data(/ns:TestElement[1]) instance of xs:decimal')  
go  
```  
  
### <a name="example-d"></a>Exemplo D  
 Neste exemplo, você primeiro cria uma coleção de esquema XML e a usa para digitar uma variável **XML** . A variável **XML** com tipo é consultada para ilustrar `instance of` a funcionalidade.  
  
 A coleção de esquema XML a seguir define um tipo simples, com MyType e um elemento, `root` <>, do tipo com MyType:  
  
```  
drop xml schema collection SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="myNS" xmlns:ns="myNS"  
xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">  
      <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
      <simpleType name="myType">  
           <restriction base="s:varchar">  
                  <maxLength value="20"/>  
            </restriction>  
      </simpleType>  
      <element name="root" type="ns:myType"/>  
</schema>'  
Go  
```  
  
 Agora, crie uma variável **XML** com tipo e a consulte:  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "https://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
   data(/ns:root[1]) instance of ns:myType')  
go  
```  
  
 Como o tipo myType é derivado pela restrição de um tipo varchar definido no esquema sqltypes, `instance of` também retornará True.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "https://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
data(/ns:root[1]) instance of sqltypes:varchar?')  
go  
```  
  
### <a name="example-e"></a>Exemplo E  
 No exemplo a seguir, a expressão recupera um dos valores do atributo IDREFS e usa `instance of` para determinar se o valor é do tipo IDREF. O exemplo executa o seguinte:  
  
-   Cria uma coleção de esquema XML na qual o `Customer` elemento <> tem um atributo de tipo IDREFS **OrderList** e o `Order` elemento> <tem um atributo de tipo ID **OrderID** .  
  
-   Cria uma variável **XML** com tipo e atribui uma instância XML de exemplo a ela.  
  
-   Especifica uma consulta em relação à variável. A expressão de consulta recupera o valor da primeira ID do pedido do atributo tipo IDRERS OrderList da primeira `Customer` <>. O valor recuperado é do tipo IDREF. Portanto, `instance of` retorna true.  
  
```  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:Customers="Customers" targetNamespace="Customers">  
            <element name="Customers" type="Customers:CustomersType"/>  
            <complexType name="CustomersType">  
                        <sequence>  
                            <element name="Customer" type="Customers:CustomerType" minOccurs="0" maxOccurs="unbounded" />  
                        </sequence>  
            </complexType>  
             <complexType name="OrderType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="OrderValue" type="integer" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="OrderID" type="ID" />  
            </complexType>  
  
            <complexType name="CustomerType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="spouse" type="string" minOccurs="0" maxOccurs="unbounded"/>  
                                <element name="Order" type="Customers:OrderType" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="CustomerID" type="string" />  
                <attribute name="OrderList" type="IDREFS" />  
            </complexType>  
 </schema>'  
go  
declare @x xml(SC)  
set @x='<CustOrders:Customers xmlns:CustOrders="Customers">  
                <Customer CustomerID="C1" OrderList="OrderA OrderB"  >  
                              <spouse>Jenny</spouse>  
                                <Order OrderID="OrderA"><OrderValue>11</OrderValue></Order>  
                                <Order OrderID="OrderB"><OrderValue>22</OrderValue></Order>  
  
                </Customer>  
                <Customer CustomerID="C2" OrderList="OrderC OrderD" >  
                                <spouse>John</spouse>  
                                <Order OrderID="OrderC"><OrderValue>33</OrderValue></Order>  
                                <Order OrderID="OrderD"><OrderValue>44</OrderValue></Order>  
  
                        </Customer>  
                <Customer CustomerID="C3"  OrderList="OrderE OrderF" >  
                                <spouse>Jane</spouse>  
                                <Order OrderID="OrderE"><OrderValue>55</OrderValue></Order>  
                                <Order OrderID="OrderF"><OrderValue>55</OrderValue></Order>  
                </Customer>  
                <Customer CustomerID="C4"  OrderList="OrderG"  >  
                                <spouse>Tim</spouse>  
                                <Order OrderID="OrderG"><OrderValue>66</OrderValue></Order>  
                        </Customer>  
                <Customer CustomerID="C5"  >  
                </Customer>  
                <Customer CustomerID="C6" >  
                </Customer>  
                <Customer CustomerID="C7"  >  
                </Customer>  
</CustOrders:Customers>'  
  
select @x.query(' declare namespace CustOrders="Customers";   
 data(CustOrders:Customers/Customer[1]/@OrderList)[1] instance of xs:IDREF ? ') as XML_result  
```  
  
### <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   Os tipos de sequência **esquema-elemento ()** e **esquema-atributo ()** não têm suporte para comparação com `instance of` o operador.  
  
-   Sequências completas, por exemplo, `(1,2) instance of xs:integer*`, não têm suporte.  
  
-   Quando você está usando uma forma do tipo de sequência **Element ()** que especifica um nome de tipo, como `element(ElementName, TypeName)`, o tipo deve ser qualificado com um ponto de interrogação (?). Por exemplo, `element(Title, xs:string?)` indica que o elemento pode ser nulo. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]não oferece suporte à detecção de tempo de execução da propriedade **xsi: nil** usando `instance of`.  
  
-   Se o valor na `Expression` vier de um elemento ou atributo digitado como uma união, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode identificar só o tipo primitivo, não derivado, do qual o tipo do valor foi derivado. Por exemplo, se <`e1`> for definido para ter um tipo estático de (xs: integer | xs: String), o seguinte retornará false.  
  
    ```  
    data(<e1>123</e1>) instance of xs:integer  
    ```  
  
     Porém, `data(<e1>123</e1>) instance of xs:decimal` retornará True.  
  
-   Para os tipos de sequência **process-instruction ()** e **document-node ()** , somente formulários sem argumentos são permitidos. Por exemplo, `processing-instruction()` é permitido, mas `processing-instruction('abc')` não é permitido.  
  
## <a name="cast-as-operator"></a>Operador cast as  
 A expressão **Cast** as pode ser usada para converter um valor em um tipo de dados específico. Por exemplo:  
  
```  
  
Expression cast as  AtomicType?  
```  
  
 Em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], o ponto de interrogação (?) é requerido depois do `AtomicType`. Por exemplo, conforme mostrado na consulta a seguir, `"2" cast as xs:integer?` converte o valor da cadeia de caracteres em um número inteiro:  
  
```  
declare @x xml  
set @x=''  
select @x.query('"2" cast as xs:integer?')  
```  
  
 Na consulta a seguir, **Data ()** retorna o valor tipado do atributo ProductModelID, um tipo de cadeia de caracteres. O `cast as`operador converte o valor para xs: Integer.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD)  
SELECT CatalogDescription.query('  
   data(/PD:ProductDescription[1]/@ProductModelID) cast as xs:integer?  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 O uso explícito de **dados ()** não é necessário nesta consulta. A expressão `cast as` executa atomização implícita na expressão de entrada.  
  
### <a name="constructor-functions"></a>Funções de construtor  
 Você pode usar as funções de construtor de tipo atômico. Por exemplo, em vez de usar `cast as` o operador `"2" cast as xs:integer?`,, você pode usar a função de construtor **xs: Integer ()** , como no exemplo a seguir:  
  
```  
declare @x xml  
set @x=''  
select @x.query('xs:integer("2")')  
```  
  
 O exemplo a seguir retorna um valor xs:date igual a 2000-01-01Z.  
  
```  
declare @x xml  
set @x=''  
select @x.query('xs:date("2000-01-01Z")')  
```  
  
 Você também pode usar construtores para os tipos atômicos definidos pelo usuário. Por exemplo, se a coleção de esquema XML associada ao tipo de dados XML definir um tipo simples, um construtor **com MyType ()** poderá ser usado para retornar um valor desse tipo.  
  
#### <a name="implementation-limitations"></a>Limitações de implementação  
  
-   Não há suporte para as expressões XQuery **typeswitch**, **castable**e **Treat** .  
  
-   **cast as** requer um ponto de interrogação (?) após o tipo atômico.  
  
-   Não há suporte para **xs: QName** como um tipo para conversão. Em vez disso, use o **QName expandido** .  
  
-   **xs: Date**, **xs: time**e **xs: DateTime** exigem um fuso horário, que é indicado por um Z.  
  
     A consulta a seguir falha, pois o fuso horário não é especificado.  
  
    ```  
    DECLARE @var XML  
    SET @var = ''  
    SELECT @var.query(' <a>{xs:date("2002-05-25")}</a>')  
    go  
    ```  
  
     Ao adicionar o indicador de fuso horário Z ao valor, a consulta funcionará.  
  
    ```  
    DECLARE @var XML  
    SET @var = ''  
    SELECT @var.query(' <a>{xs:date("2002-05-25Z")}</a>')  
    go  
    ```  
  
     Este é o resultado:  
  
    ```  
    <a>2002-05-25Z</a>  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões XQuery](../xquery/xquery-expressions.md)   
 [Digite System &#40;XQuery&#41;](../xquery/type-system-xquery.md)  
  
  
