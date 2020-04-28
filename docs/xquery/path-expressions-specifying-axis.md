---
title: Etapa especificando o eixo em uma expressão de caminho | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 07058816406ef6ac0d5a3356423e231a10ce6165
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67946488"
---
# <a name="path-expressions---specifying-axis"></a>Expressões de Caminho – Especificar Eixo
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Uma etapa de eixo em uma expressão de caminho inclui os seguintes componentes:  
  
-   Um eixo  
  
-   Um [teste de nó](../xquery/path-expressions-specifying-node-test.md)  
  
-   [Zero ou mais qualificadores de etapa (opcional)](../xquery/path-expressions-specifying-predicates.md)  
  
 Para obter mais informações, consulte [expressões de caminho &#40;&#41;XQuery ](../xquery/path-expressions-xquery.md).  
  
 A implementação XQuery no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] oferece suporte às seguintes etapas de eixo:  
  
|Axis|Descrição|  
|----------|-----------------|  
|**child**|Retorna os filhos do nó de contexto.|  
|**descendant**|Retorna todos os descendentes do nó de contexto.|  
|**primária**|Retorna o pai do nó de contexto.|  
|**Attribute**|Retorna os atributos do nó de contexto.|  
|**auto-restauração**|Retorna o próprio nó de contexto.|  
|**descendant-or-self**|Retorna o nó de contexto e todos os descendentes do nó de contexto.|  
  
 Todos esses eixos, exceto o eixo **pai** , são eixos de encaminhamento. O eixo **pai** é um eixo reverso, pois ele pesquisa retroativamente na hierarquia do documento. Por exemplo, a expressão do caminho relativo `child::ProductDescription/child::Summary` tem duas etapas, e cada etapa especifica um eixo `child`. A primeira etapa recupera os \<filhos do elemento ProductDescription> do nó de contexto. Para cada \<nó de elemento de> de ProductDescription, a segunda \<etapa recupera o resumo> nó filho de elemento.  
  
 A expressão de caminho relativo, `child::root/child::Location/attribute::LocationID`, tem três etapas. As primeiras duas etapas especificam um eixo `child` e a terceira etapa especifica o eixo `attribute`. Quando executado em relação aos documentos XML de instruções de fabricação na tabela **Production. ProductModel** , a expressão `LocationID` retorna o atributo \<do local> nó filho do elemento \<de> raiz.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos de consulta neste tópico são especificados em relação às colunas do tipo **XML** no banco de dados **AdventureWorks** .  
  
### <a name="a-specifying-a-child-axis"></a>A. Especificando um eixo filho  
 Para um modelo de produto específico, a consulta a seguir \<recupera os recursos> nó de elemento \<filho do nó do elemento ProductDescription> da descrição do catálogo de `Production.ProductModel` produtos armazenada na tabela.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  /child::PD:ProductDescription/child::PD:Features')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   O `query()` método do tipo de dados **XML** especifica a expressão de caminho.  
  
-   Ambas as etapas na expressão de caminho especificam um eixo `child` e os nomes de nó, `ProductDescription` e `Features`. Para obter informações sobre testes de nó, consulte [especificando o teste de nó em uma etapa de expressão de caminho](../xquery/path-expressions-specifying-node-test.md).  
  
### <a name="b-specifying-descendant-and-descendant-or-self-axes"></a>B. Especificando eixos descendentes e descendentes ou independentes  
 O exemplo a seguir usa os eixos descendente e descendente ou self. A consulta neste exemplo é especificada em uma variável de tipo **XML** . A instância XML é simplificada para ilustrar facilmente a diferença nos resultados gerados.  
  
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
  
 `/child::a/child::b/descendant::*`, você está solicitando todos os descendentes do nó `b` de elemento <>.  
  
 O asterisco (*) no teste de nó representa o nome do nó como um teste de nó. Dessa forma, o tipo de nó primário do eixo descendente, o nó do elemento, determina os tipos de nós retornados. Ou seja, a expressão retorna todos os nós do elemento. Não são retornados nós de texto. Para obter mais informações sobre o tipo de nó primário e sua relação com o teste de nó, consulte [especificando o teste de nó em um](../xquery/path-expressions-specifying-node-test.md) tópico de expressão de caminho.  
  
 Os nós de elemento `c` <> e `d` <> são retornados, conforme mostrado no seguinte resultado:  
  
```  
<c>text2  
     <d>text3</d>  
</c>  
<d>text3</d>  
```  
  
 Se você especificar um eixo descendente ou próprio em vez do eixo descendente, `/child::a/child::b/descendant-or-self::*` o retornará o nó de contexto, o elemento `b` <> e seu descendente.  
  
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
  
 O exemplo de consulta a seguir no banco de dados **AdventureWorks** recupera todos os nós de elemento `Features` descendentes do <elemento> `ProductDescription` filho do elemento <>:  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  /child::PD:ProductDescription/child::PD:Features/descendant::*  
')  
FROM  Production.ProductModel  
WHERE ProductModelID=19  
```  
  
### <a name="c-specifying-a-parent-axis"></a>C. Especificando um eixo pai  
 A consulta a seguir retorna o `Summary` <> filho do elemento <`ProductDescription`> no documento XML do catálogo de produtos armazenado na `Production.ProductModel` tabela.  
  
 Este exemplo usa o eixo pai para retornar ao pai do elemento <`Feature`> e recuperar o <`Summary` elemento> filho do `ProductDescription` elemento <>.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  
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
  
 Cada descrição do catálogo de modelos de produto armazenada na coluna **CatalogDescription** da tabela **ProductModel** tem um `<ProductDescription>` elemento que `ProductModelID` tem o `<Features>` atributo e o elemento filho, conforme mostrado no fragmento a seguir:  
  
```  
<ProductDescription ProductModelID="..." >  
  ...  
  <Features>  
    <Feature1>...</Feature1>  
    <Feature2>...</Feature2>  
   ...  
</ProductDescription>  
```  
  
 A consulta define uma variável iterator, `$f`, na instrução FLWOR para retornar os filhos do elemento do elemento `<Features>`. Para obter mais informações, consulte [FLWOR Statement and iteration &#40;XQuery&#41;](../xquery/flwor-statement-and-iteration-xquery.md). Para cada recurso, a cláusula `return` constrói um XML na seguinte forma:  
  
```  
<Feature ProductModelID="...">...</Feature>  
<Feature ProductModelID="...">...</Feature>  
```  
  
 Para adicionar o `ProductModelID` elemento para `<Feature` cada>, o `parent` eixo é especificado:  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
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
   xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
    <wm:Description>parts and labor</wm:Description>  
  </wm:Warranty>  
</Feature>  
<Feature ProductModelID="19">  
  <wm:Maintenance   
   xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <wm:NoOfYears>10 years</wm:NoOfYears>  
    <wm:Description>maintenance contract available through your dealer   
                  or any AdventureWorks retail store.</wm:Description>  
  </wm:Maintenance>  
</Feature>  
<Feature ProductModelID="19">  
  <p1:wheel   
   xmlns:p1="https://www.adventure-works.com/schemas/OtherFeatures">  
      High performance wheels.  
  </p1:wheel>  
</Feature>  
```  
  
 Observe que o predicado `[1]` na expressão de caminho é adicionado para assegurar que um valor de singleton seja retornado.  
  
  
