---
title: Autoexiste | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 56283497-624c-45b5-8a0d-036b0e331d22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc9aa519d37b040026414ab826373357a1ddd92f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66074726"
---
# <a name="autoexists"></a>autoexists
  O conceito de *autoexists* limita o espaço de cubo a células que, de fato, existem no cubo em contraposição às que podem existir em decorrência da criação de todas as combinações possíveis de membros de hierarquia de atributos da mesma hierarquia. Isso porque os membros de uma hierarquia de atributo não podem existir com membros de outra hierarquia de atributo na mesma dimensão. Quando duas ou mais hierarquias de atributo da mesma dimensão são usadas em uma instrução SELECT, o Analysis Services avalia as expressões dos atributos para verificar se os membros desses atributos sejam corretamente confinados para atender aos critérios de todos os outros atributos.  
  
 Por exemplo, vamos supor que você esteja trabalhando com atributos da dimensão Geografia. Se houver uma expressão que retorne todos os membros do atributo City e outra que confine os membros do atributo Country a todos os países da Europa, isso resultará no confinamento dos membros de City apenas às cidades que pertençam a países da Europa. Isso por conta da característica autoexists do Analysis Services. Autoexists somente se aplica a atributos da mesma dimensão porque tenta impedir que os registros da dimensão excluídos em uma expressão do atributo sejam incluídos pelas outras expressões do atributo. Autoexists também pode ser considerado a interseção resultante das diferentes expressões de atributo em relação às linhas de dimensão.  
  
## <a name="cell-existence"></a>Existência da célula  
 As seguintes células sempre existem:  
  
-   O membro (All), de toda hierarquia, quando cruzado com membros de outras hierarquias na mesma dimensão.  
  
-   Os membros calculados quando cruzados com seus irmãos não calculados, ou com seus pais ou descendentes de seus irmãos não calculados.  
  
## <a name="providing-non-existing-cells"></a>Fornecendo células não existentes  
 Uma célula não existente é uma célula fornecida pelo sistema como uma resposta para uma consulta ou um cálculo que solicita uma célula não existente no cubo. Por exemplo, se você tiver um cubo com uma hierarquia de atributo City e uma hierarquia de atributo Country pertencentes à dimensão Geography, além de uma medida Internet Sales Amount, o espaço desse cubo só incluirá os membros existentes entre si. Por exemplo, se a hierarquia de atributo Cidade incluir as cidades de Nova Iorque, Londres, Paris, Tóquio e Melbourne; e a hierarquia de atributo País incluir os países Estados Unidos, Reino Unido, França, Japão e Austrália; o espaço do cubo não incluirá o espaço (célula) na interseção Paris e Estados Unidos.  
  
 Ao consultar células que não existem, as células inexistentes retornarão nulas; ou seja, elas não poderão conter cálculos e você não poderá definir um cálculo que seja gravado nesse espaço. Por exemplo, a instrução a seguir inclui células que não existem.  
  
