---
title: Exibir rótulos de pontos de dados fora de um gráfico de pizza (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 959b7574-cf43-470b-b592-4944d8a9948f
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 127f597eef06a3ebb7a1361b2290c53c9479d799
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33020413"
---
# <a name="display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs"></a>Exibir rótulos de pontos de dados fora de um gráfico de pizza (Construtor de Relatórios e SSRS)
  No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], o rótulo do gráfico de pizza é otimizado para exibir rótulos apenas em várias fatias de dados. Os rótulos poderão ser sobrepostos, se o gráfico de pizza contiver muitas fatias. Uma solução é exibir os rótulos fora do gráfico de pizza, o que pode criar mais espaço para rótulos de dados mais longos. Se os rótulos ainda estiverem sobrepostos, você poderá criar mais espaço para eles habilitando 3D. Isso reduz o diâmetro do gráfico de pizza criando mais espaço em torno do gráfico.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-data-point-labels-inside-a-pie-chart"></a>Para exibir rótulos de pontos de dados dentro de um gráfico de pizza  
  
1.  Adicione um gráfico de pizza ao relatório. Para obter mais informações, consulte [Adicionar um gráfico a um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md).  
  
2.  Na superfície de design, clique com o botão direito do mouse no gráfico e selecione **Mostrar Rótulos de Dados**.  
  
### <a name="to-display-data-point-labels-outside-a-pie-chart"></a>Para exibir rótulos de pontos de dados fora de um gráfico de pizza  
  
1.  Crie um gráfico de pizza e exiba os rótulos de dados.  
  
2.  Abra o painel Propriedades.  
  
3.  Na superfície de design, clique na própria pizza para exibir as propriedades **Categoria** no painel de Propriedades.  
  
4.  Expanda o nó **CustomAttributes** . Uma lista de atributos para o gráfico de pizza é exibida.  
  
5.  Defina a propriedade **PieLabelStyle** para **Externo**.  
  
6.  Defina a propriedade **PieLineColor** para **Black**. A propriedade PieLineColor define as linhas do texto explicativo para cada rótulo de ponto de dados.  
  
### <a name="to-prevent-overlapping-labels-displayed-outside-a-pie-chart"></a>Para evitar rótulos sobrepostos exibidos fora de um gráfico de pizza  
  
1.  Crie um gráfico de pizza com rótulos externos.  
  
2.  Na superfície de design, clique com o botão direito do mouse fora do gráfico de pizza, mas dentro das bordas do gráfico e selecione **Propriedades da Área do Gráfico**. A caixa de diálogo **AreaProperties do Gráfico** é exibida.  
  
3.  Na guia **Opções 3D** , selecione **Habilitar 3D**.  
  
4.  Se desejar que o gráfico tenha mais espaço para rótulos, mas ainda pareça bidimensional, defina as propriedades **Rotação** e **Inclinação** em **0**.  
  
## <a name="see-also"></a>Consulte Também  
 [Gráficos de pizza &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
 [Coletar fatias pequenas em um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)   
 [Exibir valores percentuais em um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)  
  
  
