---
title: "Exibir valores de porcentagem em um gráfico de pizza (construtor de relatórios e SSRS) | Microsoft Docs"
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
ms.assetid: eb905fc1-5235-4773-a27e-b07be9318be5
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6c0fdf9d1b694f2f6d49389e913d1c156ba77838
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="display-percentage-values-on-a-pie-chart-report-builder-and-ssrs"></a>Exibir valores de porcentagem em um gráfico de pizza (Construtor de Relatórios e SSRS)
Em [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] relatórios paginados, por padrão, a legenda mostra as categorias. Talvez você também queira porcentagens na legenda ou as fatias da pizza próprios.   

![report-builder-pie-chart-preview-percents](../../reporting-services/media/report-builder-pie-chart-preview-percents.png)

 O [Tutorial: adicionar um gráfico de pizza ao seu relatório (construtor de relatórios)](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md) orienta adicionando porcentagens para fatias da pizza, se você gostaria de tentar isso primeiro com dados de exemplo.
 
  
## <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>Para exibir valores de porcentagem como rótulos em um gráfico de pizza  
  
1.  Adicione um gráfico de pizza ao relatório. Para obter mais informações, veja [Adicionar um gráfico a um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md).  
  
2.  Na superfície de design, clique com o botão direito do mouse no gráfico de pizza e selecione **Mostrar Rótulos de Dados**. Os rótulos de dados devem aparecer dentro de cada fatia do gráfico de pizza.  
  
3.  Na superfície de design, clique com o botão direito do mouse nos rótulos e selecione **Propriedades do Rótulo de Série**. A caixa de diálogo **Propriedades do Rótulo de Série** é exibida.  
  
4.  Digite **#PERCENT** para a opção **Dados do rótulo** .  
  
5.  (Opcional) Para especificar quantas casas decimais o rótulo deve mostrar, digite "#PERCENT {P*n*}" onde  *n*  é o número de casas decimais a serem exibidas. Por exemplo, para não exibir nenhuma casa decimal, digite "#PERCENT{P0}".  
  
## <a name="to-display-percentage-values-in-the-legend-of-a-pie-chart"></a>Para exibir valores percentuais na legenda de um gráfico de pizza  
  
1.  Na superfície de design, clique com o botão direito do mouse no gráfico de pizza e selecione **Propriedades da Série**. A caixa de diálogo **Propriedades da Série** é exibida.  
  
2.  Em **Legenda**, digite **#PERCENT** para a propriedade **Texto da legenda personalizada** .  
  
## <a name="see-also"></a>Consulte também  
* [Tutorial: Adicionar um gráfico de pizza ao relatório (construtor de relatórios)](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)
*  [Gráficos de pizza &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
*  [Formatando a legenda em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)   
*  [Exibir rótulos de pontos de dados fora de um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 
  
