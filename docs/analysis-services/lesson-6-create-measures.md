---
title: 'Lição 7: Criar medidas | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 146d93bc2c7257ce409f3a293f6c9050acde9ca7
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37994958"
---
# <a name="lesson-6-create-measures"></a>Lição 6: Criar medidas
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

Nesta lição, você criará medidas a serem incluída no modelo. Semelhante às colunas calculadas que você criou na lição anterior, uma medida é um cálculo criado usando uma fórmula DAX. No entanto, diferente das colunas calculadas, são avaliadas medidas com base em um *filtro*selecionado pelo usuário; por exemplo, uma coluna ou uma segmentação de dados adicionada ao campo Rótulos de Linha em um Tabela Dinâmica. Um valor para cada célula no filtro é calculado pela medida aplicada. As medidas são cálculos avançados e flexíveis que você deseja incluir em quase todos os modelos tabulares para executar cálculos dinâmicos em dados numéricos. Para obter mais informações, consulte [medidas](../analysis-services/tabular-models/measures-ssas-tabular.md).  
  
Para criar medidas, você usará o *grade de medida*. Por padrão, cada tabela tem uma grade de medida vazia; porém, você não criará medidas normalmente para cada tabela. A Grade de Medida aparece abaixo de uma tabela no designer de modelos em Exibição de Dados. Para ocultar ou exibir a grade de medida de uma tabela, clique no menu **Tabela** e em **Mostrar Grade de Medida**.  
  
Você pode criar uma medida clicando em uma célula vazia na grade de medida e digitando uma fórmula DAX na barra de fórmulas. Quando você clicar em ENTER para concluir a fórmula, a medida será exibida na célula. Você também pode criar medidas por meio de uma função de agregação padrão clicando em uma coluna e clicando no botão AutoSoma (**∑**) na barra de ferramentas. As medidas criadas usando o recurso AutoSoma aparecerão na célula da grade de medida diretamente abaixo da coluna, mas podem ser movidas.  
  
Nesta lição, você criará medidas inserindo uma fórmula DAX na barra de fórmulas e usando o recurso AutoSoma.  
  
Tempo estimado para concluir esta lição: **30 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 5: criar colunas calculadas](../analysis-services/lesson-5-create-calculated-columns.md).  
  
## <a name="create-measures"></a>Criar medidas  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a>Para criar uma medida DaysCurrentQuarterToDate na tabela DimDate  
  
1.  No designer de modelo, clique o **DimDate** tabela.  
  
2.  Na grade de medida, clique na célula vazia superior esquerda.  
  
3.  Na barra de fórmulas, digite a fórmula a seguir:  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    Observe que a célula superior esquerda agora contém um nome de medida **DaysCurrentQuarterToDate**, seguido do resultado **92**.
    
      ![como-tabela-lesson6-novamedida](../analysis-services/media/as-tabular-lesson6-newmeasure.png) 
    
    Ao contrário de colunas calculadas, com fórmulas de medida, você pode digitar o nome da medida, seguido por uma vírgula, seguida pela expressão da fórmula.

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a>Para criar uma medida DaysInCurrentQuarter na tabela DimDate  
  
1.  Com o **DimDate** ainda ativa no designer de modelo, na grade de medida da tabela, clique na célula vazia abaixo da medida que você acabou de criar.  
  
2.  Na barra de fórmulas, digite a fórmula a seguir:  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    Ao criar uma taxa de comparação entre um período incompleto e o período anterior, a fórmula deve levar em conta a proporção do período decorrido e compará-la à mesma proporção do período anterior. Nesse caso, [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] fornece a proporção decorrida no período atual.  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a>Para criar uma medida InternetDistinctCountSalesOrder na tabela FactInternetSales  
  
1.  Clique o **FactInternetSales** tabela.   
  
2.  Clique no **SalesOrderNumber** título de coluna.  
  
3.  Na barra de ferramentas, clique na seta para baixo ao lado do botão AutoSoma (**∑**) e selecione **DistinctCount**.  
  
    O recurso AutoSoma cria automaticamente uma medida para a coluna selecionada por meio da fórmula de agregação padrão DistinctCount.  
    
       ![como-tabela-lesson6-newmeasure2](../analysis-services/media/as-tabular-lesson6-newmeasure2.png)
  
4.  Na grade de medida, clique na nova medida e, em seguida, nos **propriedades** janela, na **nome da medida**, renomeie a medida para **InternetDistinctCountSalesOrder**. 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a>Para criar medidas adicionais na tabela FactInternetSales  
  
1.  Usando o recurso AutoSoma, crie e nomeie as seguintes medidas:  
  
    |Nome da Medida|coluna|AutoSoma (∑)|Fórmula|  
    |----------------|----------|-----------------|-----------|  
    |InternetOrderLinesCount|SalesOrderLineNumber|Count|=COUNTA([SalesOrderLineNumber])|  
    |InternetTotalUnits|OrderQuantity|SUM|=SUM([OrderQuantity])|  
    |InternetTotalDiscountAmount|DiscountAmount|SUM|=SUM([DiscountAmount])|  
    |InternetTotalProductCost|TotalProductCost|SUM|=SUM([TotalProductCost])|  
    |InternetTotalSales|SalesAmount|SUM|=SUM([SalesAmount])|  
    |InternetTotalMargin|Margem|SUM|=SUM([Margem])|  
    |InternetTotalTaxAmt|TaxAmt|SUM|=SUM([TaxAmt])|  
    |InternetTotalFreight|Freight|SUM|=SUM([Frete])|  
  
2.  Ao clicar em uma célula vazia na grade de medida e usando a barra de fórmulas, crie e nomeie as seguintes medidas na ordem:  
  
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
Vá para a próxima lição: [lição 7: criar indicadores chave de desempenho](../analysis-services/lesson-7-create-key-performance-indicators.md).  

  
