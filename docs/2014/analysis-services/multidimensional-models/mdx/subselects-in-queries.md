---
title: Subseleções em consultas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 9e361798-688e-4b11-9eef-31fc793e8ba4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9e0c2204aeb8c428d558b8bfe31f29c19ba6d773
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48212086"
---
# <a name="subselects-in-queries"></a>Subseleções em consultas
  Expressões de subseleção são expressões SELECT aninhadas que são usadas para restringir o espaço do cubo onde o SELECT externo exterior está sendo avaliado. Subseleções permitem definir um novo espaço sobre os quais todos os cálculos são avaliados.  
  
## <a name="subselects-by-example"></a>Subseleções por exemplo  
 Comecemos com um exemplo de como subseleções podem ajudar a gerar os resultados que nós queremos mostrar. Suponha que lhe peçam para gerar uma tabela que mostra o comportamento de vendas, ao longo de anos, para os 10 principais produtos.  
  
 O resultado deverá ser semelhante a esta tabela:  
  
|||||  
|-|-|-|-|  
||Soma de anos|Ano 1|...|  
|Soma dos 10 principais produtos||||  
|Produto A||||  
|...||||  
  
 Para fazer algo parecido com o exemplo acima, você pode escrever a expressão MDX a seguir:  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , TOPCOUNT( [Product].[Product].MEMBERS  
               , 10  
               , [Measures].[Sales Amount]  
               ) ON 1  
  FROM [Adventure Works]  
```  
  
 Que retorna os seguintes resultados:  
  
|||||||  
|-|-|-|-|-|-|  
||Todos os Períodos|CY 2005|CY 20062|CY 2007|CY 2008|  
|Todos os Produtos|$80,450,596.98|$8,065,435.31|$24,144,429.65|$32,202,669.43|$16,038,062.60|  
|Mountain-200 Black, 38|$1,634,647.94|(null)|(null)|$894,207.97|$740,439.97|  
|Mountain-200 Black, 42|$1,285,524.65|(null)|(null)|$722,137.65|$563,387.00|  
|Mountain-200 Silver, 38|$1,181,945.82|(null)|(null)|$634,600.78|$547,345.03|  
|Mountain-200 Black, 46|$995,927.43|(null)|(null)|$514,995.76|$480,931.68|  
|Mountain-200 Silver, 42|$1,005,111.77|(null)|(null)|$529,543.29|$475,568.49|  
|Mountain-200 Silver, 46|$975,932.56|(null)|(null)|$526,759.30|$449,173.26|  
|Road-150 Red, 56|$792,228.98|$382,159.24|$410,069.74|(null)|(null)|  
|Mountain-200 Black, 38|$1,471,078.72|(null)|$789,958.49|$681,120.23|(null)|  
|Road-350-W Yellow, 48|$1,380,253.88|(null)|(null)|$744,988.37|$635,265.50|  
  
 Isso é muito próximo do que nós estamos procurando; exceto porque a consulta retornou 9 e não 10 produtos, e o total de Todos os Produtos reflete a soma de todos os produtos, e não a soma dos 9 primeiros retornados (nesse caso). Outra tentativa para resolver o problema é apresentada na consulta MDX a seguir:  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , TOPCOUNT( [Product].[Product].CHILDREN, 10, [Measures].[Sales Amount]) ON 1  
  FROM [Adventure Works]  
```  
  
 Que retorna os seguintes resultados:  
  
