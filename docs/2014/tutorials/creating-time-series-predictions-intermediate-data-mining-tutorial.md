---
title: Criando previsões de série temporal (Tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fb22cffa-ac99-4d34-ac4a-9c93068e33e8
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 999dcdec7c6a30617c9c9e04512da26ddebfdcc3
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312944"
---
# <a name="creating-time-series-predictions-intermediate-data-mining-tutorial"></a>Criando previsões de série temporal (Tutorial de mineração de dados intermediário)
  Nas tarefas anteriores desta lição, você criou um modelo de série temporal e explorou os resultados. Por padrão, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] sempre cria um conjunto de cinco (5) previsões para um modelo de série temporal e a exibe os valores previstos como parte do gráfico de previsão. No entanto, também é possível criar previsões criando-se consultas de previsão DMX.  
  
 Nesta tarefa, você criará uma consulta de previsão que gera as mesmas previsões vistas no visualizador. Esta tarefa supõe que você já tenha concluído as lições do Tutorial de data mining básico e esteja familiarizado com a forma de usar o Construtor de Consultas de Previsão. Agora você aprenderá a criar consultas específicas dos modelos de série temporal.  
  
## <a name="creating-time-series-predictions"></a>Criando previsões de série temporal  
 Tipicamente, a primeira etapa da criação de uma consulta de previsão é selecionar um modelo de mineração e tabela de entrada. No entanto, um modelo de série temporário não requer entrada adicional para uma previsão regular. Dessa forma, não é preciso especificar uma nova fonte de dados ao fazer previsões, a menos que esteja adicionando dados ao modelo ou substituindo os dados.  
  
 Para esta lição, você deve especificar o número de etapas de previsão. É possível especificar o nome da série para obter uma previsão para determinada combinação de um produto e de uma região.  
  
#### <a name="to-select-a-model-and-input-table"></a>Para selecionar um modelo e uma tabela de entrada  
  
1.  No **previsão do modelo de mineração** guia do Designer de mineração de dados, no **modelo de mineração** , clique em **Selecionar modelo**.  
  
2.  No **Selecionar modelo de mineração** caixa de diálogo, expanda a estrutura previsão, selecione o **previsão** de modelo na lista e, em seguida, clique em **Okey**.  
  
3.  Ignorar o **Selecionar tabela (s) de entrada** caixa.  
  
    > [!NOTE]  
    >  Para um modelo de série temporal, você não precisa especificar uma entrada separada, a menos que esteja fazendo previsão cruzada.  
  
4.  No **fonte** coluna na grade de **previsão do modelo de mineração** guia, clique na célula da primeira linha vazia e, em seguida, selecione **modelo de mineração previsão**.  
  
5.  No **campo** coluna, selecione **região modelo**.  
  
     Essa ação adiciona o identificador da série à consulta de previsão para indicar a combinação de modelo e região a que a previsão se aplica.  
  
6.  Clique na próxima linha vazia no **fonte** coluna e, em seguida, selecione **função de previsão**.  
  
7.  No **campo** coluna, selecione **PredictTimeSeries**.  
  
    > [!NOTE]  
    >  Também é possível usar a função `Predict` com modelos de série temporal. No entanto, por padrão, a função Prever cria somente uma previsão para cada série. Portanto, para especificar várias etapas de previsão, você deve usar o **PredictTimeSeries** função.  
  
8.  No **modelo de mineração** painel, selecione a coluna de modelo de mineração, **quantidade.** Arraste valor até o **critérios/argumentos** caixa para o **PredictTimeSeries** função que você adicionou anteriormente.  
  
9. Clique o **critérios/argumentos** caixa e, em seguida, digite uma vírgula, seguida por **5**, após o nome do campo.  
  
     O texto a **critérios/argumentos** caixa agora deve exibir o seguinte:  
  
     `[Forecasting].[Amount],5`  
  
10. No **Alias** coluna, digite `PredictAmount`.  
  
11. Clique na próxima linha vazia no **fonte** coluna e, em seguida, selecione **função de previsão** novamente.  
  
12. No **campo** coluna, selecione **PredictTimeSeries**.  
  
13. No **modelo de mineração** painel, selecione a coluna quantidade e, em seguida, arraste-a até o **critérios/argumentos** caixa para a segunda **PredictTimeSeries** função.  
  
14. Clique o **critérios/argumentos** caixa e, em seguida, digite uma vírgula, seguida por **5**, após o nome do campo.  
  
     O texto a **critérios/argumentos** caixa agora deve exibir o seguinte:  
  
     `[Forecasting].[ Quantity],5`  
  
15. No **Alias** coluna, digite `PredictQuantity`.  
  
16. Clique em **alternar para a exibição de resultados de consulta**.  
  
     Os resultados da consulta serão exibidos em formato tabular.  
  
 Lembre-se de que você criou três tipos diferentes de resultados no construtor de consultas, um que usa valores de uma coluna e dois que obtêm valores de uma função de previsão. Dessa forma, os resultados da consulta contêm três colunas separadas. A primeira coluna contém a lista de combinações de produtos e de regiões. A segunda e a terceira colunas contêm uma tabela aninhada de resultados de previsão. Cada tabela aninhada contém a etapa temporal e os valores previstos, como na tabela a seguir:  
  
 Resultados de exemplo (os valores são truncados em duas casas decimais):  
  
 **M200 Europa PredictAmount**  
  
