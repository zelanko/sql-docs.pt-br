---
title: "Especificação de eixo em uma etapa de expressão de caminho | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- attribute axis [SQL Server]
- axis step [XQuery]
- descendant axis
- self axis
- path expressions [XQuery]
- child axis
- descendant-or-self axis
- parent axis
ms.assetid: c44fb843-0626-4496-bde0-52ca0bac0a9e
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 44ae49e51ac3fab0ca4b2cd8363601a14a3edf0b
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="path-expressions---specifying-axis"></a>Expressões de caminho - especificação de eixo
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Uma etapa de eixo em uma expressão de caminho inclui os seguintes componentes:  
  
-   Um eixo  
  
-   Um [teste de nó](../xquery/path-expressions-specifying-node-test.md)  
  
-   [Zero ou mais qualificadores de etapa (opcionais)](../xquery/path-expressions-specifying-predicates.md)  
  
 Para obter mais informações, consulte [expressões de caminho &#40; XQuery &#41; ](../xquery/path-expressions-xquery.md).  
  
 A implementação XQuery no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] oferece suporte às seguintes etapas de eixo:  
  
|Axis|Description|  
|----------|-----------------|  
|**child**|Retorna os filhos do nó de contexto.|  
|**descendant**|Retorna todos os descendentes do nó de contexto.|  
|**parent**|Retorna o pai do nó de contexto.|  
|**attribute**|Retorna os atributos do nó de contexto.|  
|**self**|Retorna o próprio nó de contexto.|  
|**descendant-or-self**|Retorna o nó de contexto e todos os descendentes do nó de contexto.|  
  
 Todos esses eixos, exceto o **pai** eixo, são eixos encaminhados. O **pai** eixo é um eixo inverso, pois ele pesquisa para trás na hierarquia do documento. Por exemplo, a expressão do caminho relativo `child::ProductDescription/child::Summary` tem duas etapas, e cada etapa especifica um eixo `child`. A primeira etapa recupera o \<ProductDescription > elemento filho do nó de contexto. Para cada \<ProductDescription > nó de elemento, a segunda etapa recupera o \<resumo > filhos do nó de elemento.  
  
 A expressão de caminho relativo, `child::root/child::Location/attribute::LocationID`, tem três etapas. As primeiras duas etapas especificam um eixo `child` e a terceira etapa especifica o eixo `attribute`. Quando executado em instruções de fabricação documentos XML no **productmodel** de tabela, a expressão retorna o `LocationID` atributo do \<local > filho do nó de elemento do \<raiz > elemento.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos de consulta neste tópico são especificados em relação **xml** colunas de tipo de **AdventureWorks** banco de dados.  
  
### <a name="a-specifying-a-child-axis"></a>A. Especificando um eixo filho  
 Para um modelo de produto específico, a consulta a seguir recupera o \<recursos > filhos do nó de elemento de \<ProductDescription > nó de elemento da descrição de catálogo de produtos armazenada no `Production.ProductModel` tabela.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  /child::PD:ProductDescription/child::PD:Features')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   O `query()` método o **xml** tipo de dados especifica a expressão de caminho.  
  
-   Ambas as etapas na expressão de caminho especificam um eixo `child` e os nomes de nó, `ProductDescription` e `Features`. Para obter informações sobre testes de nó, consulte [especificando Node Test em uma etapa de expressão de caminho](../xquery/path-expressions-specifying-node-test.md).  
  
