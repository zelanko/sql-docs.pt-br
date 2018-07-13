---
title: Formatar rótulos de eixo como datas ou moedas (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e9a01a74-2f51-4b35-be3a-a6138568f6cf
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 21281fe3b01f8b6ed89042f9abb9f8eb9f1d4edf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37192886"
---
# <a name="format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs"></a>Formatar rótulos de eixo como datas ou moedas (Construtor de Relatórios e SSRS)
  Quando você mostrar os valores DateTime formatados corretamente em um eixo, um gráfico exibirá automaticamente esses valores como dias. Para especificar um intervalo de data/hora para o eixo x, como um intervalo de meses ou de horas, você deverá formatar os rótulos dos eixos e definir o tipo de intervalo de eixo para um intervalo de data ou hora válido.  
  
> [!NOTE]  
>  Nos gráficos de coluna e de dispersão, o eixo horizontal, ou eixo x, é o eixo de categoria. Em gráficos de barras, o eixo vertical, ou eixo y, é o eixo de categoria.  
  
 Para formatar os intervalos de tempo corretamente, os valores exibidos no eixo x deverão ser avaliados para um tipo de dados <xref:System.DateTime> . Se seu campo tiver um tipo de dados <xref:System.String>, o gráfico não calculará os intervalos como datas ou horas. Para obter mais informações, consulte [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md).  
  
 Quando um valor numérico for adicionado ao eixo Y, por padrão, o gráfico não formatará o número antes de exibi-lo. Se seu campo numérico for um valor de vendas, considere formatar os números como moedas para aumentar a legibilidade do gráfico.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-format-x-axis-labels-as-monthly-intervals"></a>Para formatar os rótulos do eixo x como intervalos mensais  
  
1.  Clique com o botão direito do mouse no eixo x, ou horizontal, do gráfico e selecione **Propriedades HorizontalAxis**.  
  
2.  Na caixa de diálogo **Propriedades HorizontalAxis** , selecione **Número**.  
  
3.  Na lista de **Categorias** , selecione **Data**. Na lista **Tipo** , selecione um formato de data a ser aplicado nos rótulos do eixo x.  
  
4.  Selecione **Opções de Eixo**.  
  
5.  Em **Intervalo**, digite **1**. Na propriedade **Interval type** , selecione **Meses**.  
  
    > [!NOTE]  
    >  Se você não especificar um tipo de intervalo, o gráfico calculará os intervalos em termos de dias.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-format-y-axis-labels-using-a-currency-format"></a>Para formatar os rótulos do eixo y usando um formato de conversor de moedas  
  
1.  Clique com o botão direito do mouse no eixo vertical, ou eixo y, do gráfico e selecione **Propriedades VerticalAxis**.  
  
2.  Na caixa de diálogo **Propriedades VerticalAxis** , selecione **Número**.  
  
3.  Na lista de **Categorias** , selecione **Conversor de Moedas**. Na lista **Símbolo** , selecione um formato de moeda a ser aplicado nos rótulos do eixo Y.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Formatando rótulos dos eixos de um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Especificar uma escala logarítmica &#40;Construtor de Relatórios e SSRS&#41;](specify-a-logarithmic-scale-report-builder-and-ssrs.md)   
 [Especifique um intervalo do eixo &#40;relatórios e SSRS&#41;](specify-an-axis-interval-report-builder-and-ssrs.md)  
  
  
