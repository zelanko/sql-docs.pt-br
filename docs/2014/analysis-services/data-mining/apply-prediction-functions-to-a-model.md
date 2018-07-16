---
title: Aplicar funções de previsão em um modelo | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Mining Model Prediction [Analysis Services], selecting mining models
ms.assetid: cf9a97e2-c249-441b-af12-c977c1a91c44
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a512c4e9f288c0e776b7ac6de91604da39d9f4d7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37270012"
---
# <a name="apply-prediction-functions-to-a-model"></a>Aplicar funções de previsão a um modelo
  Para criar uma consulta de previsão, você primeiro deve selecionar o modelo de mineração no qual a consulta será baseada. Você pode selecionar qualquer modelo de mineração existente no projeto atual.  
  
 Depois de selecionar um modelo, adicione uma *função de previsão* à consulta. É importante entender que as funções de previsão são usadas para muitas finalidades — sim, você pode prever valores, mas também pode obter estatísticas relacionadas, assim como informações que foram usadas para gerar a previsão. As funções de previsão podem retornar os seguintes tipos de valores:  
  
-   O nome do atributo previsível e o valor previsto.  
  
-   As estatísticas sobre a distribuição e a variância dos valores previstos.  
  
-   A probabilidade de um resultado especificado, ou de todos os possíveis resultados.  
  
-   As pontuações ou valores superiores ou inferiores.  
  
-   Os valores associados a um nó, objeto ou atributo especificado.  
  
 Há uma ampla variedade de funções de previsão que podem ser usadas, mas você deve escolher a função que se adapta ao tipo de modelo criado. Geralmente esta escolha depende do algoritmo utilizado para criar o modelo.  
  
