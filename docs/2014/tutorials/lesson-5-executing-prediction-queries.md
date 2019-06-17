---
title: 'Lição 5: Executar consultas de previsão | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0037bd2f-aa2d-464b-bf86-b0210f0438b1
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a5f4d6dd79f62541e207df688349f694680e2421
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62822295"
---
# <a name="lesson-5-executing-prediction-queries"></a>Lição 5: Como executar consultas de previsão
  Nesta lição, você aprenderá a usar o [SELECT FROM \<modelo > PREDICTION JOIN (DMX)](/sql/dmx/select-from-model-cases-dmx) formulário da instrução SELECT para criar dois tipos diferentes de previsões com base na árvore de decisão do modelo criado por você na [ Lição 2: Adicionando modelos de mineração à estrutura de mineração de associação](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md). Esses tipos de prognóstico estão definidos abaixo.  
  
 Consulta singleton  
 Use uma consulta singleton para fornecer valores ad hoc ao fazer previsões. Por exemplo, você pode determinar se um único cliente tem probabilidade de ser um comprador de bicicleta, passando entradas à consulta, como a distância para o trabalho, o código de área ou o número de filhos do cliente. A consulta singleton retorna um valor que indica a probabilidade de a pessoa comprar uma bicicleta com base nessas entradas.  
  
 Consulta por lotes  
 Use uma consulta por lotes para determinar que clientes em potencial em uma tabela possam vir a comprar uma bicicleta. Por exemplo, se seu departamento de marketing lhe fornecer uma lista de clientes e de atributos de cliente, então você poderá usar um prognóstico por lotes para determinar quais clientes da tabela são prováveis compradores de bicicleta.  
  
 O [SELECT FROM \<modelo > PREDICTION JOIN (DMX)](/sql/dmx/select-from-model-cases-dmx) formulário da instrução SELECT contém três partes:  
  
-   Uma lista de colunas de modelo de mineração e funções de previsão retornadas nos resultados. Os resultados também podem conter colunas de entrada dos dados de origem.  
  
-   A consulta de origem que define os dados usados para criar um prognóstico. Por exemplo, uma consulta por lotes poderia ser uma lista de clientes.  
  
