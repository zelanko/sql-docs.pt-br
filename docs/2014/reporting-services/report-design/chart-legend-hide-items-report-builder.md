---
title: Ocultar itens de legenda no gráfico (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 92256240-0cd5-4be4-8904-d1e3b93cb6b3
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 13064f5d0033a1a4677789c6031b1f9b0f322379
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006760"
---
# <a name="hide-legend-items-on-the-chart-report-builder-and-ssrs"></a>Ocultar itens de legenda no gráfico (Construtor de Relatórios e SSRS)
  Por padrão, qualquer série adicionada a um gráfico que não seja de forma é adicionada como um item na legenda. Para gráficos de pizza, de rosca, de funil e de pirâmide, qualquer série adicionada ao gráfico adicionará pontos de dados individuais na legenda.  
  
 É possível ocultar qualquer item na legenda. Quando você oculta um item de legenda, ele ainda é exibido no gráfico. Isso é útil em situações em que você não deseja mostrar mais informações para uma série adicionada ao gráfico. Por exemplo, ao adicionar uma série calculada, como uma média móvel, ao gráfico, talvez você queira ocultar essa entrada na legenda para que apenas mais informações da série original sejam mostradas.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-hide-an-item-from-display-in-the-legend"></a>Para ocultar um item da exibição na legenda  
  
1.  Clique com o botão direito do mouse na série que deseja ocultar e selecione **Propriedades da Série**.  
  
2.  Clique em **Legenda**. Selecione a opção **Não mostrar esta série em uma legenda** .  
  
    > [!NOTE]  
    >  Não é possível ocultar uma série apenas de um grupo e não de outros. Se você adicionou um campo à área **Grupos de Séries** , todas as séries pertencentes a esse grupo serão ocultadas.  
  
## <a name="see-also"></a>Consulte também  
 [Formatando a legenda em um gráfico &#40;SSRS e construtor de relatórios&#41;](chart-legend-formatting-report-builder.md)   
 [Formatando pontos de dados em um gráfico &#40;SSRS e construtor de relatórios&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Alterar o texto de um item de legenda &#40;Construtor de Relatórios e SSRS&#41;](chart-legend-change-item-text-report-builder.md)   
 [Adicionar uma média móvel a um gráfico &#40;Construtor de Relatórios e SSRS&#41;](add-a-moving-average-to-a-chart-report-builder-and-ssrs.md)   
 [Caixa de diálogo Propriedades da Legenda, Geral &#40;Construtor de Relatórios e SSRS&#41;](../legend-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  