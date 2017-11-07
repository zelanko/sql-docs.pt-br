---
title: "Lição 7: Criar medidas | Microsoft Docs"
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 01bd2ad7-09b7-49ae-ad80-83f25da301aa
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f486e0094e66ed503b63fb52c4cba88dbcadbb62
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-6-create-measures"></a>Lição 6: Criar medidas
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

Nesta lição, você criará medidas a serem incluída no modelo. Semelhante às colunas calculadas que você criou na lição anterior, uma medida é um cálculo criado usando uma fórmula DAX. No entanto, diferente das colunas calculadas, são avaliadas medidas com base em um *filtro*selecionado pelo usuário; por exemplo, uma coluna ou uma segmentação de dados adicionada ao campo Rótulos de Linha em um Tabela Dinâmica. Um valor para cada célula no filtro é calculado pela medida aplicada. As medidas são cálculos avançados e flexíveis que você vai querer incluir em quase todos os modelos de tabela para executar cálculos dinâmicos em dados numéricos. Para obter mais informações, consulte [medidas](../analysis-services/tabular-models/measures-ssas-tabular.md).  
  
Para criar medidas, você usará o *grade de medida*. Por padrão, cada tabela tem uma grade de medida vazia; porém, você não criará medidas normalmente para cada tabela. A Grade de Medida aparece abaixo de uma tabela no designer de modelos em Exibição de Dados. Para ocultar ou exibir a grade de medida de uma tabela, clique no menu **Tabela** e em **Mostrar Grade de Medida**.  
  
Você pode criar uma medida clicando em uma célula vazia na grade de medida e digitando uma fórmula DAX na barra de fórmulas. Quando você clicar em ENTER para concluir a fórmula, a medida será exibida na célula. Você também pode criar medidas por meio de uma função de agregação padrão clicando em uma coluna e clicando no botão AutoSoma (**∑**) na barra de ferramentas. As medidas criadas usando o recurso AutoSoma aparecerão na célula da grade de medida diretamente abaixo da coluna, mas podem ser movidas.  
  
Nesta lição, você criará medidas inserindo uma fórmula DAX na barra de fórmulas e usando o recurso AutoSoma.  
  
Tempo estimado para concluir esta lição: **30 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 5: criar colunas calculadas](../analysis-services/lesson-5-create-calculated-columns.md).  
  
## <a name="create-measures"></a>Criar medidas  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a>Para criar uma medida de DaysCurrentQuarterToDate da tabela DimDate  
  
1.  No designer de modelo, clique o **DimDate** tabela.  
  
2.  Na grade de medida, clique na célula vazia superior esquerda.  
  
3.  Na barra de fórmulas, digite a fórmula a seguir:  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    Observe que a célula superior esquerda agora contém um nome de medida, **DaysCurrentQuarterToDate**, seguido pelo resultado, **92**.
    
      ![como-tabela-lesson6-novamedida](../analysis-services/media/as-tabular-lesson6-newmeasure.png) 
    
    Ao contrário de colunas calculadas, com fórmulas de medida, você pode digitar o nome de medida, seguido por uma vírgula, seguida pela expressão de fórmula.

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a>Para criar uma medida de DaysInCurrentQuarter da tabela DimDate  
  
1.  Com o **DimDate** tabela ainda ativa no designer de modelo, na grade de medida, clique na célula vazia abaixo da medida que você acabou de criar.  
  
2.  Na barra de fórmulas, digite a fórmula a seguir:  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    Ao criar uma taxa de comparação entre um período incompleto e o período anterior, a fórmula deve levar em conta a proporção do período decorrido e compará-la à mesma proporção do período anterior. Nesse caso, [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] fornece a proporção decorrido no período atual.  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a>Para criar uma medida InternetDistinctCountSalesOrder na tabela FactInternetSales  
  
1.  Clique o **FactInternetSales** tabela.   
  
2.  Clique no **SalesOrderNumber** título de coluna.  
  
3.  Na barra de ferramentas, clique na seta para baixo ao lado do botão AutoSoma (**∑**) e selecione **DistinctCount**.  
  
    O recurso AutoSoma cria automaticamente uma medida para a coluna selecionada por meio da fórmula de agregação padrão DistinctCount.  
    
       ![como-tabela-lesson6-newmeasure2](../analysis-services/media/as-tabular-lesson6-newmeasure2.png)
  
4.  Na grade de medida, clique em nova medida e, em seguida, no **propriedades** janela, na **nome da medida**, renomeie a medida para **InternetDistinctCountSalesOrder**. 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a>Para criar medidas adicionais na tabela FactInternetSales  
  
1.  Usando o recurso AutoSoma, crie e nomeie as seguintes medidas:  
  
    |Nome da Medida|Coluna|AutoSoma (∑)|Fórmula|  
    |----------------|----------|-----------------|-----------|  
    |InternetOrderLinesCount|SalesOrderLineNumber|Count|=COUNTA([SalesOrderLineNumber])|  
    |InternetTotalUnits|OrderQuantity|Sum|=SUM([OrderQuantity])|  
    |InternetTotalDiscountAmount|DiscountAmount|Sum|=SUM([DiscountAmount])|  
    |InternetTotalProductCost|TotalProductCost|Sum|=SUM([TotalProductCost])|  
    |InternetTotalSales|SalesAmount|Sum|=SUM([SalesAmount])|  
    |InternetTotalMargin|Margem|Sum|=SUM([Margem])|  
    |InternetTotalTaxAmt|TaxAmt|Sum|=SUM([TaxAmt])|  
    |InternetTotalFreight|Frete|Sum|=SUM([Frete])|  
  
2.  Clicando em uma célula vazia na grade de medida e usando a barra de fórmulas, crie e nomeie as seguintes medidas na ordem:  
  
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

  

