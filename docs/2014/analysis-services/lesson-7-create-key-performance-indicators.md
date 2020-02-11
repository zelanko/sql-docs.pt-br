---
title: 'Lição 8: criar indicadores chave de desempenho | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a6c8ac2b-64ba-456f-b418-7bf0afe145d1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1d9d3145583670fb849321bac5b57928caacfbc2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66078367"
---
# <a name="lesson-8-create-key-performance-indicators"></a>Lição 8: Criar indicadores chave de desempenho
  Nesta lição, você criará KPIs (indicadores chave de desempenho). Os KPIs são usados para medir o desempenho de um valor, definido por uma medida *base* , em relação a um valor de *destino* , também definido por uma medida ou por um valor absoluto. Em aplicativos cliente de relatório, KPIs podem fornecer aos profissionais de negócios uma maneira rápida e fácil de entender um resumo de sucesso nos negócios ou para identificar tendências. Para obter mais informações, consulte [KPIs &#40;SSAS Tabular&#41;](tabular-models/kpis-ssas-tabular.md).  
  
 Tempo estimado para conclusão desta lição: **15 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
 Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de executar as tarefas desta lição, você deverá ter concluído a lição anterior: [Lição 7: Criar medidas](lesson-6-create-measures.md).  
  
## <a name="create-key-performance-indicators"></a>Criar indicadores chave de desempenho  
  
#### <a name="to-create-an-internet-current-quarter-sales-performance-kpi"></a>Para criar um KPI de Desempenho de Vendas do Trimestre Atual da Internet  
  
1.  No designer de modelos, clique na tabela **Vendas pela Internet** (guia).  
  
2.  Na grade de medida, clique em uma célula vazia.  
  
3.  Na barra de fórmulas acima da tabela, digite a fórmula a seguir:  
  
     `Internet Current Quarter Sales Performance :=IFERROR([Internet Current Quarter Sales]/[Internet Previous Quarter Sales Proportion to QTD],BLANK())`  
  
     Ao concluir a criação da fórmula, pressione ENTER.  
  
     Essa medida servirá como a medida Base para o KPI.  
  
4.  Na grade de medida, clique com o botão direito do mouse na medida **Desempenho de Vendas pela Internet do Trimestre Atual** e clique em **Criar KPI**.  
  
     A caixa de diálogo **Indicador Chave de Desempenho** será aberta.  
  
5.  Na caixa de diálogo **Indicador Chave de Desempenho** , em **Definir Valor de Destino**, selecione a opção **Valor Absoluto** .  
  
6.  No campo **valor absoluto** , digite `1.1`e pressione Enter.  
  
7.  Em **definir limites de status**, no campo de controle deslizante à esquerda (baixo `1`), digite e, no campo de controle deslizante à direita `1.07`(alto), digite.  
  
8.  Em **Selecionar Estilo de Ícone**, selecione o tipo de ícone losango (vermelho), triângulo (amarelo) e círculo (verde).  
  
    > [!TIP]  
    >  Observe o campo expansível **Descrições** abaixo dos estilos de ícone disponíveis. Você pode digitar descrições para os vários elementos KPI para torná-los mais identificáveis nos aplicativos cliente.  
  
9. Clique em **OK** para concluir o KPI.  
  
     Na grade de medida, observe o ícone ao lado da medida **Desempenho de Vendas pela Internet do Trimestre Atual** . Esse ícone indica que essa medida serve como um valor Base para um KPI.  
  
#### <a name="to-create-an-internet-current-quarter-margin-performance-kpi"></a>Para criar um KPI de Desempenho de Margem do Trimestre Atual da Internet  
  
1.  Na grade de medida da tabela **Vendas pela Internet** , clique em uma célula vazia.  
  
2.  Na barra de fórmulas acima da tabela, digite a fórmula a seguir:  
  
     `Internet Current Quarter Margin Performance :=IF([Internet Previous Quarter Margin Proportion to QTD]<>0,([Internet Current Quarter Margin]-[Internet Previous Quarter Margin Proportion to QTD])/[Internet Previous Quarter Margin Proportion to QTD],BLANK())`  
  
     Ao concluir a criação da fórmula, pressione ENTER.  
  
3.  Na grade de medida, clique com o botão direito do mouse na medida **Desempenho de Margem da Internet do Trimestre Atual** e clique em **Criar KPI**.  
  
4.  Na caixa de diálogo **Indicador Chave de Desempenho** , em **Definir Valor de Destino**, selecione a opção **Valor Absoluto** .  
  
5.  No campo **valor absoluto** , digite `1.25`.  
  
6.  Em **Definir Limites de Status**, deslize o campo de controle deslizante à esquerda (baixo) até que ele exiba **0.8**e deslize o campo de controle deslizante à direita (alto) até que ele exiba **1.03**.  
  
7.  Em **Selecionar Estilo de Ícone**, selecione o tipo de ícone losango (vermelho), triângulo (amarelo), círculo (verde) e clique em **OK**.  
  
## <a name="next-step"></a>Próxima etapa  
 Para continuar este tutorial, vá para a próxima lição: [Lição 9: Criar perspectivas](lesson-8-create-perspectives.md).  
  
  
