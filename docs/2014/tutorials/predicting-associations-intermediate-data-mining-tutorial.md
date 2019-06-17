---
title: Prevendo associações (Tutorial de mineração de dados intermediário) | Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62472841"
---
# <a name="predicting-associations-intermediate-data-mining-tutorial"></a>Prevendo associações (Tutorial de mineração de dados intermediário)
  Depois que os modelos forem processados, você pode usar as informações sobre associações armazenadas no modelo para criar previsões. Na tarefa final desta lição, você aprenderá a criar consultas de previsão em modelos de associação criados por você. Esta lição supõe que você já saiba usar o Construtor de Consultas de Previsão e que deseja aprender a criar consultas de previsão em modelos de associação. Para saber como usar o construtor de consultas de previsão, consulte [Interfaces de consulta de mineração de dados](../../2014/analysis-services/data-mining/data-mining-query-tools.md).  
  
## <a name="creating-a-singleton-prediction-query"></a>Criando uma consulta de previsão singleton  
 As consultas de previsão em um modelo de associação podem ser muito úteis:  
  
-   Itens recomendados a um cliente, com base em compras prévias ou relacionadas  
  
-   Localizar eventos relacionados.  
  
-   Identificar relações entre ou em conjuntos de transações.  
  
 Para criar uma consulta de previsão, primeiro selecione o modelo de associação que deseja usar e especifique os dados de entrada. As entradas podem vir de uma fonte de dados externa, como uma lista de valores, ou você pode criar uma consulta singleton e fornecer valores à medida que avança.  
  
 Para este cenário, primeiro você criará algumas consultas de previsão singleton, para ter uma ideia de como funciona a previsão. Em seguida, você criará uma consulta para previsões em lote que poderá ser usada para fazer recomendações baseadas em compras atuais de um cliente.  
  
#### <a name="to-create-a-prediction-query-on-an-association-model"></a>Para criar uma consulta de previsão em um modelo de associação  
  
1.  Clique o **previsão de modelo de mineração** guia do Designer de mineração de dados.  
  
2.  No **modelo de mineração** painel, clique em **Selecionar modelo**. (ignore esta etapa e a próxima se o modelo correto já estiver selecionado).  
  
3.  No **Selecionar modelo de mineração** diálogo caixa, expanda o nó que representa a estrutura de mineração **associação**e selecione o modelo **associação**. Clique em **OK**.  
  
     Por ora, ignore o painel de entrada.  
  
4.  Na grade, clique na célula vazia sob **fonte** e selecione **função de previsão.** Na célula sob **campo**, selecione `PredictAssociation`.  
  
     Você também pode usar o **Predict** função para prever associações. Se você, não se esqueça de escolher a versão dos **Predict** função que usa uma coluna de tabela como argumento.  
  
5.  No **modelo de mineração** painel, selecione a tabela aninhada `vAssocSeqLineItems`e arraste-o para a grade, até a **critérios/argumento** caixa para o `PredictAssociation` função.  
  
     Arrastar e soltar nomes de tabela e de coluna permite que você crie instruções complexas sem erros de sintaxe. No entanto, ele substitui o conteúdo atual da célula, que inclui outros argumentos opcionais para o `PredictAssociation` função. Para exibir os outros argumentos, você pode adicionar temporariamente uma segunda instância da função à grade para referência.  
  
6.  Clique o **critérios/argumento** caixa e digite o seguinte texto após o nome da tabela: `,3`  
  
     O texto completo do **critérios/argumento** caixa deve ser da seguinte maneira:  
  
     `[Association].[v Assoc Seq Line Items],3`  
  
7.  Clique o **resultados** botão na parte superior do construtor de consultas de previsão.  
  
 Os resultados esperados contêm uma única coluna com o título **expressão**. O **expressão** coluna contém uma tabela aninhada com uma única coluna e três linhas a seguir. Como você não especificou um valor de entrada, estas previsões representam as associações de produto mais prováveis para o modelo como um todo.  
  
|Modelo|  
|-----------|  
|Women's Mountain Shorts|  
|Water Bottle|  
|Touring-3000|  
  
 Em seguida, você usará o **entrada de consulta Singleton** painel para especificar um produto como entrada para a consulta e exibir os produtos que provavelmente são associados ao item.  
  
#### <a name="to-create-a-singleton-prediction-query-with-nested-table-inputs"></a>Para criar uma consulta de previsão singleton com entradas de tabela aninhada  
  
1.  Clique o **Design** botão no canto do construtor de consultas de previsão para voltar à grade de criação de consultas.  
  
2.  Sobre o **modelo de mineração** menu, selecione **consulta Singleton**.  
  
3.  No **modelo de mineração** caixa de diálogo, selecione o **associação** modelo.  
  
4.  Na grade, clique na célula vazia sob **fonte** e selecione **função de previsão.** Na célula sob **campo**, selecione `PredictAssociation`.  
  
