---
title: "Exibir valores de porcentagem em um gr&#225;fico de pizza (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eb905fc1-5235-4773-a27e-b07be9318be5
caps.latest.revision: 9
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 6
---
# Exibir valores de porcentagem em um gr&#225;fico de pizza (Construtor de Relat&#243;rios e SSRS)
  Por padrão, as categorias são mostradas na legenda para identificar cada valor. Se você rotulou o gráfico de pizza usando rótulos de categorias, poderá desejar mostrar porcentagens na legenda.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### Para exibir valores de porcentagem como rótulos em um gráfico de pizza  
  
1.  Adicione um gráfico de pizza ao relatório. Para obter mais informações, veja [Adicionar um gráfico a um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md).  
  
2.  Na superfície de design, clique com o botão direito do mouse no gráfico de pizza e selecione **Mostrar Rótulos de Dados**. Os rótulos de dados devem aparecer dentro de cada fatia do gráfico de pizza.  
  
3.  Na superfície de design, clique com o botão direito do mouse nos rótulos e selecione **Propriedades do Rótulo de Série**. A caixa de diálogo **Propriedades do Rótulo de Série** é exibida.  
  
4.  Digite **#PERCENT** para a opção **Dados do rótulo**.  
  
5.  (Opcional) Para especificar quantas casas decimais o rótulo deve mostrar, digite "#PERCENT{P*n*}" em que *n* é o número de casas decimais a serem exibidas. Por exemplo, para não exibir nenhuma casa decimal, digite "#PERCENT{P0}".  
  
### Para exibir valores percentuais na legenda de um gráfico de pizza  
  
1.  Na superfície de design, clique com o botão direito do mouse no gráfico de pizza e selecione **Propriedades da Série**. A caixa de diálogo **Propriedades da Série** é exibida.  
  
2.  Em **Legenda**, digite **#PERCENT** para a propriedade **Texto da legenda personalizada**.  
  
## Consulte também  
 [Gráficos de pizza &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
 [Formatando a legenda em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-the-legend-on-a-chart-report-builder-and-ssrs.md)   
 [Exibir rótulos de pontos de dados fora de um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [Coletar fatias pequenas em um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)  
  
  