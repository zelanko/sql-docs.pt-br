---
title: Controlando títulos de linha e coluna (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4be6e836-158e-4bc9-8870-7f394d7c7e11
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eb1a0a862d3e6bf2a1d4e4361e2151c6ee4bf843
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176846"
---
# <a name="controlling-row-and-column-headings-report-builder-and-ssrs"></a>Controlando títulos de linha e coluna (Construtor de Relatórios e SSRS)
  Uma tabela, matriz ou região de dados de lista pode conter várias páginas no sentido horizontal ou vertical. Você pode especificar se deseja repetir cabeçalhos de linha ou coluna em cada página. Em um renderizador interativo, como o Gerenciador de Relatórios ou visualização de relatório, você pode especificar também se deseja congelar cabeçalhos de linha ou coluna para mantê-los na exibição quando você percorre um relatório. Em uma tabela ou matriz, a primeira linha contém normalmente cabeçalhos de coluna que rotulam dados em cada coluna; a primeira coluna normalmente contém cabeçalhos de linha que rotulam os dados em cada linha. Para grupos aninhados, talvez você queira repetir o conjunto inicial de cabeçalhos de linha e coluna que contêm rótulos de grupo. Por padrão, uma região de dados de lista não inclui cabeçalhos.

 O modo como você controla se os cabeçalhos se repetem ou congelam depende do seguinte:

-   Para cabeçalhos de coluna que se repetem na parte superior de cada página:

    -   Se a tabela ou matriz tiver uma área de grupo de colunas que se expanda horizontalmente.

    -   Se você quiser controlar todas as linhas associadas a grupos de colunas como uma unidade.

-   Para cabeçalhos de linha que se repetem ao longo de cada página:

    -   Se a tabela ou matriz tiver uma área de grupo de linhas que se expanda verticalmente. Somente são suportados cabeçalhos de linha para grupos de linhas com um cabeçalho de grupo de linhas.

> [!NOTE]
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]

## <a name="understanding-rows-and-columns-in-a-tablix-data-region"></a>Compreendendo as linhas e colunas em uma região de dados Tablix
 Uma tabela ou matriz é um modelo para a região de dados tablix subjacente. Uma região de dados tablix tem quatro áreas possíveis: a área do grupo de linhas que controla linhas que se expandem por um relatório, a área do grupo de colunas que controla as colunas que se expandem em um relatório, o corpo que exibe dados e o canto. Para entender onde definir propriedades para controlar a repetição ou o congelamento de cabeçalhos, é útil entender que há duas representações para uma região de dados tablix:

-   **Na definição de relatório** Cada linha ou coluna em uma definição de região de dados tablix é um membro tablix de um grupo específico de linhas ou colunas. Um membro tablix é estático ou dinâmico. Um membro tablix estático contém rótulos ou subtotais e se repete uma vez por grupo. Um membro tablix dinâmico contém valores de grupo e se repete uma vez por valor exclusivo de um grupo, também conhecido como instância de grupo.

