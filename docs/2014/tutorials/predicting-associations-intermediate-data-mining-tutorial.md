---
title: Prevendo associações (tutorial de mineração de dados intermediários) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9140c5f2-b340-45a6-9c27-d870d15aafea
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bee5ca4ded1b2fd5cbda0712cb766c825b9d0318
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62472841"
---
# <a name="predicting-associations-intermediate-data-mining-tutorial"></a>Prevendo associações (Tutorial de mineração de dados intermediário)
  Depois que os modelos forem processados, você pode usar as informações sobre associações armazenadas no modelo para criar previsões. Na tarefa final desta lição, você aprenderá a criar consultas de previsão em modelos de associação criados por você. Esta lição supõe que você já saiba usar o Construtor de Consultas de Previsão e que deseja aprender a criar consultas de previsão em modelos de associação. Para obter mais informações sobre como usar Construtor de Consultas de previsão, consulte [interfaces de consulta de mineração de dados](../../2014/analysis-services/data-mining/data-mining-query-tools.md).  
  
## <a name="creating-a-singleton-prediction-query"></a>Criando uma consulta de previsão singleton  
 As consultas de previsão em um modelo de associação podem ser muito úteis:  
  
-   Itens recomendados a um cliente, com base em compras prévias ou relacionadas  
  
-   Localizar eventos relacionados.  
  
-   Identificar relações entre ou em conjuntos de transações.  
  
 Para criar uma consulta de previsão, primeiro selecione o modelo de associação que deseja usar e especifique os dados de entrada. As entradas podem vir de uma fonte de dados externa, como uma lista de valores, ou você pode criar uma consulta singleton e fornecer valores à medida que avança.  
  
 Para este cenário, primeiro você criará algumas consultas de previsão singleton, para ter uma ideia de como funciona a previsão. Em seguida, você criará uma consulta para previsões em lote que poderá ser usada para fazer recomendações baseadas em compras atuais de um cliente.  
  
#### <a name="to-create-a-prediction-query-on-an-association-model"></a>Para criar uma consulta de previsão em um modelo de associação  
  
1.  Clique na guia **previsão do modelo de mineração** do designer de mineração de dados.  
  
2.  No painel **modelo de mineração** , clique em **selecionar modelo**. (ignore esta etapa e a próxima se o modelo correto já estiver selecionado).  
  
3.  Na caixa de diálogo **selecionar modelo de mineração** , expanda o nó que representa a **Associação**da estrutura de mineração e selecione a **Associação**de modelo. Clique em **OK**.  
  
     Por ora, ignore o painel de entrada.  
  
4.  Na grade, clique na célula vazia em **origem** e selecione **função de previsão.** Na célula em **campo**, selecione `PredictAssociation`.  
  
     Você também pode usar a função **Predict** para prever associações. Se você fizer isso, certifique-se de escolher a versão da função **Predict** que usa uma coluna de tabela como argumento.  
  
5.  No painel **modelo de mineração** , selecione a tabela `vAssocSeqLineItems`aninhada e arraste-a para a grade, para a caixa **critérios/argumento** da `PredictAssociation` função.  
  
     Arrastar e soltar nomes de tabela e de coluna permite que você crie instruções complexas sem erros de sintaxe. No entanto, ele substitui o conteúdo atual da célula, que inclui outros argumentos opcionais `PredictAssociation` para a função. Para exibir os outros argumentos, você pode adicionar temporariamente uma segunda instância da função à grade para referência.  
  
6.  Clique na caixa **critérios/argumento** e digite o seguinte texto após o nome da tabela:`,3`  
  
     O texto completo na caixa **critérios/argumento** deve ser o seguinte:  
  
     `[Association].[v Assoc Seq Line Items],3`  
  
7.  Clique no botão **resultados** no canto superior do construtor de consultas de previsão.  
  
 Os resultados esperados contêm uma única coluna com a **expressão**de cabeçalho. A coluna **expressão** contém uma tabela aninhada com uma única coluna e as três linhas a seguir. Como você não especificou um valor de entrada, estas previsões representam as associações de produto mais prováveis para o modelo como um todo.  
  
|Modelo|  
|-----------|  
|Women's Mountain Shorts|  
|Water Bottle|  
|Touring-3000|  
  
 Em seguida, você usará o painel **entrada de consulta singleton** para especificar um produto como entrada para a consulta e exibir os produtos que provavelmente estão associados a esse item.  
  
#### <a name="to-create-a-singleton-prediction-query-with-nested-table-inputs"></a>Para criar uma consulta de previsão singleton com entradas de tabela aninhada  
  
1.  Clique no botão **design** no canto do construtor de consultas de previsão para voltar para a grade de construção da consulta.  
  
2.  No menu **modelo de mineração** , selecione **consulta singleton**.  
  
3.  Na caixa de diálogo **modelo de mineração** , selecione o modelo de **Associação** .  
  
