---
title: Exibir valores de percentual em um gráfico de pizza (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: eb905fc1-5235-4773-a27e-b07be9318be5
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: d8c4cc67ad7a3719db277840e4ca535a373e8b44
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37287012"
---
# <a name="display-percentage-values-on-a-pie-chart-report-builder-and-ssrs"></a>Exibir valores de porcentagem em um gráfico de pizza (Construtor de Relatórios e SSRS)
  Por padrão, as categorias são mostradas na legenda para identificar cada valor. Se você rotulou o gráfico de pizza usando rótulos de categorias, poderá desejar mostrar porcentagens na legenda.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>Para exibir valores de porcentagem como rótulos em um gráfico de pizza  
  
1.  Adicione um gráfico de pizza ao relatório. Para obter mais informações, consulte [Adicionar um gráfico a um relatório &#40;Construtor de Relatórios e SSRS&#41;](add-a-chart-to-a-report-report-builder-and-ssrs.md).  
  
2.  Na superfície de design, clique com o botão direito do mouse no gráfico de pizza e selecione **Mostrar Rótulos de Dados**. Os rótulos de dados devem aparecer dentro de cada fatia do gráfico de pizza.  
  
3.  Na superfície de design, clique com o botão direito do mouse nos rótulos e selecione **Propriedades do Rótulo de Série**. A caixa de diálogo **Propriedades do Rótulo de Série** é exibida.  
  
4.  Tipo de `#PERCENT` para o **Rotular dados** opção.  
  
5.  (Opcional) Para especificar quantas casas decimais o rótulo deve mostrar, digite "#PERCENT{P*n*}" em que *n* é o número de casas decimais a serem exibidas. Por exemplo, para não exibir nenhuma casa decimal, digite "#PERCENT{P0}".  
  
### <a name="to-display-percentage-values-in-the-legend-of-a-pie-chart"></a>Para exibir valores percentuais na legenda de um gráfico de pizza  
  
1.  Na superfície de design, clique com o botão direito do mouse no gráfico de pizza e selecione **Propriedades da Série**. A caixa de diálogo **Propriedades da Série** é exibida.  
  
2.  Na **legenda**, digite `#PERCENT` para o **texto da legenda personalizada** propriedade.  
  
## <a name="see-also"></a>Consulte também  
 [Gráficos de pizza &#40;relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Formatando a legenda em um gráfico &#40;relatórios e SSRS&#41;](chart-legend-formatting-report-builder.md)   
 [Rótulos de ponto de dados de exibição fora de um gráfico de pizza &#40;relatórios e SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [Coletar fatias pequenas em um gráfico de pizza &#40;relatórios e SSRS&#41;](collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)  
  
  
