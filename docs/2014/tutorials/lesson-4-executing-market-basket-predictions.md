---
title: 'Lição 4: Execução de previsões de Market Basket | Microsoft Docs'
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
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63312106"
---
# <a name="lesson-4-executing-market-basket-predictions"></a>Lição 4: Como executar previsões de Market Basket
  Nesta lição, você aprenderá a usar o DMX `SELECT` instrução para criar previsões com base na associação de modelos criada na [lição 2: Adicionando modelos de mineração à estrutura de mineração de Market Basket](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md). Uma consulta de previsão é criada usando a instrução `SELECT` do DMX e adicionando uma cláusula `PREDICTION JOIN`. Para obter mais informações sobre a sintaxe de uma junção de previsão, consulte [SELECT FROM &#60;modelo&#62; PREDICTION JOIN &#40;DMX&#41;](/sql/dmx/select-from-model-cases-dmx).  
  
 O **SELECT FROM \<modelo > PREDICTION JOIN** forma do `SELECT` instrução contém três partes:  
  
-   Uma lista de colunas de modelo de mineração e funções de previsão que são retornadas no conjunto de resultados. Essa lista também pode conter colunas de entrada de dados de origem.  
  
-   Uma consulta de origem que define os dados que estão sendo usados para criar uma previsão. Por exemplo, se você estiver criando muitas previsões em um lote, a consulta de origem poderá recuperar uma lista de clientes.  
  
-   Um mapeamento entre as colunas de modelo de mineração e os dados de origem. Se os nomes de colunas corresponderem, será possível usar a sintaxe `NATURAL PREDICTION JOIN` e omitir os mapeamentos de coluna.  
  
 É possível melhorar a consulta usando as funções de previsão. As funções de previsão fornecem informações adicionais, como a probabilidade de uma previsão, ou suporte à previsão no conjunto de dados de treinamento. Para obter mais informações sobre funções de previsão, consulte [funções &#40;DMX&#41;](/sql/dmx/functions-dmx).  
  
 Também é possível usar o construtor de consultas de previsão no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para criar as consultas de previsão.  
  
## <a name="singleton-prediction-join-statement"></a>Instrução singleton PREDICTION JOIN  
 A primeira etapa é criar uma consulta singleton, usando o **SELECT FROM \<modelo > PREDICTION JOIN** sintaxe e fornecendo um único conjunto de valores como entrada. Segue um exemplo genérico da instrução singleton:  
  
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
  
-   Crie uma consulta que prevê quais outros itens de um cliente provavelmente comprará, com base nos itens já existentes no carrinho de compras. Você irá criar esta consulta usando o modelo de mineração com o padrão *MINIMUM_PROBABILITY*.  
  
-   Criar uma consulta que prevê quais os outros itens que um cliente provavelmente comprará, com base nos itens já existentes em seu carrinho de compras. Esta consulta baseia-se em um modelo diferente, na qual *MINIMUM_PROBABILITY* foi definida como 0,01. Como o valor padrão para *MINIMUM_PROBABILITY* em modelos de associação é 0,3, a consulta neste modelo deve retornar mais itens que a consulta no modelo padrão.  
  
## <a name="create-a-prediction-by-using-a-model-with-the-default-minimumprobability"></a>Criar uma previsão usando um modelo com o padrão MINIMUM_PROBABILITY  
  
#### <a name="to-create-an-association-query"></a>Para criar uma consulta de associação  
  
1.  Na **Pesquisador de objetos**, clique com botão direito a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], aponte para **nova consulta**e, em seguida, clique em **DMX** para abrir o Editor de consultas.  
  
2.  Copie o exemplo genérico da instrução `PREDICTION JOIN` na consulta em branco.  
  
3.  Substitua o seguinte:  
  
    ```  
    <select list>   
    ```  
  
     por:  
  
    ```  
    PREDICT([Default Association].[Products],INCLUDE_STATISTICS,3)  
    ```  
  
     Você poderia apenas incluir o nome da coluna [Products], mas usando o [Predict &#40;DMX&#41; ](/sql/dmx/predict-dmx) função, você pode limitar o número de produtos que são retornados pelo algoritmo para três. Também poderá usar `INCLUDE_STATISTICS` que retorna o suporte e a probabilidade, além de permitir ajustar a probabilidade para cada produto. Essas estatísticas ajudam a definir a taxa de exatidão da previsão.  
  
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
  
6.  Sobre o **arquivo** menu, clique em **salvar DMXQuery1.dmx como**.  
  
7.  No **Salvar como** caixa de diálogo, navegue até a pasta apropriada e nomeie o arquivo `Association Prediction.dmx`.  
  
8.  Na barra de ferramentas, clique o **Execute** botão.  
  
     A consulta retorna uma tabela que contém três produtos: HL Mountain Tire, conjunto de lama - Mountain e ML Mountain Tire. A tabela lista esses produtos retornados em ordem de probabilidade. O produto retornado que provavelmente será incluído no mesmo carrinho de compras juntamente com os três produtos especificados na consulta aparece no topo da tabela. Os dois produtos que seguem são provavelmente o próximo item que será incluído no carrinho de compra. A tabela também contém estatísticas que descrevem a exatidão da previsão.  
  
## <a name="create-a-prediction-by-using-a-model-with-a-minimumprobability-of-001"></a>Criar uma previsão usando um modelo com uma MINIMUM_PROBABILITY de 0,01  
  
#### <a name="to-create-an-association-query"></a>Para criar uma consulta de associação  
  
1.  Na **Pesquisador de objetos**, clique com botão direito a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], aponte para **nova consulta**e, em seguida, clique em **DMX** para abrir o Editor de consultas.  
  
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
  
6.  Sobre o **arquivo** menu, clique em **salvar DMXQuery1.dmx como**.  
  
7.  No **Salvar como** caixa de diálogo, navegue até a pasta apropriada e nomeie o arquivo `Modified Association Prediction.dmx`.  
  
8.  Na barra de ferramentas, clique o **Execute** botão.  
  
     A consulta retorna uma tabela que contém três produtos: Conjunto de lama - Mountain, Water Bottle e HL Mountain Tire. A tabela lista esses produtos em ordem de probabilidade. O produto que aparece no topo da tabela é o produto que provavelmente será incluído no mesmo carrinho de compras juntamente com os três produtos especificados na consulta. Os produtos restantes são provavelmente os próximos que serão incluídos no carrinho de compras. A tabela também contém estatísticas que descrevem a precisão da previsão.  
  
     Você pode ver os resultados dessa consulta que o valor da *MINIMUM_PROBABILITY* parâmetro afeta os resultados retornados pela consulta.  
  
 Esta é a última etapa no tutorial da cesta básica. Agora você tem um conjunto de modelos que pode ser usado para prever os produtos que os clientes podem comprar ao mesmo tempo.  
  
 Para saber como usar DMX em outro cenário de previsão, consulte [Bike Buyer DMX Tutorial](../../2014/tutorials/bike-buyer-dmx-tutorial.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exemplos de consulta de um modelo de associação](../../2014/analysis-services/data-mining/association-model-query-examples.md)   
 [Interfaces de Consulta de Mineração de Dados](../../2014/analysis-services/data-mining/data-mining-query-tools.md)  
  
  
