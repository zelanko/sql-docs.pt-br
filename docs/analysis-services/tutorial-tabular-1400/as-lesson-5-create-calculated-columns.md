---
title: 'Lição 5 do tutorial de serviços de análise: criar colunas calculadas | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 476eca07ed1367141372586ca13bd2a93d9d8105
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37973046"
---
# <a name="create-calculated-columns"></a>Criar colunas calculadas

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Nesta lição, você criará dados em seu modelo adicionando colunas calculadas. Você pode criar colunas calculadas (como colunas personalizadas) ao usar obter dados, usando o Editor de consultas ou posteriormente no similares de designer de modelo você fazer aqui. Para obter mais informações, consulte [colunas calculadas](../tabular-models/ssas-calculated-columns.md).
  
Você pode criar cinco novas colunas calculadas em três tabelas diferentes. As etapas são ligeiramente diferentes para cada tarefa, mostrando que há várias maneiras de criar colunas, renomeá-los e colocá-los em vários locais em uma tabela.  

Esta lição também é onde você usar expressões DAX (Data Analysis) pela primeira vez. DAX é uma linguagem especial para criar expressões de fórmula altamente personalizáveis para modelos de tabela. Neste tutorial, você pode usar DAX para criar colunas calculadas, medidas e filtros de função. Para obter mais informações, consulte [DAX em modelos de tabela](../tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md). 
  
Tempo estimado para concluir esta lição: **15 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  

Este artigo faz parte de um tutorial de modelagem de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 4: criar relações](../tutorial-tabular-1400/as-lesson-4-create-relationships.md). 
  
## <a name="create-calculated-columns"></a>Criar colunas calculadas  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a>Criar uma coluna calculada MonthCalendar na tabela DimDate  
  
1.  Clique o **modelo** menu > **exibição de modelo** > **exibição de dados**.  
  
    Colunas calculadas só podem ser criadas usando o designer de modelos na exibição de dados.  
  
2.  No designer de modelo, clique o **DimDate** tabela (guia).  
  
3.  Clique com botão direito do **CalendarQuarter** cabeçalho de coluna e clique **Inserir coluna**.  
  
    Uma nova coluna nomeada **Calculated Column 1** é inserida à esquerda da coluna **Calendar Quarter** .  
  
4.  Na barra de fórmulas acima da tabela, digite a seguinte fórmula DAX: preenchimento automático ajuda você a digitar os nomes totalmente qualificados de colunas e tabelas e lista as funções que estão disponíveis.  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    Os valores são preenchidos em todas as linhas da coluna calculada. Se você rolar para baixo na tabela, verá linhas podem ter valores diferentes para esta coluna, com base nos dados de cada linha.    
  
5.  Renomeie esta coluna como **MonthCalendar**. 

    ![as-lesson5-newcolumn](../tutorial-tabular-1400/media/as-lesson5-newcolumn.png) 
  
O MonthCalendar calculado coluna fornece um nome classificável para o mês.  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a>Criar uma coluna calculada DayOfWeek na tabela DimDate  
  
1.  Com o **DimDate** ainda ativa, clique de tabela os **coluna** menu e, em seguida, clique **adicionar coluna**.  
  
2.  Na barra de fórmulas, digite a fórmula a seguir:  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    Quando você terminar a criação da fórmula, pressione ENTER. A nova coluna será adicionada à extrema direita da tabela.  
  
3.  Renomeie a coluna como **DayOfWeek**.  
  
4.  Clique no título de coluna e, em seguida, arraste a coluna entre a **EnglishDayNameOfWeek** coluna e o **DayNumberOfMonth** coluna.  
  
    > [!TIP]  
    > A movimentação das colunas na tabela facilita a navegação.  
  
A coluna calculada DayOfWeek fornece um nome classificável para o dia da semana.  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a>Criar uma coluna calculada ProductSubcategoryName na tabela DimProduct  
  
  
1.  No **DimProduct** tabela, role até a extrema direita da tabela. Observe que a coluna mais à direita é chamada **Adicionar Coluna** (em itálico); clique no título de coluna.  
  
2.  Na barra de fórmulas, digite a fórmula a seguir:  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  Renomeie a coluna como **ProductSubcategoryName**.  
  
A coluna calculada ProductSubcategoryName é usada para criar uma hierarquia na tabela DimProduct, a qual inclui dados da coluna EnglishProductSubcategoryName na tabela DimProductSubcategory. As hierarquias não podem ultrapassar mais de uma tabela. Você pode criar hierarquias posteriormente na lição 9.  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a>Criar uma coluna calculada ProductCategoryName na tabela DimProduct  
  
1.  Com o **DimProduct** ainda ativa, clique de tabela os **coluna** menu e, em seguida, clique **adicionar coluna**.  
  
2.  Na barra de fórmulas, digite a fórmula a seguir:  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  Renomeie a coluna como **ProductCategoryName**.  
  
A coluna calculada ProductCategoryName é usada para criar uma hierarquia na tabela DimProduct, a qual inclui dados da coluna EnglishProductCategoryName na tabela DimProductCategory. As hierarquias não podem ultrapassar mais de uma tabela.  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a>Criar uma coluna calculada Margin na tabela FactInternetSales  
  
1.  No designer de modelo, selecione a **FactInternetSales** tabela.  
  
2.  Criar uma nova coluna calculada entre o **SalesAmount** coluna e o **TaxAmt** coluna.  
  
3.  Na barra de fórmulas, digite a fórmula a seguir:  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  Renomeie a coluna como **Margin**.  
 
      ![as-lesson5-newmargin](../tutorial-tabular-1400/media/as-lesson5-newmargin.png)
      
    A coluna calculada Margin é usada para analisar as margens de lucro de cada venda.  
  
## <a name="whats-next"></a>O que vem a seguir?

[Lição 6: Criar medidas](../tutorial-tabular-1400/as-lesson-6-create-measures.md).
  
  
  
