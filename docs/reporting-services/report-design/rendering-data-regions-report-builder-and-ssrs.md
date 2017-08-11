---
title: "Renderizando regiões de dados (construtor de relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4f3b2c7d-3669-457f-899b-b758d1db3426
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 99ca6c9509f25c118931ccab981987b3427e4b2d
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="rendering-data-regions-report-builder-and-ssrs"></a>Renderizando regiões de dados (Construtor de Relatórios e SSRS)
  Além dos comportamentos de renderização gerais que se aplicam a todos os itens de relatório, as regiões de dados têm comportamentos de paginação e renderização adicionais que elas adotam. As regras de renderização específicas por região de dados incluem como uma região de dados cresce, como as células especiais como as células de canto ou células de cabeçalho são renderizadas e como uma região de dados para leitura da direita para a esquerda é renderizada. Esse tópico aborda como as várias partes de uma região de dados são renderizadas.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="tablix-data-regions"></a>Regiões de dados Tablix  
 A região de dados tablix, que permite que você crie tabelas, matrizes e listas, é renderizada como uma grade composta de colunas e linhas. A interseção de uma linha e uma coluna é uma célula. Quando renderizada, essa célula pode conter dados e outros itens de relatório como imagens, retângulos, caixas de texto ou sub-relatórios. Uma região de dados tablix pode crescer na vertical e/ou horizontal. Além disso, a célula do canto, as células do cabeçalho da região de dados e as células do corpo da região de dados podem crescer com base em seu conteúdo. Se a região de dados ocupar várias páginas, os itens de relatório definidos para serem repetidos com a região de dados serão renderizados em cada página na qual a região de dados for exibida. Para obter mais informações, consulte [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
### <a name="right-to-left"></a>Da direita para a esquerda  
 Uma região de dados tablix definida para ser exibida da direita para a esquerda é renderizada com sua estrutura como uma imagem espelho da região de dados se ela tiver sido renderizada da esquerda para a direita. O canto da região de dados é exibido no canto superior direito. Se existirem colunas dinâmicas no relatório, eles expandirão para a esquerda. As configurações da direita para a esquerda não afetam a ordem dos dados na região de dados; suas colunas são simplesmente ordenadas de maneira diferente.  
  
### <a name="tablix-headers"></a>Cabeçalhos Tablix  
 Os cabeçalhos Tablix são renderizados como um cabeçalho de linha ou um cabeçalho de coluna, dependendo de onde a célula do cabeçalho é exibida na hierarquia do grupo de linhas ou da hierarquia do grupo de colunas. Se existir uma quebra de página lógica dentro do conteúdo da célula de um cabeçalho, ele será ignorado. As quebras de página lógicas em grupos de coluna são ignoradas.  
  
 As quebras de página lógicas em grupos não fazem com que os cabeçalhos de grupo externos sejam quebrados. Por exemplo, vamos supor que seu relatório tenha um grupo externo de países e um grupo interno de região de países. Se houver uma quebra de página lógica entre instância do grupo de região de país, o grupo externo, o país, aparecerá em ambas as páginas do relatório.  
  
#### <a name="repeated-tablix-headers"></a>Cabeçalhos Tablix repetidos  
 Quando a propriedade RepeatWith é definida no painel **Propriedades** , os itens que não são alterados na região de dados, como cabeçalhos de colunas, se repetem em cada página na qual essa parte da região de dados é renderizada. Por exemplo, se uma linha de dados for exibida na próxima página e a propriedade Repeat With for definida, os cabeçalhos de colunas serão exibidos na página renderizada também.  
  
### <a name="tablix-corner"></a>Canto do Tablix  
 O canto superior esquerdo é chamado canto tablix. O canto Tablix pode conter outros itens de relatórios nele, mas, se as quebras de página lógicas forem inseridas no canto, elas serão ignoradas quando a região de dados Tablix for renderizada.  
  
### <a name="tablix-body"></a>Corpo Tablix  
 O corpo Tablix é composto por células Tablix. O corpo Tablix é renderizado com base nos comportamentos de regras de paginação e renderização dos itens de relatório. Para obter mais informações, consulte [Renderizando itens de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md).  
  
## <a name="chart-gauge-and-map-data-regions"></a>Regiões de Dados Mapa, Medidor e Gráfico  
 As regiões de dados Gráfico, Medidor e Mapa se comportam como imagens quando elas são renderizadas e exibidas no corpo do relatório. Os valores na região de dados podem ter ações associadas, como link para outro relatório ou ir para um marcador; e essas ações podem ser renderizadas também, se o renderizador oferecer suporte a elas.  
  
## <a name="see-also"></a>Consulte também  
 [Paginação no Reporting Services &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Comportamentos de renderização &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Funcionalidade interativa para extensões &#40; de renderização de relatório diferente Construtor de relatórios e SSRS &#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Renderizando itens de relatório &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas de &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Gráficos de &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Medidores &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  
