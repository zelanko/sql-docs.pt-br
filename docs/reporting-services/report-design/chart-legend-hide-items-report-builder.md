---
title: Ocultar itens de legenda no gráfico (Construtor de Relatórios) | Microsoft Docs
description: Saiba como escolher os itens exibidos na legenda para exibir os dados essenciais no Construtor de Relatórios.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 92256240-0cd5-4be4-8904-d1e3b93cb6b3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5f745b3eb2c862f4105bcdd872a8915845341942
ms.sourcegitcommit: 02b22274da4a103760a376c4ddf26c4829018454
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681415"
---
# <a name="chart-legend---hide-items-report-builder"></a>Legenda de gráfico – Ocultar itens (Construtor de Relatórios)
Por padrão, qualquer série adicionada a um gráfico sem forma em um relatório paginado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] será adicionada como um item na legenda. Para gráficos de pizza, de rosca, de funil e de pirâmide, qualquer série adicionada ao gráfico adicionará pontos de dados individuais na legenda.  
  
 É possível ocultar qualquer item na legenda. Quando você oculta um item de legenda, ele ainda é exibido no gráfico. Isso é útil em situações em que você não deseja mostrar mais informações para uma série adicionada ao gráfico. Por exemplo, ao adicionar uma série calculada, como uma média móvel, ao gráfico, talvez você queira ocultar essa entrada na legenda para que apenas mais informações da série original sejam mostradas.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-hide-an-item-from-display-in-the-legend"></a>Para ocultar um item da exibição na legenda  
  
1.  Clique com o botão direito do mouse na série que deseja ocultar e selecione **Propriedades da Série**.  
  
2.  Clique em **Legenda**. Selecione a opção **Não mostrar esta série em uma legenda** .  
  
    > [!NOTE]  
    >  Não é possível ocultar uma série apenas de um grupo e não de outros. Se você adicionou um campo à área **Grupos de Séries** , todas as séries pertencentes a esse grupo serão ocultadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Formatando a legenda em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)   
 [Formatando pontos de dados em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Alterar o texto de um item de legenda &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/chart-legend-change-item-text-report-builder.md)   
 [Adicionar uma média móvel a um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-moving-average-to-a-chart-report-builder-and-ssrs.md)   
 [Caixa de diálogo Propriedades da Legenda, Geral &#40;Construtor de Relatórios e SSRS&#41;](https://msdn.microsoft.com/library/db718f8f-f185-422f-871c-96f0749e5893)  
  
  
