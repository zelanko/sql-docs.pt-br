---
title: "Adicionar inclinação, relevo e estilos de textura a um gráfico (construtor de relatórios e SSRS) | Microsoft Docs"
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
ms.assetid: 737cfc80-b39e-497c-817b-b46693deb58f
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 2081d22c9e0aefd82cda5dff97b8ece503fdd9b0
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="chart-effects---add-bevel-emboss-or-texture-report-builder"></a>Efeitos do gráfico - adicionar inclinação, relevo, ou textura (construtor de relatórios)
  Ao usar determinados tipos de gráficos, você pode especificar um efeito de desenho para aumentar o impacto visual do seu gráfico. Esses efeitos de desenho só são aplicados à série de seu gráfico. Eles não têm nenhum efeito sobre qualquer outro elemento do gráfico.  
  
 Quando você está usando qualquer variante de um gráfico de pizza ou rosca, você pode especificar uma borda suave ou um estilo de desenho côncavo, semelhante aos efeitos de inclinação e relevo que podem ser aplicados a uma imagem.  
  
 Quando você está usando qualquer variante de um gráfico de colunas ou barras, você pode aplicar estilos de textura, como cilindro, entalhe e claro para escuro às colunas ou barras individuais.  
  
 Além desses estilos de desenho, você pode adicionar bordas e sombras a muitos elementos de gráfico para dar a ilusão de profundidade. Para obter mais informações sobre outras maneiras de formatar o gráfico, consulte [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-bevel-or-emboss-styles-to-a-pie-or-doughnut-chart"></a>Para adicionar estilos de inclinação ou relevo a um gráfico de pizza ou rosca  
  
1.  Na guia **Exibir** , selecione **Propriedades** para abrir o painel Propriedades.  
  
2.  Selecione o gráfico de pizza ou rosca que deseja aprimorar. Selecione o campo de dados no gráfico, não o gráfico inteiro.  
  
3.  No painel Propriedades, expanda o nó **CustomAttributes** .  
  
4.  Para PieDrawingStyle, selecione um estilo na lista suspensa.  
  
> [!NOTE]  
>  Você não pode ter os estilos 3D e bisel ou alto-relevo no mesmo gráfico. Se você habilitou 3D para o gráfico, não verá a propriedade PieDrawingStyle.  
  
 ![Gráfico de pizza com estilo de desenho Côncavo](../../reporting-services/report-design/media/rs-piedrawingeffects-concave.gif "gráfico de pizza com estilo de desenho Côncavo")  
  
### <a name="to-add-texture-styles-to-a-bar-or-column-chart"></a>Para adicionar estilos de textura a um gráfico de barras ou coluna  
  
1.  Selecione o gráfico de barras ou colunas que deseja aprimorar. Selecione o campo de dados no gráfico, não o gráfico inteiro.  
  
2.  Abra o painel Propriedades.  
  
3.  Expanda o nó **CustomAttributes** .  
  
4.  Para DrawingStyle, selecione um estilo na lista suspensa.  
  
> [!NOTE]  
>  Você não pode ter os estilos 3D e bisel ou alto-relevo no mesmo gráfico. Se você habilitou 3D para o gráfico, não verá a propriedade PieDrawingStyle.  
  
 ![Gráfico de barras com efeito de desenho LightToDark](../../reporting-services/report-design/media/rs-bardrawingeffects-lighttodark.gif "gráfico de barras com efeito de desenho LightToDark")  
  
## <a name="see-also"></a>Consulte também  
 [Gráficos de barras &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)   
 [Gráficos de colunas &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md)   
 [Gráficos de pizza &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
 [Formatando um gráfico de &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)  
  
  