-   Para obter uma lista das funções de previsão com suporte em quase todos os tipos de modelo, consulte [Funções de previsão geral &#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx).  
  
-   Além disso, os algoritmos individuais dão suporte a uma variedade de funções especializadas. Por exemplo, se você criar um modelo de mineração baseado no algoritmo de clustering da Microsoft, poderá usar funções de previsão especializadas para localizar informações sobre os clusters, como a distância de um valor de dados para o centroide do cluster.  
  
     Para obter exemplos de como consultar um tipo específico de modelo de mineração, consulte o tópico de referência do algoritmo, em [Algoritmos de Data Mining &#40;Analysis Services – Data Mining&#41;](data-mining-algorithms-analysis-services-data-mining.md).  
  
### <a name="choose-a-mining-model-to-use-for-prediction"></a>Escolha um modelo de mineração para usar para previsão  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse no modelo e selecione **Criar Consulta de Previsão**.  
  
     --OU --  
  
     No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique na guia **Previsão de Modelo de Mineração**e clique em **Selecionar Modelo** na tabela  **Modelo de Mineração** .  
  
2.  Na caixa de diálogo **Selecionar o Modelo de Mineração** , selecione um modelo de mineração e, em seguida, clique em **OK**.  
  
     Você pode escolher qualquer modelo dentro do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] atual. Para criar uma consulta usando um modelo em um banco de dados diferente, você deverá abrir uma nova janela de consulta no contexto desse banco de dados ou abrir o arquivo de solução que contém esse modelo.  
  
### <a name="add-prediction-functions-to-a-query"></a>Adicionar funções de previsão a uma consulta  
  
1.  No **Construtor de Consultas de Previsão**, configure os dados de entrada usados para previsão, fornecendo valores na caixa de diálogo **Entrada de Consulta Singleton** ou mapeando o modelo para uma fonte de dados externa.  
  
     Para obter mais informações, consulte [Escolher e mapear dados de entrada para uma consulta de previsão](choose-and-map-input-data-for-a-prediction-query.md).  
  
    > [!WARNING]  
    >  Não é necessário que você forneça entradas para gerar previsões. Quando não houver nenhuma entrada, o algoritmo geralmente retornará os valores de previsão mais prováveis em todas as possíveis entradas.  
  
2.  Clique na coluna **Origem** e escolha um valor da lista:  
  
    |||  
    |-|-|  
    |**\<nome do modelo >**|Selecione esta opção para incluir os valores do modelo de mineração na saída. Somente é possível adicionar colunas previsíveis.<br /><br /> Quando você adicionar uma coluna do modelo, o resultado retornado é a lista não distinta de valores nessa coluna.<br /><br /> As colunas que você adiciona com esta opção são incluídas na parte de SELECT da instrução DMX resultante.|  
    |**Prediction Function**|Selecione esta opção para procurar uma lista de funções de previsão.<br /><br /> Os valores ou funções que você seleciona são adicionados à parte SELECT da instrução DMX resultante.<br /><br /> A lista de funções de previsão não é filtrada ou restringida pelo tipo de modelo que você selecionou. Portanto, se você tiver alguma dúvida sobre se a função tem suporte para o tipo modelo atual, bastará adicionar a função à lista e ver se há erro.<br /><br /> Itens de lista que são precedidos por $ (como $AdjustedProbability) representam colunas da tabela aninhada que é produzida quando você usa a função, `PredictHistogram`. Estes são atalhos que você pode usar para retornar uma única coluna e não uma tabela aninhada.|  
    |**Expressão personalizada**|Selecione essa opção para digitar uma expressão personalizada e atribuir um alias à saída.<br /><br /> A expressão personalizada é adicionada à parte SELECT da consulta de previsão DMX resultante.<br /><br /> Esta opção será útil se você desejar adicionar texto para saída com cada linha, chamar funções VB ou chamar procedimentos armazenados personalizados.<br /><br /> Para obter mais informações sobre como usar funções VBA e Excel no DMX, consulte [Funções VBA no MDX e no DAX](/sql/mdx/vba-functions-in-mdx-and-dax).|  
  
3.  Depois de adicionar cada função ou expressão, alterne para a exibição do DMX para ver como a função é adicionada dentro da instrução DMX.  
  
    > [!WARNING]  
    >  O Construtor de Consultas de Previsão não valida o DMX até você clicar em **Resultados**. Você poderá eventualmente descobrir que a expressão gerada pelo construtor de consultas não é um DMX válido. As causas típicas fazem referência a uma coluna que não está relacionada à coluna previsível ou tentando prever uma coluna em uma tabela aninhada, que requer uma instrução sub-SELECT. Neste momento, você pode alternar a exibição do DMX e continuar editando a instrução.  
  
### <a name="example-create-a-query-on-a-clustering-model"></a>Exemplo: criar uma consulta em um modelo de clustering  
  
1.  Se você não tiver um modelo de clustering disponível para criar esta consulta de exemplo, crie o modelo [TM_Clustering] usando o [Tutorial Básico de Data Mining](../../tutorials/basic-data-mining-tutorial.md).  
  
2.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse no modelo [TM_Clustering] e selecione **Criar Consulta de Previsão**.  
  
3.  No menu **Modelo de Mineração** , selecione **Consulta Singleton**.  
  
4.  Na caixa de diálogo **Entrada de Consulta Singleton** , defina os valores a seguir como entradas:  
  
    -   Gênero = M  
  
    -   Distância do Trabalho = 5 a 10 milhas  
  
5.  Na grade de consulta, para **Origem**, selecione modelo de mineração do TM_Clustering e adicione a coluna [Bike Buyer].  
  
6.  Para **fonte**, selecione **função de previsão**e adicione a função `Cluster`.  
  
7.  Para **fonte**, selecione **função de previsão**, adicione a função `PredictSupport`e arraste a coluna do modelo [Bike Buyer] para o **critérios/argumento** caixa. Digite **Support** na coluna **Alias** .  
  
     Copie a expressão que representa a função de previsão e referência de coluna na caixa **Critérios/Argumento** .  
  
8.  Para **Origem**, selecione **Expressão Personalizada**, digite um alias e, em seguida, faça referência à função CEILING do Excel usando a seguinte sintaxe:  
  
    ```  
    Excel![CEILING](<arguments) as <return type>  
    ```  
  
     Cole a referência de coluna como o argumento para a função.  
  
     Por exemplo, a expressão a seguir retorna CEILING do valor de suporte:  
  
    ```  
    EXCEL!CEILING(PredictSupport([TM_Clustering].[Bike Buyer]),2)  
    ```  
  
     Digite CEILING na coluna **Alias** .  
  
9. Clique em **Alternar para a exibição de texto da consulta** para examinar a instrução DMX que foi gerada e, em seguida, clique em **Alternar para a exibição de resultado da consulta** para ver a saída das colunas pela consulta de previsão.  
  
     A tabela a seguir mostra os resultados esperados:  
  
    |Bike Buyer|$Cluster|Support|CEILING|  
    |----------------|--------------|-------------|-------------|  
    |0|Cluster 8|954|953.948638926372|  
  
 Se você quiser adicionar outras cláusulas em outro lugar na instrução — por exemplo, se quiser adicionar uma cláusula WHERE — não poderá adicioná-las usando a grade; deverá primeiro alternar para a exibição DMX.  
  
## <a name="see-also"></a>Consulte também  
 [Consultas de mineração de dados](data-mining-queries.md)  
  
  
