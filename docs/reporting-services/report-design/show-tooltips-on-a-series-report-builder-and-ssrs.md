---
title: "Mostrar dicas de ferramenta em uma série (construtor de relatórios e SSRS) | Microsoft Docs"
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
ms.assetid: 4c9606ff-e1c3-4cf7-a4e7-bb16f1a9e8ab
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5e963b234c5c3babb4dd2302afca2ca06ac249b1
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="show-tooltips-on-a-series-report-builder-and-ssrs"></a>Mostrar dicas de ferramenta em uma série (Construtor de Relatórios e SSRS)
  É possível adicionar uma dica de ferramenta a cada ponto de dados na série de um gráfico para exibir as informações relacionadas ao ponto de dados, por exemplo, o nome do grupo, o valor do ponto de dados ou o percentual do ponto de dados em relação ao total de série. Quando os usuários focalizam o ponto de dados em um relatório paginado renderizado, eles verão essas informações.  
  
 Você não pode adicionar uma dica de ferramenta a uma série calculada.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-specify-a-tooltip-on-each-data-point"></a>Para especificar uma dica de ferramenta em cada ponto de dados  
  
1.  Clique com o botão direito do mouse em uma série ou em um campo na área **Valores** e clique em **Propriedades da Série**.  
  
2.  Clique em **Dados da Série** e, para a propriedade **ToolTip** digite uma cadeia de caracteres ou expressão. É possível usar qualquer palavra-chave de um gráfico específico para representar outro elemento no gráfico. Para obter mais informações, consulte [Formatando pontos de dados em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Formatando pontos de dados em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Alterar o texto de um item de legenda &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/chart-legend-change-item-text-report-builder.md)   
 [Formatando as cores da série em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [Adicionar uma ação de detalhamento a um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md)  
  
  
