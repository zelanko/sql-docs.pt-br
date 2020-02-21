---
title: Exibir valores de percentual em um gráfico de pizza (Construtor de Relatórios) | Microsoft Docs
description: Em relatórios paginados do Reporting Services, por padrão, a legenda mostra as categorias. É recomendável ter percentuais na legenda ou nas próprias fatias da pizza.
ms.date: 12/09/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: eb905fc1-5235-4773-a27e-b07be9318be5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ffa11ae9d6c0d539accb4bbf6d796019cbc3371e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75254605"
---
# <a name="display-percentage-values-on-a-pie-chart-report-builder-and-ssrs"></a>Exibir valores de porcentagem em um gráfico de pizza (Construtor de Relatórios e SSRS)
Em relatórios paginados do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)], por padrão, a legenda mostra as categorias. É recomendável ter percentuais na legenda ou nas próprias fatias da pizza.   

![report-builder-pie-chart-preview-percents](../../reporting-services/media/report-builder-pie-chart-preview-percents.png)

 O [Tutorial: Adicionar um gráfico de pizza ao relatório (Construtor de Relatórios)](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md) explica como adicionar percentuais a fatias de pizza, caso você deseje testar isso com os dados de exemplo primeiro.
 
  
## <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>Para exibir valores de porcentagem como rótulos em um gráfico de pizza  
  
1.  Adicione um gráfico de pizza ao relatório. Para obter mais informações, consulte [Adicionar um gráfico a um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md).  
  
2.  Na superfície de design, clique com o botão direito do mouse no gráfico de pizza e selecione **Mostrar Rótulos de Dados**. Os rótulos de dados devem aparecer dentro de cada fatia do gráfico de pizza.  
  
3.  Na superfície de design, clique com o botão direito do mouse nos rótulos e selecione **Propriedades do Rótulo de Série**. A caixa de diálogo **Propriedades do Rótulo de Série** é exibida.  
  
4.  Digite **#PERCENT** para a opção **Dados do rótulo** .  
  
5.  (Opcional) Para especificar quantas casas decimais o rótulo deve mostrar, digite "#PERCENT{P*n*}" em que *n* é o número de casas decimais a serem exibidas. Por exemplo, para não exibir nenhuma casa decimal, digite "#PERCENT{P0}".  
  
## <a name="to-display-percentage-values-in-the-legend-of-a-pie-chart"></a>Para exibir valores percentuais na legenda de um gráfico de pizza  
  
1.  Na superfície de design, clique com o botão direito do mouse no gráfico de pizza e selecione **Propriedades da Série**. A caixa de diálogo **Propriedades da Série** é exibida.  
  
2.  Em **Legenda**, digite **#PERCENT** para a propriedade **Texto da legenda personalizada** .  
  
## <a name="see-also"></a>Consulte Também  
* [Tutorial: Adicionar um gráfico de pizza ao relatório (Construtor de Relatórios)](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)
*  [Gráficos de pizza &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
*  [Formatando a legenda em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)   
*  [Exibir rótulos de pontos de dados fora de um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 
  
