---
title: 'Lição 2: adicionando modelos de mineração à estrutura de mineração da cesta de mercado | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d96a7a7d-35d7-4b34-abb5-f0822c256253
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b9573d9359983e33cf23533787c26039572710ea
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63204724"
---
# <a name="lesson-2-adding-mining-models-to-the-market-basket-mining-structure"></a>Lição 2: Adicionando modelos de mineração à estrutura de mineração do Market Basket 
  Nesta lição, você adicionará dois modelos de mineração à estrutura de mineração de cesta de mercado criada na [lição 1: criando a estrutura de mineração de cesta de compras](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md). Estes modelos de mineração permitirão criar previsões.  
  
 Para prever os tipos de produtos que os clientes tendem a comprar ao mesmo tempo, você criará dois modelos de mineração usando o [algoritmo de associação da Microsoft](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md) e dois valores diferentes para o parâmetro *MINIMUM_PROBABILTY* .  
  
 *MINIMUM_PROBABILTY* é um [!INCLUDE[msCoName](../includes/msconame-md.md)] parâmetro de algoritmo de associação que ajuda a determinar o número de regras que um modelo de mineração conterá, especificando a probabilidade mínima que uma regra deve ter. Por exemplo, definindo-se esse valor como 0,4, uma regra é especificada, a qual só poderá ser gerada se a combinação de produtos que a regra descreve tiver, pelo menos, 40% de probabilidade de ocorrência.  
  
 Você exibirá o efeito de alterar o parâmetro *MINIMUM_PROBABILTY* em uma lição posterior.  
  
