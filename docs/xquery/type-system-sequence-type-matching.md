---
title: Correspondência de tipo de sequência | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sequence type matching [XQuery]
- XQuery, sequence type matching
ms.assetid: 8c56fb69-ca04-4aba-b55a-64ae216c492d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b6850f15718cb810b5428f75980983fc4a8a0a88
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2019
ms.locfileid: "54255241"
---
# <a name="type-system---sequence-type-matching"></a>Sistema de Tipos – Correspondência de Tipo de Sequência
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Um valor de expressão do XQuery sempre é uma sequência de zero ou mais itens. Um item pode ser tanto um valor atômico quanto um nó. O tipo de sequência se refere à habilidade de associar o tipo de sequência retornada por uma expressão de consulta com um tipo específico. Por exemplo:  
  
-   Se o valor de expressão for atômico, você poderá querer saber se ela é um número inteiro, decimal ou tipo de cadeia de caracteres.  
  
-   Se o valor de expressão for um nó XML, você poderá querer saber se é um nó de comentário, um nó de instrução de processamento ou um nó de texto.  
  
-   Você pode querer saber se a expressão retorna um elemento XML ou um nó de atributo de um nome e tipo específicos.  
  
 Você pode usar o operador Booliano `instance of` na correspondência do tipo de sequência. Para obter mais informações sobre o `instance of` expressão, consulte [expressões SequenceType &#40;XQuery&#41;](../xquery/sequencetype-expressions-xquery.md).  
  
## <a name="comparing-the-atomic-value-type-returned-by-an-expression"></a>Comparando o tipo do valor atômico retornado por uma expressão  
 Se uma expressão retornar uma sequência de valores atômicos, você terá que achar o tipo do valor na sequência. Os exemplos a seguir ilustram como o tipo da sintaxe de sequência pode ser usado para avaliar o tipo de valor atômico retornado por uma expressão.  
  
### <a name="example-determining-whether-a-sequence-is-empty"></a>Exemplo: Determinando se uma sequência está vazia  
 O **Empty ()** tipo de sequência pode ser usado em uma expressão de tipo de sequência para determinar se a sequência retornada pela expressão especificada é uma sequência vazia.  
  
 No exemplo a seguir, o esquema XML permite que o elemento <`root`> seja anulado:  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" nillable="true" type="byte"/>  
</schema>'  
GO  
```  
  
 Agora, se uma instância XML digitada especificar um valor para o elemento <`root`>, `instance of empty()` retornará False.  
  
```  
DECLARE @var XML(SC1)  
SET @var = '<root>1</root>'  
-- The following returns False  
SELECT @var.query('data(/root[1]) instance of  empty() ')  
GO  
```  
  
 Se o elemento <`root`> for anulado na instância, seu valor será uma sequência vazia, e `instance of empty()` retornará True.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" />'  
SELECT @var.query('data(/root[1]) instance of  empty() ')  
GO  
```  
  
### <a name="example-determining-the-type-of-an-attribute-value"></a>Exemplo: Determinando o tipo de um valor de atributo  
 Às vezes, você pode querer avaliar o tipo de sequência retornado por uma expressão antes do processamento. Por exemplo, você pode ter um esquema XML em que um nó está definido como um tipo de união. No exemplo seguinte, o esquema XML na coleção define o atributo `a` como um tipo de união cujo valor pode ser decimal ou um tipo de cadeia de caracteres.  
  
```  
-- Drop schema collection if it exists.  
-- DROP XML SCHEMA COLLECTION SC.  
-- GO  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
  <element name="root">  
    <complexType>  
       <sequence/>  
         <attribute name="a">  
            <simpleType>  
               <union memberTypes="decimal string"/>  
            </simpleType>  
         </attribute>  
     </complexType>  
  </element>  
</schema>'  
GO  
```  
  
 Antes de processar uma instância XML digitada, você pode querer saber o tipo do valor do atributo `a`. No exemplo seguinte, o valor do atributo `a` é um tipo decimal. Portanto, `, instance of xs:decimal` retorna True.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root a="2.5"/>'  
SELECT @var.query('data((/root/@a)[1]) instance of xs:decimal')  
GO  
```  
  
 Agora, altere o valor do atributo `a` para um tipo de cadeia de caracteres. O `instance of xs:string` retornará True.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root a="Hello"/>'  
SELECT @var.query('data((/root/@a)[1]) instance of xs:string')  
GO  
```  
  
### <a name="example-cardinality-in-sequence-expressions"></a>Exemplo: Cardinalidade em expressões de sequência  
 Este exemplo ilustra o efeito da cardinalidade em uma expressão de sequência. O esquema XML a seguir define um elemento <`root`> que é de tipo de byte e é anulável.  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" nillable="true" type="byte"/>  
</schema>'  
GO  
```  
  
 Na consulta a seguir, em razão de a expressão retornar um singleton de tipo de byte, `instance of` retorna True.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root>111</root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte ')   
GO  
```  
  
 Se você tornar o elemento <`root`> nulo, seu valor será uma sequência vazia. Quer dizer, a expressão `/root[1]` retorna uma sequência vazia. Portanto, `instance of xs:byte` retorna False. Observe que a cardinalidade nesse caso é 1.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"></root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte ')   
GO  
-- result = false  
```  
  
 Se você especificar a cardinalidade adicionando o indicador de ocorrência (`?`), a expressão de sequência retornará True.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"></root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte? ')   
GO  
-- result = true  
```  
  
 Observe que o teste em uma expressão de tipo de sequência é completado em duas fases:  
  
1.  Primeiro, o teste determina se o tipo de expressão corresponde ao tipo especificado.  
  
2.  Em caso afirmativo, o teste determinará então se o número de itens retornados pela expressão corresponde ao indicador de ocorrência especificado.  
  
 Se ambos forem verdadeiros, a expressão `instance of` retornará True.  
  
### <a name="example-querying-against-an-xml-type-column"></a>Exemplo: Consulta em relação a uma coluna de tipo xml  
 No exemplo a seguir, uma consulta é especificada em uma coluna de instruções do **xml** digite o [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] banco de dados. É uma coluna XML digitada porque tem um esquema associado a ela. O esquema XML define o atributo `LocationID` do tipo inteiro. Portanto, na expressão de sequência, o `instance of xs:integer?` retorna True.  
  
```  
SELECT Instructions.query('   
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
data(/AWMI:root[1]/AWMI:Location[1]/@LocationID) instance of xs:integer?') as Result   
FROM Production.ProductModel   
WHERE ProductModelID = 7  
```  
  
## <a name="comparing-the-node-type-returned-by-an-expression"></a>Comparando o tipo do nó retornado por uma expressão  
 Se uma expressão retornar uma sequência de nós, você terá de localizar o tipo do nó na sequência. Os exemplos a seguir ilustram como o tipo da sintaxe de sequência pode ser usado para avaliar o tipo de nó retornado por uma expressão. Você pode usar os seguintes tipos de sequência:  
  
-   **item()** -corresponde a qualquer item na sequência.  
  
-   **node ()** -determina se a sequência é um nó.  
  
-   **Instruction ()** -determina se a expressão retorna uma instrução de processamento.  
  
-   **Comment** -determina se a expressão retorna um comentário.  
  
-   **Document-Node()** -determina se a expressão retorna um nó de documento.  
  
 O exemplo a seguir ilustra esses tipos de sequência.  
  
### <a name="example-using-sequence-types"></a>Exemplo: Usando tipos de sequência  
 Neste exemplo, são executadas várias consultas em uma variável XML não digitada. Essas consultas ilustram o uso dos tipos de sequência.  
  
```  
DECLARE @var XML  
SET @var = '<?xml-stylesheet href="someValue" type="text/xsl" ?>  
<root>text node  
  <!-- comment 1 -->   
  <a>Data a</a>  
  <!-- comment  2 -->  
</root>'  
```  
  
 Na primeira consulta, a expressão retorna o valor digitado do elemento <`a`>. Na segunda consulta, a expressão retorna o elemento <`a`>. Ambos são itens. Portanto, ambas as consultas retornam True.  
  
```  
SELECT @var.query('data(/root[1]/a[1]) instance of item()')  
SELECT @var.query('/root[1]/a[1] instance of item()')  
```  
  
 Todas as expressões XQuery nas três consultas a seguir retornam o nó do elemento do filho do elemento <`root`>. Portanto, a expressão do tipo de sequência, `instance of node()`, retorna True, e as outras duas expressões, `instance of text()` e `instance of document-node()`, retornam False.  
  
```  
SELECT @var.query('(/root/*)[1] instance of node()')  
SELECT @var.query('(/root/*)[1] instance of text()')  
SELECT @var.query('(/root/*)[1] instance of document-node()')   
```  
  
 Na consulta a seguir, a expressão `instance of document-node()` retorna True, pois o pai do elemento <`root`> é um nó de elemento.  
  
```  
SELECT @var.query('(/root/..)[1] instance of document-node()') -- true  
```  
  
 Na consulta a seguir, a expressão recupera o primeiro nó da instância XML. Por ser um nó de instrução de processamento e expressão `instance of processing-instruction()` retorna True.  
  
```  
SELECT @var.query('(/node())[1] instance of processing-instruction()')  
```  
  
### <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações específicas:  
  
-   **Document-Node()** com tipo de conteúdo sintaxe não tem suporte.  
  
-   **processing-instruction(Name)** sintaxe não tem suporte.  
  
## <a name="element-tests"></a>Testes de elemento  
 Um teste de elemento é usado para corresponder o nó de elemento retornado por uma expressão com um nó de elemento com um nome e tipo específicos. Você pode usar estes testes de elemento:  
  
```  
element ()  
element(ElementName)  
element(ElementName, ElementType?)   
element(*, ElementType?)  
```  
  
## <a name="attribute-tests"></a>Testes de atributo  
 O teste de atributo determina se o atributo retornado por uma expressão é um nó de atributo. Você pode usar estes testes de atributo:  
  
 `attribute()`  
  
 `attribute(AttributeName)`  
  
 `attribute(AttributeName, AttributeType)`  
  
## <a name="test-examples"></a>Exemplos de teste  
 Os exemplos a seguir ilustram cenários em que os testes de elemento e de atributo são úteis.  
  
### <a name="example-a"></a>Exemplo A  
 O esquema XML a seguir define o tipo complexo `CustomerType` em que os elementos <`firstName`> e <`lastName`> são opcionais. Para uma instância XML especificada, você pode ter que determinar se o nome de um cliente específico existe.  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
targetNamespace="myNS" xmlns:ns="myNS">  
  <complexType name="CustomerType">  
     <sequence>  
        <element name="firstName" type="string" minOccurs="0"   
                  nillable="true" />  
        <element name="lastName" type="string" minOccurs="0"/>  
     </sequence>  
  </complexType>  
  <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
DECLARE @var XML(SC)  
SET @var = '<x:customer xmlns:x="myNS">  
<firstName>SomeFirstName</firstName>  
<lastName>SomeLastName</lastName>  
</x:customer>'  
```  
  
 A consulta a seguir usa uma expressão `instance of element (firstName)` para determinar se o primeiro elemento filho de <`customer`> é um elemento cujo nome é <`firstName`>. Nesse caso, ele retorna True.  
  
```  
SELECT @var.query('declare namespace x="myNS";   
     (/x:customer/*)[1] instance of element (firstName)')  
GO  
```  
  
 Se você remover o elemento <`firstName`> da instância, a consulta retornará False.  
  
 Você também pode usar o seguinte:  
  
-   A sintaxe de tipo de sequência `element(ElementName, ElementType?)`, como mostrado na consulta a seguir. Ela faz a correspondência de um nó de elemento anulado ou não anulado cujo nome é `firstName` e cujo tipo é `xs:string`.  
  
    ```  
    SELECT @var.query('declare namespace x="myNS";   
    (/x:customer/*)[1] instance of element (firstName, xs:string?)')  
    ```  
  
-   A sintaxe de tipo de sequência `element(*, type?)`, como mostrado na consulta a seguir. Ela fará a correspondência do nó de elemento se seu tipo for `xs:string`, independente de seu nome.  
  
    ```  
    SELECT @var.query('declare namespace x="myNS"; (/x:customer/*)[1] instance of element (*, xs:string?)')  
    GO  
    ```  
  
### <a name="example-b"></a>Exemplo B  
 O exemplo a seguir ilustra como determinar se o nó retornado por uma expressão é um nó de elemento com um nome específico. Ele usa o **Element ()** de teste.  
  
 No exemplo a seguir, os dois elementos <`Customer`> na instância XML que estão sendo consultados são de dois tipos diferentes: `SpecialCustomerType` e `CustomerType`. Supondo que você deseja saber o tipo do elemento <`Customer`> retornado pela expressão. A seguinte coleção de esquemas XML define os tipos `CustomerType` e `SpecialCustomerType`.  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
          targetNamespace="myNS"  xmlns:ns="myNS">  
  <complexType name="CustomerType">  
    <sequence>  
      <element name="firstName" type="string"/>  
      <element name="lastName" type="string"/>  
    </sequence>  
  </complexType>  
  <complexType name="SpecialCustomerType">  
     <complexContent>  
       <extension base="ns:CustomerType">  
        <sequence>  
            <element name="Age" type="int"/>  
        </sequence>  
       </extension>  
     </complexContent>  
    </complexType>  
   <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
```  
  
 Essa coleção de esquemas XML é usada para criar um tipado **xml** variável. A instância XML atribuída a essa variável tem dois elementos <`customer`> de dois tipos diferentes. O primeiro elemento é do tipo `CustomerType` e o segundo é do tipo `SpecialCustomerType`.  
  
```  
DECLARE @var XML(SC)  
SET @var = '  
<x:customer xmlns:x="myNS">  
   <firstName>FirstName1</firstName>  
   <lastName>LastName1</lastName>  
</x:customer>  
<x:customer xsi:type="x:SpecialCustomerType" xmlns:x="myNS" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
   <firstName> FirstName2</firstName>  
   <lastName> LastName2</lastName>  
   <Age>21</Age>  
</x:customer>'  
```  
  
 Na consulta a seguir, a expressão `instance of element (*, x:SpecialCustomerType ?)` retorna False, pois a expressão retorna o primeiro elemento de cliente que não é do tipo `SpecialCustomerType`.  
  
```  
SELECT @var.query('declare namespace x="myNS";   
    (/x:customer)[1] instance of element (*, x:SpecialCustomerType ?)')  
```  
  
 Se você alterar a expressão da consulta anterior e recuperar o segundo elemento <`customer`> (`instance of`), o `/x:customer)[2]` retornará True.  
  
### <a name="example-c"></a>Exemplo C  
 Este exemplo usa o teste de atributo. O esquema XML a seguir define o tipo complexo CustomerType com os atributos Customer ID e Age. O atributo Age é opcional. Para uma instância XML específica, você pode querer determinar se o atributo Age está presente no elemento <`customer`>.  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
       targetNamespace="myNS" xmlns:ns="myNS">  
<complexType name="CustomerType">  
  <sequence>  
     <element name="firstName" type="string" minOccurs="0"   
               nillable="true" />  
     <element name="lastName" type="string" minOccurs="0"/>  
  </sequence>  
  <attribute name="CustomerID" type="integer" use="required" />  
  <attribute name="Age" type="integer" use="optional" />  
 </complexType>  
 <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
```  
  
 A consulta a seguir retorna True, porque há um nó de atributo cujo nome é `Age` na instância XML que está sendo consultada. O teste de atributo `attribute(Age)` é usado nessa expressão. Em razão dos atributos não terem nenhuma ordem, a consulta usa a expressão FLWOR para recuperar todos os atributos e depois testar cada atributo usando a expressão `instance of`. O exemplo cria uma coleção de esquemas XML para criar um tipado **xml** variável.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<x:customer xmlns:x="myNS" CustomerID="1" Age="22" >  
<firstName>SomeFName</firstName>  
<lastName>SomeLName</lastName>  
</x:customer>'  
SELECT @var.query('declare namespace x="myNS";   
FOR $i in /x:customer/@*  
RETURN  
    IF ($i instance of attribute (Age)) THEN  
        "true"  
        ELSE  
        ()')     
GO  
  
```  
  
 Se você remover o atributo opcional `Age` da instância, a consulta anterior retornará False.  
  
 Você pode especificar o tipo e nome de atributo (`attribute(name,type)`) no teste de atributo.  
  
```  
SELECT @var.query('declare namespace x="myNS";   
FOR $i in /x:customer/@*  
RETURN  
    IF ($i instance of attribute (Age, xs:integer)) THEN  
        "true"  
        ELSE  
        ()')  
```  
  
 Como alternativa, você pode especificar o `attribute(*, type)` sintaxe de tipo de sequência. Isso corresponderá ao nó de atributo se o tipo de atributo corresponder ao tipo especificado, independente do nome.  
  
### <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações específicas:  
  
-   No teste de elemento, o nome do tipo deve ser seguido pelo indicador de ocorrência (**?**).  
  
-   **Element (ElementName, TypeName)** não tem suporte.  
  
-   **elemento (\*, TypeName)** não tem suporte.  
  
-   **Schema-Element()** não tem suporte.  
  
-   **Schema-Attribute(AttributeName)** não tem suporte.  
  
-   Consultando explicitamente **xsi: Type** ou **xsi: nil** não tem suporte.  
  
## <a name="see-also"></a>Consulte também  
 [Sistema de tipo &#40;XQuery&#41;](../xquery/type-system-xquery.md)  
  
  
