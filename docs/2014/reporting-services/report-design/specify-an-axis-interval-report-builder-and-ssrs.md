---
title: Especificar um intervalo do eixo (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: ae46712d-a5bf-44c0-9929-e30ccc1e7e33
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 46984681329be6e236cac6271d3768705a26dd7b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56027547"
---
# <a name="specify-an-axis-interval-report-builder-and-ssrs"></a>Especificar um intervalo do eixo (Construtor de Relatórios e SSRS)
  O intervalo do eixo define o número de rótulos e as marcas de escala associadas em um eixo. No eixo de valor, os intervalos do eixo fornecem uma medida consistente dos pontos de dados no gráfico. No entanto, no eixo de categoria, esta funcionalidade pode fazer com que as categorias sejam exibidas sem os rótulos do eixo. Você pode especificar o número de intervalos que deseja na propriedade Intervalo do eixo. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] calcula o número de intervalos no tempo de execução, com base nos dados do conjunto de resultados. Para obter mais informações sobre como os intervalos de eixo são calculados, consulte [Formatação de rótulos de eixo de um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md).  
  
 Este tópico não é aplicável para valores de data ou hora no eixo de categoria. Por padrão, os valores de `DateTime` são exibidos como dias. Para especificar um intervalo de data ou hora diferente, como um intervalo de mês ou hora, você deve formatar os rótulos dos eixos e definir o eixo para exibir instâncias de tipos `DateTime` em vez de tipos `String`. Além disso, você deve definir a propriedade Intervalo. Para obter mais informações, consulte [Formatar rótulos de eixo como datas ou moedas &#40;Construtor de Relatórios e SSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md).  
  
 Este tópico não se aplica a gráficos de pizza, rosca, funil ou pirâmide que não possuem eixos.  
  
> [!NOTE]  
>  O eixo de categoria geralmente é o eixo horizontal ou o eixo x. No entanto, para os gráficos de barras, o eixo de categoria é o vertical ou eixo y.  
  
 Um exemplo de um gráfico que especifica intervalos de eixos diferentes está disponível como um relatório de exemplo. Para obter mais informações sobre como baixar esse relatório de exemplo e outros, consulte [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][Relatórios de exemplo do Construtor de Relatórios e do Designer de Relatórios](https://go.microsoft.com/fwlink/?LinkId=198283).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-show-all-category-labels-on-the-x-axis"></a>Para mostrar todos os rótulos de categorias no eixo x  
  
1.  Clique com o botão direito do mouse no eixo da categoria e clique em **Propriedades do Eixo**. A caixa de diálogo **Propriedades do Eixo** é aberta.  
  
2.  Na **opções de eixo**, defina `Interval` à **1**. Cada rótulo do grupo de categorias é exibido. Para mostrar cada rótulo de outro grupo de categorias no eixo x, digite **2**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Quando um intervalo do eixo é definido, todos os rótulos automáticos são desabilitados. Se um valor para o intervalo do eixo for especificado, poderá ocorrer um comportamento imprevisível do rótulo, dependendo da quantidade de categorias existentes no eixo de categoria.  
  
### <a name="to-enable-a-variable-interval-calculation-on-an-axis"></a>Para habilitar um cálculo do intervalo de variáveis em um eixo  
  
1.  Clique com o botão direito do mouse no eixo do gráfico que deseja alterar e clique em **Propriedades do Eixo**. A caixa de diálogo **Propriedades do Eixo** é aberta.  
  
2.  Na **opções de eixo**, defina `Interval` à **automática**. O gráfico exibirá o número ideal de rótulos de categorias que podem se ajustar ao longo do eixo.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Formatando pontos de dados em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Classificar dados em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [Caixa de diálogo Propriedades do Eixo, Opções de Eixo &#40;Construtor de Relatórios e SSRS&#41;](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)   
 [Especificar uma escala logarítmica &#40;Construtor de Relatórios e SSRS&#41;](specify-a-logarithmic-scale-report-builder-and-ssrs.md)   
 [Plotar dados em um eixo secundário &#40;Construtor de Relatórios e SSRS&#41;](plot-data-on-a-secondary-axis-report-builder-and-ssrs.md)  
  
  
