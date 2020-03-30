---
title: Regiões de dados e mapas (Construtor de Relatórios) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
helpviewer_keywords:
- data regions
ms.assetid: 3afb8874-b36c-4e44-a0d8-80d2f7135fb1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5cdc8e2cb16b4a73122ffbdc60a845a3b258a108
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77080544"
---
# <a name="data-regions-and-maps-report-builder-and-ssrs"></a>Regiões de dados e mapas (Construtor de Relatórios e SSRS)
  Uma região de dados é um relatório que exibe dados de um conjunto de dados do relatório. Os dados do relatório podem ser exibidos como números e texto em uma tabela, matriz ou lista; graficamente em um gráfico ou medidor; e sobre um plano de fundo geográfico em um mapa. Tabelas, matrizes e listas se baseiam na região de dados *tablix* , que se expande conforme o necessário para exibir todos os dados do conjunto de dados. Uma região de dados tablix oferece suporte a vários grupos de linhas e colunas e a linhas, bem como colunas estáticas e dinâmicas. Um gráfico exibe vários grupos de categorias e séries em diversos formatos de gráfico. Um medidor exibe um único valor ou um valor agregado para um conjunto de dados. Um mapa exibe dados espaciais como elementos do mapa cuja aparência pode variar com base nos dados agregados de um conjunto de dados.  
  
 Você pode salvar uma região ou um mapa de dados como *parte de um relatório*. Leia mais sobre as [Partes do relatório](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="table"></a>Tabela  
 Uma tabela é uma região de dados que apresenta dados linha a linha. Colunas da tabela são estáticas: você determina o número de colunas quando você cria seu relatório. Linhas da tabela são dinâmicas: elas se expandem para baixo para acomodar os dados. Você pode adicionar grupos às tabelas, organizando os dados selecionados por campos ou expressões. Para obter informações sobre como adicionar uma tabela a um relatório, consulte [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md).  
  
## <a name="matrix"></a>Matriz  
 Uma matriz também é conhecida como uma tabela de referência cruzada. Uma região de dados de matriz contém as colunas e linhas dinâmicas: elas se expandem para acomodar os dados. As colunas e as linhas de uma matriz podem ser dinâmicas ou estáticas. As colunas ou as linhas podem conter outras colunas ou linhas e podem ser usadas para agrupar dados. Leia mais sobre [como adicionar uma matriz a um relatório](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md).  
  
## <a name="list"></a>Lista  
 Uma lista é uma região de dados que apresenta dados organizados de uma forma livre. Você pode organizar os itens de relatório para criar um formulário com caixas de texto, imagens e outras regiões de dados posicionadas em qualquer local dentro da lista. Leia mais sobre [como adicionar uma lista a um relatório](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md).  
  
## <a name="chart"></a>Gráfico  
 Um gráfico apresenta os dados de maneira gráfica. Os exemplos de gráficos incluem barra, pizza e gráficos de linhas, mas muitos outros estilos podem ser considerados. Leia mais sobre [como adicionar um gráfico a um relatório](../../reporting-services/report-design/charts-report-builder-and-ssrs.md).  
  
## <a name="gauge"></a>Medidor  
 Um medidor apresenta os dados como um intervalo com um indicador apontando para um valor específico dentro do intervalo. Os indicadores são usados para exibir KPIs (indicadores chave de desempenho) e outras métricas. Os exemplos de medidores incluem linear e circular. Leia mais sobre [como adicionar um medidor a um relatório](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md).  
  
## <a name="map"></a>Mapeamento  
 Um mapa permite a você apresentar dados em relação a um plano de fundo geográfico. Dados de mapa podem ser dados espaciais de uma consulta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , um arquivo de forma ESRI ou peças de mapa do Bing [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Os dados espaciais consistem em conjuntos de coordenadas que definem polígonos que representam formas ou áreas, linhas que representam rotas ou caminhos e pontos representados por marcadores. Você pode associar dados de agregação a elementos do mapa para variar a cor e o tamanho deles automaticamente. Por exemplo, você pode variar o tipo de marcador de uma loja com base na quantidade de vendas ou na cor de uma estrada com base no limite de velocidade. Para obter mais informações, consulte [Mapas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md).  
  
## <a name="data-regions-in-the-report-layout"></a>Regiões de dados no layout do relatório  
 Você pode adicionar várias regiões de dados a um relatório. As regiões de dados crescem para acomodar os dados do conjunto de dados do relatório ao qual estão vinculadas. Por exemplo, uma matriz que exibe as vendas de cada produto por ano tem um grupo de linhas baseado em nomes de produtos e um grupo de colunas baseado no ano. Quando você executar o relatório, a matriz se expandirá para baixo na página para cada produto e para o lado para cada ano. Um gráfico colocado próximo à matriz na superfície de design do relatório é exibido próximo à matriz expandida no relatório renderizado. O modo de renderização das regiões em uma página segue um conjunto de regras baseado no formato de saída de um relatório. Por exemplo, para ajudar a controlar o modo como um gráfico e uma matriz são renderizados em uma página, é possível usar um retângulo como um contêiner ou aninhar regiões de dados em uma lista. Para obter mais informações, consulte [Layout da página e renderização &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/page-layout-and-rendering-report-builder-and-ssrs.md).  
  
## <a name="nested-data-regions"></a>Regiões de dados aninhadas  
 É possível aninhar regiões de dados dentro de outras regiões de dados. Por exemplo, se quiser criar um registro de vendas para cada vendedor em um banco de dados, você poderá criar uma lista com caixas de texto e uma imagem para exibir as informações sobre o funcionário e, em seguida, adicionar a essa lista as regiões de dados de tabela e gráfico para mostrar o registro de vendas do funcionário. Para obter mais informações, consulte [Regiões de dados aninhadas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md).  
  
## <a name="multiple-data-regions-linked-to-the-same-dataset"></a>Várias regiões de dados vinculadas ao mesmo conjunto de dados  
 Você pode vincular mais de uma região de dados ao mesmo conjunto de dados para fornecer diferentes exibições dos mesmos dados. Por exemplo, é possível mostrar os mesmos dados em uma tabela e em um gráfico. Você pode criar o relatório para fornecer botões de classificação interativos na tabela, de forma que, ao classificar a tabela, o gráfico seja classificado automaticamente. Para obter mais informações, consulte [Vinculando várias regiões de dados ao mesmo conjunto de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md).  
  
## <a name="data-for-a-data-region"></a>Dados para uma região de dados  
 Cada tablix, gráfico e medidor é criado para exibir dados de um único conjunto de dados. Um mapa exibe dados espaciais e dados analíticos dos mesmos conjuntos de dados ou de conjuntos de dados diferentes. Você também pode incluir valores de conjuntos de dados que não são vinculados à região de dados das seguintes maneiras:  
  
-   Valores de agregação que não dependem de ordem de classificação ou agrupamento com escopo em um conjunto de dados diferente.  
  
-   Valores de pesquisa de pares de nome/valor em um conjunto de dados diferente.  
  
 Para obter mais informações, consulte [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos de Serviços de Relatórios (SSRS)](../reporting-services-concepts-ssrs.md) [Relatórios, partes de relatório e definições de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [Layout da página e renderização &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/page-layout-and-rendering-report-builder-and-ssrs.md)   
 [Tutoriais do Construtor de Relatórios](../../reporting-services/report-builder-tutorials.md)   
 [Tutoriais do Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)  
  
  
