---
title: Construção XML (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- white space [XQuery]
- computed constructor
- construct XML structures [XQuery]
- constructors [XQuery]
- prolog
- direct constructor [SQL Server]
- XML [SQL Server], construction
- XQuery, XML construction
ms.assetid: a6330b74-4e52-42a4-91ca-3f440b3223cf
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5861d48490df31e731113b673972a7768867a5ab
ms.sourcegitcommit: 08b3de02475314c07a82a88c77926d226098e23f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49119894"
---
# <a name="xml-construction-xquery"></a>Construção XML (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  No XQuery, você pode usar o **direto** e **computado** construtores para construir estruturas XML dentro de uma consulta.  
  
> [!NOTE]  
>  Não há nenhuma diferença entre o **direto** e **computado** construtores.  
  
## <a name="using-direct-constructors"></a>Usando construtores diretos  
 Ao usar construtores diretos, você especifica a sintaxe semelhante a XML ao construir o XML. Os exemplos a seguir ilustram a construção XML pelos construtores diretos.  
  
### <a name="constructing-elements"></a>Construindo elementos  
 Usando notações de XML, é possível construir elementos. O exemplo a seguir usa a expressão do construtor de elemento direto e cria um \<ProductModel > elemento. O elemento construído tem três elementos filho  
  
-   Um nó de texto.  
  
-   Dois nós de elemento \<Summary > e \<recursos >.  
  
    -   O \<resumo > elemento tem um nó de texto filho cujo valor é "Some description".  
  
    -   O \<recursos > elemento tem três filhos do nó de elemento, \<Color >, \<peso >, e \<garantia >. Cada um desses nós tem um nó de texto filho e os valores Red, 25, 2 years parts and labor, respectivamente.  
  
```sql
declare @x xml;  
set @x='';  
select @x.query('<ProductModel ProductModelID="111">;  
This is product model catalog description.  
<Summary>Some description</Summary>  
<Features>  
  <Color>Red</Color>  
  <Weight>25</Weight>  
  <Warranty>2 years parts and labor</Warranty>  
</Features></ProductModel>')  
  
```  
  
 Este é o XML resultante:  
  
```xml
<ProductModel ProductModelID="111">  
  This is product model catalog description.  
  <Summary>Some description</Summary>  
  <Features>  
    <Color>Red</Color>  
    <Weight>25</Weight>  
    <Warranty>2 years parts and labor</Warranty>  
  </Features>  
</ProductModel>  
```  
  
 Embora seja útil construir elementos de expressões constantes, como mostrado neste exemplo, o verdadeiro poder desse recurso de linguagem do XQuery é a capacidade de construir XML capaz de extrair dinamicamente dados de um banco de dados. Você pode usar chaves para especificar expressões de consulta. No XML resultante, a expressão é substituída por seu valor. Por exemplo, a consulta a seguir constrói um elemento <`NewRoot`> com um elemento filho (<`e`>). O valor do elemento <`e`> é computado pela especificação de uma expressão de caminho entre chaves ({..." }").  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
SELECT @x.query('<NewRoot><e> { /root } </e></NewRoot>');  
```  
  
 As chaves agem como tokens de troca de contexto e alternam a consulta da construção XML para avaliação de consulta. Nesse caso, a expressão de caminho XQuery dentro das chaves, `/root`, é avaliada e os resultados são substituídos por ela.  
  
 Este é o resultado:  
  
```xml
<NewRoot>  
  <e>  
    <root>5</root>  
  </e>  
</NewRoot>  
```  
  
 A consulta a seguir é semelhante à anterior. No entanto, a expressão entre chaves Especifica a **Data ()** função para recuperar o valor atômico da <`root`> elemento e o atribui ao elemento construído, <`e`>.  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('  
                           <NewRoot>  
                             <e> { data(/root) } </e>  
                           </NewRoot>' ));  
SELECT @y;  
```  
  
 Este é o resultado:  
  
```xml
<NewRoot>  
  <e>5</e>  
</NewRoot>  
```  
  
 Para usar as chaves como parte do texto em vez de tokens de troca de contexto, é possível não utilizá-las como "\} \} " ou "\{\{", como mostrado neste exemplo:  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('  
<NewRoot> Hello, I can use {{ and  }} as part of my text</NewRoot>'));  
SELECT @y;  
```  
  
 Este é o resultado:  
  
```xml
<NewRoot> Hello, I can use { and  } as part of my text</NewRoot>  
```  
  
 A consulta a seguir é outro exemplo de construção de elementos com o uso do construtor de elemento direto. Além disso, o valor do elemento <`FirstLocation`> é obtido pela execução da expressão entre chaves. A expressão de consulta retorna as etapas de fabricação no primeiro local de centro de trabalho da coluna Instructions da tabela Production.ProductModel.  
  
```sql
SELECT Instructions.query('  
    declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        <FirstLocation>  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 Este é o resultado:  
  
```xml
<FirstLocation>  
  <AWMI:step xmlns:AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">  
      Insert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>.   
  </AWMI:step>  
  <AWMI:step xmlns:AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">  
      Attach <AWMI:tool>Trim Jig TJ-26</AWMI:tool> to the upper and lower right corners of the aluminum sheet.   
  </AWMI:step>  
   ...  
</FirstLocation>  
```  
  
#### <a name="element-content-in-xml-construction"></a>Conteúdo de elemento na construção XML  
 O exemplo a seguir ilustra o comportamento das expressões na construção do conteúdo de elemento com o uso do construtor de elemento direto. No exemplo a seguir, o construtor de elemento direto especifica uma expressão. Para essa expressão, um nó de texto é criado no XML resultante.  
  
```sql
declare @x xml;  
set @x='  
<root>  
  <step>This is step 1</step>  
  <step>This is step 2</step>  
  <step>This is step 3</step>  
</root>';  
select @x.query('  
<result>  
 { for $i in /root[1]/step  
    return string($i)  
 }  
</result>');  
  
```  
  
 A sequência de valor atômico resultante da avaliação de expressão é adicionada ao nó de texto com um espaço adicionado entre os valores atômicos adjacentes, como mostrado no resultado. O elemento construído tem um filho. Ele é um nó de texto que contém o valor mostrado no resultado.  
  
```xml
<result>This is step 1 This is step 2 This is step 3</result>  
```  
  
 Em vez de uma expressão, se você especificar três expressões separadas que geram três nós de texto, os nós de texto adjacentes serão mesclados em um único nó de texto, por meio de concatenação, no XML resultante.  
  
```sql
declare @x xml;  
set @x='  
<root>  
  <step>This is step 1</step>  
  <step>This is step 2</step>  
  <step>This is step 3</step>  
</root>';  
select @x.query('  
<result>  
 { string(/root[1]/step[1]) }  
 { string(/root[1]/step[2]) }  
 { string(/root[1]/step[3]) }  
</result>');  
```  
  
 O nó de elemento construído tem um filho. Ele é um nó de texto que contém o valor mostrado no resultado.  
  
```xml
<result>This is step 1This is step 2This is step 3</result>  
```  
  
### <a name="constructing-attributes"></a>Construindo atributos  
 Ao construir elementos usando o construtor de elemento direto, também é possível especificar atributos do elemento usando sintaxe similar a XML, como mostrado neste exemplo:  
  
```sql
declare @x xml;  
set @x='';  
select @x.query('<ProductModel ProductModelID="111">;  
This is product model catalog description.  
<Summary>Some description</Summary>  
</ProductModel>')  
```  
  
 Este é o XML resultante:  
  
```xml
<ProductModel ProductModelID="111">  
  This is product model catalog description.  
  <Summary>Some description</Summary>  
</ProductModel>  
```  
  
 O elemento <`ProductModel`> construído tem um atributo ProductModelID e estes nós filho:  
  
-   Um nó de texto, `This is product model catalog description.`  
  
-   Um nó de elemento, <`Summary`>. Esse nó tem um filho de nó de texto, `Some description`.  
  
 Ao construir um atributo, é possível especificar seu valor com uma expressão entre chaves. Nesse caso, o resultado da expressão é retornado como o valor de atributo.  
  
 No exemplo a seguir, o **Data ()** função não é estritamente necessária. Como você está atribuindo o valor da expressão a um atributo **Data ()** é aplicado implicitamente para recuperar o valor digitado da expressão especificada.  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('<NewRoot attr="{ data(/root) }" ></NewRoot>'));  
SELECT @y;  
```  
  
 Este é o resultado:  
  
```xml
<NewRoot attr="5" />  
```  
  
 A seguir, um outro exemplo no qual são especificadas expressões para a construção de atributo LocationID e SetupHrs. Essas expressões são avaliadas com base no XML na coluna Instruction. O valor digitado da expressão é atribuído aos atributos.  
  
```sql
SELECT Instructions.query('  
    declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        <FirstLocation   
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7;  
```  
  
 Este é o resultado parcial:  
  
```xml
<FirstLocation LocationID="10" SetupHours="0.5" >  
  <AWMI:step …   
  </AWMI:step>  
  ...  
</FirstLocation>  
```  
  
#### <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   Não há suporte a expressões de atributo múltiplas ou mistas (cadeia de caracteres e expressão XQuery). Por exemplo, como mostrado na consulta a seguir, você constrói um XML em que `Item` é uma constante e o valor `5` é obtido avaliando uma expressão de consulta:  
  
    ```xml
    <a attr="Item 5" />  
    ```  
  
     A consulta a seguir retorna um erro, pois você está misturando cadeia de caracteres constante com uma expressão ({/x}) e não há suporte para isso:  
  
    ```sql
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    SELECT @x.query( '<a attr="Item {/x}"/>' )   
    ```  
  
     Nesse caso, você tem as seguintes opções:  
  
    -   Forme o valor de atributo pela concatenação de dois valores atômicos. Esses valores atômicos são serializados no valor de atributo com um espaço entre os valores atômicos:  
  
        ```sql
        SELECT @x.query( '<a attr="{''Item'', data(/x)}"/>' )   
        ```  
  
         Este é o resultado:  
  
        ```xml
        <a attr="Item 5" />  
        ```  
  
    -   Use o [função concat](../xquery/functions-on-string-values-concat.md) para concatenar os argumentos de cadeia de caracteres de dois em valor de atributo resultante:  
  
        ```sql
        SELECT @x.query( '<a attr="{concat(''Item'', /x[1])}"/>' )   
        ```  
  
         Nesse caso, não há espaço adicionado entre os dois valores de cadeia de caracteres. Se quiser um espaço entre os dois valores, insira-o explicitamente.  
  
         Este é o resultado:  
  
        ```xml
        <a attr="Item5" />  
        ```  
  
-   Não há suporte para expressões múltiplas como um valor de atributo. Por exemplo, a consulta a seguir retorna um erro:  
  
    ```sql
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    SELECT @x.query( '<a attr="{/x}{/x}"/>' )  
    ```  
  
-   Não há suporte para sequências heterogêneas. Qualquer tentativa para atribuir uma sequência heterogênea como um valor de atributo retornará um erro, como mostrado no exemplo a seguir. Neste exemplo, uma sequência heterogênea - um "Item" de cadeia de caracteres e um elemento <`x`> - é especificada como o valor de atributo:  
  
    ```sql
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    select @x.query( '<a attr="{''Item'', /x }" />')  
    ```  
  
     Se você aplicar a **Data ()** função, a consulta funcionará, pois ele recupera o valor atômico da expressão, `/x`, que é concatenado com a cadeia de caracteres. Apresentamos a seguir uma sequência de valores atômicos:  
  
    ```sql
    SELECT @x.query( '<a attr="{''Item'', data(/x)}"/>' )   
    ```  
  
     Este é o resultado:  
  
    ```xml
    <a attr="Item 5" />  
    ```  
  
-   A ordem de nó do atributo é aplicada durante a serialização e não durante a verificação de tipo estático. Por exemplo, a consulta a seguir falha, pois tenta adicionar um atributo depois de um nó sem-atributo.  
  
    ```sql
    select convert(xml, '').query('  
    element x { attribute att { "pass" }, element y { "Element text" }, attribute att2 { "fail" } }  
    ')  
    go  
    ```  
  
     A consulta anterior retorna o seguinte erro:  
  
    ```  
    XML well-formedness check: Attribute cannot appear outside of element declaration. Rewrite your XQuery so it returns well-formed XML.  
    ```  
  
### <a name="adding-namespaces"></a>Adicionando namespaces  
 Ao construir XML usando os construtores diretos, o elemento construído e os nomes de atributo podem ser qualificados com o uso de um prefixo de namespace. É possível associar o prefixo ao namespace das seguintes formas:  
  
-   Usando um atributo de declaração de namespace.  
  
-   Usando a cláusula WITH XMLNAMESPACES.  
  
-   No prólogo do XQuery.  
  
#### <a name="using-a-namespace-declaration-attribute-to-add-namespaces"></a>Usando um atributo de declaração de namespace para adicionar namespaces  
 O exemplo a seguir usa um atributo de declaração de namespace na construção do elemento <`a`> para declarar um namespace padrão. A construção do elemento filho <`b`> desfaz a declaração do namespace padrão declarada no elemento pai.  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <a xmlns="a">  
    <b xmlns=""/>  
  </a>' )   
```  
  
 Este é o resultado:  
  
```xml
<a xmlns="a">  
  <b xmlns="" />  
</a>  
```  
  
 É possível atribuir um prefixo ao namespace. O prefixo é especificado na construção do elemento <`a`>.  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <x:a xmlns:x="a">  
    <b/>  
  </x:a>' )  
```  
  
 Este é o resultado:  
  
```xml
<x:a xmlns:x="a">  
  <b />  
</x:a>  
```  
  
 É possível desfazer a declaração de um namespace padrão na construção XML, mas não desfazer a declaração de um prefixo de namespace. A consulta a seguir retorna um erro, pois não é possível desfazer a declaração de um prefixo especificado na construção do elemento <`b`>.  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <x:a xmlns:x="a">  
    <b xmlns:x=""/>  
  </x:a>' )  
```  
  
 O namespace recentemente construído está disponível para uso na consulta. Por exemplo, a consulta a seguir declara um namespace na construção do elemento, <`FirstLocation`>, bem como especifica o prefixo nas expressões para obter os valores de atributo LocationID e SetupHrs.  
  
```sql
SELECT Instructions.query('  
        <FirstLocation xmlns:AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
 Observe que a criação de um novo prefixo de namespace desse modo substituirá qualquer declaração preexistente de namespace desse prefixo. Por exemplo, a declaração de namespace, `AWMI="http://someURI"`, no prólogo de consulta é anulada pela declaração de namespace no elemento <`FirstLocation`>.  
  
```sql
SELECT Instructions.query('  
declare namespace AWMI="http://someURI";  
        <FirstLocation xmlns:AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
#### <a name="using-a-prolog-to-add-namespaces"></a>Usando um prólogo para adicionar namespaces  
 Este exemplo ilustra como podem ser adicionados namespaces ao XML construído. Um namespace padrão é declarado no prólogo de consulta.  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
           declare default element namespace "a";  
            <a><b xmlns=""/></a>' )  
```  
  
 Observe que na construção do elemento <`b`>, o atributo de declaração de namespace é especificado com uma cadeia de caracteres vazia como seu valor. Isso desfaz a declaração do namespace padrão declarado no pai.  
  

Este é o resultado:  

```xml
<a xmlns="a">  
  <b xmlns="" />  
</a>  
```  
  
### <a name="xml-construction-and-white-space-handling"></a>Tratamento de espaços em branco e construção XML  
 O conteúdo de elemento na construção XML pode incluir caracteres de espaço em branco. Esses caracteres são tratados das seguintes formas:  
  
-   Os caracteres de espaço em branco em namespace URIs são tratados como o tipo XSD **anyURI**. Especificamente, eles são tratados da seguinte forma:  
  
    -   Qualquer caractere com espaço em branco no início e término é eliminado.  
  
    -   Os valores de caractere com espaço em branco são reduzidos para um único espaço.  
  
-   Os caracteres de avanço de linha no conteúdo de atributo são substituídos por espaços. Todos os outros caracteres com espaço em branco permanecem inalterados.  
  
-   O espaço em branco nos elementos é preservado.  
  
 O exemplo a seguir ilustra o tratamento de espaço em branco na construção XML:  
  
```sql
-- line feed is repaced by space.  
declare @x xml  
set @x=''  
select @x.query('  
  
declare namespace myNS="   http://       
 abc/  
xyz  
  
";  
<test attr="    my   
test   attr   
value    " >  
  
<a>  
  
This     is  a  
  
test  
  
</a>  
</test>  
') as XML_Result  
  
```  
  
 Este é o resultado:  
  
```xml
-- result  
<test attr="<test attr="    my test   attr  value    "><a>  
  
This     is  a  
  
test  
  
</a></test>  
"><a>  
  
This     is  a  
  
test  
  
</a></test>  
```  
  
### <a name="other-direct-xml-constructors"></a>Outros construtores XML diretos  
 Os construtores de processamento de instruções e comentários XML usam a mesma sintaxe do construtor XML correspondente. Também há suporte para construtores computados para nós de texto, mas eles são usados principalmente em XML DML para construir nós de texto.  
  
 **Observação** para obter um exemplo de como usar um construtor de nó de texto explícito, consulte o exemplo específico na [insert &#40;XML DML&#41;](../t-sql/xml/insert-xml-dml.md).  
  
 Na consulta a seguir, o XML construído inclui um elemento, dois atributos, um comentário e uma instrução de processamento. Observe que uma vírgula é usada antes de <`FirstLocation`>, pois uma sequência está sendo construída.  
  
```sql
SELECT Instructions.query('  
  declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   <?myProcessingInstr abc="value" ?>,   
   <FirstLocation   
        WorkCtrID = "{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
        SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
       <!-- some comment -->  
       <?myPI some processing instructions ?>  
       { (/AWMI:root/AWMI:Location[1]/AWMI:step) }  
    </FirstLocation>   
') as Result   
FROM Production.ProductModel  
where ProductModelID=7;  
  
```  
  
 Este é o resultado parcial:  
  
```xml
<?myProcessingInstr abc="value" ?>  
<FirstLocation WorkCtrID="10" SetupHrs="0.5">  
  <!-- some comment -->  
  <?myPI some processing instructions ?>  
  <AWMI:step xmlns:AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">I  
  nsert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>.   
  </AWMI:step>  
    ...  
</FirstLocation>  
  
```  
  
## <a name="using-computed-constructors"></a>Usando construtores computados  
 para obter informações sobre a ferramenta de configuração e recursos adicionais. Nesse caso, especifique as palavras-chave que identificam o tipo de nó que você deseja construir. São suportadas apenas as seguintes palavras-chave:  
  
-   elemento  
  
-   atributo  
  
-   text  
  
 Para elemento e nós de atributo, essas palavras-chave são seguidas pelo nome de nó e também pela expressão, entre chaves, que gera o conteúdo para esse nó. No exemplo a seguir, você está construindo este XML:  
  
```xml
<root>  
  <ProductModel PID="5">Some text <summary>Some Summary</summary></ProductModel>  
</root>  
```  
  
 Esta é a consulta que usa construtores computados para gerar o XML:  
  
```sql
declare @x xml  
set @x=''  
select @x.query('element root   
               {   
                  element ProductModel  
     {  
attribute PID { 5 },  
text{"Some text "},  
    element summary { "Some Summary" }  
 }  
               } ')  
  
```  
  
 A expressão que gera o conteúdo de nó pode especificar uma expressão de consulta.  
  
```sql
declare @x xml  
set @x='<a attr="5"><b>some summary</b></a>'  
select @x.query('element root   
               {   
                  element ProductModel  
     {  
attribute PID { /a/@attr },  
text{"Some text "},  
    element summary { /a/b }  
 }  
               } ')  
```  
  
 Observe que o elemento computado e os construtores de atributo, como definidos na especificação de XQuery, permitem computar os nomes de nó. Ao usar construtores diretos no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], os nomes de nó, como elemento e atributo, deverão ser especificados como literais constantes. Portanto, não há diferença entre construtores diretos e construtores computados para elementos e atributos.  
  
 No exemplo a seguir, o conteúdo para os nós construídos é obtido de instruções de fabricação de XML armazenadas na coluna Instructions do **xml** tipo de dados na tabela ProductModel.  
  
```sql
SELECT Instructions.query('  
  declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   element FirstLocation   
     {  
        attribute LocationID { (/AWMI:root/AWMI:Location[1]/@LocationID)[1] },  
        element   AllTheSteps { /AWMI:root/AWMI:Location[1]/AWMI:step }  
     }  
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
 Este é o resultado parcial:  
  
```xml
<FirstLocation LocationID="10">  
  <AllTheSteps>  
    <AWMI:step> ... </AWMI:step>  
    <AWMI:step> ... </AWMI:step>  
    ...  
  </AllTheSteps>  
</FirstLocation>    
```  
  
## <a name="additional-implementation-limitations"></a>Limitações adicionais de implementação  
 Não podem ser usados construtores de atributo computados para declarar um novo namespace. Além disso, não há suporte no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para os seguintes construtores computados:  
  
-   Construtores de nó de documento computados  
  
-   Construtores de instrução de processamento computados  
  
-   Construtores de comentário computados  
  
## <a name="see-also"></a>Consulte também  
 [Expressões XQuery](../xquery/xquery-expressions.md)  
  
  
