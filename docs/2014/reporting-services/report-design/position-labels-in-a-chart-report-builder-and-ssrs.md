---
title: Posicionar rótulos em um gráfico (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5db74e0b-8be8-4b47-b386-faab56dffa9b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fc04d47058c1ef1bc3929d941a6680eb013fcc53
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105437"
---
# <a name="position-labels-in-a-chart-report-builder-and-ssrs"></a>Posicionar rótulos em um gráfico (Construtor de Relatórios e SSRS)
  Como cada tipo de gráfico tem uma forma diferente, os rótulos de ponto de dados são colocados em um local ideal de forma que não interfiram no gráfico. A posição padrão dos rótulos varia com o tipo de gráfico:  
  
-   Em gráficos empilhados, os rótulos só podem ser posicionados nas séries.  
  
-   Nos gráficos de funil ou pirâmide, os rótulos são posicionados fora de uma coluna.  
  
-   Em gráficos de pizza, os rótulos são posicionados nas fatias individuais em um gráfico de pizza.  
  
-   Nos gráficos de barras, os rótulos são posicionados fora das barras que representam os pontos de dados.  
  
-   Nos gráficos polares, os rótulos são posicionados fora da área circular que representa os pontos de dados.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-position-of-point-labels-in-a-pie-chart"></a>Para alterar a posição dos rótulos de pontos em um gráfico de pizza  
  
1.  Crie um gráfico de pizza.  
  
2.  Na superfície de design, clique com o botão direito do mouse no gráfico e selecione **Mostrar Rótulos de Dados**.  
  
3.  Abra o painel Propriedades. Na guia **Exibir** , clique em **Propriedades**.  
  
4.  Na superfície de design, clique no gráfico. As propriedades para o gráfico são exibidas no painel Propriedades.  
  
5.  Na seção **Geral** , expanda o nó **CustomAttributes** . Uma lista de atributos para o gráfico de pizza é exibida.  
  
6.  Selecione um valor para a propriedade PieLabelStyle.  
  
### <a name="to-change-the-position-of-point-labels-in-a-funnel-or-pyramid-chart"></a>Para alterar a posição dos rótulos de pontos em um Gráfico de funil ou pirâmide  
  
1.  Crie um gráfico de funil ou pirâmide.  
  
2.  Na superfície de design, clique com o botão direito do mouse no gráfico e selecione **Mostrar Rótulos de Dados**.  
  
3.  Abra o painel Propriedades. Na guia **Exibir** , clique em **Propriedades**  
  
4.  Na superfície de design, clique no gráfico. As propriedades para o gráfico são exibidas no painel Propriedades.  
  
5.  Na seção **Geral** , expanda o nó **CustomAttributes** . Uma lista de atributos para o gráfico de funil é exibida.  
  
6.  Para um gráfico de funil, selecione um valor para a propriedade FunnelLabelStyle. Para um gráfico de pirâmide, selecione um valor para a propriedade PyramidLabelStyle.  
  
    > [!NOTE]  
    >  Quando essa propriedade é definida com um valor `OutsideInColumn`, os rótulos são desenhados em uma coluna vertical. Não há como alterar a posição da coluna.  
  
### <a name="to-change-the-position-of-point-labels-in-a-bar-chart"></a>Para alterar a posição dos rótulos de pontos em um gráfico de barras  
  
1.  Crie um gráfico de barras.  
  
2.  Na superfície de design, clique com o botão direito do mouse no gráfico e selecione **Mostrar Rótulos de Dados**.  
  
3.  Abra o painel Propriedades. Na guia **Exibir** , clique em **Propriedades**  
  
4.  Na superfície de design, clique no gráfico. As propriedades para o gráfico são exibidas no painel Propriedades.  
  
5.  Na seção **Geral** , expanda o nó **CustomAttributes** . Uma lista de atributos para o gráfico de barras é exibida.  
  
6.  Selecione um valor para a propriedade BarLabelStyle.  
  
 Se o estilo do rótulo da barra for definido como `Outside`, os rótulos serão colocados fora da barra, contanto que caibam na área do gráfico. Se o rótulo não puder ser colocado fora da barra, mas dentro da área de gráfico, o rótulo será colocado dentro da barra na posição mais próxima do final da barra.  
  
### <a name="to-change-the-position-of-point-labels-in-an-area-column-line-or-scatter-chart"></a>Para alterar a posição dos rótulos de pontos em um gráfico de Área, Coluna, Linha ou Dispersão  
  
1.  Crie um gráfico de Área, Coluna, Linha ou Dispersão.  
  
2.  Na superfície de design, clique com o botão direito do mouse no gráfico e selecione **Mostrar Rótulos de Dados**.  
  
3.  Abra o painel Propriedades. Na guia **Exibir** , clique em **Propriedades**  
  
4.  Na superfície de design, clique na série. As propriedades da série são exibidas no painel Propriedades.  
  
5.  Na seção **Dados** , expanda o nó **DataPoint** e o nó **Rótulo**.  
  
6.  Selecione um valor para a propriedade Position.  
  
## <a name="see-also"></a>Consulte também  
 [Gráficos de pizza &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Gráficos de barras &#40;Construtor de Relatórios e SSRS&#41;](bar-charts-report-builder-and-ssrs.md)   
 [Formatando rótulos dos eixos de um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Formatar rótulos de eixo como datas ou moedas &#40;Construtor de Relatórios e SSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [Exibir rótulos de pontos de dados fora de um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [Formatando pontos de dados em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)  
  
  
