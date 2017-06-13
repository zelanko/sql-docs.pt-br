---
title: "Região de dados Tablix (construtor de relatórios e SSRS) | Microsoft Docs"
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
ms.assetid: 99f83b32-4b86-4d40-973c-9a328d23ac8b
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cbe2dd936369c89b52302b1d244829dcb12744bc
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="tablix-data-region-report-builder-and-ssrs"></a>Região de dados Tablix (Construtor de Relatórios e SSRS)
  No, [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)], a região de dados Tablix é um item de relatório de layout generalizado que exibe dados de relatórios paginados em células organizadas em linhas e em colunas. Os dados do relatório podem ser dados detalhados, já que são recuperados da fonte de dados, ou dados detalhados agregados, organizados em grupos especificados. Cada célula tablix pode conter um item de relatório, como uma caixa de texto ou uma imagem, ou outra região de dados, como uma região, um gráfico ou um medidor tablix. Para adicionar vários itens de relatório a uma célula, adicione primeiro um retângulo para atuar como contêiner. Em seguida, adicione os itens de relatório ao retângulo.  
  
 A tabela, a matriz e as regiões de dados da lista são representadas na faixa de opções por modelos referentes à região de dados tablix subjacente. Ao adicionar um desses modelos a um relatório, você está, na verdade, adicionando uma região de dados tablix otimizada para um layout de dados específico. Por padrão, um modelo de tabela exibe dados detalhados em um layout de grade, uma matriz exibe dados do grupo em um layout de grade e uma lista, dados detalhados em um layout sem-forma.  
  
 Por padrão, cada célula tablix de uma tabela ou matriz contém uma caixa de texto. A célula de uma lista contém um retângulo. É possível substituir um item de relatório padrão por outro item de relatório, como uma imagem.  
  
 Quando você define grupos para uma tabela, matriz ou lista, o Construtor de Relatórios ou Designer de Relatórios adiciona linhas e colunas à região de dados tablix em que os dados agrupados são exibidos.  
  
 Para entender a região de dados Tablix, é recomendado entender o seguinte:  
  
*   A diferença entre dados detalhados e dados agrupados.  
  
*   Grupos, que são organizados como membros de hierarquias de grupo no eixo horizontal como grupos de linhas, e no eixo vertical como grupos de colunas.  
  
*  A finalidade das células tablix nas quatro áreas de uma região de dados tablix: o corpo, os cabeçalhos do grupo de linhas, os cabeçalhos do grupo de colunas e o canto.  
  
