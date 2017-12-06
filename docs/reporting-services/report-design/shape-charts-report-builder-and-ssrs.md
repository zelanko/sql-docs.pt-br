---
title: "Gráficos de forma (Construtor de Relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b8404c1-aa89-4350-8bd6-203bc0446ee4
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 9229677bb7c9dada48a91f6d9fad0d361a2b8b44
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="shape-charts-report-builder-and-ssrs"></a>Gráficos de forma (Construtor de Relatórios e SSRS)
  Um gráfico de forma exibe os dados de valor como porcentagens do todo. São usados gráficos de forma normalmente para mostrar comparações proporcionais entre valores diferentes em um conjunto. Categorias são representadas por segmentos individuais da forma. O tamanho do segmento é determinado pelo valor. Os gráficos de forma tem uso semelhante aos gráficos de pizza, exceto que eles classificam as categorias do maior para o menor.  
  
 Um gráfico de funil exibe valores como proporções que diminuem progressivamente. O tamanho da área é determinado pelo valor da série como porcentagem do total de todos os valores. Por exemplo, você pode usar um gráfico de funil para exibir tendências de visita do site. É provável que o gráfico de funil exibirá um ampla área na parte superior, indicando o número de vez que uma página é visitada e as outras áreas serão proporcionalmente menores. Para obter mais informações sobre como adicionar dados a um gráfico de funil, consulte [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md).  
  
 A ilustração a seguir mostra um exemplo de gráfico de funil.  
  
 ![Gráfico de funil](../../reporting-services/report-design/media/rs-funnelchart.gif "Gráfico de funil")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>Variações  
  
-   **Pirâmide**. Um gráfico de pirâmide exibe dados proporcionais de forma que o gráfico se parece com uma pirâmide.  
  
## <a name="data-considerations-for-shape-charts"></a>Considerações de dados para gráficos de forma  
  
-   Gráficos de forma são comuns em relatórios devido ao seu impacto visual. Porém, os gráficos de forma são um tipo de gráfico muito simplificado que pode não representar da melhor maneira os seus dados. Considere usar um gráfico de forma apenas assim que os dados tiverem sido agregados a sete pontos de dados ou menos. Em geral, use o gráfico de forma para exibir só uma categoria por região de dados.  
  
-   Os gráficos de forma exibem cada grupo de dados como um segmento separado de gráfico. Você deve adicionar pelo menos um campo de dados e um campo de categoria. Se mais de um campo de dados for adicionado ao gráfico de forma, ele exibirá os campos de dados no mesmo gráfico.  
  
-   Os gráficos de forma são mais eficientes para mostrar porcentagens proporcionais na ordem classificada. No entanto, para manter a consistência, o gráfico não classifica os valores no seu conjunto de dados por padrão. Considere classificar seus valores do mais alto para o mais baixo para representar com mais precisão seus dados como um funil ou uma pirâmide. Para obter mais informações, consulte [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
-   Valores nulos, vazios, negativos e zero não têm nenhum valor quando for calcular as razões. Por isso, esses valores não são mostrados em um gráfico de forma. Se quiser indicar visualmente esse tipo de valores no seu gráfico, mude o tipo de gráfico para algo diferente de gráfico de forma. Para obter mais informações sobre como adicionar pontos vazios a um gráfico sem forma, consulte [Adicionar pontos vazios a um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-empty-points-to-a-chart-report-builder-and-ssrs.md).  
  
-   Se estiver definindo suas próprias cores em um gráfico de forma usando uma paleta personalizada, certifique-se de ter cores suficientes na sua paleta para realçar cada ponto de dados com sua própria cor exclusiva. Para obter mais informações, consulte [Formatando as cores da série em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md).  
  
-   De modo diferente dos todos os outros tipos de gráficos, um gráfico de forma exibirá na sua legenda os pontos de dados individuais, e não as séries individuais.  
  
-   As configurações dos eixos de valor e categoria são ignoradas nos gráficos de funil. Se houver vários grupos de categorias ou de séries, os rótulos dos grupos serão exibidos na legenda do gráfico.  
  
-   Os tipos de gráfico de forma não podem ser combinados com qualquer outro tipo de gráfico na mesma área de gráfico. Se você mostrar comparações entre os dados exibidos em um gráfico de forma e os dados exibidos em outro tipo de gráfico, você precisará adicionar uma segunda área de gráfico.  
  
-   Você pode aplicar estilos de desenho adicionais a gráficos de pizza e rosca para melhorar o impacto visual. Consulte [Formatando as cores de série em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md) para obter mais informações.  
  
## <a name="see-also"></a>Consulte também  
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Pontos de dados vazios e nulos em gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
 [Gráficos de pizza &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)  
  
  
