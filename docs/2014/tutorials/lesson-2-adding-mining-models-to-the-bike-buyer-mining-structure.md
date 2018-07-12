---
title: 'Lição 2: Adicionando modelos de mineração à estrutura de mineração de comprador de bicicleta | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 03fe44c5-6452-4ed0-95f6-9682670c0f52
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 055450b7461accaa62b1c9bafe4273f6fc3f9dd7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37149547"
---
# <a name="lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure"></a>Lição 2: Adicionando modelos de mineração à estrutura de mineração de Comprador de Bicicleta
  Nesta lição, você adicionará dois modelos de mineração à estrutura de mineração de comprador de bicicleta que você criou [lição 1: Criando a estrutura de mineração de comprador de bicicleta](../../2014/tutorials/lesson-1-creating-the-bike-buyer-mining-structure.md). Esses modelos de mineração lhe permitirão explorar os dados usando um modelo e criar previsões usando outro.  
  
 Para explorar como os clientes potenciais podem ser categorizados por suas características, você criará um modelo de mineração com base nas [algoritmo Microsoft Clustering](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md). Em uma lição posterior, você explorará como esse algoritmo localiza clusters de clientes que compartilham características semelhantes. Por exemplo, você pode identificar que alguns clientes tendem a viver perto de outros, andar de bicicleta e ter formação acadêmica similar. É possível usar esses clusters para entender melhor como clientes diferentes estão relacionados e usar as informações para criar uma estratégia de marketing cujo alvo são clientes específicos.  
  
 Para prever se um cliente potencial é a probabilidade de comprar uma bicicleta, você criará um modelo de mineração com base nas [algoritmo de árvores de decisão Microsoft](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md). Esse algoritmo verifica as informações associadas a cada cliente potencial e identifica características que são úteis para prever se eles comprarão uma bicicleta. Em seguida, ele compara os valores das características dos compradores de bicicletas anteriores com as dos novos clientes potenciais para determinar se esses clientes novos têm probabilidade de comprar uma bicicleta.  
  
## <a name="alter-mining-structure-statement"></a>Instrução ALTER MINING STRUCTURE  
 Para adicionar um modelo de mineração à estrutura de mineração, use o [ALTER MINING STRUCTURE &#40;DMX&#41;] (instrução (~/dmx/alter-mining-structure-dmx.md). O código na instrução pode ser dividido nas seguintes partes:  
  
-   Identificando a estrutura de mineração  
  
-   Nomeando o modelo de mineração  
  
-   Definindo a coluna de chave  
  
-   Definindo as colunas de entrada e as previsíveis  
  
-   Identificando as alterações de algoritmo e de parâmetro  
  
 Veja a seguir um exemplo genérico da instrução ALTER MINING MODEL:  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
ADD MINING MODEL [<mining model name>]  
(  
    [<key column>],  
    <mining model columns>,  
) USING <algorithm name>( <algorithm parameters> )  
WITH FILTER (<expression>)  
```  
  
 A primeira linha do código identifica a estrutura de mineração existente à qual os modelos de mineração serão adicionados:  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
```  
  
 A linha seguinte do código nomeia o modelo de mineração que será adicionado à estrutura de mineração:  
  
```  
ADD MINING MODEL [<mining model name>]  
```  
  
 Para obter informações sobre como nomear um objeto no DMX, consulte [identificadores &#40;DMX&#41;](/sql/dmx/identifiers-dmx).  
  
 As linhas seguintes do código definem as colunas a partir da estrutura de mineração que será usada pelo modelo de mineração:  
  
```  
[<key column>],  
<mining model columns>  
```  
  
 Você só pode usar colunas que já existem na estrutura de mineração, e a primeira coluna na lista deve ser a coluna de chave da estrutura de mineração.  
  
 A linha seguinte do código define o algoritmo de mineração que gera o modelo de mineração e os parâmetros que podem ser definidos no algoritmo:  
  
```  
) USING <algorithm name>( <algorithm parameters> )  
```  
  
 Para obter mais informações sobre os parâmetros do algoritmo que você pode ajustar, consulte [algoritmo de árvores de decisão do Microsoft](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md) e [algoritmo Microsoft Clustering](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md).  
  
 Você pode especificar que uma coluna no modelo de mineração seja utilizada para previsão usando a seguinte sintaxe:  
  
```  
<mining model column> PREDICT  
```  
  
 A última linha do código, que é opcional, define o filtro que é aplicado para treinamento e teste do modelo. Para obter mais informações sobre como aplicar filtros para modelos de mineração, consulte [filtros para modelos de mineração &#40;Analysis Services - mineração de dados&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
 Você executará as seguintes tarefas nesta lição:  
  
-   Adicionar um modelo de mineração de árvore de decisão à estrutura do Comprador de Bicicleta usando o algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../includes/msconame-md.md)]  
  
-   Adicionar um modelo de mineração de clustering à estrutura do Comprador de Bicicleta usando o algoritmo Clustering da [!INCLUDE[msCoName](../includes/msconame-md.md)]  
  
-   Como deseja ver os resultados de todos os casos, você ainda não adicionará um filtro a nenhum modelo.  
  
## <a name="adding-a-decision-tree-mining-model-to-the-structure"></a>Adicionando um modelo de mineração de árvore de decisão à estrutura  
 A primeira etapa é adicionar um modelo de mineração baseado no algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
#### <a name="to-add-a-decision-tree-mining-model"></a>Para adicionar um modelo de mineração de árvore de decisão  
  
1.  Na **Pesquisador de objetos**, clique com botão direito a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], aponte para **nova consulta**e, em seguida, clique em **DMX** para abrir o Editor de consulta e uma nova consulta em branco.  
  