4.  Na grade, clique na célula vazia em **origem** e selecione **função de previsão.** Na célula em **campo**, selecione `PredictAssociation`.  
  
5.  No painel **modelo de mineração** , selecione a tabela `vAssocSeqLineItems`aninhada e arraste-a para a grade, para a caixa **critérios/argumento** da `PredictAssociation` função. Digite `,3` após o nome da tabela aninhada, assim como no procedimento anterior.  
  
6.  Na caixa de diálogo **entrada de consulta singleton** , clique na caixa **valor** ao lado de **itens de linha vAssoc Seq**e clique no botão **(...)** .  
  
7.  Na caixa de diálogo **entrada de tabela aninhada** , selecione `Touring Tire` no painel **coluna de chave** e clique em **Adicionar**.  
  
8.  Clique no botão **resultados** .  
  
 Os resultados mostrarão as previsões para produtos que têm mais probabilidade de estarem associados ao Pneu de Passeio.  
  
|Modelo|  
|-----------|  
|Tubo de pneu para passeio|  
|Sport-100|  
|Water Bottle|  
  
 No entanto, você já sabe, pela exploração do modelo, que o Tubo de Pneu para Passeio é frequentemente comprado com o Pneu de Passeio; você está mais interessado em saber que produtos poderá recomendar aos clientes que compram esses itens juntos. Altere a consulta para que ela preveja produtos relacionados baseados em dois itens da cesta. Você também modificará a consulta para adicionar a probabilidade de cada produto previsto.  
  
#### <a name="to-add-inputs-and-probabilities-to-the-singleton-prediction-query"></a>Para adicionar entradas e probabilidades à consulta de previsão singleton  
  
1.  Clique no botão **design** no canto do construtor de consultas de previsão para voltar para a grade de construção da consulta.  
  
2.  Na caixa de diálogo **entrada de consulta singleton** , clique na caixa **valor** ao lado de **itens de linha vAssoc Seq**e clique no botão **(...)** .  
  
3.  No painel **coluna de chave** , selecione `Touring Tire`e clique em **Adicionar**.  
  
4.  Na grade, clique na célula vazia em **origem** e selecione **função de previsão.** Na célula em **campo**, selecione `PredictAssociation`.  
  
5.  No painel **modelo de mineração** , selecione a tabela `vAssocSeqLineItems`aninhada e arraste-a para a grade, para a caixa **critérios/argumento** da `PredictAssociation` função. Digite `,3` após o nome da tabela aninhada, assim como no procedimento anterior.  
  
6.  Na caixa de diálogo **entrada de tabela aninhada** , selecione `Touring Tire Tube` no painel **coluna de chave** e clique em **Adicionar**.  
  
7.  Na grade, na linha da `PredictAssociation` função, clique na caixa **critérios/argumento** e altere os argumentos para adicionar o argumento, INCLUDE_STATISTICS.  
  
     O texto completo na caixa **critérios/argumento** deve ser o seguinte:  
  
     `[Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3`  
  
