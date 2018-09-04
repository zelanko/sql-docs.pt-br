---
title: Especificar uma escala logarítmica (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: f3092c1c-b128-433d-9a95-983508b2a8d4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d90feceb685fe70038bfa1e9af14ddc95fb6087c
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43276248"
---
# <a name="specify-a-logarithmic-scale-report-builder-and-ssrs"></a>Especificar uma escala logarítmica (Construtor de Relatórios e SSRS)
  Se você tem dados que são logaritmicamente proporcionais, é recomendável usar uma escala logarítmica em um gráfico em um relatório paginado do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] . Isso ajuda a melhorar a aparência do gráfico tornando seus dados mais gerenciáveis. A maioria das escalas logarítmicas usa uma base de 10.  
  
 Esse recurso está disponível somente no eixo de valor. Geralmente, o eixo de valor é o eixo vertical, ou eixo y. No entanto, em gráficos de barras, ele é o eixo horizontal, ou eixo x.  
  
 Se seu eixo for logarítmico, todas as outras propriedades relacionadas ao eixo serão logaritmicamente escaladas. Por exemplo, se você especificar uma escala logarítmica de base 10 em seu eixo, definir um intervalo de eixo de 2 gerará intervalos em magnitudes de 10 para a potência de 2 ou 100. Isso significa que os valores do eixo lerão 1, 100, 10.000, em vez do resultado padrão de 1, 10, 100, 1.000, 10.000.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-specify-a-logarithmic-scale"></a>Para especificar uma escala logarítmica  
  
1.  Clique com o botão direito do mouse no eixo y de seu gráfico e clique em **Propriedades VerticalAxis**. A caixa de diálogo **Propriedades VerticalAxis** aparece.  
  
2.  Em **Opções de Eixo**, selecione **Escala Uselogarithmic**.  
  
3.  Na caixa de texto **Base de log** , digite um valor positivo para a base logarítmica. Se nenhum valor for especificado, a base logarítmica assumirá 10 como padrão.  
  
## <a name="see-also"></a>Consulte Também  
 [Formatando rótulos dos eixos de um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Formatar rótulos de eixo como datas ou moedas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