|$TIME|Valor|  
|-----------|------------|  
|25/7/2008|99978.00|  
|25/8/2008|145575.07|  
|25/9/2008|116835.19|  
|25/10/2008|116537.38|  
|25/11/2008|107760.55|  
  
 **M200 Europa PredictQuantity**  
  
|$TIME|Quantidade|  
|-----------|--------------|  
|25/7/2008|52|  
|25/8/2008|67|  
|25/9/2008|58|  
|25/10/2008|57|  
|25/11/2008|54|  
  
 **M200 América do Norte - PredictAmount**  
  
|$TIME|Valor|  
|-----------|------------|  
|25/7/2008|348533.93|  
|25/8/2008|340097.98|  
|25/9/2008|257986.19|  
|25/10/2008|374658.24|  
|25/11/2008|379241.44|  
  
 **M200 América do Norte - PredictQuantity**  
  
|$TIME|Quantidade|  
|-----------|--------------|  
|25/7/2008|272|  
|25/8/2008|152|  
|25/9/2008|250|  
|25/10/2008|181|  
|25/11/2008|290|  
  
> [!WARNING]  
>  As datas que são usadas no banco de dados de exemplo foram alteradas para esta versão. Se você estiver usando uma versão anterior dos dados de exemplo, poderá ver resultados diferentes.  
  
## <a name="saving-the-prediction-results"></a>Salvando os resultados da previsão  
 Você tem várias opções diferentes para usar os resultados da previsão. É possível simplificar os resultados, copiar os dados da exibição Resultados e colá-los em uma planilha do Excel ou outro arquivo.  
  
 Para simplificar o processo de salvar os resultados, o Designer de Mineração de Dados fornece também o recurso para salvar os dados em uma exibição da fonte de dados. A funcionalidade para salvar resultados em uma exibição da fonte de dados só está disponível no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Os resultados só podem ser armazenados em um formato simplificado.  
  
#### <a name="to-flatten-the-results-in-the-results-pane"></a>Para mesclar os resultados no painel Resultados  
  
1.  No construtor de consultas de previsão, clique em **alternar para modo de design de consulta**.  
  
     A exibição é alterada para permitir a edição manual do texto da consulta DMX.  
  
2.  Digite a palavra-chave `FLATTENED` após a palavra-chave `SELECT`. O texto completo da consulta deve ser assim:  
  
    ```  
    SELECT FLATTENED  
      [Forecasting].[Model Region],  
      (PredictTimeSeries([Forecasting].[Amount],5)) as [PredictAmount],  
      (PredictTimeSeries([Forecasting].[Quantity],5)) as [PredictQuantity]  
    FROM  
      [Forecasting]  
    ```  
  
3.  Como opção, você pode digitar uma cláusula para restringir os resultados, como o exemplo a seguir:  
  
    ```  
    SELECT FLATTENED  
      [Forecasting].[Model Region],  
      (PredictTimeSeries([Forecasting].[Amount],5)) as [PredictAmount],  
      (PredictTimeSeries([Forecasting].[Quantity],5)) as [PredictQuantity]  
    FROM  
      [Forecasting]  
    WHERE [Forecasting].[Model Region] = 'M200 North America'   
    OR [Forecasting].[Model Region] = 'M200 Europe'  
  
    ```  
  
4.  Clique em **alternar para a exibição de resultados de consulta**.  
  
#### <a name="to-export-prediction-query-results"></a>Para exportar resultados da consulta de previsão  
  
1.  Clique em **salvar resultados de consulta**.  
  
2.  No **Salvar resultado mineração de dados consulta** caixa de diálogo para **fonte de dados**, selecione [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]. Também será possível criar uma fonte de dados se você quiser salvar os dados em um banco de dados relacional diferente.  
  
3.  No **nome de tabela** coluna, digite um novo temporário tabela nome, como **previsões de teste**.  
  
4.  Clique em **Salvar**.  
  
    > [!NOTE]  
    >  Para exibir a tabela criada, crie uma conexão ao mecanismo de banco de dados da instância onde os dados foram salvos e crie uma consulta.  
  
## <a name="conclusion"></a>Conclusão  
 Você aprendeu a criar um modelo de série temporal básico, interpretar as previsões e criar previsões.  
  
 As tarefas restantes deste tutorial são opcionais e descrevem previsões de série temporal avançadas. Se você decidir ir adiante, aprenderá a adicionar novos dados ao seu modelo e criar previsões na série estendida. Você também aprenderá a executar a previsão cruzada, usando a tendência no modelo, mas substituindo os dados por uma nova série de dados.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Advanced previsões de série temporal &#40;intermediário de Tutorial de mineração de dados&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplos de consulta de modelos de série temporal](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)  
  
  