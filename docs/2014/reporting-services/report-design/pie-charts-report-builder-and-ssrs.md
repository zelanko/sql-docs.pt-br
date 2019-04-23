---
title: Gráficos de pizza (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 536efa9c-c6fb-4cdd-b41f-ff5382910bd7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f10e941ef5acd180e8b279762e84535bad5689e4
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59971882"
---
# <a name="pie-charts-report-builder-and-ssrs"></a>Gráficos de pizza (Construtor de Relatórios e SSRS)
  Gráficos de pizza e gráficos de rosca exibem dados como uma proporção do todo. Os gráficos de pizza são os mais usados para fazer comparações entre grupos. Gráficos de pizza e de rosca, além dos gráficos pirâmide e funil, compõem um grupo de gráficos conhecidos como gráficos de forma. Os gráficos de forma não têm nenhum eixo. Quando um campo numérico é solto em um gráfico de forma, o gráfico calcula a porcentagem de cada valor com relação ao total. Para obter mais informações sobre gráficos de forma, consulte [Gráficos de forma &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md).  
  
 A ilustração a seguir mostra um gráfico de pizza em 3-D com nomes de rótulos formatados como porcentagens.  A legenda está posicionada no centro-direito.  
  
 ![Gráfico de pizza](../media/piechart.gif "Gráfico de pizza")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>Variações  
  
-   **Pizza destacada**. Um gráfico de pizza onde todas as fatias são distanciadas do centro da pizza. Além do gráfico de pizza destacada, no qual todas as fatias estão separadas, você pode criar um gráfico com fatias destacadas, no qual apenas uma fatia é chamada.  
  
-   **Rosca**. Um gráfico de pizza que tem um espaço aberto no centro.  
  
-   **Rosca destacada**. Um gráfico de rosca onde todas as fatias são distanciadas do centro da rosca.  
  
-   **Pizza em 3D**. O gráfico de pizza que tem um estilo 3D aplicado.  
  
-   **Pizza Destacada em 3D**. Um gráfico de pizza destacada que tem um estilo 3D aplicado.  
  
## <a name="data-considerations-for-display-on-a-pie-chart"></a>Considerações de dados para exibição em um gráfico de pizza  
  
-   Gráficos de pizza são comuns em relatórios devido ao seu impacto visual. Porém, gráficos de pizza são um tipo de gráfico muito simplificado que pode não representar da melhor maneira os seus dados. Considere usar um gráfico de pizza apenas após os dados terem sido agregados a sete pontos de dados ou menos.  
  
-   Os gráficos de pizza exibem cada grupo de dados como uma fatia separada no gráfico. Você deve acrescentar pelo menos um campo de dados e um campo de categoria ao gráfico de pizza. Se mais de um campo de dados for acrescido a um gráfico de pizza, este gráfico exibirá esse dois campos no mesmo gráfico.  
  
-   Valores nulos, vazios, negativos e zero não têm nenhum valor quando for calcular as razões. Por isto, estes valores não são mostrados em um gráfico de pizza. Se quiser indicar visualmente esse tipo de valores no seu gráfico, mude o tipo de gráfico para algo diferente de gráfico de pizza.  
  
-   Se estiver definindo suas próprias cores em um gráfico de pizza usando uma paleta personalizada, certifique-se para ter cores suficientes na sua paleta para exibir cada ponto de dados com sua própria cor exclusiva. Para obter mais informações, consulte [Formatando as cores da série em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md).  
  
-   De modo diferente dos demais tipos de gráficos, um gráfico de pizza exibirá na sua legenda os pontos de dados individuais, e não as séries individuais.  
  
-   Um gráfico de pizza requer no mínimo dois valores para poder realizar uma comparação válida entre as proporções. Se o seu gráfico de pizza contém apenas uma cor, verifique se você adicionou um campo de categoria para o agrupamento. Quando um gráfico de pizza não contém categorias, ele agrega os valores do seu campo de dados em um valor para exibição.  
  
-   De modo igual a todos os demais tipos de gráficos, um gráfico pizza gera as cores com base nos valores das cores incluídas na paleta padrão. Esta abordagem faz com que gráficos de pizza diferentes podem colorir pontos de dados de modo diferente quando estiver usando vários gráficos de pizza em um relatório. Se tiver vários gráficos de pizza no seu relatório, talvez seja melhor definir cores manualmente para cada grupo de categoria a fim de reter a mesma cor nos diferentes gráficos. Para obter mais informações sobre como definir cores em um gráfico, consulte [Formatando as cores da série em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md).  
  
## <a name="applying-drawing-styles-to-a-pie-chart"></a>Aplicando estilos de desenho a um gráfico de pizza  
 Você pode acrescentar estilos de desenho especiais ao gráfico de pizza para aumentar seu impacto visual. Estilos de desenho incluem efeitos oblíquos e côncavos. Esses efeitos estão disponíveis apenas em um gráfico de pizza 2D. A ilustração a seguir mostra um exemplo dos estilos de desenho oblíquos e côncavos em um gráfico de pizza.  
  
 ![Estilos de desenho de pizza](../media/rs-piedrawingeffects-concave2.gif "Estilos de desenho de pizza")  
  
 Para obter mais informações, consulte [Como adicionar bisel, alto-relevo e estilos de textura a um gráfico &#40;Construtor de Relatórios e SSRS&#41;](chart-effects-add-bevel-emboss-or-texture-report-builder.md).  
  
## <a name="displaying-percentage-values-on-a-pie-chart"></a>Exibindo valores de porcentagem em um gráfico de pizza  
 De modo similar aos demais gráficos de Forma, os gráficos de pizza representam proporções do total. Como resultado, está comum formatar os rótulos de gráfico de pizza como porcentagens. Para ser consistente com os demais tipos de gráfico, o gráfico não exibe os rótulos de porcentagem por padrão. Para obter mais informações sobre como exibir valores como porcentagens no gráfico, consulte [Exibir valores percentuais em um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md). Para obter mais informações sobre como formatar números como porcentagens em seu relatório, consulte [Formatação de números e datas &#40;Construtor de Relatórios e SSRS&#41;](formatting-numbers-and-dates-report-builder-and-ssrs.md).  
  
 ![Gráfico de pizza com rótulos de ponto de dados como percentuais](../media/rs-piechartpercentages.gif "Gráfico de pizza com rótulos de ponto de dados como percentuais")  
  
## <a name="preventing-overlapped-labels-on-a-pie-chart"></a>Impedindo a sobreposição de rótulos em um gráfico de pizza  
 Se houver muitos pontos de dados em um gráfico de pizza, os rótulos dos dados serão sobrepostos. Há vários modos para impedir a sobreposição de rótulos:  
  
-   Diminuir o tamanho da fonte dos rótulos do ponto de dados.  
  
-   Aumentar a largura e a altura de seu gráfico para permitir maior espaço para os rótulos.  
  
-   Exibir os rótulos da pizza fora da área do gráfico. Para obter mais informações, consulte [Exibir rótulos de pontos de dados fora de um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md).  
  
-   Coletar as pequenas fatias da pizza em uma fatia.  
  
## <a name="consolidating-small-slices-on-a-pie-chart"></a>Consolidando fatias pequenas em um gráfico de pizza  
 Quando o gráfico de pizza tiver muitos pontos, os dados ficarão obscuros e difíceis de ler. Caso os dados tenham muitos pontos de dados pequenos, há dois modos de coletar várias fatias:  
  
-   Colete fatias de dados menores em uma fatia do gráfico de pizza. Isso é muito útil nas situações em que, por exemplo, você quer que o gráfico de pizza tenha "outro" ponto de dados que apenas colete os demais dados. Para obter mais informações, consulte [Coletar fatias pequenas em um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md).  
  
-   Colete fatias pequenas em um gráfico de pizza suplementar. O segundo gráfico de pizza não é exibido no designer. Na verdade, durante o processamento do relatório, o gráfico calcula se um segundo gráfico de pizza deve ser mostrado com base nos valores dos pontos de dados. Nesse caso, os valores são adicionados a outro gráfico de pizza.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir rótulos de pontos de dados fora de um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [Coletar fatias pequenas em um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)   
 [Exibir valores percentuais em um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)   
 [Tutorial: Adicionar um gráfico de pizza ao relatório &#40;Construtor de Relatórios&#41;](../tutorial-add-a-pie-chart-to-your-report-report-builder.md)   
 [Formatando a legenda em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](chart-legend-formatting-report-builder.md)   
 [Pontos de dados vazios e nulos em gráficos &#40;Construtor de Relatórios e SSRS&#41;](empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
 [Formatando as cores da série em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)  
  
  
