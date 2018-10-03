---
title: Coletar fatias pequenas em um gráfico de pizza (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 21c2b8cb-b9ca-4bc0-bf49-50ba432562f6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: fc92ab82ed0a452a96ccfa5a14a5abc33e154efc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48108956"
---
# <a name="collect-small-slices-on-a-pie-chart-report-builder-and-ssrs"></a>Coletar fatias pequenas em um gráfico de pizza (Construtor de Relatórios e SSRS)
  Quando os gráficos de pizza exibem muitos pontos de dados, eles começam a parecer clusterizados. Para resolver esse problema, você pode mostrar todos os dados sejam inferiores a um determinado valor como uma fatia no gráfico de pizza.  
  
 Para coletar pequenas fatias em uma fatia, primeiro decida se o limite para coleta de pequenas fatias será medido como uma porcentagem do gráfico de pizza ou como um valor fixo. Em seguida, defina as propriedades CollectedThreshold e CollectedThresholdUsePercent. Defina a propriedade CollectedThreshold como a porcentagem do gráfico à qual um valor deve ser inferior para ser coletado ou o valor de dados limite real para coleta. Defina a propriedade CollectedThresholdUsePercent como `True` para usar uma porcentagem ou `False` para usar um valor real.  
  
 Também é possível coletar pequenas fatias em um segundo gráfico de pizza que é retirado de uma fatia coletada do primeiro gráfico de pizza. O segundo gráfico de pizza é desenhado à direita do gráfico de pizza original.  
  
 Não é possível combinar fatias de gráficos de funil ou de pirâmide em uma fatia.  
  
 Um exemplo deste gráfico está disponível como um relatório de exemplo. Para obter mais informações sobre como baixar esse relatório de exemplo e outros, consulte [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][(Relatórios de exemplo do Construtor de relatórios e Designer de relatórios) do](http://go.microsoft.com/fwlink/?LinkId=198283).  
  
### <a name="to-collect-small-slices-into-a-single-slice-on-a-pie-chart"></a>Para coletar pequenas fatias em uma única fatia em um gráfico de pizza  
  
1.  Abra o painel Propriedades.  
  
2.  Na superfície de design, clique em qualquer fatia do gráfico de pizza. As propriedades da série são exibidas no painel Propriedades.  
  
3.  Na seção **Geral** , expanda o nó **CustomAttributes** .  
  
4.  Defina a propriedade CollectedStyle como **SingleSlice**.  
  
5.  Defina o valor do limite coletado e o tipo de limite. Os exemplos a seguir são maneiras comuns de configurar limites coletados.  
  
    -   **Por porcentagem.** Por exemplo, para coletar qualquer fatia no gráfico de pizza que seja menor do que 10% em uma única fatia:  
  
         Defina a propriedade CollectedThresholdUsePercent como `True`.  
  
         Defina a propriedade CollectedThreshold como **10**.  
  
        > [!NOTE]  
        >  Se você definir CollectedStyle como **SingleSlice**, CollectedThreshold com um valor maior que **100**, e CollectedThresholdUsePercent for `True`, o gráfico gerará uma exceção porque ele não é possível Calcule uma porcentagem. Para resolver esse problema, defina CollectedThreshold como um valor menor do que **100**.  
  
    -   **Por valor de dados.** Por exemplo, para coletar qualquer fatia no gráfico de pizza que seja menor do que 5000 em uma única fatia:  
  
         Defina a propriedade CollectedThresholdUsePercent como `False`.  
  
         Defina a propriedade CollectedThreshold como **5000**.  
  
6.  Defina a propriedade CollectedLabel como uma cadeia de caracteres que represente o rótulo do texto que será mostrado na fatia coletada.  
  
7.  (Opcional) Defina as propriedades CollectedSliceExploded, CollectedColor, CollectedLegendText e CollectedToolTip. Essas propriedades alteram a aparência, a cor, o texto do rótulo, o texto da legenda e aspectos da dica de ferramenta da única fatia.  
  
### <a name="to-collect-small-slices-into-a-secondary-callout-pie-chart"></a>Para coletar pequenas fatias em um gráfico de pizza de texto explicativo secundário  
  
1.  Siga as etapas 1 a 3 acima.  
  
2.  Defina a propriedade CollectedStyle como **CollectedPie**.  
  
3.  Defina a propriedade CollectedThreshold como um valor que represente o limite no qual pequenas fatias serão coletadas em uma fatia. Quando a propriedade CollectedStyle é definida como **CollectedPie**, CollectedThresholdUsePercentproperty é sempre definido como `True`, e o limite coletado será sempre medido em porcentagem.  
  
4.  (Opcional) Defina as propriedades CollectedColor, CollectedLabel, CollectedLegendText e CollectedToolTip. Todas as outras propriedades denominadas "Coletadas" não se aplicam ao gráfico de pizza coletado.  
  
> [!NOTE]  
>  O gráfico de pizza secundário é calculado com base nas pequenas fatias dos dados, portanto, ele só é exibido na Visualização. Ele não é exibido na superfície de design.  
  
> [!NOTE]  
>  Não é possível formatar o gráfico de pizza secundário. Por esse motivo, é altamente recomendável usar a primeira abordagem ao coletar fatias da pizza.  
  
## <a name="see-also"></a>Consulte também  
 [Gráficos de pizza &#40;relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Formatando pontos de dados em um gráfico &#40;relatórios e SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Rótulos de ponto de dados de exibição fora de um gráfico de pizza &#40;relatórios e SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [Exibir valores percentuais em um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)   
 [Adicionar efeitos 3D a um gráfico &#40;Construtor de Relatórios e SSRS&#41;](chart-effects-add-3d-effects-report-builder.md)  
  
  
