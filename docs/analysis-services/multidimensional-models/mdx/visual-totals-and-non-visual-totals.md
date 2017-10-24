---
title: "Totais visuais e totais não visuais | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ea9d02f2-a668-4547-ade5-e3d077a2e1bd
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ee15de7e61b6ebf53fdbd6cb8f1fb3920c010134
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="visual-totals-and-non-visual-totals"></a>Totais visuais e totais não visuais
  Totais visuais são totais no final de uma coluna ou linha que somam todos os itens visíveis na coluna ou linha. Esse é o comportamento padrão da maioria das tabelas ao serem exibidas. Porém, ocasionalmente o usuário desejará exibir somente certas colunas em uma tabela, mas manter os totais da linha inteira, inclusive das colunas que não são exibidas. Esses são chamados de **Totais não visuais**, porque o total provém de valores tanto visíveis como não visíveis.  
  
 O cenário a seguir demonstra o comportamento dos totais Não Visuais. A primeira etapa mostra o comportamento padrão dos Totais Visuais.  
  
 O exemplo a seguir é uma consulta da [Adventure Works] para obter números de [Valor das Vendas do Revendedor] em uma tabela em que as categorias de produto são as colunas e os tipos de negócios dos revendedores são as linhas. Observe que são fornecidos totais para produtos e revendedores quando a seguinte instrução SELECT é emitida:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Gera os seguintes resultados:  
  
|||||||  
|-|-|-|-|-|-|  
||**Todos os Produtos**|**Acessórios**|**Bikes**|**Clothing**|**Componentes**|  
|**Todos os Revendedores**|**$80,450,596.98**|**$571,297.93**|**$66,302,381.56**|**$1,777,840.84**|**$11,799,076.66**|  
|**Specialty Bike Shop**|**$6,756,166.18**|**$65,125.48**|**$6,080,117.73**|**$252,933.91**|**$357,989.07**|  
|**Revendedor de Valor Agregado**|**$34,967,517.33**|**$175,002.81**|**$30,892,354.33**|**$592,385.71**|**$3,307,774.48**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$29,329,909.50**|**$932,521.23**|**$8,133,313.11**|  
  
## <a name="non-visual-on-rows-and-columns"></a>Não visual em linhas e colunas  
 Para produzir uma tabela somente com dados dos produtos Accessories e Clothing, revendedores Value Added Reseller e Warehouse, mas mantendo os totais gerais, o seguinte poderia ser escrito usando NON VISUAL:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works])`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Gera os seguintes resultados:  
  
|||||  
|-|-|-|-|  
||**Todos os Produtos**|**Acessórios**|**Clothing**|  
|**Todos os Revendedores**|**$80,450,596.98**|**$571,297.93**|**$1,777,840.84**|  
|**Revendedor de Valor Agregado**|**$34,967,517.33**|**$175,002.81**|**$592,385.71**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$932,521.23**|  
  
## <a name="non-visual-on-rows"></a>Não visual em linhas  
 Para criar uma tabela que totalize visualmente as colunas, mas nos totais de linhas exiba o total verdadeiro de todos os itens em [Category], a seguinte consulta deve ser emitida:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0`  
  
 `from ( Select {[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 0`  
  
 `from [Adventure Works])`  
  
 `)`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Observe como NON VISUAL é aplicado somente a [Category].  
  
 A consulta anterior gera os seguintes resultados:  
  
|||||  
|-|-|-|-|  
||Todos os Produtos|Acessórios|Clothing|  
|Todos os Revendedores|$73,694,430.80|$506,172.45|$1,524,906.93|  
|Revendedor de Valor Agregado|$34,967,517.33|$175,002.81|$592,385.71|  
|Warehouse|$38,726,913.48|$331,169.64|$932,521.23|  
  
 Quando comparados aos resultados anteriores, você poderá observar que a linha [Todos os Revendedores] agora soma os valores exibidos para [Revendedor de Valor Agregado] e [Warehouse], mas a coluna [Todos os Produtos] mostra o valor total para todos os produtos, inclusive aqueles não exibidos.  
  
## <a name="see-also"></a>Consulte também  
 [Principais conceitos em MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [Autoexists](../../../analysis-services/multidimensional-models/mdx/autoexists.md)   
 [Trabalhando com membros, tuplas e conjuntos &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [Conceitos básicos de consulta MDX &#40; Analysis Services &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)   
 [A consulta MDX básica &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md)   
 [Restringindo a consulta com a consulta e os eixos de segmentação de dados &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md)   
 [Estabelecendo o contexto de cubo em uma consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)  
  
  