-   **Na superfície de design** Na superfície de design, as linhas pontilhadas dividem uma região de dados tablix nas quatro áreas. Cada célula em uma área da região de dados tablix é organizada em linhas e colunas. As linhas e as colunas são associadas a grupos, inclusive o grupo de detalhes. Para uma região de dados tablix selecionada, as linha e as colunas e administram e realçam as barras que indicam associação em grupo. As células na área do grupo de linhas ou de grupo de colunas representa cabeçalhos de grupo para membros tablix. Uma única linha ou coluna pode ser associada a vários grupos.

     Para obter mais informações, consulte [Região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md) e [Células, linhas e colunas da região de dados Tablix &#40;Construtor de Relatórios&#41; e SSRS](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).

 Para regiões de dados tablix com áreas de grupos de linhas ou colunas, controle as linhas e as colunas associadas definindo propriedades na região de dados tablix. Para todos os outros casos, controle as linhas e as colunas definindo propriedades no painel Propriedades para o membro tablix selecionado. Para obter instruções passo a passo, consulte [Exibir cabeçalhos de linhas e colunas em várias páginas e &#40;Construtor de Relatórios e SSRS&#41;](display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md) e [Manter os cabeçalhos visíveis ao rolar por um relatório &#40;Construtor de Relatórios e SSRS&#41;](keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md).

##  <a name="examples"></a><a name="Top"></a> Exemplos
 Os exemplos mais comuns de regiões de dados tablix são para uma matriz, uma tabela sem grupos, e uma tabela com um grupo de linhas e um cabeçalho de grupo de linhas e uma tabela com um grupo de linhas, mas nenhum cabeçalho de grupo de linhas. Para controlar o modo como repetir ou congelar cabeçalhos, você deve determinar se as linhas ou as colunas que deseja controlar estão associadas a um cabeçalho de grupo na área de grupos de linhas ou grupos de colunas.

 As seções seguintes fornecem exemplos para layouts comuns para uma região de dados tablix:

-   [Tabela](#Matrix)

-   [Tabela sem grupos](#TableNoGroups)

-   [Tabela com grupos de linhas e área de grupo de linhas](#TableRowGroupsGroupHeader)

-   [Tabela com grupos de linhas, mas nenhuma área de grupo de linhas](#TableRowGroupsNoGroupHeader)

###  <a name="matrix"></a><a name="Matrix"></a>Tabela
 Por padrão, uma matriz simples tem um grupo de linhas e um grupo de colunas. A figura seguinte mostra uma matriz com um grupo de linhas baseado na Categoria e um grupo de colunas baseado na Geografia:

 ![Matriz, linha Categoria e grupo de colunas Geografia](../media/rs-basicmatrixdesign.gif "Matriz, linha Categoria e grupo de colunas Geografia")

 As linhas pontilhadas mostram as quatro áreas de tablix. A área de grupo de linhas tem um cabeçalho de grupo de linhas que controla os rótulos da categoria na primeira coluna. De modo semelhante, a área do grupo de colunas tem um cabeçalho de grupo de colunas que controla os rótulos geográficos na primeira linha. Na visualização, à medida que a matriz se expande pela página, a primeira linha exibe os cabeçalhos de coluna, como mostrado na figura seguinte:

 ![Visualização de matriz renderizada com grupos expandidos](../media/rs-basicmatrixpreview.gif "Visualização de matriz renderizada com grupos expandidos")

 Para repetir ou congelar cabeçalhos de coluna na primeira linha, defina as propriedades para cabeçalhos de coluna na região de dados tablix. Cabeçalhos de coluna para grupos de colunas aninhados são incluídos automaticamente.

 Para repetir ou congelar cabeçalhos de linha na primeira coluna, defina as propriedades para cabeçalhos de linha na região de dados tablix. Cabeçalhos de linha para grupos de linha aninhados são incluídos automaticamente.

 [Voltar ao início](#Top)

###  <a name="table-with-no-row-groups"></a><a name="TableNoGroups"></a>Tabela sem grupos de linhas
 Por padrão, uma tabela simples sem grupos inclui o grupo de detalhes. A figura seguinte mostra uma tabela que exibe a categoria, o número do pedido e os dados da venda:

 ![Design, tabela com uma linha estática e uma dinâmica](../media/rs-tableheaderstaticdesign.gif "Design, tabela com uma linha estática e uma dinâmica")

 Não há nenhuma linha pontilhada porque a tabela consiste apenas na área de corpo do tablix. A primeira linha exibe cabeçalhos de coluna e representa um membro tablix estático que não é associado a um grupo. A segunda linha exibe dados de detalhes e representa um membro tablix dinâmico associado ao grupo de detalhes. A seguinte figura mostra a tabela na visualização:

 ![Visualização, tabela com uma linha estática e uma dinâmica](../media/rs-tableheaderstaticpreview.gif "Visualização, tabela com uma linha estática e uma dinâmica")

 Para repetir ou congelar cabeçalhos de colunas, defina as propriedades no membro tablix da linha estática que faz parte da definição da região de dados tablix. Para selecionar a linha estática, você deve usar o modo Avançado do painel Agrupamento. A figura seguinte mostra o painel Grupos de Linhas:

 ![Grupos de linhas, tabela com uma linha estática e uma linha dinâmica](../media/rs-tableheaderstaticgroupingpanedefault.gif "Grupos de linhas, tabela com uma linha estática e uma linha dinâmica")

 No modo Avançado, a figura seguinte mostra os membros tablix estáticos e dinâmicos para os grupos de linhas na tabela:

 ![Grupos de linhas, Avançado para tabela padrão](../media/rs-tableheaderstaticgroupingpaneadvanced.gif "Grupos de linhas, Avançado para tabela padrão")

 Para repetir ou congelar cabeçalhos de colunas para o membro tablix, selecione a linha estática rotulada (**Estático**). O painel de propriedades exibe as propriedades do membro tablix selecionado. Definindo propriedades para esse membro tablix, você pode controlar o modo como a primeira linha se repete ou permanece visível.

 [Voltar ao início](#Top)

###  <a name="table-with-row-groups-and-a-row-group-area"></a><a name="TableRowGroupsGroupHeader"></a>Tabela com grupos de linhas e uma área de grupo de linhas
 Se você adicionar um grupo de linhas a uma tabela simples, uma área de grupo de linhas será adicionada à tabela na superfície de design. A figura seguinte mostra uma tabela com um grupo de linhas baseado na Categoria:

 ![Design, tabela com grupo de uma linha e detalhes](../media/rs-tableheaderdynamicwithgroupheadercelldesign.gif "Design, tabela com grupo de uma linha e detalhes")

 As linhas pontilhadas mostram a área dos grupos de linhas tablix e a área do corpo tablix. A área de grupo de linhas tem um cabeçalho de grupo de linhas, mas nenhum cabeçalho de grupo de colunas. A figura seguinte mostra essa tabela na visualização:

 ![Visualização, tabela com grupo de uma linha e detalhes](../media/rs-tableheaderdynamicwithgroupheadercellpreview.gif "Visualização, tabela com grupo de uma linha e detalhes")

 Para repetir ou congelar cabeçalhos de coluna, use a mesma abordagem do exemplo anterior. A figura seguinte mostra a exibição padrão do painel Grupos de Linhas:

 ![Grupos de linhas, padrão com membros dinâmicos](../media/rs-tableheaderdynamicgroupingpanedefault.gif "Grupos de linhas, padrão com membros dinâmicos")

 Use o modo **Avançado** do painel Grupos de Linhas para exibir os membros tablix, como mostrado na figura seguinte:

 ![Grupos de linhas, modo Avançado com membros estáticos](../media/rs-tableheaderdynamicwithgroupheadercelladvanced.gif "Grupos de linhas, modo Avançado com membros estáticos")

 Para membros tablix são listados os itens: **Estático**, (**Estático**), Categoria e (**Detalhes**). Um membro tablix que inclui parênteses () indica que não há nenhum cabeçalho de grupo correspondente. Para repetir ou congelar cabeçalhos de coluna, selecione o membro tablix Estático superior e defina as propriedades no painel Propriedades.

 [Voltar ao início](#Top)

###  <a name="table-with-row-groups-and-no-row-group-area"></a><a name="TableRowGroupsNoGroupHeader"></a>Tabela com grupos de linhas e nenhuma área de grupo de linhas
 Uma tabela pode ter grupos de linhas, mas nenhuma área de grupos de linhas de vários modos. Dois modos possíveis que isso ocorra incluem:

-   Comece com uma tabela com grupos de linhas e uma área de grupo de linhas e exclua as colunas para a área de grupo de linhas. Exclua as colunas apenas e não os grupos. Por exemplo, talvez você queira controlar o formato de tabela para ser uma grade simples.

-   Atualize um relatório que foi criado para uma versão de RDL anterior, antes da introdução das regiões de dados tablix.

 A figura seguinte mostra uma tabela com um grupo de linhas, mas nenhuma área do grupo de linhas na superfície de design:

 ![Design, tabela tem grupo de linhas, mas nenhum cabeçalho de grupo](../media/rs-tableheaderdynamicwithnogroupheadercelldesign.gif "Design, tabela tem grupo de linhas, mas nenhum cabeçalho de grupo")

 A tabela tem três linhas. A primeira linha contém cabeçalhos de coluna. A segunda linha contém o valor de grupo e os subtotais. A terceira linha contém os dados de detalhes. Não há nenhuma linha pontilhada porque há apenas uma área de corpo do tablix. A figura seguinte mostra essa tabela na visualização:

 ![Visualização, tabela tem grupo de linhas, mas nenhum cabeçalho de grupo](../media/rs-tableheaderdynamicwithnogroupheadercellpreview.gif "Visualização, tabela tem grupo de linhas, mas nenhum cabeçalho de grupo")

 Para controlar o modo como as linhas se repetem ou permanecem visíveis, você deve definir propriedades no membro tablix para cada linha. No modo padrão, não há nenhuma diferença entre esse exemplo e o exemplo anterior para uma tabela com um grupo de linhas e um cabeçalho de grupo. A figura seguinte mostra o painel Agrupamento no modo padrão para essa tabela:

 ![Grupos de linhas, padrão com membros dinâmicos](../media/rs-tableheaderdynamicgroupingpanedefault.gif "Grupos de linhas, padrão com membros dinâmicos")

 No entanto, no modo avançado, essa estrutura de layout mostra um conjunto diferente de membros tablix. A figura seguinte mostra o painel Agrupamento no modo avançado para essa tabela:

 ![Grupos de linhas, Avançado, sem cabeçalho de grupo.](../media/rs-tableheaderdynamicwithnogroupheadercelladvanced.gif "Grupos de linhas, Avançado, sem cabeçalho de grupo.")

 No painel Grupos de Linhas, os membros tablix seguintes são listados: (**Estático**), (Categoria), (**Estático**) e (**Detalhes**). Para repetir ou congelar cabeçalhos de coluna, selecione o membro tablix (**Estático**) superior e defina as propriedades no painel Propriedades.

 [Voltar ao início](#Top)

## <a name="renderer-support-for-repeating-or-freezing-headers"></a>Suporte de renderizador para repetir ou congelar cabeçalhos
 Os renderizadores variam no suporte para a repetição ou o congelamento de cabeçalhos.

 Os renderizadores que usam páginas físicas (PDF, Imagem, Impressão) suportam os recursos seguintes:

-   Repetição de cabeçalhos de linha quando uma região de dados tablix se expande horizontalmente por várias páginas.

-   Repetição de cabeçalhos de coluna quando uma região de dados tablix se expande verticalmente por várias páginas.

 Além disso, os renderizadores que usam quebras de páginas flexíveis (Gerenciador de Relatórios, visualização de relatório ou controle de visualizador de relatório) oferece suporte aos seguintes recursos:

-   Mantenha cabeçalhos de linha na exibição quando você percorrer horizontalmente um relatório.

-   Mantenha cabeçalhos de coluna na exibição quando você percorrer verticalmente um relatório.

 Para obter mais informações, consulte [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md).

## <a name="see-also"></a>Consulte Também
 [Filtrar, agrupar e classificar dados &#40;Construtor de relatórios e ssrs&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md) [listas &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md) [paginação em Reporting Services &#40;Construtor de relatórios e SSRS&#41;](pagination-in-reporting-services-report-builder-and-ssrs.md) [exportar relatórios &#40;Construtor de relatórios e SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)