|||||||  
|-|-|-|-|-|-|  
||Todos os Períodos|CY 2005|CY 2006|CY 2007|CY 2008|  
|Mountain-200 Black, 38|$1,634,647.94|(null)|(null)|$894,207.97|$740,439.97|  
|Mountain-200 Black, 42|$1,285,524.65|(null)|(null)|$722,137.65|$563,387.00|  
|Mountain-200 Silver, 38|$1,181,945.82|(null)|(null)|$634,600.78|$547,345.03|  
|Mountain-200 Black, 46|$995,927.43|(null)|(null)|$514,995.76|$480,931.68|  
|Mountain-200 Silver, 42|$1,005,111.77|(null)|(null)|$529,543.29|$475,568.49|  
|Mountain-200 Silver, 46|$975,932.56|(null)|(null)|$526,759.30|$449,173.26|  
|Road-150 Red, 56|$792,228.98|$382,159.24|$410,069.74|(null)|(null)|  
|Mountain-200 Black, 38|$1,471,078.72|(null)|$789,958.49|$681,120.23|(null)|  
|Road-350-W Yellow, 48|$1,380,253.88|(null)|(null)|$744,988.37|$635,265.50|  
|Road-150 Red, 62|$566,797.97|$234,018.86|$332,779.11|(null)|(null)|  
  
 Isso é muito próximo do resultado desejado, porque só faltou a soma dos produtos. Neste momento, você pode tentar consertar a expressão MDX acima para adicionar a linha perdida; porém, essa tarefa seria um incômodo.  
  
 Outra abordagem para resolver o problema seria redefinir o espaço do cubo sobre o qual a expressão MDX é resolvida. E se o 'novo' cubo somente contiver dados dos 10 principais produtos? Esse cubo terá o membro All ajustado somente para os 10 principais produtos e agora uma simples consulta resolveria o problema.  
  
 A expressão MDX a seguir usa uma instrução de subseleção para redefinir o espaço de cubo para os 10 principais produtos e gerar os resultados desejados:  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN  
                       , 10  
                       , [Measures].[Sales Amount]  
                       ) ON 0  
          FROM [Adventure Works]  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 A expressão acima retorna os seguintes resultados:  
  
|||||||  
|-|-|-|-|-|-|  
||Todos os Períodos|CY 2005|CY 2006|CY 2007|CY 2008|  
|Todos os Produtos|$19,997,183.30|$1,696,815.63|$2,816,611.28|$7,930,797.72|$7,552,958.66|  
|Mountain-200 Silver, 38|$2,160,981.60|(null)|(null)|$1,024,359.10|$1,136,622.49|  
|Mountain-200 Silver, 42|$1,914,547.85|(null)|(null)|$903,061.68|$1,011,486.18|  
|Mountain-200 Silver, 46|$1,906,248.55|(null)|(null)|$877,077.79|$1,029,170.76|  
|Mountain-200 Black, 38|$1,811,229.02|(null)|$896,511.60|$914,717.43|(null)|  
|Mountain-200 Black, 38|$2,589,363.78|(null)|(null)|$1,261,406.37|$1,327,957.41|  
|Mountain-200 Black, 42|$2,265,485.38|(null)|(null)|$1,126,055.89|$1,139,429.49|  
|Mountain-200 Black, 46|$1,957,528.24|(null)|(null)|$946,453.88|$1,011,074.37|  
|Road-150 Red, 62|$1,769,096.69|$828,011.68|$941,085.01|(null)|(null)|  
|Road-150 Red, 56|$1,847,818.63|$868,803.96|$979,014.67|(null)|(null)|  
|Road-350-W Yellow, 48|$1,774,883.56|(null)|(null)|$877,665.59|$897,217.96|  
  
 Os resultados acima são exatamente o que nós estamos procurando.  
  
 Vamos analisar o que exatamente a subseleção faz. A subseleção retornou para nós um novo cubo que continha todas as outras dimensões de produto como eles são; mas, na dimensão de produto, ela filtrou todos os membros para corresponder aos 10 primeiros produtos pelos quais estamos interessados. Era como se tivéssemos removido todos os dados que não atenderam ao critério de 10 primeiros e tivéssemos reconstruído o cubo. O outro conceito importante para entender neste exemplo é o fato de que os 10 primeiros produtos foram calculados sobre o membro All de todas as outras dimensões no cubo; o primeiro é verdadeiro porque nenhuma outra restrição de filtragem foi imposta na subseleção.  
  
 Subseleções podem ser tão complexas quanto você desejar; o exemplo a seguir ilustrará como gerar uma tabela semelhante à mencionada acima, mas filtrada por França na dimensão Território de Vendas e por Internet na dimensão Canal de Vendas.  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN  
                       , 10  
                       , [Measures].[Sales Amount]  
                       ) ON 0  
             , [Sales Territory].[Sales Territory].[Region].[France] on 1  
             ,  [Sales Channel].[Sales Channel].[Internet] on 2  
          FROM [Adventure Works]  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 Gerou os seguintes resultados:  
  
