---
title: "Coletar fatias pequenas em um gráfico de pizza (construtor de relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21c2b8cb-b9ca-4bc0-bf49-50ba432562f6
caps.latest.revision: 10
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: e25526de7b4ae194d0aa510c12a9a995208c035a
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="collect-small-slices-on-a-pie-chart-report-builder-and-ssrs"></a>Coletar fatias pequenas em um gráfico de pizza (Construtor de Relatórios e SSRS)
Gráficos de pizza com muitas fatias pode parecer clusterizados. Saiba como coletar várias fatias pequenas em um gráfico de pizza em uma única fatia em [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] relatórios paginados.
 
 Para coletar pequenas fatias em uma fatia, primeiro decida se o limite para coleta de pequenas fatias será medido como uma porcentagem do gráfico de pizza ou como um valor fixo. 
 
 O [Tutorial: adicionar um gráfico de pizza ao seu relatório (construtor de relatórios)](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md) orienta você por meio de coleta de pequenas fatias em uma única fatia, se você gostaria de tentar isso primeiro com dados de exemplo.
 
 ![Report-Builder-Pie-Chart-Other-Slice](../../reporting-services/report-design/media/report-builder-pie-chart-other-slice.png)
  
 Também é possível coletar pequenas fatias em um segundo gráfico de pizza que é retirado de uma fatia coletada do primeiro gráfico de pizza. O segundo gráfico de pizza é desenhado à direita do gráfico de pizza original.  
  
 Não é possível combinar fatias de gráficos de funil ou de pirâmide em uma fatia.  
  
 
## <a name="to-collect-small-slices-into-a-single-slice-on-a-pie-chart"></a>Para coletar pequenas fatias em uma única fatia em um gráfico de pizza  
  
1.  Abra o painel Propriedades.  
  
2.  Na superfície de design, clique em qualquer fatia do gráfico de pizza. As propriedades da série são exibidas no painel Propriedades.  
  
3.  Na seção **Geral** , expanda o nó **CustomAttributes** .  
  
4.  Defina a propriedade CollectedStyle como **SingleSlice**.  

    ![report-builder-pie-chart-single-slice-property](../../reporting-services/media/report-builder-pie-chart-single-slice-property.png)
  
5.  Defina o valor do limite coletado e o tipo de limite. Os exemplos a seguir são maneiras comuns de configurar limites coletados.  
  
    -   **Por porcentagem.** Por exemplo, para coletar qualquer fatia no gráfico de pizza que seja menor do que 10% em uma única fatia:  
  
         Defina a propriedade CollectedThresholdUsePercent como **True**.  
  
         Defina a propriedade CollectedThreshold como **10**.  
  
        > [!NOTE]  
        >  Se você definir CollectedStyle como **SingleSlice**, CollectedThreshold para um valor maior que **100**e CollectedThresholdUsePercent para **True**, o gráfico gerará uma exceção porque não é possível calcular uma porcentagem. Para resolver esse problema, defina CollectedThreshold como um valor menor que **100**.  
  
    -   **Por valor de dados.** Por exemplo, para coletar qualquer fatia no gráfico de pizza que seja menor do que 5000 em uma única fatia:  
  
         Defina a propriedade CollectedThresholdUsePercent como **False**.  
  
         Defina a propriedade CollectedThreshold como **5000**.  
  
6.  Defina a propriedade CollectedLabel como uma cadeia de caracteres que represente o rótulo do texto que será mostrado na fatia coletada.  
  
7.  (Opcional) Defina as propriedades CollectedSliceExploded, CollectedColor, CollectedLegendText e CollectedToolTip. Essas propriedades alteram a aparência, a cor, o texto do rótulo, o texto da legenda e aspectos da dica de ferramenta da única fatia.  
  
## <a name="to-collect-small-slices-into-a-secondary-callout-pie-chart"></a>Para coletar pequenas fatias em um gráfico de pizza de texto explicativo secundário  
  
1.  Siga as etapas 1 a 3 acima.  
  
2.  Defina a propriedade CollectedStyle como **CollectedPie**.  
  
3.  Defina a propriedade CollectedThreshold como um valor que represente o limite no qual pequenas fatias serão coletadas em uma fatia. Quando a propriedade CollectedStyle é definida como **CollectedPie**, CollectedThresholdUsePercentproperty é sempre definido como **True**, e o limite coletado é sempre medido como uma porcentagem.  
  
4.  (Opcional) Defina as propriedades CollectedColor, CollectedLabel, CollectedLegendText e CollectedToolTip. Todas as outras propriedades denominadas "Coletadas" não se aplicam ao gráfico de pizza coletado.  
  
> [!NOTE]  
>  O gráfico de pizza secundário é calculado com base nas pequenas fatias dos dados, portanto, ele só é exibido na Visualização. Ele não é exibido na superfície de design.  
  
> [!NOTE]  
>  Não é possível formatar o gráfico de pizza secundário. Por esse motivo, é altamente recomendável usar a primeira abordagem ao coletar fatias da pizza.  
  
## <a name="see-also"></a>Consulte também  
* [Tutorial: Adicionar um gráfico de pizza ao relatório (construtor de relatórios)](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)
*  [Gráficos de pizza &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
*  [Formatando pontos de dados em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
*  [Exibir rótulos de pontos de dados fora de um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
*  [Exibir valores de porcentagem em um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)     
  
