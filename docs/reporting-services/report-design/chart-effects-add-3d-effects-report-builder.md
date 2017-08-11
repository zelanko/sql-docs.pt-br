---
title: "Adicionar efeitos 3D a um gráfico (construtor de relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ab9625d8-6557-4a4d-8123-eefa7c066ff5
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 7170699a3f0cbb26dd2376a8805978fe792223f0
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="chart-effects---add-3d-effects-report-builder"></a>Gráfico efeitos - adicionar efeitos 3D (construtor de relatórios)
  É possível usar efeitos 3D (tridimensionais) para fornecer profundidade e adicionar impacto visual aos gráficos em seus relatórios paginados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Por exemplo, para enfatizar uma fatia específica de um gráfico de pizza destacada, você pode girar e alterar a perspectiva do gráfico de modo que as pessoas observem essa fatia primeiro. Quando efeitos 3D são aplicados ao gráfico, todas as cores de gradiente e estilos de hachurado são desabilitados.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-apply-3d-effects-to-a-range-area-line-scatter-or-polar-chart"></a>Para aplicar efeitos 3D a um gráfico de intervalo, área, linha, dispersão ou polar  
  
1.  Clique com o botão direito do mouse em qualquer lugar na área do gráfico e selecione **Efeitos 3D**. A caixa de diálogo **Propriedades da Área do Gráfico** é exibida.  
  
2.  Em **Opções 3D**, selecione a opção **Habilitar 3D** .  
  
3.  (Opcional) Em **Opções 3D**, é possível definir uma variedade de propriedades referentes às opções de ângulos e cena em 3D. Para obter mais informações sobre essas propriedades, consulte [Efeitos 3D, bisel e outros efeitos em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/chart-effects-3d-bevel-and-other-report-builder.md).  
  
4.  Clique em **OK**.  
  
## <a name="to-apply-3d-effects-to-a-funnel-chart"></a>Para aplicar efeitos 3D a um gráfico de funil  
  
1.  Clique com o botão direito do mouse em qualquer lugar na área do gráfico e selecione **Efeitos 3D**. A caixa de diálogo **Propriedades da Área do Gráfico** é exibida.  
  
2.  Em **Opções 3D**, selecione a opção **Habilitar 3D** . Clique em **OK**.  
  
3.  (Opcional) Para personalizar a aparência visual do gráfico de funil, é possível ir para o painel Propriedades e alterar as propriedades específicas ao gráfico de funil.  
  
    1.  Abra o painel Propriedades.  
  
    2.  Na superfície de design, clique em qualquer lugar no funil. As propriedades para a série do gráfico de funil são exibidas no painel Propriedades.  
  
    3.  Na seção **Geral** , expanda o nó **CustomAttributes** .  
  
    4.  Para a propriedade **Funnel3DDrawingStyle** , selecione se o funil deve ser mostrado em forma circular ou quadrada.  
  
    5.  Para a propriedade **Funnel3DRotationAngle** , defina um valor entre -10 e 10. Isso determinará o grau de inclinação a ser exibido no gráfico de funil 3D.  
  
## <a name="to-apply-3d-effects-to-a-pie-chart"></a>Para aplicar efeitos 3D a um gráfico de pizza  
  
1.  Clique com o botão direito do mouse em qualquer lugar da área do gráfico e selecione Efeitos 3D. A caixa de diálogo **Propriedades da Área do Gráfico** é exibida.  
  
2.  Em **Opções 3D**, selecione a opção **Habilitar 3D** . Clique em **OK**.  
  
3.  (Opcional) Em **Rotação**, digite um valor inteiro que represente a rotação horizontal do gráfico de pizza.  
  
4.  (Opcional) Em **Inclinação**, digite um valor inteiro que represente a rotação da inclinação vertical do gráfico de pizza.  
  
5.  Clique em **OK**.  
  
## <a name="to-apply-3d-effects-to-a-bar-or-column-chart"></a>Para aplicar efeitos 3D a um gráfico de barras ou de colunas  
  
1.  Clique com o botão direito do mouse em qualquer lugar na área do gráfico e selecione **Efeitos 3D**. A caixa de diálogo **Propriedades da Área do Gráfico** é exibida.  
  
2.  Selecione a opção **Habilitar 3D** . Clique em **OK**.  
  
3.  (Opcional) Selecione a opção **Habilitar clustering da série** . Se o gráfico contiver várias séries de gráficos de barras ou de colunas, essa opção exibirá a série como clusterizada. Por padrão, várias séries de barras ou colunas são mostradas lado a lado.  
  
4.  Clique em **OK**.  
  
5.  (Opcional) Para adicionar efeitos de cilindro a um gráfico de barras ou de colunas, siga estas etapas:  
  
    1.  Abra o painel Propriedades.  
  
    2.  Na superfície de design, clique em qualquer uma das barras na série. As propriedades da série são exibidas no painel Propriedades.  
  
    3.  Na seção **Geral** , expanda o nó **CustomAttributes** .  
  
    4.  Para a propriedade **DrawingStyle** , especifique o valor do **Cilindro** .  
  
## <a name="see-also"></a>Consulte também  
 [Efeitos 3D, bisel e outros efeitos em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/chart-effects-3d-bevel-and-other-report-builder.md)   
 [Formatando um gráfico de &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Gráficos de &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
