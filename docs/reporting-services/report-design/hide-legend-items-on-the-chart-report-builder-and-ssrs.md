---
title: "Ocultar itens de legenda no gr&#225;fico (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "12/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 92256240-0cd5-4be4-8904-d1e3b93cb6b3
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# Ocultar itens de legenda no gr&#225;fico (Construtor de Relat&#243;rios e SSRS)
Por padrão, qualquer série adicionada a um gráfico sem forma em um relatório paginado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] será adicionada como um item na legenda. Para gráficos de pizza, de rosca, de funil e de pirâmide, qualquer série adicionada ao gráfico adicionará pontos de dados individuais na legenda.  
  
 É possível ocultar qualquer item na legenda. Quando você oculta um item de legenda, ele ainda é exibido no gráfico. Isso é útil em situações em que você não deseja mostrar mais informações para uma série adicionada ao gráfico. Por exemplo, ao adicionar uma série calculada, como uma média móvel, ao gráfico, talvez você queira ocultar essa entrada na legenda para que apenas mais informações da série original sejam mostradas.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Para ocultar um item da exibição na legenda  
  
1.  Clique com o botão direito do mouse na série que deseja ocultar e selecione **Propriedades da Série**.  
  
2.  Clique em **Legenda**. Selecione a opção **Não mostrar esta série em uma legenda** .  
  
    > [!NOTE]  
    >  Não é possível ocultar uma série apenas de um grupo e não de outros. Se você adicionou um campo à área **Grupos de Séries** , todas as séries pertencentes a esse grupo serão ocultadas.  
  
## Consulte também  
 [Formatando a legenda em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-the-legend-on-a-chart-report-builder-and-ssrs.md)   
 [Formatando pontos de dados em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Alterar o texto de um item de legenda &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/change-the-text-of-a-legend-item-report-builder-and-ssrs.md)   
 [Adicionar uma média móvel a um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-moving-average-to-a-chart-report-builder-and-ssrs.md)   
 [Caixa de diálogo Propriedades da Legenda, Geral &#40;Construtor de Relatórios e SSRS&#41;](../Topic/Legend%20Properties%20Dialog%20Box,%20General%20\(Report%20Builder%20and%20SSRS\).md)  
  
  