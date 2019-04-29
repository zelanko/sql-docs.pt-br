---
title: Exibir rótulos de pontos de dados fora de um gráfico de pizza (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 959b7574-cf43-470b-b592-4944d8a9948f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 49ea3e0e87d9594ff16b3512533597ea9a9ea37c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63185510"
---
# <a name="display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs"></a>Exibir rótulos de pontos de dados fora de um gráfico de pizza (Construtor de Relatórios e SSRS)
  No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], o rótulo do gráfico de pizza é otimizado para exibir rótulos apenas em várias fatias de dados. Os rótulos poderão ser sobrepostos, se o gráfico de pizza contiver muitas fatias. Uma solução é exibir os rótulos fora do gráfico de pizza, o que pode criar mais espaço para rótulos de dados mais longos. Se os rótulos ainda estiverem sobrepostos, você poderá criar mais espaço para eles habilitando 3D. Isso reduz o diâmetro do gráfico de pizza criando mais espaço em torno do gráfico.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-data-point-labels-inside-a-pie-chart"></a>Para exibir rótulos de pontos de dados dentro de um gráfico de pizza  
  
1.  Adicione um gráfico de pizza ao relatório. Para obter mais informações, consulte [Adicionar um gráfico a um relatório &#40;Construtor de Relatórios e SSRS&#41;](add-a-chart-to-a-report-report-builder-and-ssrs.md).  
  
2.  Na superfície de design, clique com o botão direito do mouse no gráfico e selecione **Mostrar Rótulos de Dados**.  
  
### <a name="to-display-data-point-labels-outside-a-pie-chart"></a>Para exibir rótulos de pontos de dados fora de um gráfico de pizza  
  
1.  Crie um gráfico de pizza e exiba os rótulos de dados.  
  
2.  Abra o painel Propriedades.  
  
3.  Na superfície de design, clique na própria pizza para exibir as propriedades **Categoria** no painel de Propriedades.  
  
4.  Expanda o nó **CustomAttributes** . Uma lista de atributos para o gráfico de pizza é exibida.  
  
5.  Defina a propriedade **PieLabelStyle** para **Externo**.  
  
6.  Defina as `PieLineColor` propriedade para **preto**. A propriedade PieLineColor define as linhas do texto explicativo para cada rótulo de ponto de dados.  
  
### <a name="to-prevent-overlapping-labels-displayed-outside-a-pie-chart"></a>Para evitar rótulos sobrepostos exibidos fora de um gráfico de pizza  
  
1.  Crie um gráfico de pizza com rótulos externos.  
  
2.  Na superfície de design, clique com o botão direito do mouse fora do gráfico de pizza, mas dentro das bordas do gráfico e selecione **Propriedades da Área do Gráfico**. A caixa de diálogo **AreaProperties do Gráfico** é exibida.  
  
3.  Na guia **Opções 3D** , selecione **Habilitar 3D**.  
  
4.  Se desejar que o gráfico tenha mais espaço para rótulos, mas ainda pareça bidimensional, defina as propriedades **Rotação** e **Inclinação** em **0**.  
  
## <a name="see-also"></a>Consulte também  
 [Gráficos de pizza &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Coletar fatias pequenas em um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)   
 [Exibir valores percentuais em um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)  
  
  