|||||||  
|-|-|-|-|-|-|  
||Todos os Períodos|CY 2005|CY 2006|CY 2007|CY 2008|  
|Todos os Produtos|$748,682.49|$32,204.43|$73,125.18|$269,506.56|$373,846.32|  
|Mountain-200 Silver, 38|$90,479.61|(null)|(null)|$41,759.82|$48,719.79|  
|Mountain-200 Silver, 42|$97,439.58|(null)|(null)|$39,439.83|$57,999.75|  
|Mountain-200 Silver, 46|$102,079.56|(null)|(null)|$27,839.88|$74,239.68|  
|Mountain-200 Black, 38|$26,638.28|(null)|$12,294.59|$14,343.69|(null)|  
|Mountain-200 Black, 38|$96,389.58|(null)|(null)|$41,309.82|$55,079.76|  
|Mountain-200 Black, 42|$80,324.65|(null)|(null)|$43,604.81|$36,719.84|  
|Mountain-200 Black, 46|$107,864.53|(null)|(null)|$45,899.80|$61,964.73|  
|Road-150 Red, 62|$46,517.51|$14,313.08|$32,204.43|(null)|(null)|  
|Road-150 Red, 56|$46,517.51|$17,891.35|$28,626.16|(null)|(null)|  
|Road-350-W Yellow, 48|$54,431.68|(null)|(null)|$15,308.91|$39,122.77|  
  
 Os resultados acima são os 10 primeiros produtos vendidos na França pela Internet.  
  
## <a name="subselect-statement"></a>Instrução Subselect  
 O BNF para o Subselect é:  
  
```  
[WITH [<calc-clause> ...]]  
SELECT [<axis-spec> [, <axis-spec> ...]]  
FROM [<identifier> | (< sub-select-statement >)]  
[WHERE <slicer>]  
[[CELL] PROPERTIES <cellprop> [, <cellprop> ...]]  
  
< sub-select-statement > :=  
   SELECT [<axis-spec> [, <axis-spec> ...]]  
   FROM [<identifier> | (< sub-select-statement >)]  
   [WHERE <slicer>]  
  
```  
  
 Subselect é outra instrução Select em que as especificações de eixo e a especificação de segmentação de dados filtram o espaço do cubo no qual a seleção externa é avaliada.  
  
 Quando um membro é especificado em um dos eixos ou cláusula de segmentação de dados, o membro com seus ascendentes e descendentes é incluído no espaço de subcubo para a subseleção; todos os membros irmãos não mencionados, no eixo ou na cláusula de segmentação de dados, e os seus descendentes são filtrados do subespaço. Desta maneira, o espaço da seleção externa foi limitado aos membros existentes na cláusula de eixo ou cláusula de segmentação de dados, com ascendentes e descendentes como mencionado acima.  
  
 Como o membro All de todas as dimensões não mencionadas em cláusulas de eixo ou de segmentação de dados pertencem ao espaço da seleção, então, todos os descendentes do membro All nessas dimensões são, também, parte do espaço da subseleção.  
  
 O membro All, em todas as dimensões, no espaço de subcubo, é reavaliado para refletir o impacto do restrições do novo espaço.  
  
 O exemplo a seguir mostrará o que foi dito acima; a primeira expressão MDX ajuda a exibir os valores não filtrados no cubo, o segundo MDX ilustra o efeito de se filtrar na cláusula Subselect:  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,  {[Measures].[Internet Sales Amount], [Measures].[Reseller Sales Amount]} ON 0  
  FROM [Adventure Works]  
```  
  
 Retorna os seguintes valores:  
  
||||  
|-|-|-|  
||Valor das Vendas pela Internet|Reseller Sales Amount|  
|All Customers|$29,358,677.22|$80,450,596.98|  
|Estados Unidos|$9,389,789.51|$80,450,596.98|  
|Oregon|$1,170,991.54|$80,450,596.98|  
|Portland|$110,649.54|$80,450,596.98|  
|Washington|$2,467,248.34|$80,450,596.98|  
|Seattle|$75,164.86|$80,450,596.98|  
  
 No exemplo anterior, Seattle é filho de Washington, Portland é filho de Oregon, Oregon e Washington são filhos de Estados Unidos e Estados Unidos é um filho de [Customer Geography]. [All Customers]. Todos os membros mostrados neste exemplo têm outros irmãos que contribuem para o valor de agregação pai; ou seja, Spokane, Tacoma e Everett são cidades irmãs de Seattle e todas elas contribuem para o Valor das Vendas pela Internet de Washington. O Valor das Vendas do Revendedor é independente do atributo Geografia de Cliente; consequentemente o valor Todos é exibido nos resultados. A próxima expressão MDX ilustra o efeito de filtragem da cláusula subselect:  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,  {[Measures].[Internet Sales Amount], [Measures].[Reseller Sales Amount]} ON 0  
  FROM ( SELECT [Customer].[State-Province].&[WA]&[US] ON 0  
           FROM [Adventure Works]  
        )  
```  
  
 Retorna os seguintes valores:  
  
