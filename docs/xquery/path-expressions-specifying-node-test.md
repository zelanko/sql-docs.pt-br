---
title: Especificando Node Test em uma etapa de expressão de caminho | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- axis step [XQuery]
- node test [XQuery]
ms.assetid: ffe27a4c-fdf3-4c66-94f1-7e955a36cadd
caps.latest.revision: 24
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3460ecf0a821d5c7ffa39f242650e06c0e8ddaf4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="path-expressions---specifying-node-test"></a>Expressões de caminho - especificando Node Test
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Uma etapa de eixo em uma expressão de caminho inclui os seguintes componentes:  
  
-   [Um eixo](../xquery/path-expressions-specifying-axis.md)  
  
-   Um node test  
  
-   [Zero ou mais qualificadores de etapa (opcionais)](../xquery/path-expressions-specifying-predicates.md)  
  
 Para obter mais informações, consulte [expressões de caminho &#40;XQuery&#41;](../xquery/path-expressions-xquery.md).  
  
 Um node test é uma condição e é o segundo componente da etapa de eixo em uma expressão de caminho. Todos os nós selecionados por uma etapa devem satisfazer essa condição. Para a expressão de caminho, `/child::ProductDescription`, o node test é `ProductDescription`. Essa etapa recupera somente os filhos do nó de elemento cujo nome é ProductDescription.  
  
 Uma condição de node test pode incluir o seguinte:  
  
-   Um nome de nó. Só são retornados nós do tipo de nó principal com o nome especificado.  
  
-   Um tipo de nó. Só são retornados nós do tipo especificado.  
  
> [!NOTE]  
>  Os nomes de nó especificados em expressões de caminho XQuery não estão sujeitos às mesmas regras que diferenciam agrupamento, como consultas Transact-SQL, e diferenciam sempre maiúsculas de minúsculas.  
  
## <a name="node-name-as-node-test"></a>Nome de nó como node test  
 Ao especificar um nome de nó como um node test em uma etapa de expressão de caminho, você deve entender o conceito de tipo de nó principal. Todo eixo, filho, pai ou atributo, tem um tipo de nó principal. Por exemplo:  
  
-   Um eixo de atributo só pode conter atributos. Portanto, o nó de atributo é o tipo de nó principal do eixo de atributo.  
  
-   Para outros eixos, se os nós selecionados pelo eixo puderem conter nós de elemento, o elemento será o tipo de nó principal.  
  
 Quando você especificar um nome de nó como um node test, a etapa retornará os seguintes tipos de nós:  
  
-   Nós que são o tipo de nó principal do eixo.  
  
-   Nós que têm o mesmo nome, conforme especificado no node test.  
  
 Por exemplo, considere a seguinte expressão de caminho:  
  
```  
child::ProductDescription   
```  
  
 Essa expressão de uma etapa especifica um eixo `child` e o nome de nó `ProductDescription` como o node test. A expressão retorna apenas nós que são do tipo de nó principal do eixo filho, nós de elemento e os que tenham ProductDescription como nome.  
  
 A expressão de caminho, `/child::PD:ProductDescription/child::PD:Features/descendant::*,` tem três etapas. Tais etapas especificam os eixos filho e descendente. Em cada etapa, o nome de nó é especificado como o node test. O caractere curinga (`*`) na terceira etapa indica todos os nós do tipo de nó de principal para o eixo descendente. O tipo de nó principal do eixo determina o tipo de nó selecionado e os filtros de nome de nó que os nós selecionaram.  
  
 Como resultado, quando essa expressão é executada em documentos XML do catálogo de produtos no **ProductModel** tabela, ele recupera todos os filhos do nó de elemento do \<recursos > filho do nó de elemento de \< ProductDescription > elemento.  
  
 A expressão de caminho, `/child::PD:ProductDescription/attribute::ProductModelID`, é composto de duas etapas. Ambas as etapas especificam um nome de nó como o node test. Além disso, a segunda etapa usa o eixo de atributo. Como resultado, cada etapa seleciona nós do tipo de nó principal de seu eixo com o nome especificado como o node test. Assim, a expressão retorna **ProductModelID** nó de atributo do \<ProductDescription > nó de elemento.  
  
 Ao especificar os nomes de nós para node tests, você também pode usar o caractere curinga (*) para especificar o nome local de um nó ou para seu prefixo de namespace, como mostrado no seguinte exemplo:  
  
```  
declare @x xml  
set @x = '  
<greeting xmlns="ns1">  
   <salutation>hello</salutation>  
</greeting>  
<greeting xmlns="ns2">  
   <salutation>welcome</salutation>  
</greeting>  
<farewell xmlns="ns1" />'  
select @x.query('//*:greeting')  
select @x.query('declare namespace ns="ns1"; /ns:*')  
```  
  
## <a name="node-type-as-node-test"></a>Tipo de nó como node test  
 Para consultar os tipos de nó que não sejam os nós de elemento, use um teste do tipo de nó. Como mostrado na tabela a seguir, há quatro testes do tipo de nó disponíveis.  
  
|Tipo de nó|Retorna|Exemplo|  
|---------------|-------------|-------------|  
|`comment()`|True para um nó de comentário.|`following::comment()` seleciona todos os nós de comentário exibidos depois do nó de contexto.|  
|`node()`|True para um nó de qualquer tipo.|`preceding::node()` seleciona todos os nós de comentário exibidos antes do nó de contexto.|  
|`processing-instruction()`|True para um nó de instrução de processamento.|`self::processing instruction()` seleciona todos os nós de instrução de processamento no nó de contexto.|  
|`text()`|True para um nó de texto.|`child::text()` seleciona os nós de texto que são os filhos do nó de contexto.|  
  
 Se o tipo de nó, como text() ou comment()..., for especificado como o node test, a etapa apenas retornará nós de tipo especificado, independentemente do tipo de nó principal do eixo. Por exemplo, a seguinte expressão de caminho retorna apenas os filhos de nó de comentário do nó de contexto:  
  
```  
child::comment()  
```  
  
 Da mesma forma, `/child::ProductDescription/child::Features/child::comment()` filhos do nó de comentário recupera o \<recursos > filho do nó de elemento de \<ProductDescription > nó de elemento.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir comparam nome de nó e tipo de nó.  
  
### <a name="a-results-of-specifying-the-node-name-and-the-node-type-as-node-tests-in-a-path-expression"></a>A. Resultados da especificação do nome de nó e do tipo de nó como node tests em uma expressão de caminho  
 No exemplo a seguir, um documento XML simples é atribuído a um **xml** variável de tipo. O documento é consultado usando expressões de caminho diferentes. Os resultados são comparados.  
  
```  
declare @x xml  
set @x='  
<a>  
 <b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
 </b>  
</a>'  
select @x.query('  
/child::a/child::b/descendant::*  
')  
```  
  
 Essa expressão solicita os nós de elemento descendentes do nó de elemento `<b>`.  
  
 O asterisco (`*`) no node test indica um caractere curinga para o nome de nó. O eixo descendente tem o nó de elemento como seu tipo de nó primário. Portanto, a expressão retorna todos os nós de elemento descendentes do nó de elemento `<b>`. Ou seja, são retornados os nós de elemento `<c>` e `<d>`, como mostrado no seguinte resultado:  
  
```  
<c>text2  
     <d>text3</d>  
</c>  
<d>text3</d>  
```  
  
 Se você especificar um eixo descendente ou independente em vez de especificar um eixo descendente, o nó de contexto será retornado, além de seus descendentes:  
  
```  
/child::a/child::b/descendant-or-self::*  
```  
  
 Essa expressão retorna o nó de elemento `<b>` e seus nós de elemento descendentes. Ao retornar os nós descendentes, o tipo de nó primário do eixo descendente ou independente, o tipo de nó de elemento, determina que tipo de nós são retornados.  
  
 Este é o resultado:  
  
```  
<b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
</b>  
  
<c>text2  
     <d>text3</d>  
</c>  
  
<d>text3</d>   
```  
  
 A expressão anterior usava um caractere curinga como um nome de nó. Em vez disso, você pode usar a função `node()`, como mostrado nesta expressão:  
  
```  
/child::a/child::b/descendant::node()  
```  
  
 Porque `node()` é um tipo de nó, você receberá todos os nós do eixo descendente. Este é o resultado:  
  
```  
text1  
<c>text2  
     <d>text3</d>  
</c>  
text2  
<d>text3</d>  
text3  
```  
  
 Novamente, se você especificar eixo descendente ou independente e `node()` como o node test, receberá todos os descendentes, elementos e nós de texto, e também o nó de contexto, o elemento `<b>`.  
  
```  
<b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
</b>  
text1  
<c>text2  
     <d>text3</d>  
</c>  
text2  
<d>text3</d>  
text3  
```  
  
### <a name="b-specifying-a-node-name-in-the-node-test"></a>B. Especificando um nome de nó no node test  
 O exemplo a seguir especifica um nome de nó como o node test em todas as expressões de caminho. Como resultado, todas as expressões retornam nós do tipo de nó principal do eixo que tem o nome de nó especificado no node test.  
  
 A expressão de consulta a seguir retorna o elemento <`Warranty`> do documento XML do catálogo de produtos na tabela `Production.ProductModel`:  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::wm:Warranty  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A palavra-chave `namespace` no prólogo do XQuery define um prefixo usado no corpo da consulta. Para obter mais informações sobre o prólogo do XQuery, consulte [prólogo do XQuery](../xquery/modules-and-prologs-xquery-prolog.md) .  
  
-   Todas as três etapas na expressão de caminho especificam o eixo filho e um nome de nó como o node test.  
  
-   A parte do qualificador de etapa opcional da etapa de eixo não é especificada nas etapas da expressão.  
  
 A consulta retorna os filhos do elemento <`Warranty`> do filho do elemento <`Features`> do elemento <`ProductDescription`>.  
  
 Este é o resultado:  
  
```  
<wm:Warranty xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
  <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
  <wm:Description>parts and labor</wm:Description>  
</wm:Warranty>     
```  
  
 Na consulta a seguir, a expressão de caminho especifica um caractere curinga (`*`) em um node test.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::*  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 O caractere curinga é especificado para o nome de nó. Dessa forma, a consulta retorna todos os filhos do nó de elemento do filho do nó de elemento <`Features`> do nó de elemento <`ProductDescription`>.  
  
 A consulta a seguir é semelhante à consulta anterior, exceto que junto com o caractere curinga, é especificado um namespace. Como resultado, são retornados todos os filhos do nó de elemento nesse namespace. Observe que o elemento <`Features`> pode conter elementos de namespaces diferentes.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::wm:*  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Você pode usar o caractere curinga como um prefixo de namespace, como mostrado nesta consulta:  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::*:Maintenance  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Essa consulta retorna os filhos do nó de elemento <`Maintenance`> em todos os namespaces do documento XML do catálogo de produtos.  
  
### <a name="c-specifying-node-kind-in-the-node-test"></a>C. Especificando o tipo de nó no node test  
 O exemplo a seguir especifica um tipo de nó como o node test em todas as expressões de caminho. Como resultado, todas as expressões retornam nós do tipo especificado no node test.  
  
 Na consulta a seguir, a expressão de caminho especifica um tipo de nó em sua terceira etapa:  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::text()  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Na próxima consulta, é especificado o seguinte:  
  
-   A expressão de caminho tem três etapas separadas por uma barra (`/`).  
  
-   Cada uma dessas etapas especifica um eixo filho.  
  
-   As primeiras duas etapas especificam um nome de nó como o node test, e a terceira etapa especifica um tipo de nó como o node test.  
  
-   A expressão retorna os filhos do nó de texto do filho do elemento <`Features`> do nó de elemento <`ProductDescription`>.  
  
 Apenas um nó de texto é retornado. Este é o resultado:  
  
```  
These are the product highlights.   
```  
  
 A consulta a seguir retorna os filhos do nó de comentário do elemento <`ProductDescription`>.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::comment()  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A segunda etapa especifica um tipo de nó como o node test.  
  
-   Consequentemente, a expressão retorna os filhos do nó de comentário dos nós de elemento <`ProductDescription`>.  
  
 Este é o resultado:  
  
```  
<!-- add one or more of these elements... one for each specific product in this product model -->  
<!-- add any tags in <specifications> -->      
```  
  
 A seguinte consulta recupera os nós de instrução de processamento de nível superior:  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::processing-instruction()  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Este é o resultado:  
  
```  
<?xml-stylesheet href="ProductDescription.xsl" type="text/xsl"?>   
```  
  
 Você pode passar um parâmetro literal de cadeia de caracteres para o node test `processing-instruction()`. Nesse caso, a consulta retorna as instruções de processamento cujo valor do atributo de nome é o literal de cadeia de caracteres especificado no argumento.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::processing-instruction("xml-stylesheet")  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
## <a name="implementation-limitations"></a>Limitações de implementação  
 A seguir, são apresentadas as limitações específicas  
  
-   Não é oferecido suporte aos node tests SequenceType estendidos.  
  
-   Não é oferecido suporte a processing-instruction(name). Em vez disso, insira o nome entre aspas.  
  
  