*  Linhas e colunas estáticas e dinâmicas, além de como elas se relacionam com os grupos.  
  
 Este artigo esclarece esses conceitos para explicar a estrutura que o Construtor de Relatórios e o Designer de Relatórios adicionam quando você adiciona modelos e cria grupos, permitindo que você modifique a estrutura de acordo com as suas necessidades. O Construtor de Relatórios e o Designer de Relatórios fornecem vários indicadores visuais para ajudá-lo a reconhecer a estrutura da região de dados tablix. Para obter mais informações, consulte [Células, linhas e colunas da região de dados Tablix &#40;Construtor de Relatórios&#41; e SSRS](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="understanding-detail-and-grouped-data"></a>Entendendo dados detalhados e agrupados  
 Detalhados são todos os dados de um conjunto de dados de relatório quando voltam da fonte de dados. Os dados detalhados são essencialmente o que você vê no painel de resultados do designer de consulta ao executar uma consulta de conjunto de dados. Entre os dados detalhados reais estão campos calculados criados por você e que são restringidos por filtros definidos no conjunto de dados, na região de dados e no grupo detalhado. Você exibe dados detalhados em uma linha detalhada usando uma expressão simples como, por exemplo, [Quantidade]. Quando o relatório é executado, a linha detalhada se repete uma vez para cada linha dos resultados da consulta em tempo de execução.  
  
 Os dados agrupados são dados detalhados organizados por um valor especificado na definição de grupo, como [SalesOrder]. Você exibe dados agrupados em linhas e colunas de grupo usando expressões simples que agregam os dados agrupados, como [Soma (Quantidade)]. Para obter mais informações, consulte [Compreendendo grupos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
## <a name="understanding-group-hierarchies"></a>Entendendo hierarquias de grupo  
 Grupos são organizados como membros de hierarquias de grupo. As hierarquias dos grupos de linhas e de colunas são estruturas idênticas em eixos diferentes. Pense nos grupos de linhas sendo expandidos na página para baixo e nos grupos de colunas sendo expandidos na página lateralmente.  
  
 Uma estrutura de árvore representa grupos de linhas e colunas aninhadas com uma relação pai/filho, como uma categoria com subcategorias. O grupo pai é a raiz da árvore; os grupos filho, suas ramificações. Os grupos também podem ter uma relação independente e adjacente, como vendas por território e vendas por ano. Várias hierarquias de árvore não relacionadas são chamadas de floresta. Em uma região de dados tablix, grupos de linhas e de colunas são individualmente representados como florestas independentes. Para obter mais informações, consulte [Compreendendo grupos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
## <a name="understanding-tablix-data-region-areas"></a>Entendendo as áreas da região de dados tablix  
 Uma região de dados tablix tem quatro áreas possíveis para células: o canto tablix, a hierarquia do grupo de linhas tablix, a hierarquia do grupo de colunas tablix ou o corpo tablix. Sempre há um corpo tablix. As demais áreas são opcionais.  
  
 As células na área do corpo tablix exibem dados detalhados e agrupados.  
  
 As células na área Grupos de Linhas são criadas automaticamente quando você cria um grupo de linhas. Essas são células do cabeçalho do grupo de linhas e, por padrão, exibem valores da instância de grupo da linha. Por exemplo, quando você agrupa por [SalesOrder], os valores de instância de grupo são as ordens de venda individuais pelas quais você está agrupando.  
  
 As células na área Grupos de Colunas são criadas automaticamente quando você cria um grupo de colunas. Essas são células do cabeçalho do grupo de colunas e, por padrão, exibem valores da instância do grupo de colunas. Por exemplo, quando você agrupa por [Ano], os valores da instância de grupo são os anos individuais pelos quais você está agrupando.  
  
 As células no canto tablix são área criadas automaticamente quando você tem grupos de linhas e de colunas definidos. As células nessa área podem exibir rótulos, ou é possível mesclá-las e criar um título.  
  
 Para obter mais informações, consulte [Áreas da região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tablix-data-region-areas-report-builder-and-ssrs.md).  
  
## <a name="understanding-static-and-dynamic-rows-and-columns"></a>Compreendendo linhas e colunas estáticas e dinâmicas  
 Uma região de dados tablix organiza células em linhas e colunas associadas a grupos. As estruturas de grupo para grupos de linhas e colunas são idênticas. Este exemplo usa grupos de linhas, mas é possível aplicar os mesmos conceitos a grupos de colunas.  
  
 Uma linha é estática ou dinâmica. Uma linha estática não é associada a um grupo. Quando o relatório é executado, uma linha estática é renderizada uma vez. Cabeçalhos e rodapés de tabela são linhas estáticas. Linhas estáticas exibem rótulos e totais. O escopo das células de uma linha estática é a região de dados.  
  
 Uma linha dinâmica é associada a um ou mais grupos. Uma linha dinâmica é renderizada uma vez para cada valor de grupo exclusivo do grupo interno. O escopo das células de uma linha dinâmica é o grupo de linhas e de colunas interno ao qual a célula pertence.  
  
 As linhas dinâmicas detalhadas são associadas ao grupo Detalhes, criado automaticamente quando você adiciona uma tabela ou lista à superfície de design. Por definição, Detalhes é o grupo interno de uma região de dados tablix. As células das linhas detalhadas exibem dados detalhados.  
  
 As linhas dinâmicas agrupadas são criadas quando você adiciona um grupo de linhas ou de colunas a uma região de dados tablix existente. As células das linhas dinâmicas agrupadas exibem valores agregados referentes ao escopo padrão.  
  
 O recurso Adicionar Total cria automaticamente uma linha fora do grupo atual no qual os valores de escopo do grupo são exibidos. Também é possível adicionar manualmente linhas estáticas e dinâmicas. Os indicadores visuais ajudam a compreender quais linhas são estáticas e quais são dinâmicas. Para obter mais informações, consulte [Células, linhas e colunas da região de dados Tablix &#40;Construtor de Relatórios&#41; e SSRS](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Vinculando várias regiões de dados ao mesmo conjunto de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [Controlando a exibição da região de dados Tablix em uma página do relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md)   
 [Explorando a flexibilidade de uma região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
