---
title: 'Lição 4: navegando pelos modelos de mineração de compradores de bicicletas | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 8de3c500-f881-42da-a096-b6c03300d58d
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 709df371d840d4b24e420b4fcd08750fd31e8075
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63070871"
---
# <a name="lesson-4-browsing-the-bike-buyer-mining-models"></a>Lição 4: Explorando modelos de mineração Comprador de Bicicleta
  Nesta lição, você usará a instrução [Select (DMX)](/sql/dmx/select-dmx) para explorar o conteúdo na árvore de decisão e os modelos de mineração de cluster que você criou na [lição 2: adicionando modelos de mineração à estrutura de mineração preditiva](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md).  
  
 As colunas contidas em um modelo de mineração não são as colunas definidas pela estrutura de mineração. Ao contrário, constituem um conjunto específico de colunas que descrevem as tendências e os padrões encontrados pelo algoritmo. Essas colunas de modelo de mineração são descritas no conjunto de linhas de esquema [DMSCHEMA_MINING_MODEL_CONTENT conjunto de linhas](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset) . Por exemplo, a coluna de MODEL_NAME no conjunto de linhas de esquema de conteúdo traz o nome do modelo de mineração. Para um modelo de mineração de clustering, a coluna de NODE_CAPTION contém o nome de cada cluster e a coluna NODE_DESCRIPTION contém a descrição das características de cada cluster. Você pode procurar essas colunas usando a> selecionar do \<modelo. Demonstrativo de conteúdo no DMX. Também pode usar essa instrução para explorar os dados usados para criar o modelo de mineração. O uso dessa instrução requer que as análises sejam habilitadas na estrutura de mineração. Para obter mais informações sobre a instrução, consulte [selecionar do modelo de &#60;&#62;. CASOS &#40;&#41;DMX ](/sql/dmx/select-from-model-content-dmx).  
  
 Você também pode retornar todos os estados de uma coluna discreta usando a instrução SELECT DISTINCT. Por exemplo, se você executar esta operação na coluna gênero, a consulta retornará `male` e `female`.  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
 Você executará as seguintes tarefas nesta lição:  
  
-   Explore o conteúdo inserido nos modelos de mineração.  
  
-   Retorne as ocorrências dos dados de origem usadas para fazer um treinamento com os modelos de mineração  
  
-   Explore os diferentes estados disponíveis de uma coluna discreta específica  
  
## <a name="returning-the-content-of-a-mining-model"></a>Retornando o conteúdo de um modelo de mineração  
 Nesta lição, você usará a [&#62; de modelo selecionar de &#60;. CONTENT &#40;instrução&#41;DMX](/sql/dmx/select-from-model-dimension-content-dmx) para retornar o conteúdo do modelo de clustering.  
  
 Veja a seguir um exemplo genérico do> de seleção \<do modelo. Instrução de conteúdo:  
  
```  
SELECT <select list> FROM [<mining model>].CONTENT  
WHERE <where clause>  
```  
  
 A primeira linha do código define que as colunas retornem do conteúdo do modelo de mineração e do modelo de mineração com as quais estão associadas:  
  
```  
SELECT <select list> FROM [<mining model].CONTENT  
```  
  
 A cláusula .CONTENT, próxima ao nome do modelo de mineração, determina que você está retornando conteúdo do modelo de mineração. Para obter mais informações sobre as colunas contidas no modelo de mineração, consulte [DMSCHEMA_MINING_MODEL_CONTENT conjunto de linhas](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset).  
  
 Você pode optar por usar a linha final do código para filtrar os resultados retornados pela instrução:  
  
```  
WHERE <where clause>  
```  
  
 Por exemplo, se você quiser restringir os resultados da consulta apenas aos clusters que contêm um número elevado de ocorrências, você poderá adicionar a cláusula WHERE à instrução SELECT:  
  
```  
WHERE NODE_SUPPORT > 100  
```  
  
 Para obter mais informações sobre como usar a instrução WHERE, consulte [SELECT &#40;DMX&#41;](/sql/dmx/select-dmx).  
  
#### <a name="to-return-the-content-of-the-clustering-mining-model"></a>Para retornar o conteúdo do modelo de mineração de clustering  
  
1.  No Pesquisador de **objetos**, clique com o botão [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]direito do mouse na instância do, aponte para **nova consulta**e clique em **DMX**.  
  
     O Editor de Consultas é exibido com uma consulta nova em branco.  
  
2.  Copie o exemplo genérico do> de seleção \<do modelo. Instrução de conteúdo na consulta em branco.  
  
3.  Substitua o seguinte:  
  
    ```  
    <select list>   
    ```  
  
     por:  
  
    ```  
    *  
    ```  
  
     Você também pode substituir * por uma lista de qualquer uma das colunas contidas no [conjunto de linhas DMSCHEMA_MINING_MODEL_CONTENT](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset).  
  
4.  Substitua o seguinte:  
  
    ```  
    [<mining model>]   
    ```  
  
     por:  
  
    ```  
    [Clustering]  
    ```  
  
     A instrução completa agora deve ser:  
  
    ```  
    SELECT * FROM [Clustering].CONTENT  
    ```  
  
5.  No menu **arquivo** , clique em **salvar DMXQuery1. DMX como**.  
  
6.  Na caixa de diálogo **salvar como** , navegue até a pasta apropriada e nomeie o arquivo `SELECT_CONTENT.dmx`.  
  
7.  Na barra de ferramentas, clique no botão **executar** .  
  
     A consulta retorna o conteúdo de um modelo de mineração.  
  
## <a name="use-drillthrough"></a>Use a análise  
 O próximo passo é usar a instrução de análise para retornar uma amostragem dos casos usados para treinar o modelo de mineração de árvore de decisão. Nesta lição, você usará a [&#62; de modelo selecionar de &#60;. CASOS &#40;instrução&#41;DMX](/sql/dmx/select-from-model-content-dmx) para retornar o conteúdo do modelo de árvore de decisão.  
  
 Veja a seguir um exemplo genérico do> de seleção \<do modelo. Instrução CASEs:  
  
```  
SELECT <select list>   
FROM [<mining model>].CASES  
WHERE IsInNode('<node id>')  
```  
  
 A primeira linha do código define que as colunas retornem dos dados de origem, e do modelo de mineração a que pertencem:  
  
```  
SELECT <select list> FROM [<mining model>].CASES  
```  
  
 A cláusula .CASES especifica que você está executando uma consulta para análise. Para usar o detalhamento, você deve habilitá-lo durante a criação do modelo de mineração.  
  
 A linha final do código é opcional e especifica o nó no modelo de mineração do qual você está solicitando os casos:  
  
```  
WHERE IsInNode('<node id>')  
```  
  
 Para obter mais informações sobre como usar a instrução WHERE com IsInNode, consulte [selecionar do modelo de &#60;&#62;. CASOS &#40;&#41;DMX ](/sql/dmx/select-from-model-content-dmx).  
  
#### <a name="to-return-the-cases-that-were-used-to-train-the-mining-model"></a>Para retornar os casos usados para treinar o modelo de mineração  
  
1.  No Pesquisador de **objetos**, clique com o botão [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]direito do mouse na instância do, aponte para **nova consulta**e clique em **DMX**.  
  
     O Editor de Consultas é exibido com uma consulta nova em branco.  
  
2.  Copie o exemplo genérico do> de seleção \<do modelo. Instrução CASEs na consulta em branco.  
  
3.  Substitua o seguinte:  
  
    ```  
    <select list>   
    ```  
  
     por:  
  
    ```  
    *  
    ```  
  
     Você também pode substituir * por qualquer lista de colunas presente nos dados de origem (como [Comprador de Bicicleta]).  
  
4.  Substitua o seguinte:  
  
    ```  
    [<mining model>]   
    ```  
  
     por:  
  
    ```  
    [Decision Tree]  
    ```  
  
     A instrução completa agora deve ser:  
  
    ```  
    SELECT *   
    FROM [Decision Tree].CASES  
    ```  
  
5.  No menu **arquivo** , clique em **salvar DMXQuery1. DMX como**.  
  
6.  Na caixa de diálogo **salvar como** , navegue até a pasta apropriada e nomeie o arquivo `SELECT_DRILLTHROUGH.dmx`.  
  
7.  Na barra de ferramentas, clique no botão **executar** .  
  
     A consulta retorna os dados de origem que foram usados para treinar os modelos de mineração da árvore de decisão.  
  
## <a name="return-the-states-of-a-discrete-mining-model-column"></a>Retorne os estados de uma coluna discreta do modelo de mineração  
 O próximo passo é usar a instrução SELECT DISTINCT para retornar possíveis estados diferentes na coluna de modelo de mineração especificada.  
  
 Segue um exemplo genérico da instrução SELECT DISTINCT:  
  
```  
SELECT DISTINCT [<column>]   
FROM [<mining model>]  
```  
  
 A primeira linha do código define as colunas do modelo de mineração para as quais os estados retornam:  
  
```  
SELECT DISTINCT [<column>]   
```  
  
 Você deve incluir DISTINCT para retornar todos os estados da coluna. Se você excluir DISTINCT, então a instrução toda se tornará um atalho para uma previsão e retornará o estado mais provável da coluna especificada. Para obter mais informações, consulte [SELECT &#40;DMX&#41;](/sql/dmx/select-dmx).  
  
#### <a name="to-return-the-states-of-a-discrete-column"></a>Para retornar os estados de uma coluna discreta  
  
1.  No Pesquisador de **objetos**, clique com o botão [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]direito do mouse na instância do, aponte para **nova consulta**e clique em **DMX**.  
  
     O Editor de Consultas é exibido com uma consulta nova em branco.  
  
2.  Copie o exemplo genérico da instrução SELECT Distinct, no campo em branco da consulta.  
  
3.  Substitua o seguinte:  
  
    ```  
    [<column,name>   
    ```  
  
     por:  
  
    ```  
    [Bike Buyer]  
    ```  
  
4.  Substitua o seguinte:  
  
    ```  
    [<mining model>]   
    ```  
  
     por:  
  
    ```  
    [Decision Tree]  
    ```  
  
     A instrução completa agora deve ser:  
  
    ```  
    SELECT DISTINCT [Bike Buyer]   
    FROM [Decision Tree]  
    ```  
  
5.  No menu **arquivo** , clique em **salvar DMXQuery1. DMX como**.  
  
6.  Na caixa de diálogo **salvar como** , navegue até a pasta apropriada e nomeie o arquivo `SELECT_DISCRETE.dmx`.  
  
7.  Na barra de ferramentas, clique no botão **executar** .  
  
     A consulta retorna os estados possíveis da coluna Comprador de Bicicleta.  
  
 Na próxima lição, você poderá prever se os clientes potenciais serão os compradores de bicicleta usando o modelo de mineração da árvore de decisão.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 5: Executando previsão de consultas](../../2014/tutorials/lesson-5-executing-prediction-queries.md)  
  
  