5.  No **modelo de mineração** painel, selecione a tabela aninhada `vAssocSeqLineItems`e arraste-o para a grade, até a **critérios/argumento** caixa para o `PredictAssociation` função. Tipo `,3` após o nome de tabela aninhada, assim como no procedimento anterior.  
  
6.  No **entrada de consulta Singleton** caixa de diálogo, clique o **valor** caixa ao lado **vAssoc Seq Line Items**e, em seguida, clique no **(...)**  botão.  
  
7.  No **entrada de tabela aninhada** caixa de diálogo, selecione `Touring Tire` no **coluna chave** painel e clique **Add**.  
  
8.  Clique o **resultados** botão.  
  
 Os resultados mostrarão as previsões para produtos que têm mais probabilidade de estarem associados ao Pneu de Passeio.  
  
|Modelo|  
|-----------|  
|Tubo de pneu para passeio|  
|Sport-100|  
|Water Bottle|  
  
 No entanto, você já sabe, pela exploração do modelo, que o Tubo de Pneu para Passeio é frequentemente comprado com o Pneu de Passeio; você está mais interessado em saber que produtos poderá recomendar aos clientes que compram esses itens juntos. Altere a consulta para que ela preveja produtos relacionados baseados em dois itens da cesta. Você também modificará a consulta para adicionar a probabilidade de cada produto previsto.  
  
#### <a name="to-add-inputs-and-probabilities-to-the-singleton-prediction-query"></a>Para adicionar entradas e probabilidades à consulta de previsão singleton  
  
1.  Clique o **Design** botão no canto do construtor de consultas de previsão para voltar à grade de criação de consultas.  
  
2.  No **entrada de consulta Singleton** caixa de diálogo, clique o **valor** caixa ao lado **vAssoc Seq Line Items**e, em seguida, clique no **(...)**  botão.  
  
3.  No **coluna de chave** painel, selecione `Touring Tire`e, em seguida, clique em **Add**.  
  
4.  Na grade, clique na célula vazia sob **fonte** e selecione **função de previsão.** Na célula sob **campo**, selecione `PredictAssociation`.  
  
5.  No **modelo de mineração** painel, selecione a tabela aninhada `vAssocSeqLineItems`e arraste-o para a grade, até a **critérios/argumento** caixa para o `PredictAssociation` função. Tipo `,3` após o nome de tabela aninhada, assim como no procedimento anterior.  
  
6.  No **entrada de tabela aninhada** caixa de diálogo, selecione `Touring Tire Tube` no **coluna chave** painel e clique **Add**.  
  
7.  Na grade, na linha para o `PredictAssociation` de função, clique em de **critérios/argumento** caixa e alterar os argumentos para adicionar o argumento, INCLUDE_STATISTICS.  
  
     O texto completo do **critérios/argumento** caixa deve ser da seguinte maneira:  
  
     `[Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3`  
  