## <a name="alter-mining-structure-statement"></a>Instrução ALTER MINING STRUCTURE  
 Para adicionar um modelo de mineração que contém uma tabela aninhada a uma estrutura de mineração, use a instrução [ALTER MINING structure &#40;DMX&#41;](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016) . O código na instrução pode ser dividido nas seguintes partes:  
  
-   Identificando a estrutura de mineração  
  
-   Nomeando o modelo de mineração  
  
-   Definindo a coluna de chave  
  
-   Definindo as colunas de entrada e as previsíveis  
  
-   Definindo as colunas de tabelas aninhadas  
  
-   Identificando as alterações de algoritmo e de parâmetro  
  
 A seguir, está um exemplo genérico da instrução `ALTER MINING STRUCTURE` que adiciona um modelo de mineração a uma estrutura que inclui colunas de tabelas aninhadas:  
  
```  
ALTER MINING STRUCTURE [<Mining Structure Name>]  
ADD MINING MODEL [<Mining Model Name>]  
(  
    [<key column>],  
    <mining model column> <usage>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
) USING <algorithm>( <algorithm parameters> )  
```  
  
 A primeira linha do código identifica a estrutura de mineração existente à qual o modelo de mineração será adicionada:  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
```  
  
 A linha seguinte do código nomeia o modelo de mineração que será adicionado à estrutura de mineração:  
  
```  
ADD MINING MODEL [<mining model name>]  
```  
  
 Para obter informações sobre como nomear um objeto em DMX (extensões de mineração de dados), consulte [identificadores &#40;&#41;DMX ](/sql/dmx/identifiers-dmx).  
  
 As linhas seguintes do código definem as colunas da estrutura de mineração que será usada pelo modelo de mineração:  
  
```  
[<key column>],  
<mining model columns> <usage>,  
```  
  
 Você só pode usar colunas que já existam na estrutura de mineração.  
  
 A primeira coluna na lista de colunas do modelo de mineração deve ser a coluna de chave na estrutura de mineração. No entanto, você não precisa digitar `KEY` após a coluna de chave para especificar o uso. Isso é porque você já definiu a coluna como uma chave quando criou a estrutura de mineração.  
  
 As linhas restantes especificam o uso das colunas no novo modelo de mineração. Você pode especificar que uma coluna no modelo de mineração será utilizada para previsão usando a seguinte sintaxe:  
  
```  
<column name> PREDICT,  
```  
  
 Se você não especificar o uso, não terá que incluir uma coluna de estrutura de mineração de dados na lista. Todas as colunas usadas pela estrutura de mineração de dados referenciada estão automaticamente disponíveis para uso pelos modelos de mineração que se baseiam nessa estrutura. Porém, o modelo não usará as colunas para treinamento, a menos que você especifique o uso.  
  
 A última linha do código define o algoritmo e os parâmetros de algoritmo que serão usados para gerar o modelo de mineração.  
  
```  
) USING <algorithm>( <algorithm parameters> )  
```  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
 Você executará as seguintes tarefas nesta lição:  
  
-   Adicione um modelo de mineração de associação à estrutura, usando a probabilidade padrão  
  
-   Adicione um modelo de mineração de associação à estrutura, usando uma probabilidade modificada  
  
## <a name="adding-an-association-mining-model-to-the-structure-using-the-default-minimum_probability"></a>Acrescentando um Modelo de Mineração de Associação à estrutura usando MINIMUM_PROBABILITY padrão  
 A primeira tarefa é adicionar um novo modelo de mineração à estrutura de mineração de cesta de mercado com [!INCLUDE[msCoName](../includes/msconame-md.md)] base no algoritmo de associação usando o valor padrão para *MINIMUM_PROBABILITY*.  
  
#### <a name="to-add-an-association-mining-model"></a>Para adicionar um modelo de mineração de Associação  
  
1.  No Pesquisador de **objetos**, clique com o botão [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]direito do mouse na instância do, aponte para **nova consulta**e clique em **DMX**.  
  
     O Editor de Consultas é exibido com uma consulta nova em branco.  
  
    > [!NOTE]  
    >  Para criar uma consulta DMX para um banco de dados [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] específico, clique com o botão direito do mouse no banco de dados em vez da instância.  
  
2.  Copie o exemplo genérico da instrução `ALTER MINING STRUCTURE` na consulta em branco.  
  
3.  Substitua o seguinte:  
  
    ```  
    <mining structure name>   
    ```  
  
     por:  
  
    ```  
    [Market Basket]  
    ```  
  
4.  Substitua o seguinte:  
  
    ```  
    <mining model name>   
    ```  
  
     por:  
  
    ```  
    [Default Association]  
    ```  
  
5.  Substitua o seguinte:  
  
    ```  
    [<key column>],  
    <mining model columns>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
    ```  
  
     por:  
  
    ```  
    OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    ```  
  
     Nesse caso, a tabela `[Products]` foi designada como a coluna previsível`.` Além disso, a coluna `[Model]` é incluída na lista de colunas de tabelas aninhadas, porque ela é a coluna de chave da tabela aninhada.  
  
    > [!NOTE]  
    >  Lembre-se de que uma chave aninhada é diferente de uma chave de caso. Uma chave de caso é um identificador exclusivo do caso, enquanto a chave aninhada é um atributo que você quer modelar.  
  
6.  Substitua o seguinte:  
  
    ```  
    USING <algorithm>( <algorithm parameters> )  
    ```  
  
     por:  
  
    ```  
    Using Microsoft_Association_Rules  
    ```  
  
     A instrução resultante deverá ser agora:  
  
    ```  
    ALTER MINING STRUCTURE [Market Basket]  
    ADD MINING MODEL [Default Association]  
    (  
        OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    )  
    Using Microsoft_Association_Rules  
    ```  
  
7.  No menu **arquivo** , clique em **salvar DMXQuery1. DMX como**.  
  
8.  Na caixa de diálogo **salvar como** , navegue até a pasta apropriada e nomeie o arquivo `Default_Association_Model.dmx`.  
  
9. Na barra de ferramentas, clique no botão **executar** .  
  
## <a name="adding-an-association-mining-model-to-the-structure-changing-the-default-minimum_probability"></a>Acrescentando um Modelo de Mineração de Associação à estrutura alterando MINIMUM_PROBABILITY padrão  
 A próxima tarefa é adicionar um novo modelo de mineração à estrutura de mineração da cesta de compras, com base no algoritmo Associação da [!INCLUDE[msCoName](../includes/msconame-md.md)] e alterar o valor padrão de MINIMUM_PROBABILITY para 0,01. A alteração do parâmetro fará com que o algoritmo de Associação [!INCLUDE[msCoName](../includes/msconame-md.md)] crie mais regras.  
  
#### <a name="to-add-an-association-mining-model"></a>Para adicionar um modelo de mineração de Associação  
  
1.  No Pesquisador de **objetos**, clique com o botão [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]direito do mouse na instância do, aponte para **nova consulta**e clique em **DMX**.  
  
     O Editor de Consultas é exibido com uma consulta nova em branco.  
  
2.  Copie o exemplo genérico da instrução `ALTER MINING STRUCTURE` na consulta em branco.  
  
3.  Substitua o seguinte:  
  
    ```  
    <mining structure name>   
    ```  
  
     por:  
  
    ```  
    Market Basket  
    ```  
  
4.  Substitua o seguinte:  
  
    ```  
    <mining model name>   
    ```  
  
     por:  
  
    ```  
    [Modified Association]  
    ```  
  
5.  Substitua o seguinte:  
  
    ```  
    <mining model columns>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
    ```  
  
     por:  
  
    ```  
    OrderNumber,  
    [Products] PREDICT (  
            [Model]  
        )  
    ```  
  
     Neste caso, a tabela `[Products]` foi designada como a coluna previsível. Também, a coluna `[MODEL]` é incluída na lista, porque é a coluna de chave na tabela aninhada.  
  
6.  Substitua o seguinte:  
  
    ```  
    USING <algorithm>( <algorithm parameters> )  
    ```  
  
     por:  
  
    ```  
    USING Microsoft_Association_Rules (Minimum_Probability = 0.1)  
    ```  
  
     A instrução resultante deverá ser agora:  
  
    ```  
    ALTER MINING STRUCTURE [Market Basket]  
    ADD MINING MODEL [Modified Assocation]  
    (  
        OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    )  
    USING Microsoft_Association_Rules (Minimum_Probability = 0.1)  
    ```  
  
7.  No menu **arquivo** , clique em **salvar DMXQuery1. DMX como**.  
  
8.  Na caixa de diálogo **salvar como** , navegue até a pasta apropriada e nomeie o arquivo `Modified Association_Model.dmx`.  
  
9. Na barra de ferramentas, clique no botão **executar** .  
  
 Nesta próxima lição você processará a estrutura de mineração da cesta básica junto com seus modelos de mineração associados.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 3: Processando a estrutura de mineração do Market Basket](../../2014/tutorials/lesson-3-processing-the-market-basket-mining-structure.md)  
  
  
