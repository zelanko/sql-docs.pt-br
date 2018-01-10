---
title: "Gráficos de ações (Construtor de Relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f75ca11e-b7f5-4ac0-ba17-fe6f82742dad
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f92366bf3f1e262f033827a5db0aa44d3526bde5
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="stock-charts-report-builder-and-ssrs"></a>Gráficos de ações (Construtor de Relatórios e SSRS)

  Um gráfico de estoque é especificamente projetado para dados financeiros ou científicos que usam até quatro valores por ponto de dados. Esses valores se alinham com os valores alto, baixo, aberto e fechado usados para plotar dados de estoque financeiro. Esse tipo de gráfico exibe valores de abertura e fechamento usando marcadores, que geralmente são linhas ou triângulos. No exemplo a seguir, os valores de abertura são mostrados pelos marcados à esquerda e os valores de fechamento são mostrados pelos marcadores à direita.  
  
 ![Gráfico de ações](../../reporting-services/report-design/media/rs-stockchart.gif "Gráfico de ações")  
  
 Um exemplo de um gráfico de ações está disponível como um relatório de exemplo do Construtor de Relatórios. Para obter mais informações sobre como baixar esse relatório de exemplo e outros, consulte [(Relatórios de exemplo do Construtor de relatórios e Designer de relatórios) do](http://go.microsoft.com/fwlink/?LinkId=198283).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>Variações  
  
-   **Velas**. O gráfico de velas é uma forma especializada do gráfico de estoque, na qual as caixas são usadas para mostrar a faixa entre os valores de abertura e fechamento. Da mesma forma que o gráfico de estoque, o gráfico de velas pode exibir até quatro valores por ponto de dados.  
  
## <a name="data-considerations-for-stock-charts"></a>Considerações de dados para gráficos de estoque  
  
-   Ao apresentar muitos pontos de dados de estoque, como tendências de preço de estoque anual, é difícil distinguir entre os valores aberto, fechado, alto e baixo de cada ponto de dados. Nesse cenário, considere usar um gráfico de linhas em vez de um gráfico de estoque.  
  
-   Quando os rótulos de eixos são gerados, a rotulação geralmente começa em zero.  Em geral, os preços de estoque não flutuam no mesmo grau que os outros conjuntos de dados. Por esse motivo, talvez você queira desativar os rótulos de eixos de iniciar em zero para obter uma melhor exibição de seus dados. Para fazer isso, defina **IncludeZero** como **false** na caixa de diálogo **Propriedades do Eixo** ou na janela Propriedades. Para obter mais informações sobre como o gráfico gera rótulos de eixo, consulte [Formatação de rótulos de eixo de um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md).  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece muitas fórmulas calculadas para uso com gráficos de estoque, inclusive Indicador de Preços, Índice de Força Relativa, MACD e outros.  

## <a name="next-steps"></a>Próximas etapas

[Gráficos de intervalo](../../reporting-services/report-design/range-charts-report-builder-and-ssrs.md)   
[Gráficos](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
[Formatando um gráfico](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
[Caixa de diálogo Propriedades do Eixo, Opções de Eixo](http://msdn.microsoft.com/library/b276e210-7a12-48ae-971b-7dabae51df11)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
