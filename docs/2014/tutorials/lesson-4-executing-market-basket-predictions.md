---
title: 'Lição 4: executando previsões de cesta de mercado | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b3238f1b-ea04-4253-ade2-838a806b62fe
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3b49fc242eb8b2242269c5af33cc094937bbe0de
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63312106"
---
# <a name="lesson-4-executing-market-basket-predictions"></a>Lição 4: Executando previsões de Market Basket
  Nesta lição, você usará a instrução DMX `SELECT` para criar previsões com base nos modelos de associação criados na [lição 2: adicionando modelos de mineração à estrutura de mineração da cesta de compras](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md). Uma consulta de previsão é criada usando a instrução `SELECT` do DMX e adicionando uma cláusula `PREDICTION JOIN`. Para obter mais informações sobre a sintaxe de uma junção de previsão, consulte [selecionar do modelo de &#60;&#62; junção de previsão &#40;&#41;DMX ](/sql/dmx/select-from-model-cases-dmx).  
  
 O formulário **selecionar \<do modelo> junção de previsão** da `SELECT` instrução contém três partes:  
  
-   Uma lista de colunas de modelo de mineração e funções de previsão que são retornadas no conjunto de resultados. Essa lista também pode conter colunas de entrada de dados de origem.  
  
-   Uma consulta de origem que define os dados que estão sendo usados para criar uma previsão. Por exemplo, se você estiver criando muitas previsões em um lote, a consulta de origem poderá recuperar uma lista de clientes.  
  
-   Um mapeamento entre as colunas de modelo de mineração e os dados de origem. Se os nomes de colunas corresponderem, será possível usar a sintaxe `NATURAL PREDICTION JOIN` e omitir os mapeamentos de coluna.  
  
 É possível melhorar a consulta usando as funções de previsão. As funções de previsão fornecem informações adicionais, como a probabilidade de uma previsão, ou suporte à previsão no conjunto de dados de treinamento. Para obter mais informações sobre funções de previsão, consulte [funções &#40;DMX&#41;](/sql/dmx/functions-dmx).  
  
 Também é possível usar o construtor de consultas de previsão no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para criar as consultas de previsão.  
  
## <a name="singleton-prediction-join-statement"></a>Instrução singleton PREDICTION JOIN  
 A primeira etapa é criar uma consulta singleton, usando o **modelo SELECT FROM> \<sintaxe de junção de previsão** e fornecendo um único conjunto de valores como entrada. Segue um exemplo genérico da instrução singleton:  
  
```  
SELECT <select list>  
    FROM [<mining model>]   
[NATURAL] PREDICTION JOIN  
(SELECT '<value>' AS [<column>],   
    (SELECT 'value' AS [<nested column>] UNION  
        SELECT 'value' AS [<nested column>] ...)   
    AS [<nested table>])  
AS [<input alias>]  
```  
  
 A primeira linha do código define as colunas do modelo de mineração que a consulta retorna e especifica o nome do modelo de mineração usado para gerar a previsão:  
  
```  
SELECT <select list> FROM [<mining model>]   
```  
  
 A próxima linha do código indica a operação a ser executada. Como você especificará os valores de cada coluna e digitará os nomes das colunas exatamente da maneira correspondente ao modelo, a sintaxe `NATURAL PREDICTION JOIN` poderá ser aplicada. No entanto, se os nomes de coluna fossem diferentes, você teria de especificar mapeamentos entre as colunas no modelo e as colunas dos dados novos adicionando uma cláusula `ON`.  
  
```  
[NATURAL] PREDICTION JOIN  
```  
  
 As próximas linhas do código definem os produtos no carrinho de compras com o objetivo de prever os produtos adicionais que serão adicionados pelo cliente:  
  
```  
(SELECT '<value>' AS [<column>],   
    (SELECT 'value' AS [<nested column>] UNION  
        SELECT 'value' AS [<nested column>] ...)   
    AS [<nested table>])  
```  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
 Você executará as seguintes tarefas nesta lição:  
  
-   Crie uma consulta que prevê o que os outros itens que um cliente provavelmente comprará, com base nos itens já existentes em seu carrinho de compras. Você criará essa consulta usando o modelo de mineração com o *MINIMUM_PROBABILITY*padrão.  
  
-   Criar uma consulta que prevê quais os outros itens que um cliente provavelmente comprará, com base nos itens já existentes em seu carrinho de compras. Essa consulta se baseia em um modelo diferente, no qual *MINIMUM_PROBABILITY* foi definido como 0, 1. Como o valor padrão para *MINIMUM_PROBABILITY* em modelos de associação é 0,3, a consulta nesse modelo deve retornar mais itens possíveis do que a consulta no modelo padrão.  
  
## <a name="create-a-prediction-by-using-a-model-with-the-default-minimum_probability"></a>Criar uma previsão usando um modelo com o padrão MINIMUM_PROBABILITY  
  
#### <a name="to-create-an-association-query"></a>Para criar uma consulta de associação  
  
1.  No Pesquisador de **objetos**, clique com o botão [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]direito do mouse na instância do, aponte para **nova consulta**e clique em **DMX** para abrir o editor de consultas.  
  
2.  Copie o exemplo genérico da instrução `PREDICTION JOIN` na consulta em branco.  
  
3.  Substitua o seguinte:  
  
    ```  
    <select list>   
    ```  
  
     por:  
  
    ```  
    PREDICT([Default Association].[Products],INCLUDE_STATISTICS,3)  
    ```  
  
     Você pode apenas incluir o nome da coluna [Products], mas usando a função [Predict &#40;DMX&#41;](/sql/dmx/predict-dmx) , você pode limitar o número de produtos retornados pelo algoritmo a três. Também poderá usar `INCLUDE_STATISTICS` que retorna o suporte e a probabilidade, além de permitir ajustar a probabilidade para cada produto. Essas estatísticas ajudam a definir a taxa de exatidão da previsão.  
  
4.  Substitua o seguinte:  
  
    ```  
    [<mining model>]   
    ```  
  
     por:  
  
    ```  
    [Default Association]  
    ```  
  
5.  Substitua o seguinte:  
  
    ```  
    (SELECT '<value>' AS [<column>],   
        (SELECT 'value' AS [<nested column>] UNION  
            SELECT 'value' AS [<nested column>] ...)   
        AS [<nested table>])  
    ```  
  
     por:  
  
    ```  
    (SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
      UNION SELECT 'Mountain Tire Tube' AS [Model]  
      UNION SELECT 'Mountain-200' AS [Model]) AS [Products]) AS t  
    ```  
  
     Essa instrução usa a instrução `UNION` para especificar três produtos que devem ser incluídos no carrinho de compras junto com os produtos previstos. A coluna Model na instrução `SELECT` corresponde à coluna de modelo contida na tabela de produtos aninhados.  
  
     A instrução completa agora deve ser:  
  
    ```  
    SELECT  
      PREDICT([Default Association].[Products],INCLUDE_STATISTICS,3)  
    From  
      [Default Association]  
    NATURAL PREDICTION JOIN  
    (SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
      UNION SELECT 'Mountain Tire Tube' AS [Model]  
      UNION SELECT 'Mountain-200' AS [Model]) AS [Products]) AS t  
    ```  
  
6.  No menu **arquivo** , clique em **salvar DMXQuery1. DMX como**.  
  
7.  Na caixa de diálogo **salvar como** , navegue até a pasta apropriada e nomeie o arquivo `Association Prediction.dmx`.  
  
8.  Na barra de ferramentas, clique no botão **executar** .  
  
     A consulta retorna uma tabela que contém três produtos: HL Mountain Tire, Fender Set - Mountain e ML Mountain Tire. A tabela lista esses produtos retornados em ordem de probabilidade. O produto retornado que provavelmente será incluído no mesmo carrinho de compras juntamente com os três produtos especificados na consulta aparece no topo da tabela. Os dois produtos que seguem são provavelmente o próximo item que será incluído no carrinho de compra. A tabela também contém estatísticas que descrevem a exatidão da previsão.  
  
## <a name="create-a-prediction-by-using-a-model-with-a-minimum_probability-of-001"></a>Criar uma previsão usando um modelo com uma MINIMUM_PROBABILITY de 0,01  
  
#### <a name="to-create-an-association-query"></a>Para criar uma consulta de associação  
  
1.  No Pesquisador de **objetos**, clique com o botão [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]direito do mouse na instância do, aponte para **nova consulta**e clique em **DMX** para abrir o editor de consultas.  
  
2.  Copie o exemplo genérico da instrução `PREDICTION JOIN` na consulta em branco.  
  
3.  Substitua o seguinte:  
  
    ```  
    <select list>   
    ```  
  
     por:  
  
    ```  
    PREDICT([Modified Association].[Products],INCLUDE_STATISTICS,3)  
    ```  
  
4.  Substitua o seguinte:  
  
    ```  
    [<mining model>]   
    ```  
  
     por:  
  
    ```  
    [Modified Association]  
    ```  
  
5.  Substitua o seguinte:  
  
    ```  
    (SELECT '<value>' AS [<column>],   
        (SELECT 'value' AS [<nested column>] UNION  
            SELECT 'value' AS [<nested column>] ...)   
        AS [<nested table>])  
    ```  
  
     por:  
  
    ```  
    (SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
      UNION SELECT 'Mountain Tire Tube' AS [Model]  
      UNION SELECT 'Mountain-200' AS [Model]) AS [Products]) AS t  
    ```  
  
     Essa instrução usa a instrução `UNION` para especificar três produtos que devem ser incluídos no carrinho de compras junto com os produtos previstos. A coluna `[Model]` na instrução `SELECT` corresponde à coluna na tabela de produtos aninhados.  
  
     A instrução completa agora deve ser:  
  
    ```  
    SELECT  
      PREDICT([Modified Association].[Products],INCLUDE_STATISTICS,3)  
    From  
      [Modified Association]  
    NATURAL PREDICTION JOIN  
    (SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
      UNION SELECT 'Mountain Tire Tube' AS [Model]  
      UNION SELECT 'Mountain-200' AS [Model]) AS [Products]) AS t  
    ```  
  
6.  No menu **arquivo** , clique em **salvar DMXQuery1. DMX como**.  
  
7.  Na caixa de diálogo **salvar como** , navegue até a pasta apropriada e nomeie o arquivo `Modified Association Prediction.dmx`.  
  
8.  Na barra de ferramentas, clique no botão **executar** .  
  
     A consulta retorna uma tabela que contém três produtos: tubo de pneu para mountain bike, garrafa de água e kit para montanhismo. A tabela lista esses produtos em ordem de probabilidade. O produto que aparece no topo da tabela é o produto que provavelmente será incluído no mesmo carrinho de compras juntamente com os três produtos especificados na consulta. Os produtos restantes são provavelmente os próximos que serão incluídos no carrinho de compras. A tabela também contém estatísticas que descrevem a precisão da previsão.  
  
     Você pode ver nos resultados dessa consulta que o valor do parâmetro *MINIMUM_PROBABILITY* afeta os resultados retornados pela consulta.  
  
 Esta é a última etapa no tutorial da cesta básica. Agora você tem um conjunto de modelos que pode ser usado para prever os produtos que os clientes podem comprar ao mesmo tempo.  
  
 Para saber como usar o DMX em outro cenário de previsão, confira [tutorial de compra do DMX para bicicletas](../../2014/tutorials/bike-buyer-dmx-tutorial.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplos de consulta de modelo de associação](../../2014/analysis-services/data-mining/association-model-query-examples.md)   
 [Interfaces de Consulta de Mineração de Dados](../../2014/analysis-services/data-mining/data-mining-query-tools.md)  
  
  