8.  Clique no botão **resultados** .  
  
 Os resultados da tabela aninhada foram alterados para mostrar as previsões, além do suporte e da probabilidade. Para obter mais informações sobre como interpretar esses valores, consulte [conteúdo do modelo de mineração para modelos de associação &#40;&#41;de mineração de dados de Analysis Services ](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md).  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0,291...|0,252...|  
|Water Bottle|2866|0,192...|0,175...|  
|Patch Kit|2113|0,142...|0,132|  
  
## <a name="working-with-results"></a>Trabalhando com resultados  
 Quando houver muitas tabelas aninhadas nos resultados, talvez seja melhor mesclá-los para obter uma exibição melhor. Para isso, modifique a consulta manualmente e adicione a palavra-chave `FLATTENED`.  
  
#### <a name="to-flatten-nested-rowsets-in-a-prediction-query"></a>Para mesclar conjuntos de linhas aninhadas em uma consulta de previsão  
  
1.  Clique no botão **SQL** no canto da Construtor de consultas de previsão.  
  
     A grade se transformará em um painel aberto, onde você poderá exibir e modificar a instrução DMX criada pelo Construtor de Consultas de Previsão.  
  
2.  Após a palavra-chave `SELECT`, digite `FLATTENED`.  
  
     O texto completo da consulta deve ser o seguinte:  
  
    ```  
    SELECT FLATTENED  
      PredictAssociation([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,3)  
    FROM  
      [Association]  
    NATURAL PREDICTION JOIN  
    (SELECT (SELECT 'Touring Tire' AS [Model]  
      UNION SELECT 'Touring Tire Tube' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
    ```  
  
3.  Clique no botão **resultados** no canto superior do construtor de consultas de previsão.  
  
 Observe que, depois de editar manualmente uma consulta, você não conseguirá voltar ao modo Design sem perder as alterações. Se quiser salvar a consulta, copie a instrução DMX criada manualmente em um arquivo de texto. Quando você voltar ao modo Design, a consulta será revertida para a última versão válida desse modo.  
  
## <a name="creating-multiple-predictions"></a>Criando várias previsões  
 Suponha que você queira saber quais são as melhores previsões para clientes individuais com base em compras passadas. Você pode usar dados externos como entrada para a consulta de previsão, como tabelas com a ID do cliente a as compras de produtos mais recentes. É necessário que as tabelas de dados já estejam definidas como uma exibição da fonte de dados do Analysis Services; além disso, os dados de entrada devem conter tabelas de caso e aninhadas como as usadas no modelo. Elas não precisam ter os mesmos nomes, mas a estrutura deve ser similar. Para fins deste tutorial, serão usadas as tabelas originais nas quais o modelo foi treinado.  
  
#### <a name="to-change-the-input-method-for-the-prediction-query"></a>Para alterar o método de entrada da consulta de previsão  
  
1.  No menu **modelo de mineração** , selecione **consulta singleton** novamente para desmarcar a marca de seleção.  
  
2.  Será exibida uma mensagem de erro avisando que a sua consulta singleton será perdida. Clique em **Sim**.  
  
     O nome da caixa de diálogo de entrada é alterado para **selecionar tabela (s) de entrada**.  
  
 Como você está interessado na criação de uma consulta de previsão que ofereça ID do Cliente e uma lista de produtos como entrada, adicione a tabela de clientes como uma tabela de caso e a tabela de compras como a tabela aninhada. Em seguida, adicione funções de previsão para criar recomendações.  
  
#### <a name="to-create-a-prediction-query-using-nested-table-inputs"></a>Para criar uma consulta de previsão usando entradas de tabela aninhada  
  
1.  No painel Modelo de Mineração, selecione o modelo Associação Filtrada.  
  
2.  Na caixa de diálogo **selecionar tabela (s) de entrada** , clique em **selecionar tabela de casos**.  
  
3.  Na caixa de diálogo **selecionar tabela** , para **fonte de dados**, selecione AdventureWorksDW2008. Na lista **nome da tabela/exibição** , selecione vAssocSeqOrders e clique em **OK**.  
  
     A tabela vAssocSeqOrders será adicionada ao painel.  
  
4.  Na caixa de diálogo **selecionar tabela (s) de entrada** , clique em **selecionar tabela aninhada**.  
  
5.  Na caixa de diálogo **selecionar tabela** , para **fonte de dados**, selecione AdventureWorksDW2008. Na lista **nome da tabela/exibição** , selecione vAssocSeqLineItems e clique em **OK**.  
  
     A tabela vAssocSeqLineItems será adicionada ao painel.  
  
6.  Na caixa de diálogo **especificar junção aninhada** , arraste o campo OrderNumber da tabela de casos e solte-o no campo OrderNumber na tabela aninhada.  
  
     Você também pode clicar em **Adicionar relação** e criar a relação selecionando colunas em uma lista.  
  
7.  Na caixa de diálogo **especificar relação** , verifique se os campos OrderNumber estão mapeados corretamente e clique em **OK**.  
  
8.  Clique em **OK** para fechar a caixa de diálogo **especificar junção aninhada** .  
  
     As tabelas de casos e aninhada são atualizadas no painel de design para mostrarem as junções que conectam as colunas de dados externos às colunas do modelo. Se as relações estiverem erradas, você poderá clicar com o botão direito do mouse na linha de junção e selecionar **Modificar Conexões** para editar o mapeamento de coluna ou clicar com o botão direito do mouse na linha de junção e selecionar **excluir** para remover completamente a relação.  
  
9. Adicione uma nova linha à grade. Para **origem**, selecione **tabela vAssocSeqOrders**. Para **campo**, selecione CustomerKey.  
  
10. Adicione uma nova linha à grade. Para **origem**, selecione **tabela vAssocSeqOrders**. Para **campo**, selecione região.  
  
11. Adicione uma nova linha à grade. Para **origem**, selecione **função de previsão**e, para **campo**, selecione `PredictAssociation`.  
  
12. Arraste vAssocSeqLineItems para a caixa **critérios/argumento** da `PredictAssociation` linha. Clique no final da caixa **critérios/argumento** e digite o seguinte texto:`INCLUDE_STATISTICS,3`  
  
     O texto completo na caixa **critérios/argumento** deve ser:`[Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3`  
  
13. Clique no botão **resultado** para exibir as previsões para cada cliente.  
  
 Você pode tentar criar uma consulta de previsão similar nos vários modelos para ver se a filtragem altera os resultados da previsão. Para obter mais informações sobre como criar previsões e outros tipos de consultas, consulte [exemplos de consulta de modelo de associação](../../2014/analysis-services/data-mining/association-model-query-examples.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Conteúdo do modelo de mineração para modelos de associação &#40;mineração de dados Analysis Services&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)   
 [&#41;&#40;DMX PredictAssociation](/sql/dmx/predictassociation-dmx)   
 [Criar uma consulta de previsão usando o construtor de consultas de previsão](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
