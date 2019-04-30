---
title: Controlando a exibição de região de dados Tablix em uma página de relatório (construtor de relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f81c48cc-f038-4f57-988d-e9a3cbb46424
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3f740965cdc0b3c17e1a889975fae72bf37a85a6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63206509"
---
# <a name="controlling-the-tablix-data-region-display-on-a-report-page-report-builder-and-ssrs"></a>Controlando a exibição da região de dados Tablix em uma página do relatório (Construtor de Relatórios e SSRS)
  Este tópico descreve as propriedades de uma região de dados Tablix que pode ser modificada para alterar a forma como uma região de dados Tablix é exibida quando visualizada em um relatório.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="controlling-the-appearance-of-data"></a>Controlando a aparência dos dados  
 Os seguintes recursos ajudam a controlar a aparência de uma região de dados Tablix:  
  
-   **Formatando dados.** Para formatar dados em uma tabela, matriz ou lista, defina as propriedades de formato da caixa de texto na célula. É possível definir propriedades para várias células ao mesmo tempo. Para formatar dados em um gráfico, defina as propriedades de formatação na série. Para obter mais informações, consulte [Formatando itens de relatório &#40;Construtor de Relatórios e SSRS&#41;](formatting-report-items-report-builder-and-ssrs.md) e [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md).  
  
-   **Gravando expressões**. Para obter mais informações, consulte [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md) e [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md).  
  
-   **Controlando a ordem de classificação**. Para controlar a ordem de classificação, você deve definir expressões de classificação na região de dados. Para controlar a ordem de classificação das linhas e das colunas associadas a um grupo, você deve definir expressões de classificação no grupo, inclusive os grupos detalhados. Também é possível adicionar botões de classificação interativos para permitir que o usuário classifique uma região de dados Tablix ou seus grupos. Para obter mais informações, consulte [Classificar dados em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](sort-data-in-a-data-region-report-builder-and-ssrs.md).  
  
-   **Exibindo uma mensagem quando não há dados**. Quando não há dados de um conjunto de dados de relatório em tempo de execução, é possível escrever uma mensagem própria a ser exibida em lugar da região de dados. Para obter mais informações, consulte [Definir uma mensagem Nenhum Dado para uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](../report-data/set-a-no-data-message-for-a-data-region-report-builder-and-ssrs.md).  
  
-   **Ocultando dados condicionalmente**. Para controlar condicionalmente se deverá mostrar ou ocultar uma região de dados ou partes de uma região de dados, você pode definir a propriedade Hidden `True` ou como uma expressão. Entre as expressões podem estar referências a parâmetros de relatório. Também é possível especificar um item de alternância, para que usuário possa optar por exibir dados detalhados. Para obter mais informações, consulte [Ação de análise detalhada &#40;Construtor de Relatórios e SSRS&#41;](drilldown-action-report-builder-and-ssrs.md).  
  
-   **Mesclando células.** Várias células contíguas em uma tabela podem ser integradas em uma única célula. Isso é conhecido como abrangência de coluna ou mesclagem de célula. As células só podem ser combinadas horizontal ou verticalmente. Quando você mescla células, apenas os dados na primeira célula são preservados. Os dados das demais células são removidos. As células mescladas podem ser divididas nas colunas originais. Para obter mais informações, consulte [Mesclar células em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](merge-cells-in-a-data-region-report-builder-and-ssrs.md).  
  
## <a name="controlling-tablix-data-region-position-and-expansion-on-a-page"></a>Controlando a posição da região de dados Tablix e a expansão em uma página  
 Os seguintes recursos ajudam a controlar a forma como uma região de dados Tablix é exibida em um relatório renderizado:  
  
-   **Controlando a posição de uma região de dados Tablix em relação a outros itens de relatório**. Uma região de dados Tablix pode ser posicionada acima, próxima a, ou abaixo dos demais itens de relatório na superfície de design de relatório. Em tempo de execução, o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] expande a região de dados Tablix conforme necessário para os dados recuperados do conjunto de dados vinculado, movendo itens de relatório semelhantes além do necessário. Para ancorar um Tablix próximo a outro item de relatório, você deve criar os itens de relatório semelhantes e ajustar as posições relativas. Para obter mais informações, consulte [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md).  
  
-   **Alterando a direção de expansão**. Para controlar se uma região de dados tablix se expande na página LTR (da esquerda para direita) ou RTL (da direita para esquerda), use a propriedade Direction, que pode ser acessada na janela Propriedades. Para obter mais informações, consulte [Renderizando regiões de dados &#40;Construtor de Relatórios e SSRS&#41;](rendering-data-regions-report-builder-and-ssrs.md).  
  
## <a name="controlling-how-a-tablix-data-region-renders-on-a-page"></a>Controlando a forma de renderização de uma região de dados Tablix em uma página  
 A lista a seguir descreve modos que podem ajudar a controlar como uma região de dados Tablix aparece em um relatório:  
  
-   **Controlando a paginação**. Para controlar a quantidade de dados exibidos em todas as páginas de relatório, é possível definir quebras de página em regiões de dados. Você também pode definir quebras de página em grupos. As quebras de página podem afetar o desempenho da renderização sob demanda reduzindo a quantidade de dados que precisam ser processados em cada página. Para obter mais informações, consulte [Paginação no Reporting Services &#40;Construtor de Relatórios e SSRS&#41;](pagination-in-reporting-services-report-builder-and-ssrs.md) e [Adicionar uma quebra de página &#40;Construtor de Relatórios e SSRS&#41;](add-a-page-break-report-builder-and-ssrs.md).  
  
-   **Exibindo dados em qualquer lado dos cabeçalhos de linha**. Você não está limitado a exibir cabeçalhos de linha no lado de uma região de dados Tablix. É possível mover os cabeçalhos de linha entre colunas, para que as colunas de dados sejam exibidas antes dos cabeçalhos de linha. Para fazer isso, modifique a propriedade GroupsBeforeRowHeaders para a matriz. É possível acessar essa propriedade usando a janela Propriedades. O valor dessa propriedade é um inteiro. Por exemplo, um valor igual a 2 exibirá duas instâncias de grupos dos dados de coluna da região de dados antes da exibição da coluna que contém os cabeçalhos de linha.  
  
## <a name="controlling-how-tablix-row-and-column-groups-render"></a>Controlando como os grupos de linhas e de colunas Tablix são processados  
 A renderização dos grupos de regiões de dados Tablix depende da estrutura de grupo. Uma região de dados Tablix pode ter quatro áreas, como mostra a figura a seguir:  
  
 ![Tablix data region areas](../media/rs-tablixareas.gif "Tablix data region areas")  
  
 A área do grupo de linhas e a área do grupo de colunas contêm cabeçalhos de grupo. Quando uma região de dados Tablix tem cabeçalhos de grupo, você pode controlar a repetição de linhas e colunas definindo as propriedades na página **Geral** da caixa de diálogo **Propriedades do Tablix** .  
  
 Se uma região de dados Tablix tiver apenas uma área de corpo Tablix, não haverá nenhum cabeçalho de grupo. Só existem membros de tablix estáticos e dinâmicos. Um membro estático é exibido uma vez em relação a um grupo de linhas ou colunas Tablix. Um membro dinâmico ocorre uma vez para cada valor de grupo exclusivo. Por exemplo, em uma região de dados Tablix que exibe um pedido de vendas, os nomes de coluna podem ser exibidos no pedido de vendas em um membro de linha estático. Cada linha do pedido de vendas é exibido em um membro de linha dinâmico.  
  
 Você pode ajudar a controlar como um membro Tablix é processado definindo propriedades no painel Propriedades. Para obter mais informações, consulte “Modo avançado” em [Painel Agrupamento &#40;Construtor de Relatórios&#41;](grouping-pane-report-builder.md).  
  
 A lista a seguir descreve modos que podem ajudar a controlar como uma região de dados Tablix aparece em um relatório:  
  
-   **Repetindo cabeçalhos de linha e coluna em várias páginas**.É possível exibir cabeçalhos de linha e coluna em todas as páginas abrangidas em uma região de dados tablix. Para obter informações, consulte [Exibir cabeçalhos de linhas e colunas em várias páginas &#40;Construtor de Relatórios e SSRS&#41;](display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md).  
  
-   **Mantendo cabeçalhos de linha e coluna na exibição durante a rolagem**. É possível controlar se você deve manter os cabeçalhos de linha e coluna na exibição ao rolar um relatório usando um navegador. Para obter informações, consulte [Manter os cabeçalhos visíveis ao rolar por um relatório &#40;Construtor de Relatórios e SSRS&#41;](keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md).  
  
 Para obter mais informações sobre como a exportação de um relatório de formatos diferentes afeta a maneira como uma região de dados Tablix é renderizada em uma página, consulte [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Vinculando várias regiões de dados ao mesmo conjunto de dados &#40;Construtor de Relatórios e SSRS&#41;](linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [Regiões de dados aninhadas &#40;Construtor de Relatórios e SSRS&#41;](nested-data-regions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)   
 [Controlando quebras de páginas, títulos, colunas e linhas &#40;Construtor de Relatórios e SSRS&#41;](controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
 [Região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrizes &#40;Construtor de Relatórios e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
