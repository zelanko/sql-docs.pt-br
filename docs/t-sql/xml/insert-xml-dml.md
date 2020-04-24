---
title: insert (XML DML) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- XML DML [SQL Server]
- inserting nodes
- insert keyword [XML DML]
- insert XML DML statement
ms.assetid: 0c95c2b3-5cc2-4c38-9e25-86493096c442
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 84f502edda64fef31acfad4747e669843602e4cb
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81632446"
---
# <a name="insert-xml-dml"></a>inserir (XML DML)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Insere um ou mais nós identificados por *Expression1* como nós filhos ou irmãos do nó identificado por *Expression2*.  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
  
insert   
      Expression1 (  
                 {as first | as last} into | after | before  
                                    Expression2  
                )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expression1*  
 Identifica um ou mais nós para inserir. Pode ser uma instância XML constante, uma referência a uma instância do tipo de dados XML tipada da mesma coleção de esquema XML em que o método modificado está sendo aplicado, uma instância do tipo de dados XML não tipada que usa a função autônoma **sql:column()** /**sql:variable()** ou uma expressão XQuery. A expressão pode resultar em um nó, e também um nó de texto, ou em uma sequência ordenada de nós. Não pode ser resolvida no nó de raiz (/). Se a expressão resultar em um valor ou sequência de valores, os valores serão inseridos como um único nó de texto com um espaço separando cada valor na sequência. Se você especificar vários nós como constantes, os nós serão incluídos em parênteses e separados por vírgulas. Não é possível inserir sequências heterogêneas como uma sequência de elementos, atributos ou valores. Se a *Expression1* for resolvida para uma sequência vazia, não ocorrerá nenhuma inserção e nenhum erro será retornado.  
  
 into  
 Os nós identificados por *Expression1* são inseridos como descendentes diretos (nós filhos) do nó identificado por *Expression2*. Se o nó em *Expression2* já tiver um ou mais nós filhos, será necessário usar **as first** ou **as last** para especificar onde você deseja que o novo nó seja adicionado. Por exemplo, no início ou no fim da lista de filhos, respectivamente. As palavras-chave **as first** e **as last** serão ignoradas quando forem inseridos atributos.  
  
 after  
 Os nós identificados por *Expression1* são inseridos como irmãos diretamente após o nó identificado por *Expression2*. A palavra-chave **after** não pode ser usada para inserir atributos. Por exemplo, não pode ser usada para inserir um construtor de atributo ou para retornar um atributo de um XQuery.  
  
 before  
 Os nós identificados por *Expression1* são inseridos como irmãos diretamente antes do nó identificado por *Expression2*. A palavra-chave **before** não pode ser usada quando atributos estão sendo inseridos. Por exemplo, não pode ser usada para inserir um construtor de atributo ou para retornar um atributo de um XQuery.  
  
 *Expression2*  
 Identifica um nó. Os nós identificados em *Expression1* são inseridos em relação ao nó identificado por *Expression2*. Isso pode ser uma expressão XQuery que retorna uma referência a um nó que existe no documente atualmente referenciado. Se mais de um nó for retornado, a inserção falhará. Se *Expression2* retornar uma sequência vazia, não ocorrerá nenhuma inserção e nenhum erro será retornado. Se *Expression2* não for estatisticamente um singleton, será retornado um erro estático. *Expression2* não pode ser uma instrução de processamento, comentário ou atributo. Observe que *Expression2* precisa ser uma referência a um nó existente no documento e não a um nó construído.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-inserting-element-nodes-into-the-document"></a>a. Inserção de nós de elemento no documento  
 O exemplo a seguir ilustra como inserir elementos em um documento. Primeiro, um documento XML é atribuído a uma variável do tipo **XML**. Em seguida, por meio de várias instruções XML DML **insert** , o exemplo ilustra como nós de elemento são inseridos no documento. Depois de cada inserção, a instrução SELECT exibe o resultado.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;         
SET @myDoc = '<Root>         
    <ProductDescription ProductID="1" ProductName="Road Bike">         
        <Features>         
        </Features>         
    </ProductDescription>         
</Root>'  ;       
SELECT @myDoc;     
-- insert first feature child (no need to specify as first or as last)         
SET @myDoc.modify('         
insert <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>   
into (/Root/ProductDescription/Features)[1]') ;  
SELECT @myDoc ;        
-- insert second feature. We want this to be the first in sequence so use 'as first'         
set @myDoc.modify('         
insert <Warranty>1 year parts and labor</Warranty>          
as first         
into (/Root/ProductDescription/Features)[1]         
')  ;       
SELECT @myDoc  ;       
-- insert third feature child. This one is the last child of <Features> so use 'as last'         
SELECT @myDoc         
SET @myDoc.modify('         
insert <Material>Aluminium</Material>          
as last         
into (/Root/ProductDescription/Features)[1]         
')         
SELECT @myDoc ;        
-- Add fourth feature - this time as a sibling (and not a child)         
-- 'after' keyword is used (instead of as first or as last child)         
SELECT @myDoc  ;       
set @myDoc.modify('         
insert <BikeFrame>Strong long lasting</BikeFrame>   
after (/Root/ProductDescription/Features/Material)[1]         
')  ;       
SELECT @myDoc;  
GO  
```  
  
 Observe que várias expressões de caminho neste exemplo especificam" [1]" como um requisito de digitação estática. Isso assegura um único nó de destino.  
  
### <a name="b-inserting-multiple-elements-into-the-document"></a>B. Inserção de vários elementos no documento  
 No exemplo a seguir, um documento é atribuído primeiro a uma variável do tipo **XML**. Em seguida, uma sequência de dois elementos, que representa os recursos do produto, é atribuída a uma segunda variável do tipo **XML**. Essa sequência é inserida na primeira variável.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc = N'<Root>             
<ProductDescription ProductID="1" ProductName="Road Bike">             
    <Features> </Features>             
</ProductDescription>             
</Root>';  
DECLARE @newFeatures xml;  
SET @newFeatures = N'<Warranty>1 year parts and labor</Warranty>            
<Maintenance>3 year parts and labor extended maintenance is available</Maintenance>';           
-- insert new features from specified variable            
SET @myDoc.modify('             
insert sql:variable("@newFeatures")             
into (/Root/ProductDescription/Features)[1] ')             
SELECT @myDoc;  
GO  
```  
  
### <a name="c-inserting-attributes-into-a-document"></a>C. Inserção de atributos em um documento  
 O exemplo a seguir ilustra como são inseridos atributos em um documento. Primeiro, um documento é atribuído a uma variável do tipo **xml**. Em seguida, uma série de instruções XML DML **insert** é usada para inserir atributos no documento. Depois de cada inserção de atributo, a instrução SELECT exibe o resultado.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml ;            
SET @myDoc =   
'<Root>             
    <Location LocationID="10" >             
        <step>Manufacturing step 1 at this work center</step>             
        <step>Manufacturing step 2 at this work center</step>             
    </Location>             
</Root>' ;  
SELECT @myDoc  ;          
-- insert LaborHours attribute             
SET @myDoc.modify('             
insert attribute LaborHours {".5" }             
into (/Root/Location[@LocationID=10])[1] ') ;           
SELECT @myDoc  ;          
-- insert MachineHours attribute but its value is retrived from a sql variable @Hrs             
DECLARE @Hrs float ;            
SET @Hrs =.2   ;          
SET @myDoc.modify('             
insert attribute MachineHours {sql:variable("@Hrs") }             
into   (/Root/Location[@LocationID=10])[1] ');            
SELECT @myDoc;             
-- insert sequence of attribute nodes (note the use of ',' and ()              
-- around the attributes.             
SET @myDoc.modify('             
insert (              
           attribute SetupHours {".5" },             
           attribute SomeOtherAtt {".2"}             
        )             
into (/Root/Location[@LocationID=10])[1] ');             
SELECT @myDoc;  
GO  
```  
  
### <a name="d-inserting-a-comment-node"></a>D. Inserção de um nó de comentário  
 Nesta consulta, um documento XML é atribuído primeiro a uma variável do tipo **XML**. Em seguida, XML DML é usado para inserir um nó de comentário depois do primeiro elemento <`step`>.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;             
SET @myDoc =   
'<Root>             
    <Location LocationID="10" >             
        <step>Manufacturing step 1 at this work center</step>             
        <step>Manufacturing step 2 at this work center</step>             
    </Location>             
</Root>' ;           
SELECT @myDoc;             
SET @myDoc.modify('             
insert <!-- some comment -->             
after (/Root/Location[@LocationID=10]/step[1])[1] ');            
SELECT @myDoc;  
GO  
```  
  
### <a name="e-inserting-a-processing-instruction"></a>E. Inserção de uma instrução de processamento  
 Na consulta a seguir, um documento XML é atribuído primeiro a uma variável do tipo **XML**. Em seguida, a palavra-chave XML DML é usada para inserir uma instrução de processamento no início do documento.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc =   
'<Root>   
    <Location LocationID="10" >   
        <step>Manufacturing step 1 at this work center</step>   
        <step>Manufacturing step 2 at this work center</step>   
    </Location>   
</Root>' ;  
SELECT @myDoc ;  
SET @myDoc.modify('   
insert <?Program = "Instructions.exe" ?>   
before (/Root)[1] ') ;  
SELECT @myDoc ;  
GO  
```  
  
### <a name="f-inserting-data-using-a-cdata-section"></a>F. Inserção de dados que usam uma seção CDATA  
 Quando você insere texto que inclui caracteres inválidos no XML, como < ou >, você poderá usar seções CDATA para inserir os dados conforme mostrado na consulta a seguir. A consulta especifica uma seção CDATA, mas é adicionada como nó de texto com caracteres inválidos convertidos em entidades. Por exemplo, '<' é salvo como &lt;.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;             
SET @myDoc =   
'<Root>             
    <ProductDescription ProductID="1" ProductName="Road Bike">             
        <Features> </Features>             
    </ProductDescription>             
</Root>' ;            
SELECT @myDoc ;            
SET @myDoc.modify('             
insert <![CDATA[ <notxml> as text </notxml> or cdata ]]>   
into  (/Root/ProductDescription/Features)[1] ') ;   
SELECT @myDoc ;  
GO  
```  
  
 A consulta insere um nó de texto no elemento <`Features`>:  
  
```  
<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features> <notxml> as text </notxml> or cdata </Features>  
</ProductDescription>  
</Root>       
```  
  
### <a name="g-inserting-text-node"></a>G. Inserção de nó de texto  
 Nesta consulta, um documento XML é atribuído primeiro a uma variável do tipo **XML**. Em seguida, XML DML é usado para inserir um nó de texto como o primeiro filho do elemento <`Root`>. O construtor de texto é usado para especificar o texto.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc = '<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  
</Features>  
</ProductDescription>  
</Root>'  
SELECT @myDoc;  
set @myDoc.modify('  
 insert text{"Product Catalog Description"}   
 as first into (/Root)[1]  
');  
SELECT @myDoc;  
```  
  
### <a name="h-inserting-a-new-element-into-an-untyped-xml-column"></a>H. Inserção de um novo elemento em uma coluna xml não digitada  
 O exemplo a seguir aplica XML DML para atualizar uma instância XML armazenada em uma coluna do tipo **XML**:  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE T (i int, x xml);  
go  
INSERT INTO T VALUES(1,'<Root>  
    <ProductDescription ProductID="1" ProductName="Road Bike">  
        <Features>  
            <Warranty>1 year parts and labor</Warranty>  
            <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
        </Features>  
    </ProductDescription>  
</Root>');  
go  
-- insert a new element  
UPDATE T  
SET x.modify('insert <Material>Aluminium</Material> as first  
  into   (/Root/ProductDescription/Features)[1]  
');  
GO  
```  
  
 Novamente, quando o nó do elemento <`Material`> for inserido, a expressão de caminho deverá retornar um único destino. Isso é especificado explicitamente somando um [1] no final da expressão.  
  
```  
-- check the update  
SELECT x.query(' //ProductDescription/Features')  
FROM T;  
GO  
```  
  
### <a name="i-inserting-based-on-an-if-condition-statement"></a>I. Inserção baseada em uma instrução de condição se  
 No exemplo a seguir, uma condição IF é especificada como parte da Expression1 na instrução XML DML **insert**. Se a condição for True, um atributo será adicionado ao elemento <`WorkCenter`>.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc =   
'<Root>  
    <Location LocationID="10" LaborHours="1.2" >  
        <step>Manufacturing step 1 at this work center</step>  
    <step>Manufacturing step 2 at this work center</step>  
    </Location>  
</Root>';  
SELECT @myDoc  
SET @myDoc.modify('  
insert  
if (/Root/Location[@LocationID=10])  
then attribute MachineHours {".5"}  
else ()  
    as first into   (/Root/Location[@LocationID=10])[1] ');  
SELECT @myDoc;  
GO  
```  
  
 O exemplo a seguir é semelhante, exceto que a instrução XML DML **insert** inserirá um elemento no documento se a condição for True. Isto é, se o elemento <`WorkCenter`> tiver um número inferior ou igual a dois elementos filho <`step`>.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc =   
'<Root>  
    <Location LocationID="10" LaborHours="1.2" >  
        <step>Manufacturing step 1 at this work center</step>  
        <step>Manufacturing step 2 at this work center</step>  
    </Location>  
</Root>';  
SELECT @myDoc;  
SET @myDoc.modify('  
insert  
if (count(/Root/Location/step) <= 2)  
then element step { "This is a new step" }  
else ()  
    as last into   (/Root/Location[@LocationID=10])[1] ');  
SELECT @myDoc;  
GO  
```  
  
 Este é o resultado:  
  
```  
<Root>  
 <WorkCenter WorkCenterID="10" LaborHours="1.2">  
  <step>Manufacturing step 1 at this work center</step>  
  <step>Manufacturing step 2 at this work center</step>  
  <step>This is a new step</step>  
 </WorkCenter>  
```  
  
### <a name="j-inserting-nodes-in-a-typed-xml-column"></a>J. Inserção de nós em uma coluna xml digitada  
 Este exemplo insere um elemento e um atributo em um XML de instruções de fabricação armazenado em uma coluna **XML** tipada.  
  
 No exemplo, primeiro você cria uma tabela (T) com uma coluna **XML** tipada no banco de dados AdventureWorks. Depois, você copia a instância XML de instruções de fabricação da coluna Instructions na tabela ProductModel para a tabela T. Em seguida, as inserções são aplicadas ao XML na tabela T.  
  
```  
USE AdventureWorks;  
GO            
DROP TABLE T;  
GO             
CREATE TABLE T(ProductModelID int primary key,    
Instructions xml (Production.ManuInstructionsSchemaCollection));  
GO  
INSERT T              
    SELECT ProductModelID, Instructions             
    FROM Production.ProductModel             
    WHERE ProductModelID=7;  
GO             
SELECT Instructions             
FROM T;  
-- now insertion begins             
--1) insert a new manu. Location. The <Root> specified as              
-- expression 2 in the insert() must be singleton.      
UPDATE T   
set Instructions.modify('   
declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
insert <MI:Location LocationID="1000" >   
           <MI:step>New instructions go here</MI:step>   
         </MI:Location>   
as first   
into   (/MI:root)[1]   
') ;  
  
SELECT Instructions             
FROM T ;  
-- 2) insert attributes in the new <Location>             
UPDATE T             
SET Instructions.modify('             
declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";             
insert attribute LaborHours { "1000" }             
into (/MI:root/MI:Location[@LocationID=1000])[1] ');   
GO             
SELECT Instructions             
FROM T ;  
GO             
--cleanup             
DROP TABLE T ;  
GO             
```  
  
## <a name="see-also"></a>Consulte Também  
 [Comparar XML digitado com XML não digitado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Criar instâncias de dados XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [Métodos de tipos de dados xml](../../t-sql/xml/xml-data-type-methods.md)   
 [XML DML &#40;linguagem de manipulação de dados XML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
