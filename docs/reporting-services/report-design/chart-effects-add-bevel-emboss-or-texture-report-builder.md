---
title: Adicionar estilos de bisel, auto-relevo e textura a um gráfico (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 737cfc80-b39e-497c-817b-b46693deb58f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 34f69e4c8c1b62e01f8cb73e26f84d05e427a9ed
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65581654"
---
# <a name="chart-effects---add-bevel-emboss-or-texture-report-builder"></a>Efeitos de gráfico – Adicionar bisel, alto-relevo ou textura (Construtor de Relatórios)
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
  
 ![Gráfico de pizza com estilo de desenho côncavo](../../reporting-services/report-design/media/rs-piedrawingeffects-concave.gif "Gráfico de pizza com estilo de desenho côncavo")  
  
### <a name="to-add-texture-styles-to-a-bar-or-column-chart"></a>Para adicionar estilos de textura a um gráfico de barras ou coluna  
  
1.  Selecione o gráfico de barras ou colunas que deseja aprimorar. Selecione o campo de dados no gráfico, não o gráfico inteiro.  
  
2.  Abra o painel Propriedades.  
  
3.  Expanda o nó **CustomAttributes** .  
  
4.  Para DrawingStyle, selecione um estilo na lista suspensa.  
  
> [!NOTE]  
>  Você não pode ter os estilos 3D e bisel ou alto-relevo no mesmo gráfico. Se você habilitou 3D para o gráfico, não verá a propriedade PieDrawingStyle.  
  
 ![Gráfico de barras com efeito de desenho LightToDark](../../reporting-services/report-design/media/rs-bardrawingeffects-lighttodark.gif "Gráfico de barras com efeito de desenho LightToDark")  
  
## <a name="see-also"></a>Consulte Também  
 [Gráficos de barras &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)   
 [Gráficos de colunas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md)   
 [Gráficos de pizza &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
 [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)  
  
  