8.  Clique o **resultados** botão.  
  
 Os resultados da tabela aninhada foram alterados para mostrar as previsões, além do suporte e da probabilidade. Para obter mais informações sobre como interpretar esses valores, consulte [modelo de conteúdo de mineração para modelos de associação &#40;Analysis Services - mineração de dados&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md).  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291...|0.252...|  
|Water Bottle|2866|0.192...|0.175...|  
|Patch Kit|2113|0.142...|0.132|  
  
## <a name="working-with-results"></a>Trabalhando com resultados  
 Quando houver muitas tabelas aninhadas nos resultados, talvez seja melhor mesclá-los para obter uma exibição melhor. Para isso, modifique a consulta manualmente e adicione a palavra-chave `FLATTENED`.  
  
#### <a name="to-flatten-nested-rowsets-in-a-prediction-query"></a>Para mesclar conjuntos de linhas aninhadas em uma consulta de previsão  
  
1.  Clique o **SQL** botão no canto do construtor de consultas de previsão.  
  
     A grade se transformará em um painel aberto, onde você poderá exibir e modificar a instrução DMX criada pelo Construtor de Consultas de Previsão.  
  
2.  Após a palavra-chave `SELECT`, digite `FLATTENED`.  
  
     O texto completo da consulta deve ser da seguinte maneira:  
  
    ```  
    SELECT FLATTENED  
      PredictAssociation([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,3)  
    FROM  
      [Association]  
    NATURAL PREDICTION JOIN  
    (SELECT (SELECT 'Touring Tire' AS [Model]  
      UNION SELECT 'Touring Tire Tube' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
    ```  
  
3.  Clique o **resultados** botão na parte superior do construtor de consultas de previsão.  
  
 Observe que, depois de editar manualmente uma consulta, você não conseguirá voltar ao modo Design sem perder as alterações. Se quiser salvar a consulta, copie a instrução DMX criada manualmente em um arquivo de texto. Quando você voltar ao modo Design, a consulta será revertida para a última versão válida desse modo.  
  
## <a name="creating-multiple-predictions"></a>Criando várias previsões  
 Suponha que você queira saber quais são as melhores previsões para clientes individuais com base em compras passadas. Você pode usar dados externos como entrada para a consulta de previsão, como tabelas com a ID do cliente a as compras de produtos mais recentes. É necessário que as tabelas de dados já estejam definidas como uma exibição da fonte de dados do Analysis Services; além disso, os dados de entrada devem conter tabelas de caso e aninhadas como as usadas no modelo. Elas não precisam ter os mesmos nomes, mas a estrutura deve ser similar. Para fins deste tutorial, serão usadas as tabelas originais nas quais o modelo foi treinado.  
  
#### <a name="to-change-the-input-method-for-the-prediction-query"></a>Para alterar o método de entrada da consulta de previsão  
  
1.  No **modelo de mineração** menu, selecione **consulta Singleton** novamente, para limpar a marca de seleção.  
  
2.  Será exibida uma mensagem de erro avisando que a sua consulta singleton será perdida. Clique em **Sim**.  
  
     O nome da caixa de diálogo de entrada muda para **Selecionar tabela de entrada**.  
  
 Como você está interessado na criação de uma consulta de previsão que ofereça ID do Cliente e uma lista de produtos como entrada, adicione a tabela de clientes como uma tabela de caso e a tabela de compras como a tabela aninhada. Em seguida, adicione funções de previsão para criar recomendações.  
  
#### <a name="to-create-a-prediction-query-using-nested-table-inputs"></a>Para criar uma consulta de previsão usando entradas de tabela aninhada  
  
1.  No painel Modelo de Mineração, selecione o modelo Associação Filtrada.  
  
2.  No **Selecionar tabela (s) de entrada** caixa de diálogo, clique em **Selecionar tabela de casos**.  
  
3.  No **Selecionar tabela** caixa de diálogo, para **fonte de dados**, selecione AdventureWorksDW2008. No **nome da tabela/exibição** lista, selecione vAssocSeqOrders e, em seguida, clique em **Okey**.  
  
     A tabela vAssocSeqOrders será adicionada ao painel.  
  
4.  No **Selecionar tabela (s) de entrada** caixa de diálogo, clique em **Selecionar tabela aninhada**.  
  
5.  No **Selecionar tabela** caixa de diálogo, para **fonte de dados**, selecione AdventureWorksDW2008. No **nome da tabela/exibição** lista, selecione vAssocSeqLineItems e, em seguida, clique em **Okey**.  
  
     A tabela vAssocSeqLineItems será adicionada ao painel.  
  
6.  No **especificar junção aninhada** caixa de diálogo, arraste o OrderNumber campo da tabela de casos e solte-o campo OrderNumber da tabela aninhada.  
  
     Você também pode clicar **Adicionar relação** e criar a relação selecionando colunas de uma lista.  
  
7.  No **especifique a relação** diálogo caixa, verifique se os campos OrderNumber foram mapeados corretamente e, em seguida, clique em **Okey**.  
  
8.  Clique em **Okey** para fechar o **especificar junção aninhada** caixa de diálogo.  
  
     As tabelas de casos e aninhada são atualizadas no painel de design para mostrarem as junções que conectam as colunas de dados externos às colunas do modelo. Se os relacionamentos estiverem incorretos, você pode clique com botão direito na linha de junção e selecione **modificar conexões** para editar a coluna de mapeamento, ou com o botão direito na linha de junção e selecione **excluir** para remover o relação completamente.  
  
9. Adicione uma nova linha à grade. Para **fonte**, selecione **tabela vAssocSeqOrders**. Para **campo**, selecione CustomerKey.  
  
10. Adicione uma nova linha à grade. Para **fonte**, selecione **tabela vAssocSeqOrders**. Para **campo**, selecione a região.  
  
11. Adicione uma nova linha à grade. Para **fonte**, selecione **função de previsão**e para **campo**, selecione `PredictAssociation`.  
  
12. Arraste vAssocSeqLineItems até a **critérios/argumento** caixa do `PredictAssociation` linha. Clique no final de **critérios/argumento** caixa e, em seguida, digite o seguinte texto: `INCLUDE_STATISTICS,3`  
  
     O texto completo do **critérios/argumento** caixa deve ser: `[Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3`  
  
13. Clique o **resultado** botão para exibir as previsões para cada cliente.  
  
 Você pode tentar criar uma consulta de previsão similar nos vários modelos para ver se a filtragem altera os resultados da previsão. Para obter mais informações sobre a criação de previsões e outros tipos de consultas, consulte [exemplos de consulta de modelo de associação](../../2014/analysis-services/data-mining/association-model-query-examples.md).  
  
## <a name="see-also"></a>Consulte também  
 [Conteúdo do modelo de mineração para modelos de associação &#40; Analysis Services – mineração de dados &#41;](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)   
 [PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)   
 [Criar uma consulta de previsão usando o Construtor de Consultas de previsão](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
