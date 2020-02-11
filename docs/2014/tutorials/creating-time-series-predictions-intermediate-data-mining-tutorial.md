---
title: Criando previsões de série temporal (tutorial intermediário de mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: fb22cffa-ac99-4d34-ac4a-9c93068e33e8
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ca1aa4022931c78f6139a8058c05adc707af5e77
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63313885"
---
# <a name="creating-time-series-predictions-intermediate-data-mining-tutorial"></a>Criando previsões de série temporal (Tutorial de mineração de dados intermediário)
  Nas tarefas anteriores desta lição, você criou um modelo de série temporal e explorou os resultados. Por padrão, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] sempre cria um conjunto de cinco (5) previsões para um modelo de série temporal e a exibe os valores previstos como parte do gráfico de previsão. No entanto, também é possível criar previsões criando-se consultas de previsão DMX.  
  
 Nesta tarefa, você criará uma consulta de previsão que gera as mesmas previsões vistas no visualizador. Esta tarefa supõe que você já tenha concluído as lições do Tutorial de data mining básico e esteja familiarizado com a forma de usar o Construtor de Consultas de Previsão. Agora você aprenderá a criar consultas específicas dos modelos de série temporal.  
  
## <a name="creating-time-series-predictions"></a>Criando previsões de série temporal  
 Tipicamente, a primeira etapa da criação de uma consulta de previsão é selecionar um modelo de mineração e tabela de entrada. No entanto, um modelo de série temporário não requer entrada adicional para uma previsão regular. Dessa forma, não é preciso especificar uma nova fonte de dados ao fazer previsões, a menos que esteja adicionando dados ao modelo ou substituindo os dados.  
  
 Para esta lição, você deve especificar o número de etapas de previsão. É possível especificar o nome da série para obter uma previsão para determinada combinação de um produto e de uma região.  
  
#### <a name="to-select-a-model-and-input-table"></a>Para selecionar um modelo e uma tabela de entrada  
  
1.  Na guia **previsão do modelo de mineração** do designer de mineração de dados, na caixa **modelo de mineração** , clique em **selecionar modelo**.  
  
2.  Na caixa de diálogo **selecionar modelo de mineração** , expanda a estrutura de previsão, selecione o modelo de **previsão** na lista e clique em **OK**.  
  
3.  Ignore a caixa **selecionar tabela (s) de entrada** .  
  
    > [!NOTE]  
    >  Para um modelo de série temporal, você não precisa especificar uma entrada separada, a menos que esteja fazendo previsão cruzada.  
  
4.  Na coluna **origem** , na grade da guia Previsão do **modelo de mineração** , clique na célula da primeira linha vazia e selecione **previsão modelo de mineração**.  
  
5.  Na coluna **campo** , selecione **região do modelo**.  
  
     Essa ação adiciona o identificador da série à consulta de previsão para indicar a combinação de modelo e região a que a previsão se aplica.  
  
6.  Clique na próxima linha vazia na coluna **origem** e selecione **função de previsão**.  
  
7.  Na coluna **campo** , selecione **PredictTimeSeries**.  
  
    > [!NOTE]  
    >  Também é possível usar a função `Predict` com modelos de série temporal. No entanto, por padrão, a função Prever cria somente uma previsão para cada série. Portanto, para especificar várias etapas de previsão, você deve usar a função **PredictTimeSeries** .  
  
8.  No painel **modelo de mineração** , selecione a coluna do modelo de mineração, **valor.** Arraste valor para a caixa **critérios/argumentos** para a função **PredictTimeSeries** que você adicionou anteriormente.  
  
9. Clique na caixa **critérios/argumentos** e digite uma vírgula, seguida por **5**, após o nome do campo.  
  
     O texto na caixa **critérios/argumentos** agora deve exibir o seguinte:  
  
     `[Forecasting].[Amount],5`  
  
10. Na coluna **alias** , digite `PredictAmount`.  
  
11. Clique na próxima linha vazia na coluna **origem** e selecione a função de **previsão** novamente.  
  
12. Na coluna **campo** , selecione **PredictTimeSeries**.  
  
13. No painel **modelo de mineração** , selecione a quantidade da coluna e arraste-a para a caixa **critérios/argumentos** da segunda função **PredictTimeSeries** .  
  
14. Clique na caixa **critérios/argumentos** e digite uma vírgula, seguida por **5**, após o nome do campo.  
  
     O texto na caixa **critérios/argumentos** agora deve exibir o seguinte:  
  
     `[Forecasting].[ Quantity],5`  
  