2.  Copie o exemplo genérico da instrução ALTER MINING STRUCTURE na consulta em branco.  
  
3.  Substitua o seguinte:  
  
    ```  
    <mining structure name>   
    ```  
  
     por:  
  
    ```  
    [Bike Buyer]  
    ```  
  
4.  Substitua o seguinte:  
  
    ```  
    <mining model name>   
    ```  
  
     por:  
  
    ```  
    Decision Tree  
    ```  
  
5.  Substitua o seguinte:  
  
    ```  
    <mining model columns>,  
    ```  
  
     por:  
  
    ```  
    (  
       CustomerKey,  
       [Age],  
       [Bike Buyer] PREDICT,  
       [Commute Distance],  
       [Education],  
       [Gender],  
       [House Owner Flag],  
       [Marital Status],  
       [Number Cars Owned],  
       [Number Children At Home],  
       [Occupation],  
       [Region],  
       [Total Children],  
       [Yearly Income]  
    ```  
  
     Nesse caso, a coluna `[Bike Buyer]` foi designada como a coluna PREDICT.  
  
6.  Substitua o seguinte:  
  
    ```  
    USING <algorithm name>( <algorithm parameters> )   
    ```  
  
     por:  
  
    ```  
    Using Microsoft_Decision_Trees  
    WITH DRILLTHROUGH  
    ```  
  
     A instrução WITH DRILLTHROUGH permite explorar os casos que foram usados para criar o modelo de mineração.  
  
     A instrução resultante deverá ser agora:  
  
    ```  
    ALTER MINING STRUCTURE [Bike Buyer]  
    ADD MINING MODEL [Decision Tree]  
    (  
       CustomerKey,  
       [Age],  
       [Bike Buyer] PREDICT,  
       [Commute Distance],  
       [Education],  
       [Gender],  
       [House Owner Flag],  
       [Marital Status],  
       [Number Cars Owned],  
       [Number Children At Home],  
       [Occupation],  
       [Region],  
       [Total Children],  
       [Yearly Income]  
    ) USING Microsoft_Decision_Trees  
    WITH DRILLTHROUGH  
    ```  
  
7.  Sobre o **arquivo** menu, clique em **salvar DMXQuery1.dmx como**.  
  
8.  No **Salvar como** caixa de diálogo, navegue até a pasta apropriada e nomeie o arquivo `DT_Model.dmx`.  
  
9. Na barra de ferramentas, clique o **Execute** botão.  
  
## <a name="adding-a-clustering-mining-model-to-the-structure"></a>Adicionando um modelo de mineração de clustering à estrutura  
 Agora você pode adicionar um modelo de estrutura de mineração do Comprador de Bicicleta com base no algoritmo Clustering da [!INCLUDE[msCoName](../includes/msconame-md.md)] Como o modelo de mineração de clustering usará todas as colunas definidas na estrutura de mineração, você pode usar um atalho para adicionar o modelo à estrutura omitindo a definição das colunas de mineração.  
  
#### <a name="to-add-a-clustering-mining-model"></a>Para adicionar um modelo de mineração de Clustering  
  
1.  Na **Pesquisador de objetos**, clique com botão direito a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], aponte para **nova consulta**e, em seguida, clique em **DMX** para abrir o Editor de consultas e uma nova consulta em branco.  
  
2.  Copie o exemplo genérico da instrução ALTER MINING STRUCTURE na consulta em branco.  
  
3.  Substitua o seguinte:  
  
    ```  
    <mining structure name>   
    ```  
  
     por:  
  
    ```  
    [Bike Buyer]  
    ```  
  
4.  Substitua o seguinte:  
  
    ```  
    <mining model>   
    ```  
  
     por:  
  
    ```  
    Clustering Model  
    ```  
  
5.  Exclua:  
  
    ```  
    (  
        [<key column>],  
        <mining model columns>,  
    )  
    ```  
  
6.  Substitua o seguinte:  
  
    ```  
    USING <algorithm name>( <algorithm parameters> )  
    ```  
  
     por:  
  
    ```  
    USING Microsoft_Clustering  
    ```  
  
     A instrução completa agora deve ser:  
  
    ```  
    ALTER MINING STRUCTURE [Bike Buyer]  
    ADD MINING MODEL [Clustering]  
    USING Microsoft_Clustering   
    ```  
  
7.  Sobre o **arquivo** menu, clique em **salvar DMXQuery1.dmx como**.  
  
8.  No **Salvar como** caixa de diálogo, navegue até a pasta apropriada e nomeie o arquivo `Clustering_Model.dmx`.  
  
9. Na barra de ferramentas, clique o **Execute** botão.  
  
 Na próxima lição, você processará os modelos e a estrutura de mineração.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 3: Processando a estrutura de mineração Comprador de Bicicleta](../../2014/tutorials/lesson-3-processing-the-bike-buyer-mining-structure.md)  
  
  
