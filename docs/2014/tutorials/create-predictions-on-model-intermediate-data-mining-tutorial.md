---
title: Criando previsões em um modelo de clustering de sequência (tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 94a8d4f9-a76a-49c5-9785-917010359511
author: minewiskan
ms.author: owend
manager: kfilee
ms.openlocfilehash: 893067e234d868ae6dde2f93d93bfd50458bfeb2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63217739"
---
# <a name="creating-predictions-on-a-sequence-clustering-model-intermediate-data-mining-tutorial"></a>Criando previsões em um modelo de cluster de sequências (Tutorial de mineração de dados intermediário)
  Depois de entender melhor o modelo de clustering de sequências navegando no visualizador, você pode criar consultas de previsão usando a previsão Construtor de Consultas na guia **previsão do modelo de mineração** no designer de mineração de dados. Para criar uma previsão, primeiro selecione o modelo de clustering de sequências e selecione os dados de entrada. Para entradas, use uma fonte de dados externa ou crie uma consulta singleton e forneça valores em uma caixa de diálogo.  
  
 Esta lição supõe que você já saiba usar o construtor de consultas de previsão e que deseja aprender a criar consultas específicas de um modelo de clustering de sequências. Para obter informações gerais sobre como usar Construtor de Consultas de previsão, consulte [interfaces de consulta de mineração de dados](../../2014/analysis-services/data-mining/data-mining-query-tools.md) ou a seção do tutorial de mineração de dados básico, [Criando previsões &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/creating-predictions-basic-data-mining-tutorial.md).  
  
## <a name="creating-predictions-on-the-regional-model"></a>Criando previsões em um modelo regional  
 Para este cenário, primeiro você criará algumas consultas de previsão singleton, para ter uma ideia de como as previsões podem variar por região.  
  
#### <a name="to-create-a-singleton-query-on-a-sequence-clustering-model"></a>Para criar uma consulta de previsão singleton em um modelo de clustering de sequências  
  
1.  Clique na guia **previsão do modelo de mineração** do designer de mineração de dados.  
  
2.  No menu de colunas do **modelo de mineração** , selecione **consulta singleton**.  
  
     O painel **modelo de mineração** e o painel entrada de **consulta singleton** são exibidos.  
  
3.  No painel **modelo de mineração** , clique em **selecionar modelo**. (se o modo de clustering de sequências já tiver sido selecionado, você poderá ignorar esta etapa).  
  
     A caixa de diálogo **selecionar modelo de mineração** é aberta.  
  
4.  Expanda o nó que representa o **clustering de sequência**da estrutura de mineração com região e selecione o **clustering de sequência de modelo com região**. Clique em **OK**. Por ora, ignore o painel de entrada; você especificará as entradas depois de configurar as funções de previsão.  
  
5.  Na grade, clique na célula vazia em **origem** e selecione **função de previsão.** Na célula em **campo**, selecione **PredictSequence**.  
  
    > [!NOTE]  
    >  Você também pode usar a função **Predict** . Se você fizer isso, certifique-se de escolher a versão da função **Predict** que usa uma coluna de tabela como argumento.  
  
6.  No painel **modelo de mineração** , selecione a tabela `v Assoc Seq Line Items`aninhada e arraste-a para a grade, para a caixa **critérios/argumento** da função **PredictSequence** .  
  
     Arrastar e soltar nomes de tabela e coluna permite que você crie instruções complexas sem erros de sintaxe. No entanto, ele substitui o conteúdo atual da célula, que inclui outros argumentos opcionais para a função **PredictSequence** . Para exibir os outros argumentos, você pode adicionar temporariamente uma segunda instância da função à grade para referência.  
  
7.  Clique no botão **resultado** no canto superior do construtor de consultas de previsão.  
  
 Os resultados esperados contêm uma única coluna com a **expressão**de cabeçalho. A coluna **expressão** contém uma tabela aninhada com três colunas da seguinte maneira:  
  
|$SEQUENCE|Número da Linha|Modelo|  
|---------------|-----------------|-----------|  
|1||Mountain-200|  
  
 O que significam esses resultados? Lembre-se de que você não especificou entradas. Dessa forma, a previsão é feita em relação à toda a população de casos, e o Analysis Services retorna a previsão geral mais provável.  
  
### <a name="adding-inputs-to-a-singleton-prediction-query"></a>Adicionando entradas a uma consulta de previsão singleton  
 Até agora, você não especificou entradas. Na próxima tarefa, você usará o painel **entrada de consulta singleton** para especificar algumas entradas para a consulta. Primeiro, use [Região] como uma entrada do modelo de clustering de sequências regional para determinar se as sequências previstas são iguais para todas as regiões. Assim, você aprenderá a modificar a consulta para adicionar a probabilidade de cada previsão e mesclar os resultados para facilitar sua exibição.  
  
##### <a name="to-generate-predictions-for-a-specific-customer-group"></a>Para gerar previsões para um grupo de clientes específico  
  
1.  Clique no botão **design** no canto superior esquerdo do construtor de consultas de previsão para voltar para a grade de construção da consulta.  
  
2.  Na caixa de diálogo **entrada de consulta singleton** , clique **Value** na caixa valor `Region`para e selecione **Europa**.  
  
3.  Clique no botão **resultado** para exibir previsões para clientes na Europa.  
  
4.  Clique no botão **design** no canto superior esquerdo do construtor de consultas de previsão para voltar para a grade de construção da consulta.  
  
5.  Na caixa de diálogo **entrada de consulta singleton** , clique **Value** na caixa valor `Region`para e selecione **América do Norte**.  
  
6.  Clique no botão **resultado** para exibir previsões para clientes em América do Norte.  
  
### <a name="adding-probabilities-by-using-a-custom-expression"></a>Adicionando probabilidades usando uma expressão personalizada  
 Gerar a probabilidade de cada previsão é ligeiramente mais complicado, já que a probabilidade é um atributo da previsão e é gerada como uma tabela aninhada. Se você já conhece DMX (Data Mining Extensions), poderá alterar com facilidade a consulta e adicionar uma instrução de subseleção na tabela aninhada. No entanto, você também poderá criar uma instrução de subseleção no Construtor de Consultas de Previsão ao adicionar uma expressão personalizada.  
  
##### <a name="to-output-probabilities-for-a-predicted-sequence-by-using-a-custom-expression"></a>Para gerar probabilidades para uma sequência prevista usando uma expressão personalizada  
  
1.  Clique no botão **design** no canto superior esquerdo do construtor de consultas de previsão para voltar para a grade de construção da consulta.  
  
2.  Na grade, em **origem**, clique em uma nova linha e selecione **expressão personalizada**.  
  
3.  Deixe a caixa sob o **campo** em branco.  
  
4.  Para **alias**, digite `t`.  
  
5.  Na caixa **critérios/argumento** , digite a instrução de subseleção completa, conforme mostrado no exemplo de código a seguir. Não se esqueça de incluir os parênteses inicial e final.  
  
    ```  
    (SELECT PredictProbability([Model]) FROM PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]))  
    ```  
  
6.  Clique no botão **resultado** para exibir previsões para clientes na Europa.  
  
 Agora, os resultados contêm duas tabelas aninhadas, uma com a previsão e outra com a probabilidade da previsão. Se a consulta não funcionar, você poderá alternar para o modo de design e examinar a instrução completa da consulta, que deve ser assim:  
  
```  
SELECT  
  PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]),  
  ( (SELECT PredictProbability([Model]) FROM PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]))) as [t]  
FROM  
  [Sequence Clustering with Region]  
NATURAL PREDICTION JOIN  
(SELECT 'Europe' AS [Region]) AS t  
```  
  
### <a name="working-with-results"></a>Trabalhando com resultados  
 Quando houver muitas tabelas aninhadas nos resultados, talvez seja melhor mesclá-los para obter uma exibição melhor. Para isso, modifique a consulta manualmente e adicione a palavra-chave `FLATTENED`.  
  
##### <a name="to-flatten-nested-rowsets-in-a-prediction-query"></a>Para mesclar conjuntos de linhas aninhadas em uma consulta de previsão  
  
1.  Clique no botão **consulta** no canto do construtor de consultas de previsão.  
  
     A grade se transformará em um painel aberto, onde você poderá exibir e modificar a instrução DMX criada pelo Construtor de Consultas de Previsão.  
  
2.  Após a palavra-chave `SELECT`, digite `FLATTENED`.  
  
     O texto completo da consulta deve ser similar ao seguinte:  
  
    ```  
    SELECT FLATTENED  
      PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]),  
      ( (SELECT PredictProbability([Model]) FROM PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]))) as [t]  
    FROM  
      [Sequence Clustering with Region]  
    NATURAL PREDICTION JOIN  
    (SELECT 'Europe' AS [Region]) AS t  
    ```  
  
3.  Clique no botão **resultados** no canto superior do construtor de consultas de previsão.  
  
 Depois de editar manualmente uma consulta, você não conseguirá voltar ao modo Design sem perder as alterações. No entanto, é possível salvar a instrução DMX criada manualmente em um arquivo de texto e então voltar para o modo Design. Quando você fizer isso, a consulta será revertida para a última versão válida do modo Design.  
  
## <a name="creating-predictions-on-the-related-model"></a>Criando previsões em um modelo relacionado  
 Os exemplos anteriores usaram uma coluna da tabela de casos, Região, como a entrada da consulta de previsão singleton, porque você estava interessado em saber se o modelo encontrou diferenças entre regiões. No entanto, depois de explorar o modelo, você decidiu que as diferenças não são significativas o suficiente para justificar recomendações de personalização de produtos por região. O que realmente interessa a você na previsão são os itens selecionados pelos clientes. Dessa forma, nas consultas a seguir, você usará o modelo de clustering de sequências que não inclui Região para gerar recomendações para todos os clientes.  
  
### <a name="using-nested-table-columns-as-input"></a>Usando colunas da tabela aninhada como entrada  
 Primeiro, você criará uma consulta de previsão singleton que obtém um único item como entrada e retorna o próximo item mais provável. Para obter uma previsão desse tipo, use uma coluna de tabela aninhada como o valor de entrada. Isso acontece porque o atributo que está sendo previsto, Modelo, faz parte de uma tabela aninhada. Analysis Services fornece a caixa de diálogo **entrada de tabela aninhada** para ajudá-lo a criar facilmente consultas de previsão em atributos de tabela aninhada, usando o construtor de consultas de previsão.  
  
##### <a name="to-use-a-nested-table-as-input-to-a-prediction"></a>Para usar uma tabela aninhada como entrada para uma previsão  
  
1.  Clique no botão **design** no canto superior esquerdo do construtor de consultas de previsão para voltar para a grade de construção da consulta.  
  
2.  Na caixa de diálogo **entrada de consulta singleton** , clique **Value** na caixa valor `Region`para e selecione a linha vazia para limpar a entrada desse campo.  
  
3.  Na caixa de diálogo **entrada de consulta singleton** , clique **Value** na caixa valor `vAssocSeqLineItems`para e, em seguida, clique no botão (...).  
  
4.  Na caixa de diálogo **entrada de tabela aninhada** , clique em **Adicionar**.  
  
5.  Na nova linha, clique na caixa em `Model`e selecione aro de passeio na lista. Clique em **OK**.  
  
6.  Clique no botão **resultado** para exibir as previsões.  
  
 O modelo recomenda os itens a seguir para todos os clientes que escolherem Pneu de Passeio como o primeiro item. Você já sabe, pela exploração do modelo, que os clientes frequentemente compram os produtos Pneu de Passeio e Tubo de Pneu para Passeio juntos e, portanto, essas recomendações parecem boas.  
  
|$SEQUENCE|Número da Linha|Modelo|  
|---------------|-----------------|-----------|  
|1||Tubo de pneu para passeio|  
|2||Sport-100|  
|3||Jersey Logo de manga longa|  
  
### <a name="creating-a-bulk-prediction-query-using-nested-table-inputs"></a>Criando uma consulta de previsão em massa usando entradas de tabela aninhada  
 Agora que você já está satisfeito com o modelo que cria o tipo de previsões que poderão ser usadas em recomendações, crie uma consulta de previsão mapeada para uma fonte de dados externa. Essa fonte de dados fornecerá valores que representam produtos atuais. Como você está interessado na criação de uma consulta de previsão que ofereça ID do Cliente e uma lista de produtos como entrada, adicione a tabela de clientes como uma tabela de caso e a tabela de compras como a tabela aninhada. Em seguida, adicione funções de previsão, como feito anteriormente, para criar recomendações.  
  
 Esse procedimento é igual ao usado na criação de previsões para o cenário de cesta de compras da Lição 3; no entanto, em um modelo de clustering de sequências, as previsões também precisam do pedido como entrada.  
  
##### <a name="to-create-a-prediction-query-using-nested-table-inputs"></a>Para criar uma consulta de previsão usando entradas de tabela aninhada  
  
1.  No painel **modelo de mineração** , selecione o modelo de clustering de sequência, se ainda não estiver selecionado.  
  
2.  Na caixa de diálogo **selecionar tabela (s) de entrada** , clique em **selecionar tabela de casos**.  
  
3.  Na caixa de diálogo **selecionar tabela** , para fonte de dados, selecione pedidos. Na lista **nome da tabela/exibição** , selecione vAssocSeqOrders e clique em **OK**.  
  
4.  Na caixa de diálogo **selecionar tabela (s) de entrada** , clique em **selecionar tabela aninhada**.  
  
5.  Na caixa de diálogo **selecionar tabela** , para **fonte de dados**, selecione pedidos. Na lista **nome da tabela/exibição** , selecione vAssocSeqLineItems e clique em **OK**.  
  
     O Analysis Services tentará detectar relacionamentos e os criará automaticamente, caso os tipos de dados forem iguais e se os nomes de colunas forem similares. Se as relações que ele cria estiverem erradas, você poderá clicar com o botão direito do mouse na linha de junção e selecionar **Modificar Conexões** para editar o mapeamento de coluna ou clicar com o botão direito do mouse na linha de junção e selecionar **excluir** para remover completamente a relação. Nesse caso, como as tabelas já foram unidas na exibição da fonte de dados, esses relacionamentos serão automaticamente adicionados ao painel de design.  
  
6.  Adicione uma nova linha à grade. Para **origem**, selecione vAssocSeqOrders e, para **campo**, selecione CustomerKey.  
  
7.  Adicione uma nova linha à grade. Para **origem**, selecione **função de previsão**e, para **campo**, selecione **PredictSequence**.  
  
8.  Arraste vAssocSeqLineItems para a caixa **critérios/argumento** . Clique no final da caixa **critérios/argumento** e digite os seguintes argumentos: `2`.  
  
     O texto completo na caixa **critérios/argumento** deve ser:`[Sequence Clustering].[v Assoc Seq Line Items],2`  
  
9. Clique no botão **resultado** para exibir as previsões para cada cliente.  
  
 Você concluiu o tutorial sobre modelos de clustering de sequências.  
  
## <a name="next-steps"></a>Próximas etapas  
 Se você tiver concluído todas as seções no [tutorial de mineração de dados intermediário &#40;Analysis Services&#41;de mineração de dados ](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md), a próxima etapa poderá ser aprender a usar as instruções DMX (Data Mining Extensions) para criar modelos e gerar previsões. Para obter mais informações, consulte [criando e consultando modelos de mineração de dados com DMX: tutoriais &#40;Analysis Services&#41;de mineração de dados ](../../2014/tutorials/create-query-data-mining-models-dmx-tutorials.md).  
  
 Se você já conhece conceitos de programação, também poderá usar Objetos de Gerenciamento de Análise (AMO) para começar a trabalhar com objetos de mineração de dados programaticamente. Para obter mais informações, consulte [Classes de mineração de dados AMO](https://docs.microsoft.com/bi-reference/amo/amo-data-mining-classes).  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplos de consulta de modelo de clustering de sequência](../../2014/analysis-services/data-mining/sequence-clustering-model-query-examples.md)   
 [Conteúdo do modelo de mineração para modelos de clustering de sequência &#40;Analysis Services – Data Mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)  
  
  
