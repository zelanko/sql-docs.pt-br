---
title: Exibir valores de percentual em um gráfico de pizza (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: eb905fc1-5235-4773-a27e-b07be9318be5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 007a4be9ae31ca6588f1381bc6fa0f4c658d2c35
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59955592"
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
 [Gráficos de pizza &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Formatando a legenda em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](chart-legend-formatting-report-builder.md)   
 [Exibir rótulos de pontos de dados fora de um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [Coletar fatias pequenas em um gráfico de pizza &#40;Construtor de Relatórios e SSRS&#41;](collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)  
  
  
