---
title: Testando a exatidão com gráficos de comparação de precisão (tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 822d414b-4a39-473f-80c3-53476e30655a
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 06cefcdac192b715fe843f842088456f769cdd24
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63042568"
---
# <a name="testing-accuracy-with-lift-charts-basic-data-mining-tutorial"></a>Testando a precisão com gráficos de comparação de precisão (Tutorial de mineração de dados básico)
  Na guia **gráfico de precisão de mineração** do designer de mineração de dados, você pode calcular como cada um de seus modelos faz previsões e comparar os resultados de cada modelo diretamente com os resultados dos outros modelos. Esse método de comparação é conhecido como um gráfico de aumento de *precisão*. Normalmente, a precisão da previsão de um modelo de mineração é medida pela comparação de precisão ou pela precisão de classificação. Para este tutorial, só usaremos o gráfico de comparação de precisão.  
  
 Neste tópico, você executará as seguintes tarefas:  
  
-   [Escolher os dados de entrada](#BKMK_InputData)  
  
-   [Configurar parâmetros do gráfico de precisão](#BKMK_Selecting)  
  
##  <a name="BKMK_InputData"></a>Escolhendo os dados de entrada  
 A primeira etapa para testar a precisão dos modelos de mineração é selecionar a fonte de dados que será usada para teste. Você testará o desempenho dos modelos com os dados de teste e os usará com dados externos.  
  
#### <a name="to-select-the-data-set"></a>Para selecionar o conjunto de dados  
  
1.  Alterne para a guia **gráfico de precisão de mineração** no designer de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] mineração de dados no e selecione a guia **seleção de entrada** .  
  
2.  Na caixa de grupo **selecionar conjunto de dados a ser usado para o gráfico de precisão** , selecione **usar casos de teste da estrutura de mineração**. Esses são os dados de teste que você reservou quando criou a estrutura de mineração.  
  
     Para obter mais informações sobre as outras opções, consulte [escolher um tipo de gráfico de precisão e definir opções de gráfico](../../2014/analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md).  
  
##  <a name="BKMK_Selecting"></a>Definindo parâmetros de gráfico de precisão  
 Para criar um gráfico de precisão, você deve definir três parâmetros:  
  
-   Que modelos você deve incluir no gráfico de precisão?  
  
-   Que atributo previsível você deseja medir? Alguns modelos podem ter vários destinos, mas cada gráfico pode medir apenas um resultado de cada vez.  
  
     Para usar uma coluna como o **nome de coluna previsível** em um gráfico de precisão, as colunas devem ter o `Predict` tipo `Predict Only`de uso de ou. Além disso, o tipo de conteúdo da coluna de destino deve ser `Discrete` ou `Discretized`. Em outras palavras, você não pode medir a precisão em relação a resultados numéricos contínuos que usem o gráfico de comparação de precisão.  
  
-   Deseja medir a precisão geral do modelo ou sua precisão na previsão de um valor específico (como [comprador de bicicletas] = ' Sim ')  
  
#### <a name="to-generate-the-lift-chart"></a>Para gerar o gráfico de comparação de precisão  
  
1.  Na guia **seleção de entrada** do designer de mineração de dados, em **selecionar colunas do modelo de mineração previsível para mostrar no gráfico**de comparação de precisão, marque a caixa de seleção para **sincronizar colunas de previsão e valores**.  
  
2.  Na coluna **nome da coluna previsível** , verifique se o **comprador de bicicleta** está selecionado para cada modelo.  
  
3.  Na coluna **Mostrar** , selecione cada um dos modelos.  
  
     Por padrão, são selecionados todos os modelos na estrutura de mineração. Você pode optar por não incluir um modelo, mas para este tutorial deixe todos os modelos selecionados.  
  
4.  Na coluna **valor da previsão** , selecione **1**. O mesmo valor é preenchido automaticamente para cada modelo que tenha a mesma coluna previsível.  
  
5.  Selecione a guia gráfico de comparação de **precisão** .  
  
     Quando você clicar na guia, uma consulta de previsão será executada para obter as previsões dos dados de teste, e os resultados serão comparados com os valores existentes. Os resultados serão plotados no gráfico.  
  
     Se você especificou um determinado resultado de destino usando a opção **prever valor** , o gráfico de comparação de precisão plota os resultados de palpites aleatórios e os resultados de um modelo ideal.  
  
    -   A linha de estimativa aleatória mostra como a precisão do modelo seria se nenhum dado fosse usado para informar as previsões: ou seja, uma divisão 50-50 entre dois resultados. O gráfico de comparação de precisão ajuda você a visualizar melhor o desempenho do seu modelo em comparação com uma estimativa aleatória.  
  
    -   A linha de modelo ideal representa o limite superior de precisão. Ela mostra o benefício máximo possível que você poderia obter se seu modelo sempre previsse com precisão.  
  
     Em geral, os modelos de mineração criados ficarão entre esses dois extremos. Qualquer melhoria da estimativa aleatória é considerada uma *elevação*.  
  
6.  Use a legenda para localizar as linhas coloridas que representam o Modelo Ideal e o Modelo de Previsão Aleatório.  
  
     Você observará que o `TM_Decision_Tree` modelo fornece o maior aumento, o desempenho dos modelos Naive Bayes e clustering.  
  
 Para obter uma explicação detalhada de um gráfico de comparação de precisão semelhante ao criado nesta lição, consulte o gráfico de comparação de [precisão &#40;Analysis Services&#41;de mineração de dados ](../../2014/analysis-services/data-mining/lift-chart-analysis-services-data-mining.md).  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Testando um modelo filtrado &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/testing-a-filtered-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [&#40;do gráfico de comparação de precisão Analysis Services-Mineração de dados&#41;](../../2014/analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)   
 [Guia gráfico de comparação &#40;exibição de gráfico de precisão de mineração&#41;](../../2014/analysis-services/lift-chart-tab-mining-accuracy-chart-view.md)  
  
  
