---
title: Mostrar ToolTips em uma série (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4c9606ff-e1c3-4cf7-a4e7-bb16f1a9e8ab
caps.latest.revision: 5
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: ae6fc4bd445be2aab739aa23b42d1aa5a6198879
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116865"
---
# <a name="show-tooltips-on-a-series-report-builder-and-ssrs"></a>Mostrar dicas de ferramenta em uma série (Construtor de Relatórios e SSRS)
  É possível adicionar uma dica de ferramenta a cada ponto de dados na série de um gráfico para exibir as informações relacionadas ao ponto de dados como, por exemplo, o nome do grupo, o valor do ponto de dados ou a porcentagem do ponto de dados em relação ao total de série quando os usuários passam pelo ponto de dados em um relatório renderizado.  
  
 Você não pode adicionar uma dica de ferramenta a uma série calculada.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-a-tooltip-on-each-data-point"></a>Para especificar uma dica de ferramenta em cada ponto de dados  
  
1.  Clique com o botão direito do mouse em uma série ou em um campo na área **Valores** e clique em **Propriedades da Série**.  
  
2.  Clique em **Dados da Série** e, para a propriedade **ToolTip** digite uma cadeia de caracteres ou expressão. É possível usar qualquer palavra-chave de um gráfico específico para representar outro elemento no gráfico. Para obter mais informações, consulte [pontos de dados de formatação em um gráfico &#40;construtor de relatórios e SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Formatando pontos de dados em um gráfico &#40;SSRS e construtor de relatórios&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Alterar o texto de um item de legenda &#40;Construtor de Relatórios e SSRS&#41;](chart-legend-change-item-text-report-builder.md)   
 [Formatando as cores da série em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [Adicionar uma ação de detalhamento a um relatório &#40;Construtor de Relatórios e SSRS&#41;](add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md)  
  
  