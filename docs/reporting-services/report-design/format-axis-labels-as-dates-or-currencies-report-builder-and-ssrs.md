---
title: "Formatar r&#243;tulos de eixo como datas ou moedas (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e9a01a74-2f51-4b35-be3a-a6138568f6cf
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# Formatar r&#243;tulos de eixo como datas ou moedas (Construtor de Relat&#243;rios e SSRS)
Quando você mostrar os valores DateTime formatados corretamente em um eixo em um relatório paginado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], um gráfico exibirá automaticamente esses valores como dias. Para especificar um intervalo de data/hora para o eixo x, como um intervalo de meses ou de horas, você deverá formatar os rótulos dos eixos e definir o tipo de intervalo de eixo para um intervalo de data ou hora válido.  
  
> [!NOTE]  
>  Nos gráficos de coluna e de dispersão, o eixo horizontal, ou eixo x, é o eixo de categoria. Em gráficos de barras, o eixo vertical, ou eixo y, é o eixo de categoria.  
  
 Para formatar os intervalos de tempo corretamente, os valores exibidos no eixo x deverão ser avaliados para um tipo de dados <xref:System.DateTime>. Se seu campo tiver um tipo de dados <xref:System.String>, o gráfico não calculará os intervalos como datas ou horas. Para obter mais informações, consulte [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md).  
  
 Quando um valor numérico for adicionado ao eixo Y, por padrão, o gráfico não formatará o número antes de exibi-lo. Se seu campo numérico for um valor de vendas, considere formatar os números como moedas para aumentar a legibilidade do gráfico.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Para formatar os rótulos do eixo x como intervalos mensais  
  
1.  Clique com o botão direito do mouse no eixo x, ou horizontal, do gráfico e selecione **Propriedades HorizontalAxis**.  
  
2.  Na caixa de diálogo **Propriedades HorizontalAxis**, selecione **Número**.  
  
3.  Na lista de **Categorias**, selecione **Data**. Na lista **Tipo**, selecione um formato de data a ser aplicado nos rótulos do eixo x.  
  
4.  Selecione **Opções de Eixo**.  
  
5.  Em **Intervalo**, digite **1**. Na propriedade **Interval type**, selecione **Meses**.  
  
    > [!NOTE]  
    >  Se você não especificar um tipo de intervalo, o gráfico calculará os intervalos em termos de dias.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Para formatar os rótulos do eixo y usando um formato de conversor de moedas  
  
1.  Clique com o botão direito do mouse no eixo vertical, ou eixo y, do gráfico e selecione **Propriedades VerticalAxis**.  
  
2.  Na caixa de diálogo **Propriedades VerticalAxis**, selecione **Número**.  
  
3.  Na lista de **Categorias**, selecione **Conversor de Moedas**. Na lista **Símbolo**, selecione um formato de moeda a ser aplicado nos rótulos do eixo Y.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Consulte também  
 [Formatando rótulos dos eixos de um gráfico #40;Construtor de Relatórios e SSRS#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Especificar uma escala logarítmica &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/specify-a-logarithmic-scale-report-builder-and-ssrs.md)   
 [Especificar um intervalo do eixo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/specify-an-axis-interval-report-builder-and-ssrs.md)  
  
  