-   Um mapeamento entre as colunas de modelo de mineração e os dados de origem. Se esses nomes coincidirem, então você pode usar a sintaxe NATURAL e não incluir os mapeamentos de coluna.  
  
 É possível melhorar a consulta ainda mais, usando as funções de prognóstico. As funções de prognóstico fornecem informações adicionais, como a probabilidade de um prognóstico se confirmar, e dão suporte ao prognóstico no conjunto de dados de treinamento. Para obter mais informações sobre funções de previsão, consulte [funções &#40;DMX&#41;](/sql/dmx/functions-dmx).  
  
 Os prognósticos neste tutorial se baseiam na tabela ProspectiveBuyer no banco de dados de exemplo [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]. A tabela ProspectiveBuyer contém uma lista de clientes em potencial e as características associadas a eles. Os clientes nesta tabela independem dos clientes usados para criar o modelo de mineração da árvore de decisão.  
  
 Ainda é possível criar prognósticos usando o construtor de consultas de prognóstico do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
 Você executará as seguintes tarefas nesta lição:  
  
-   Crie uma consulta singleton para determinar a probabilidade de um determinado cliente vir a comprar uma bicicleta.  
  
-   Crie uma consulta em lotes para determinar quais clientes, listados em uma tabela de clientes, têm probabilidade de comprar uma bicicleta.  
  
## <a name="singleton-query"></a>Consulta singleton  
 A primeira etapa é usar o [SELECT FROM &#60;modelo&#62; PREDICTION JOIN &#40;DMX&#41; ](/sql/dmx/select-from-model-cases-dmx) em uma consulta de previsão singleton. Segue um exemplo genérico da instrução singleton:  
  
```  
SELECT <select list> FROM [<mining model name>]   
NATURAL PREDICTION JOIN  
(SELECT '<value>' AS [<column>], ...)  
AS [<input alias>]  
```  
  
 A primeira linha do código define as colunas do modelo de mineração que a consulta deve retornar e especifica o nome do modelo de mineração usado para gerar a previsão:  
  
```  
SELECT <select list> FROM [<mining model name>]   
```  
  
 Nas linhas seguintes do código são definidas as características do cliente usadas para criar um prognóstico:  
  
```  
NATURAL PREDICTION JOIN  
(SELECT '<value>' AS [<column>], ...)  
AS [<input alias>]  
ORDER BY <expression>  
```  
  
 Se você especificar NATURAL PREDICTION JOIN, o servidor faz a correspondência entre cada coluna do modelo com uma coluna dos dados de entrada, com base em nomes de coluna. Se os nomes da coluna não coincidirem, as colunas serão ignoradas.  
  
#### <a name="to-create-a-singleton-prediction-query"></a>Para criar uma consulta de prognóstico singleton  
  
1.  Na **Pesquisador de objetos**, clique com botão direito a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], aponte para **nova consulta**e, em seguida, clique em **DMX**.  
  
     O Editor de Consultas é exibido com uma consulta nova em branco.  
  
2.  Copie o exemplo genérico da instrução singleton, no campo em branco da consulta.  
  
3.  Substitua o seguinte:  
  
    ```  
    <select list>   
    ```  
  
     por:  
  
    ```  
    [Bike Buyer] AS Buyer, PredictHistogram([Bike Buyer]) AS Statistics  
    ```  
  
     A instrução AS é usada para designar um alias para as colunas que retornaram na consulta. O [PredictHistogram](/sql/dmx/predicthistogram-dmx) função retorna estatísticas sobre a previsão, incluindo a probabilidade e o suporte. Para obter mais informações sobre as funções que podem ser usados em uma instrução de previsão, consulte [funções &#40;DMX&#41;](/sql/dmx/functions-dmx).  
  
4.  Substitua o seguinte:  
  
    ```  
    [<mining model>]   
    ```  
  
     por:  
  
    ```  
    [Decision Tree]  
    ```  
  
5.  Substitua o seguinte:  
  
    ```  
    (SELECT '<value>' AS [<column name>], ...)  AS t  
    ```  
  
     por:  
  
    ```  
    (SELECT 35 AS [Age],  
      '5-10 Miles' AS [Commute Distance],  
      '1' AS [House Owner Flag],  
      2 AS [Number Cars Owned],  
      2 AS [Total Children]) AS t  
    ```  
  
     A instrução completa agora deve ser:  
  
    ```  
    SELECT  
       [Bike Buyer] AS Buyer,  
       PredictHistogram([Bike Buyer]) AS Statistics  
    FROM  
       [Decision Tree]  
    NATURAL PREDICTION JOIN  
    (SELECT 35 AS [Age],  
       '5-10 Miles' AS [Commute Distance],  
       '1' AS [House Owner Flag],  
       2 AS [Number Cars Owned],  
       2 AS [Total Children]) AS t  
    ```  
  
6.  Sobre o **arquivo** menu, clique em **salvar DMXQuery1.dmx como**.  
  
7.  No **Salvar como** caixa de diálogo, navegue até a pasta apropriada e nomeie o arquivo `Singleton_Query.dmx`.  
  
8.  Na barra de ferramentas, clique o **Execute** botão.  
  
     A consulta retorna um prognóstico sobre a possibilidade de um cliente, com as características especificadas, comprar uma bicicleta, além de as estatísticas sobre tal prognóstico.  
  
## <a name="batch-query"></a>Consulta por lotes  
 A próxima etapa é usar o [SELECT FROM &#60;modelo&#62; PREDICTION JOIN &#40;DMX&#41; ](/sql/dmx/select-from-model-cases-dmx) em uma consulta de previsão em lotes. Segue um exemplo genérico de uma instrução por lotes:  
  
```  
SELECT TOP <number> <select list>   
FROM [<mining model name>]  
PREDICTION JOIN  
OPENQUERY([<datasource>],'<SELECT statement>')  
  AS [<input alias>]  
ON <on clause, mapping,>  
WHERE <where clause, boolean expression,>  
ORDER BY <expression>  
```  
  
 Assim como na consulta singleton, as primeiras duas linhas do código definem as colunas do modelo de mineração que a consulta retorna, assim como o nome do modelo de mineração usado para gerar o prognóstico: Parte superior \<número > instrução Especifica que a consulta retornará apenas o número ou os resultados especificados por \<número >.  
  
 As próximas linhas do código definem os dados de origem nos quais os prognóstico se baseiam:  
  
```  
OPENQUERY([<datasource>],'<SELECT statement>')  
  AS [<input alias>]  
```  
  
 Você dispõe de várias opções de métodos para recuperar os dados de origem; mas, neste tutorial, usará o OPENQUERY. Para obter mais informações sobre as opções disponíveis, consulte [ &#60;consulta de fonte de dados&#62;](/sql/dmx/source-data-query).  
  
 A linha seguinte define o mapeamento entre as colunas de origem do modelo de mineração e as colunas dos dados de origem.  
  
```  
ON <column mappings>  
```  
  
 A cláusula WHERE filtra os resultados retornados pela consulta de prognóstico:  
  
```  
WHERE <where clause, boolean expression,>  
```  
  
 A última e opcional linha do código especifica a coluna segundo a qual os resultados serão ordenados:  
  
```  
ORDER BY <expression> [DESC|ASC]  
```  
  
 Usar ORDER BY em combinação com a parte superior \<número > instrução, para filtrar os resultados que são retornados. Por exemplo, neste prognóstico você devolverá os dez principais compradores de bicicleta, ordenados pela probabilidade de maior acerto. Use a sintaxe [DESC|ASC] para controlar a ordem de exibição dos resultados.  
  
#### <a name="to-create-a-batch-prediction-query"></a>Para criar uma consulta de prognóstico por lotes  
  
1.  Na **Pesquisador de objetos**, clique com botão direito a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], aponte para **nova consulta**e, em seguida, clique em **DMX**.  
  
     O Editor de Consultas é exibido com uma consulta nova em branco.  
  
2.  Copie o exemplo genérico da instrução por lotes, no campo em branco da consulta.  
  
3.  Substitua o seguinte:  
  
    ```  
    <select list>   
    ```  
  
     por:  
  
    ```  
    SELECT  
      TOP 10  
      t.[LastName],  
      t.[FirstName],  
      [Decision Tree].[Bike Buyer],  
      PredictProbability([Bike Buyer])  
    ```  
  
     A cláusula TOP 10 especifica que apenas os dez primeiros resultados serão retornados pela consulta. Nesta consulta, a instrução ORDER BY ordena os resultados segundo a maior probabilidade de acerto do prognóstico, de forma que apenas os dez resultados mais prováveis retornem.  
  
4.  Substitua o seguinte espaço reservado:  
  
    ```  
    [<mining model>]   
    ```  
  
     Pelo nome do modelo:  
  
    ```  
    [Decision Tree]  
    ```  
  
5.  Substitua a seguinte instrução OPENQUERY genérica:  
  
    ```  
    OPENQUERY([<datasource>],'<SELECT statement>')  
    ```  
  
     Por uma instrução que referencia o data warehouse atual do Adventureworks, como:  
  
    ```  
    OPENQUERY([Adventure Works DW 2014],  
      'SELECT  
        [LastName],  
        [FirstName],  
        [MaritalStatus],  
        [Gender],  
        [YearlyIncome],  
        [TotalChildren],  
        [NumberChildrenAtHome],  
        [Education],  
        [Occupation],  
        [HouseOwnerFlag],  
        [NumberCarsOwned]  
      FROM  
        [dbo].[ProspectiveBuyer]  
      ') AS t  
    ```  
  
6.  Substitua a seguinte sintaxe genérica:  
  
    ```  
    <ON clause, mapping,>   
    WHERE <where clause, boolean expression,>  
    ORDER BY <expression>  
    ```  
  
     Pelos mapeamentos de coluna necessários para este modelo e conjunto de dados de entrada:  
  
    ```  
    [Decision Tree].[Marital Status] = t.[MaritalStatus] AND  
      [Decision Tree].[Gender] = t.[Gender] AND  
      [Decision Tree].[Yearly Income] = t.[YearlyIncome] AND  
      [Decision Tree].[Total Children] = t.[TotalChildren] AND  
      [Decision Tree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
      [Decision Tree].[Education] = t.[Education] AND  
      [Decision Tree].[Occupation] = t.[Occupation] AND  
      [Decision Tree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
      [Decision Tree].[Number Cars Owned] = t.[NumberCarsOwned]  
    WHERE [Decision Tree].[Bike Buyer] =1  
    ORDER BY PredictProbability([Bike Buyer]) DESC  
    ```  
  
     Especifique `DESC` para listar os resultados mais prováveis primeiro.  
  
     A instrução completa agora deve ser:  
  
    ```  
    SELECT  
      TOP 10  
      t.[LastName],  
      t.[FirstName],  
      [Decision Tree].[Bike Buyer],  
      PredictProbability([Bike Buyer])  
    FROM  
      [Decision Tree]  
    PREDICTION JOIN  
      OPENQUERY([Adventure Works DW 2014],  
        'SELECT  
          [LastName],  
          [FirstName],  
          [MaritalStatus],  
          [Gender],  
          [YearlyIncome],  
          [TotalChildren],  
          [NumberChildrenAtHome],  
          [Education],  
          [Occupation],  
          [HouseOwnerFlag],  
          [NumberCarsOwned]  
        FROM  
          [dbo].[ProspectiveBuyer]  
        ') AS t  
    ON  
      [Decision Tree].[Marital Status] = t.[MaritalStatus] AND  
      [Decision Tree].[Gender] = t.[Gender] AND  
      [Decision Tree].[Yearly Income] = t.[YearlyIncome] AND  
      [Decision Tree].[Total Children] = t.[TotalChildren] AND  
      [Decision Tree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
      [Decision Tree].[Education] = t.[Education] AND  
      [Decision Tree].[Occupation] = t.[Occupation] AND  
      [Decision Tree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
      [Decision Tree].[Number Cars Owned] = t.[NumberCarsOwned]  
    WHERE [Decision Tree].[Bike Buyer] =1  
    ORDER BY PredictProbability([Bike Buyer]) DESC  
    ```  
  
7.  Sobre o **arquivo** menu, clique em **salvar DMXQuery1.dmx como**.  
  
8.  No **Salvar como** caixa de diálogo, navegue até a pasta apropriada e nomeie o arquivo `Batch_Prediction.dmx`.  
  
9. Na barra de ferramentas, clique o **Execute** botão.  
  
     A consulta retorna uma tabela contendo nomes de cliente, um prognóstico sobre a possibilidade de cada cliente comprar uma bicicleta e a probabilidade deste prognóstico.  
  
 Este é o último passo no tutorial de Bike Buyer. Você tem um conjunto de modelos de mineração que lhe permite explorar as semelhanças entre seus clientes e prever se os clientes em potencial comprarão uma bicicleta.  
  
 Para saber como usar DMX em um cenário de cesta de compras, consulte [Tutorial de DMX do Market Basket](../../2014/tutorials/market-basket-dmx-tutorial.md).  
  
  