||||  
|-|-|-|  
||Valor das Vendas pela Internet|Reseller Sales Amount|  
|All Customers|$2,467,248.34|$80,450,596.98|  
|United States|$2,467,248.34|$80,450,596.98|  
|Washington|$2,467,248.34|$80,450,596.98|  
|Seattle|$75,164.86|$80,450,596.98|  
  
 Os resultados acima mostram que somente ascendentes e descendentes do Estado de Washington fazem parte do subespaço em que a instrução SELECT externa foi avaliada; Oregon e Portland foram removidas do subcubo porque Oregon e todos os outros estados irmãos não foram mencionados na subseleção quando Washington foi mencionada.  
  
 O membro All foi ajustado para refletir o filtro em Washington; não foi ajustado apenas na dimensão [Geografia de Cliente], mas em todas as outras dimensões que cruzaram com [Geografia de Cliente]. Todas as dimensões que não cruzam com [Geografia de Cliente] permanecem inalteradas no subcubo.  
  
 As duas instruções MDX seguintes ilustram como o membro All em outras dimensões é ajustado para atender o efeito de filtragem da subseleção. A primeira consulta exibe os resultados inalterados e a segunda mostra o impacto da filtragem:  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,   [Product].[Product Line].MEMBERS ON 0  
  FROM [Adventure Works]  
 WHERE [Measures].[Internet Sales Amount]  
```  
  
||||||||  
|-|-|-|-|-|-|-|  
||Todos os Produtos|Acessórios|Componentes|Mountain|Road|Touring|  
|All Customers|$29,358,677.22|$604,053.30|(null)|$10,251,183.52|$14,624,108.58|$3,879,331.82|  
|Estados Unidos|$9,389,789.51|$217,168.79|(null)|$3,547,956.78|$4,322,438.41|$1,302,225.54|  
|Oregon|$1,170,991.54|$30,513.17|(null)|$443,607.98|$565,372.10|$131,498.29|  
|Portland|$110,649.54|$2,834.17|(null)|$47,099.91|$53,917.17|$6,798.29|  
|Washington|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Seattle|$75,164.86|$2,695.74|(null)|$19,914.53|$44,820.06|$7,734.54|  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,   [Product].[Product Line].MEMBERS ON 0  
  FROM ( SELECT [Customer].[State-Province].&[WA]&[US] ON 0  
           FROM [Adventure Works]  
        )  
 WHERE [Measures].[Internet Sales Amount]  
```  
  
