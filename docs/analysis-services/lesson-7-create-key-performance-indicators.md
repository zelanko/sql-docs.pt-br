---
title: 'Lição 7: Criar indicadores chave de desempenho | Microsoft Docs'
ms.date: 08/22/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ecfedbbc4b7e606f1589f2b5415c5355bb0d95e1
ms.sourcegitcommit: e8e013b4d4fbd3b25f85fd6318d3ca8ddf73f31e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42790097"
---
# <a name="lesson-7-create-key-performance-indicators"></a>Lição 7: criar indicadores chave de desempenho
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

Nesta lição, você criará KPIs (indicadores chave de desempenho). Os KPIs são usados para medir o desempenho de um valor, definido por uma medida *Base* , em relação a um valor de *Destino* , também definido por uma medida ou um valor absoluto. Nos aplicativos cliente de relatório, os KPIs podem proporcionar aos profissionais comerciais um modo rápido e fácil de entender um resumo de êxito comercial ou identificar tendências. Para obter mais informações, consulte [KPIs](../analysis-services/tabular-models/kpis-ssas-tabular.md).  
  
Tempo estimado para concluir esta lição: **15 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 6: criar medidas](../analysis-services/lesson-6-create-measures.md).   
  
## <a name="create-key-performance-indicators"></a>Criar indicadores chave de desempenho  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a>Para criar um KPI de InternetCurrentQuarterSalesPerformance  
  
1.  No designer de modelo, clique o **FactInternetSales** tabela (guia).  
  
2.  Na grade de medida, clique em uma célula vazia.  
  
3.  Na barra de fórmulas acima da tabela, digite a fórmula a seguir: 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=IFERROR([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    Esta medida servirá como medida Base para o KPI.  
  
4.  Clique com botão direito **InternetCurrentQuarterSalesPerformance** > **criar KPI**.   
  
5.  Na caixa de diálogo desempenho KPI (indicador chave), em **alvo** selecionar **valor absoluto**e, em seguida, digite **1.1**.  
  
7.  No campo de controle deslizante à esquerda (baixo), digite **1**e, no campo de controle deslizante à direita (alto), digite **1.07**.  
  
8.  Em **Selecionar Estilo de Ícone**, selecione o tipo de ícone losango (vermelho), triângulo (amarelo) e círculo (verde).
  
    ![como-tabela-lesson7-kpi](../analysis-services/media/as-tabular-lesson7-kpi.png)
    
    > [!TIP]  
    > Observe o expansível **descrições** rótulo abaixo dos estilos de ícone disponíveis. Use isso para inserir as descrições para os vários elementos KPI para torná-los mais identificáveis nos aplicativos cliente.  
  
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
  
5.  Em **Definir Limites de Status**, deslize o campo de controle deslizante à esquerda (baixo) até que ele exiba **0.8**e deslize o campo de controle deslizante à direita (alto) até que ele exiba **1.03**.  
  
6.  Em **Selecionar Estilo de Ícone**, selecione o tipo de ícone losango (vermelho), triângulo (amarelo) e círculo (verde) e clique em **OK**.  
  
## <a name="whats-next"></a>O que vem a seguir?
Vá para a próxima lição: [lição 8: criar perspectivas](../analysis-services/lesson-8-create-perspectives.md).
  
  