15. Na coluna **alias** , digite `PredictQuantity`.  
  
16. Clique em **alternar para a exibição de resultado da consulta**.  
  
     Os resultados da consulta serão exibidos em formato tabular.  
  
 Lembre-se de que você criou três tipos diferentes de resultados no construtor de consultas, um que usa valores de uma coluna e dois que obtêm valores de uma função de previsão. Dessa forma, os resultados da consulta contêm três colunas separadas. A primeira coluna contém a lista de combinações de produtos e de regiões. A segunda e a terceira colunas contêm uma tabela aninhada de resultados de previsão. Cada tabela aninhada contém a etapa temporal e os valores previstos, como na tabela a seguir:  
  
 Resultados de exemplo (os valores são truncados em duas casas decimais):  
  
 **Europa M200l PredictAmount**  
  
|$TIME|Amount|  
|-----------|------------|  
|7/25/2008|99978, 0|  
|8/25/2008|145575, 7|  
|9/25/2008|116835,19|  
|10/25/2008|116537,38|  
|11/25/2008|107760,55|  
  
 **Europa M200l PredictQuantity**  
  
|$TIME|Quantidade|  
|-----------|--------------|  
|7/25/2008|52|  
|8/25/2008|67|  
|9/25/2008|58|  
|10/25/2008|57|  
|11/25/2008|54|  
  
 **M200 América do Norte-PredictAmount**  
  
|$TIME|Amount|  
|-----------|------------|  
|7/25/2008|348533,93|  
|8/25/2008|340097,98|  
|9/25/2008|257986,19|  
|10/25/2008|374658,24|  
|11/25/2008|379241,44|  
  
 **M200 América do Norte-PredictQuantity**  
  
|$TIME|Quantidade|  
|-----------|--------------|  
|7/25/2008|272|  
|8/25/2008|152|  
|9/25/2008|250|  
|10/25/2008|181|  
|11/25/2008|290|  
  
> [!WARNING]  
>  As datas que são usadas no banco de dados de exemplo foram alteradas para esta versão. Se você estiver usando uma versão anterior dos dados de exemplo, poderá ver resultados diferentes.  
  
## <a name="saving-the-prediction-results"></a>Salvando os resultados da previsão  
 Você tem várias opções diferentes para usar os resultados da previsão. É possível simplificar os resultados, copiar os dados da exibição Resultados e colá-los em uma planilha do Excel ou outro arquivo.  
  
 Para simplificar o processo de salvar os resultados, o Designer de Mineração de Dados fornece também o recurso para salvar os dados em uma exibição da fonte de dados. A funcionalidade para salvar resultados em uma exibição da fonte de dados só está disponível no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Os resultados só podem ser armazenados em um formato simplificado.  
  
#### <a name="to-flatten-the-results-in-the-results-pane"></a>Para mesclar os resultados no painel Resultados  
  
1.  No Construtor de Consultas de previsão, clique em **alternar para a exibição de design de consulta**.  
  
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
  
4.  Clique em **alternar para a exibição de resultado da consulta**.  
  
#### <a name="to-export-prediction-query-results"></a>Para exportar resultados da consulta de previsão  
  
1.  Clique em **salvar resultados da consulta**.  
  
2.  Na caixa de diálogo **salvar resultado da consulta de mineração de dados** , para fonte [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]de **dados**, selecione. Também será possível criar uma fonte de dados se você quiser salvar os dados em um banco de dados relacional diferente.  
  
3.  Na coluna **nome da tabela** , digite um novo nome de tabela temporária, como **previsões de teste**.  
  
4.  Clique em **Save** (Salvar).  
  
    > [!NOTE]  
    >  Para exibir a tabela criada, crie uma conexão ao mecanismo de banco de dados da instância onde os dados foram salvos e crie uma consulta.  
  
## <a name="conclusion"></a>Conclusão  
 Você aprendeu a criar um modelo de série temporal básico, interpretar as previsões e criar previsões.  
  
 As tarefas restantes deste tutorial são opcionais e descrevem previsões de série temporal avançadas. Se você decidir ir adiante, aprenderá a adicionar novos dados ao seu modelo e criar previsões na série estendida. Você também aprenderá a executar a previsão cruzada, usando a tendência no modelo, mas substituindo os dados por uma nova série de dados.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Previsões de série temporal avançada &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplos de consulta de um modelo de série temporal](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)  
  
  