||||||||  
|-|-|-|-|-|-|-|  
||Todos os Produtos|Acessórios|Componentes|Mountain|Road|Touring|  
|All Customers|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Estados Unidos|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Washington|$2,467,248.34|$62,662.92|(null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Seattle|$75,164.86|$2,695.74|(null)|$19,914.53|$44,820.06|$7,734.54|  
  
 Os resultados anteriores mostram que os valores de Todos os Produtos foram ajustados para somente valores do Estado de Washington, como esperado.  
  
 As subseleções podem ser aninhadas sem limite de profundidade para aninhar subseleções, exceto memória disponível. A subseleção mais interna define o subespaço inicial sobre o qual a filtragem é aplicada e passada para a próxima seleção externa. Observe que aninhar não é uma operação comutativa; portanto, a ordem na qual o aninhamento é definido pode produzir resultados diferentes. Os exemplos a seguir devem mostrar a diferença ao escolher uma ordem de aninhamento.  
  
```  
SELECT [Sales Territory].[Sales Territory Region].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN, 5, [Measures].[Sales Amount]) ON 0  
          FROM (SELECT TOPCOUNT( [Sales Territory].[Sales Territory Region].CHILDREN, 5, [Measures].[Sales Amount]) on 0  
                  FROM [Adventure Works]  
               )  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 Retornou os seguintes resultados.  
  
||||||||  
|-|-|-|-|-|-|-|  
||Todos os Territórios de Vendas|Australia|Canada|Central|Noroeste|Sudoeste|  
|Todos os Produtos|$7,591,495.49|$1,281,059.99|$1,547,298.12|$600,205.79|$1,924,763.50|$2,238,168.08|  
|Mountain-200 Silver, 38|$1,449,576.15|$248,702.93|$275,052.45|$141,103.65|$349,487.01|$435,230.12|  
|Mountain-200 Black, 38|$1,722,896.50|$218,024.05|$418,726.43|$123,929.46|$486,694.63|$475,521.93|  
|Mountain-200 Black, 42|$1,573,655.14|$239,137.96|$319,921.61|$130,102.75|$420,445.84|$464,046.98|  
|Mountain-200 Black, 46|$1,420,500.58|$192,320.16|$230,875.99|$117,044.49|$424,813.66|$455,446.27|  
|Road-150 Red, 56|$1,424,867.11|$382,874.89|$302,721.64|$88,025.44|$243,322.36|$407,922.78|  
  
```  
SELECT [Sales Territory].[Sales Territory Region].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Sales Territory].[Sales Territory Region].CHILDREN, 5, [Measures].[Sales Amount]) ON 0  
          FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN, 5, [Measures].[Sales Amount]) on 0  
                  FROM [Adventure Works]  
               )  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 Retornou os seguintes resultados.  
  
||||||||  
|-|-|-|-|-|-|-|  
||Todos os Territórios de Vendas|Australia|Canada|Noroeste|Sudoeste|United Kingdom|  
|Todos os Produtos|$7,938,218.56|$1,096,312.24|$1,474,255.49|$2,042,674.72|$2,238,099.55|$1,086,876.56|  
|Mountain-200 Silver, 38|$1,520,958.53|$248,702.93|$275,052.45|$349,487.01|$435,230.12|$212,486.03|  
|Mountain-200 Silver, 42|$1,392,237.14|$198,127.15|$229,679.01|$361,233.58|$407,854.24|$195,343.16|  
|Mountain-200 Black, 38|$1,861,703.23|$218,024.05|$418,726.43|$486,694.63|$475,521.93|$262,736.19|  
|Mountain-200 Black, 42|$1,702,427.25|$239,137.96|$319,921.61|$420,445.84|$464,046.98|$258,874.87|  
|Mountain-200 Black, 46|$1,460,892.41|$192,320.16|$230,875.99|$424,813.66|$455,446.27|$157,436.31|  
  
 Como você pode ver, há diferenças nos resultados entre ambos os conjuntos. A primeira consulta respondeu a pergunta de quais são os melhores produtos de venda nas primeiras 5 regiões, a segunda consulta respondeu a pergunta de onde são as maiores vendas dos 5 principais produtos.  
  
### <a name="remarks"></a>Comentários  
 As subseleções têm as seguintes restrições e limitações:  
  
-   A cláusula WHERE não filtra o subespaço.  
  
-   A cláusula WHERE somente altera o membro padrão no subcubo.  
  
-   A cláusula NON EMPTY não é permitida em uma cláusula de eixo. Em vez disso, use uma expressão de função [NonEmpty &#40;MDX&#41;](/sql/mdx/nonempty-mdx).  
  
-   A cláusula HAVING não é permitida em uma cláusula de eixo. Em vez disso, use uma expressão de função [Filter &#40;MDX&#41;](/sql/mdx/filter-mdx).  
  
-   Por padrão os membros calculados não são permitidos em subseleções; No entanto, essa restrição pode ser alterada, em uma base por sessão, atribuindo um valor para o `SubQueries` propriedade de cadeia de caracteres de conexão no <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> ou `DBPROP_MSMD_SUBQUERIES` propriedade na [propriedades XMLA com suporte &#40;XMLA&#41; ](../../xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md). Ver [membros calculados em subseleções e subcubos](calculated-members-in-subselects-and-subcubes.md) para obter uma explicação detalhada do comportamento de membros calculados dependendo dos valores de `SubQueries` ou `DBPROP_MSMD_SUBQUERIES`.  
  
  