### <a name="b-specifying-descendant-and-descendant-or-self-axes"></a>B. Especificando eixos descendentes e descendentes ou independentes  
 O exemplo a seguir usa os eixos descendente e descendente ou self. A consulta neste exemplo é especificada em relação a um **xml** variável de tipo. A instância XML é simplificada para ilustrar facilmente a diferença nos resultados gerados.  
  
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
declare @y xml  
set @y = @x.query('  
  /child::a/child::b  
')  
select @y  
```  
  
 No resultado a seguir, a expressão retorna o filho do nó do elemento `<b>` do nó do elemento `<a>`:  
  
```  
<b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
</b>  
```  
  
 Nesta expressão, se você especificar um eixo descendente para a expressão de caminho,  
  
 `/child::a/child::b/descendant::*`, estará solicitando todos os descendentes do nó do elemento <`b`>.  
  
 O asterisco (*) no teste de nó representa o nome do nó como um teste de nó. Dessa forma, o tipo de nó primário do eixo descendente, o nó do elemento, determina os tipos de nós retornados. Ou seja, a expressão retorna todos os nós do elemento. Não são retornados nós de texto. Para obter mais informações sobre o tipo de nó primário e sua relação com o teste de nó, consulte [especificando o teste de nó em uma etapa de expressão de caminho](../xquery/path-expressions-specifying-node-test.md) tópico.  
  
 Os nós do elemento <`c`> e <`d`> são retornados, como mostrado no resultado a seguir:  
  
```  
<c>text2  
     <d>text3</d>  
</c>  
<d>text3</d>  
```  
  
 Se você especificar um eixo descendente ou self em vez do eixo descendente, `/child::a/child::b/descendant-or-self::*` retorna o nó de contexto, o elemento <`b`> e seu descendente.  
  
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
  
 A seguinte consulta de exemplo no **AdventureWorks** banco de dados recupera todos os nós de elemento descendentes a <`Features`> do filho do elemento de <`ProductDescription`> elemento:  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  /child::PD:ProductDescription/child::PD:Features/descendant::*  
')  
FROM  Production.ProductModel  
WHERE ProductModelID=19  
```  
  
### <a name="c-specifying-a-parent-axis"></a>C. Especificando um eixo pai  
 A consulta a seguir retorna o filho do elemento <`Summary`> do elemento <`ProductDescription`> no documento XML do catálogo de produtos armazenado na tabela `Production.ProductModel`.  
  
 Este exemplo usa o eixo pai para retornar ao pai do elemento <`Feature`> e recuperar o filho do elemento <`Summary`> do elemento <`ProductDescription`>.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  
/child::PD:ProductDescription/child::PD:Features/parent::PD:ProductDescription/child::PD:Summary  
')  
FROM   Production.ProductModel  
WHERE  ProductModelID=19  
  
```  
  
 Neste exemplo de consulta, a expressão de caminho usa o eixo `parent`. Você pode reescrever a expressão sem o eixo pai, como mostrado a seguir:  
  
```  
/child::PD:ProductDescription[child::PD:Features]/child::PD:Summary  
```  
  
 Um exemplo mais útil do eixo pai é fornecido no exemplo a seguir.  
  
 Cada descrição de catálogo de modelo do produto armazenada no **CatalogDescription** coluna o **ProductModel** tabela tem um `<ProductDescription>` elemento que tem o `ProductModelID` atributo e `<Features>`elemento filho, conforme mostrado no fragmento a seguir:  
  
```  
<ProductDescription ProductModelID="..." >  
  ...  
  <Features>  
    <Feature1>...</Feature1>  
    <Feature2>...</Feature2>  
   ...  
</ProductDescription>  
```  
  
 A consulta define uma variável iterator, `$f`, na instrução FLWOR para retornar os filhos do elemento do elemento `<Features>`. Para obter mais informações, consulte [instrução FLWOR e iteração &#40; XQuery &#41; ](../xquery/flwor-statement-and-iteration-xquery.md). Para cada recurso, a cláusula `return` constrói um XML na seguinte forma:  
  
```  
<Feature ProductModelID="...">...</Feature>  
<Feature ProductModelID="...">...</Feature>  
```  
  
 Para adicionar o `ProductModelID` para cada elemento `<Feature`>, é especificado o eixo `parent`:  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
  for $f in /child::PD:ProductDescription/child::PD:Features/child::*  
  return  
   <Feature  
     ProductModelID="{ ($f/parent::PD:Features/parent::PD:ProductDescription/attribute::ProductModelID)[1]}" >  
          { $f }  
   </Feature>  
')  
FROM  Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Este é o resultado parcial:  
  
```  
<Feature ProductModelID="19">  
  <wm:Warranty   
   xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
    <wm:Description>parts and labor</wm:Description>  
  </wm:Warranty>  
</Feature>  
<Feature ProductModelID="19">  
  <wm:Maintenance   
   xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <wm:NoOfYears>10 years</wm:NoOfYears>  
    <wm:Description>maintenance contract available through your dealer   
                  or any AdventureWorks retail store.</wm:Description>  
  </wm:Maintenance>  
</Feature>  
<Feature ProductModelID="19">  
  <p1:wheel   
   xmlns:p1="http://www.adventure-works.com/schemas/OtherFeatures">  
      High performance wheels.  
  </p1:wheel>  
</Feature>  
```  
  
 Observe que o predicado `[1]` na expressão de caminho é adicionado para assegurar que um valor de singleton seja retornado.  
  
  
