---
title: 'Analysis Services lição do tutorial 7: Criar indicadores chave de desempenho | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 348a012b5915c6b02f04481673fc33128001ff73
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685400"
---
# <a name="create-key-performance-indicators"></a>Criar indicadores chave de desempenho

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Nesta lição, você deve criar indicadores chave de desempenho (KPIs). Os KPIs são usados para medir o desempenho de um valor definido por uma *Base* medida, em relação a um *destino* também definido por uma medida ou valor absoluto do valor. Nos aplicativos cliente de relatório, os KPIs podem proporcionar aos profissionais comerciais um modo rápido e fácil de entender um resumo de êxito comercial ou identificar tendências. Para obter mais informações, consulte [KPIs](../tabular-models/kpis-ssas-tabular.md)
  
Tempo estimado para concluir esta lição: **15 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  

Este artigo faz parte de um tutorial de modelagem de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 6: Criar medidas](../tutorial-tabular-1400/as-lesson-6-create-measures.md).   
  
## <a name="create-key-performance-indicators"></a>Criar indicadores chave de desempenho  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a>Para criar um KPI de InternetCurrentQuarterSalesPerformance  
  
1.  No designer de modelo, clique o **FactInternetSales** tabela.  
  
2.  Na grade de medida, clique em uma célula vazia.  
  
3.  Na barra de fórmulas acima da tabela, digite a fórmula a seguir: 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    Essa medida serve como a medida Base para o KPI.  
  
4.  Na grade de medida, clique com botão direito **InternetCurrentQuarterSalesPerformance** > **criar KPI**.   
  
5.  Na caixa de diálogo desempenho KPI (indicador chave), em **alvo** selecionar **valor absoluto**e, em seguida, digite **1.1**.  
  
7.  No campo de controle deslizante à esquerda (baixo), digite **1**e, no campo de controle deslizante à direita (alto), digite **1.07**.  
  
8.  Em **Selecionar Estilo de Ícone**, selecione o tipo de ícone losango (vermelho), triângulo (amarelo) e círculo (verde).
  
    ![as-lesson7-kpi](../tutorial-tabular-1400/media/as-lesson7-kpi.png)
    
    > [!TIP]  
    > Observe o expansível **descrições** rótulo abaixo dos estilos de ícone disponíveis. Use as descrições para os vários elementos KPI para torná-los mais identificáveis nos aplicativos cliente.  
  
9. Clique em **OK** para concluir o KPI.  
  
    Na grade de medida, observe o ícone ao lado de **InternetCurrentQuarterSalesPerformance** medidas. Esse ícone indica que essa medida serve como um valor Base para um KPI.  
  
#### <a name="to-create-an-internetcurrentquartermarginperformance-kpi"></a>Para criar um KPI de InternetCurrentQuarterMarginPerformance  
  
1.  Na grade de medida para o **FactInternetSales** da tabela, clique em uma célula vazia.  
  
2.  Na barra de fórmulas acima da tabela, digite a fórmula a seguir:  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  Clique com botão direito **InternetCurrentQuarterMarginPerformance** > **criar KPI**.  
  
4.  Na caixa de diálogo desempenho KPI (indicador chave), em **alvo** selecionar **valor absoluto**e, em seguida, digite **1,25**.   
  
5.  No campo de controle deslizante esquerdo de (baixo), deslize até que o campo exiba **0.8**e, em seguida, deslize o controle deslizante à direita (alto) campo até que o campo exiba **1.03**.  
  
6.  Em **Selecionar Estilo de Ícone**, selecione o tipo de ícone losango (vermelho), triângulo (amarelo) e círculo (verde) e clique em **OK**.  
  
## <a name="whats-next"></a>O que vem a seguir?

[Lição 8: Criar perspectivas](../tutorial-tabular-1400/as-lesson-8-create-perspectives.md).
  
  