```  
SELECT [Customer].[Gender].[Gender].Members ON COLUMNS,  
{[Customer].[Customer].[Aaron A. Allen]  
   ,[Customer].[Customer].[Abigail Clark]} ON ROWS   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
> [!NOTE]  
>  Essa consulta usa a função [Membros (Conjunto) (MDX)](/sql/mdx/members-set-mdx) para retornar o conjunto de membros da hierarquia de atributo Sexo no eixo da coluna, e cruza esse conjunto com o conjunto especificado de membros da hierarquia de atributo Cliente no eixo de linhas.  
  
 Quando você executa a consulta anterior, a célula na interseção Aaron A. Allen e Feminino exibe um valor nulo. Similarmente, a célula na interseção Abigail Clark e Masculino exibe um valor nulo. Essas células não existem e não podem conter um valor, mas as células que não existem podem aparecer no resultado retornado por uma consulta.  
  
 Quando você usa a função [Crossjoin (MDX)](/sql/mdx/crossjoin-mdx) para retornar o produto vetorial de membros de hierarquia de atributo de hierarquias de atributo na mesma dimensão, o Autoexists limita as tuplas que são retornadas ao conjunto de tuplas que realmente existem, em vez de retornar um produto Cartesiano completo. Por exemplo, execute e examine os resultados da execução da consulta a seguir.  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
         [Customer].[State-Province].Members  
  ) ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
> [!NOTE]  
>  Note que 0 é usado para designar o eixo da coluna, que é a forma abreviada de eixo (0) – que é o eixo da coluna.  
  
 A consulta anterior somente retorna células para membros de cada hierarquia de atributo na consulta que existe um com o outro. A consulta anterior também pode ser escrita usando a nova * variante da função [de interjunção (MDX)](/sql/mdx/crossjoin-mdx) .  
  
```  
SELECT   
   [Customer].[Country].[United States] *   
      [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
 A consulta anterior também poderia ser escrita da seguinte forma:  
  
```  
SELECT [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE (Measures.[Internet Sales Amount],  
   [Customer].[Country].[United States])  
```  
  
 Os valores das células retornadas serão idênticos, apesar de os metadados no conjunto de resultados serem diferentes. Por exemplo, com a consulta anterior, a hierarquia País foi movida para o eixo do slicer (na cláusula WHERE) e, portanto, não aparece explicitamente no conjunto de resultados.  
  
 Cada uma dessas três consultas anteriores demonstra o efeito do comportamento de existência automática no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="deep-and-shallow-autoexists"></a>Autoexists Deep e Shallow  
 Autoexists pode ser aplicado às expressões como Deep ou Shallow. `Deep Autoexists` significa que todas as expressões serão avaliadas para atender o espaço mais profundo possível após a aplicação das expressões de segmentação de dados, das expressões de subseleção no eixo etc. `Shallow Autoexists` quer dizer que as expressões externas são avaliadas antes da expressão atual e esses resultados são transmitidos à expressão atual. A configuração padrão é deep autoexists.  
  
 O cenário e os exemplos a seguir ajudarão a ilustrar os tipos diferentes de Autoexistss. Nos exemplos a seguir, dois conjuntos serão criados: um como uma expressão calculada e o outro como uma expressão constante.  
  
 `//Obtain the Top 10 best reseller selling products by Name`  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 O conjunto de resultados obtido é:  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Valor de desconto**|**Desconto PCT**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Road-250**|**$9,377,457.68**|**$4,032.47**|**0, 4%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63%**|  
|**Road-650**|**$7,442,141.81**|**$39,698.30**|**0.53%**|  
|**Touring-1000**|**$6,723,794.29**|**$166,144.17**|**2,47%**|  
|**Road-550-W**|**$3,668,383.88**|**$1,901.97**|**0, 5%**|  
|**Road-350-W**|**$3,665,932.31**|**$20,946.50**|**0.57%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0, 1%**|  
|**Road-150**|**$2,363,805.16**|**$0**|**0, 0%**|  
|**Touring-3000**|**$2,046,508.26**|**$79,582.15**|**3,89%**|  
  
 O conjunto obtido com base nos produtos parece ser igual a Preferred10Products; assim, verificando o conjunto Preferred10Products:  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Preferred10Products on 1`  
  
 `from [Adventure Works]`  
  
 De acordo com os resultados a seguir, os dois conjuntos (Top10SellingProducts, Preferred10Products) são iguais  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Valor de desconto**|**Desconto PCT**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Road-250**|**$9,377,457.68**|**$4,032.47**|**0, 4%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63%**|  
|**Road-650**|**$7,442,141.81**|**$39,698.30**|**0.53%**|  
|**Touring-1000**|**$6,723,794.29**|**$166,144.17**|**2,47%**|  
|**Road-550-W**|**$3,668,383.88**|**$1,901.97**|**0, 5%**|  
|**Road-350-W**|**$3,665,932.31**|**$20,946.50**|**0.57%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0, 1%**|  
|**Road-150**|**$2,363,805.16**|**$0**|**0, 0%**|  
|**Touring-3000**|**$2,046,508.26**|**$79,582.15**|**3,89%**|  
  
 O exemplo a seguir ilustrará o conceito de Autoexists profundo. No exemplo, nós estamos filtrando Top10SellingProducts pelo atributo [Product].[Product Line] para os itens no grupo [Mountain]. Observe que os dois atributos (slicer e axis) pertencem a mesma dimensão, [Product].  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `// Preferred10Products set removed for clarity`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 Gera o seguinte conjunto de resultados:  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Valor de desconto**|**Desconto PCT**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0, 1%**|  
|**Mountain-300**|**$1,907,249.38**|**$876.95**|**0, 5%**|  
|**Mountain-500**|**$1,067,327.31**|**$17,266.09**|**1,62%**|  
|**Mountain-400-W**|**$592,450.05**|**$303.49**|**0, 5%**|  
|**LL Mountain Frame**|**$521,864.42**|**$252.41**|**0, 5%**|  
|**ML Mountain Frame-W**|**$482,953.16**|**$206.95**|**0, 4%**|  
|**ML Mountain Frame**|**$343,785.29**|**$161.82**|**0, 5%**|  
|**Women's Mountain Shorts**|**$260,304.09**|**$6,675.56**|**2.56%**|  
  
 No conjunto de resultados acima, havia sete itens novos na lista Top10SellingProducts, e Mountain-200, Mountain-100 e HL Mountain Frame foram movidos para o início da lista. No conjunto de resultados anterior, esses três valores foram intercalados.  
  
 Isso se chama Deep Autoexists, porque o conjunto Top10SellingProducts é avaliado para atender às condições de divisão da consulta. Deep Autoexists significa que todas as expressões serão avaliadas para atender o espaço mais profundo possível após a aplicação das expressões de segmentação de dados, das expressões de subseleção no eixo etc.  
  
 No entanto, pode ser que alguém queira ser capaz de executar a análise sobre Top10SellingProducts como equivalente a Preferred10Products, como no exemplo a seguir:  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Preferred10Products on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 Gera o seguinte conjunto de resultados:  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Valor de desconto**|**Desconto PCT**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0, 1%**|  
  
 Nos resultados acima, a segmentação de dados dá um resultado que contém apenas os produtos de Preferred10Products que fazem parte do grupo [Mountain] em [Product].[Product Line]; conforme o esperado, porque Preferred10Products é uma expressão constante.  
  
 Esse conjunto de resultados também é considerado Shallow Autoexists. Isso ocorre porque a expressão é avaliada antes da cláusula de divisão. No exemplo anterior, a expressão era uma expressão constante para fins de ilustração, para introduzir o conceito.  
  
 O comportamento de Autoexists pode ser modificado no nível da sessão com o uso da propriedade da cadeia de caracteres de conexão `Autoexists`. O exemplo a seguir começa abrindo uma nova sessão e adicionando a propriedade *Autoexists=3* à cadeia de conexão. Você deve abrir uma nova conexão para executar o exemplo. Após o estabelecimento da conexão com a configuração Autoexist, ela permanecerá em efeito até que a conexão seja encerrada.  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `//Preferred10Products set removed for clarity`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 O conjunto de resultados a seguir agora mostra o comportamento superficial de Autoexists.  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**Valor de desconto**|**Desconto PCT**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0, 1%**|  
  
 O comportamento de autoexisteções pode ser modificado usando o parâmetro Autoexists = [1 | 2 | 3] na cadeia de conexão; consulte [Propriedades XMLA com suporte &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) e <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> para uso de parâmetro.  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos principais em MDX &#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)   
 [Espaço do cubo](cube-space.md)   
 [Tuplas](tuples.md)   
 [Trabalhando com membros, tuplas e conjuntos &#40;&#41;MDX](working-with-members-tuples-and-sets-mdx.md)   
 [Totais visuais e totais não visuais](visual-totals-and-non-visual-totals.md)   
 [Referência de linguagem MDX &#40;&#41;MDX](/sql/mdx/mdx-language-reference-mdx)   
 [Referência de expressões multidimensionais &#40;MDX&#41;](/sql/mdx/multidimensional-expressions-mdx-reference)  
  
  
