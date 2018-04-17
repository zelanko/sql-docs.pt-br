---
title: 'Lição tutorial do Analysis Services 6: criar medidas | Microsoft Docs'
description: Descreve como criar medidas no projeto do tutorial do Analysis Services.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: d37b1c5a307ea7f9c90fa29c83536a4b3d8ef0bf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="create-measures"></a>Criar medidas

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Nesta lição, você criará medidas a serem incluídos em seu modelo. Semelhante às colunas calculadas que você criou, uma medida é um cálculo criado usando uma fórmula DAX. No entanto, ao contrário de colunas calculadas, medidas são avaliadas com base em um usuário selecionado *filtro*. Por exemplo, uma coluna específica ou segmentação de dados adicionada ao campo rótulos de linha em uma tabela dinâmica. Um valor para cada célula no filtro é calculado pela medida aplicada. As medidas são cálculos avançados e flexíveis que você deseja incluir em quase todos os modelos de tabela para executar cálculos dinâmicos em dados numéricos. Para obter mais informações, consulte [medidas](../tabular-models/measures-ssas-tabular.md).
  
Para criar medidas, você deve usar o *grade de medida*. Por padrão, cada tabela tem uma grade de medida vazia; No entanto, você normalmente não criar medidas para cada tabela. A Grade de Medida aparece abaixo de uma tabela no designer de modelos em Exibição de Dados. Para ocultar ou exibir a grade de medida de uma tabela, clique no menu **Tabela** e em **Mostrar Grade de Medida**.  
  
Você pode criar uma medida clicando em uma célula vazia na grade de medida e digitando uma fórmula DAX na barra de fórmulas. Quando você clicar em ENTER para completar a fórmula, a medida e aparecerá na célula. Você também pode criar medidas usando uma função de agregação padrão clicando em uma coluna e, em seguida, clicar no botão AutoSoma (**∑**) na barra de ferramentas. As medidas criadas usando o recurso AutoSoma aparecem na célula da grade de medida diretamente abaixo da coluna, mas podem ser movidas.  
  
Nesta lição, você criará medidas inserindo uma fórmula DAX na barra de fórmulas e usando o recurso AutoSoma.  
  
Tempo estimado para concluir esta lição: **30 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  

Este artigo faz parte de um tutorial de modelagem de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 5: criar colunas calculadas](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md).  
  
## <a name="create-measures"></a>Criar medidas  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a>Para criar uma medida de DaysCurrentQuarterToDate da tabela DimDate  
  
1.  No designer de modelo, clique o **DimDate** tabela.  
  
2.  Na grade de medida, clique na célula vazia superior esquerda.  
  
3.  Na barra de fórmulas, digite a fórmula a seguir:  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    Observe que a célula superior esquerda agora contém um nome de medida, **DaysCurrentQuarterToDate**, seguido pelo resultado, **92**. O resultado não é relevante neste momento porque nenhum filtro de usuário foi aplicado.
    
      ![novamedida como lesson6](../tutorial-tabular-1400/media/as-lesson6-newmeasure.png) 
    
    Diferente das colunas calculadas, com fórmulas de medida, você pode digitar o nome da medida, seguido por dois-pontos, seguido pela expressão de fórmula.

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a>Para criar uma medida de DaysInCurrentQuarter da tabela DimDate  
  
1.  Com o **DimDate** tabela ainda ativa no designer de modelo, na grade de medida, clique na célula vazia abaixo da medida que você criou.  
  
2.  Na barra de fórmulas, digite a fórmula a seguir:  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    Ao criar uma taxa de comparação entre um período incompleto e o período anterior. A fórmula deve calcular a proporção do período decorrido e compará-la à mesma proporção do período anterior. Nesse caso, [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] fornece a proporção decorrido no período atual.  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a>Para criar uma medida InternetDistinctCountSalesOrder na tabela FactInternetSales  
  
1.  Clique o **FactInternetSales** tabela.   
  
2.  Clique o **SalesOrderNumber** título de coluna.  
  
3.  Na barra de ferramentas, clique na seta para baixo ao lado do botão AutoSoma (**∑**) e selecione **DistinctCount**.  
  
    O recurso AutoSoma cria automaticamente uma medida para a coluna selecionada por meio da fórmula de agregação padrão DistinctCount.  
    
       ![as-lesson6-newmeasure2](../tutorial-tabular-1400/media/as-lesson6-newmeasure2.png)
  
4.  Na grade de medida, clique em nova medida e, em seguida, no **propriedades** janela, na **nome da medida**, renomeie a medida para **InternetDistinctCountSalesOrder**. 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a>Para criar medidas adicionais na tabela FactInternetSales  
  
1.  Usando o recurso AutoSoma, crie e nomeie as seguintes medidas:  

    |Coluna|Nome da medida|AutoSoma (∑)|Fórmula|  
    |----------------|----------|-----------------|-----------|  
    |SalesOrderLineNumber|InternetOrderLinesCount|Count|=COUNTA([SalesOrderLineNumber])|  
    |OrderQuantity|InternetTotalUnits|SUM|=SUM([OrderQuantity])|  
    |DiscountAmount|InternetTotalDiscountAmount|SUM|=SUM([DiscountAmount])|  
    |TotalProductCost|InternetTotalProductCost|SUM|=SUM([TotalProductCost])|  
    |SalesAmount|InternetTotalSales|SUM|=SUM([SalesAmount])|  
    |Margem|InternetTotalMargin|SUM|=SUM([Margem])|  
    |TaxAmt|InternetTotalTaxAmt|SUM|=SUM([TaxAmt])|  
    |Freight|InternetTotalFreight|SUM|=SUM([Frete])|  
  
2.  Ao clicar em uma célula vazia na grade de medida e usando a barra de fórmulas, crie, as seguintes medidas personalizadas na ordem:  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
As medidas criadas para a tabela FactInternetSales podem ser usadas para analisar dados financeiros essenciais, como vendas, custos e margem de lucro para itens definidos pelo filtro selecionado de usuário.  
  
## <a name="whats-next"></a>O que vem a seguir?

[Lição 7: Criar indicadores chave de desempenho](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md).  

  
