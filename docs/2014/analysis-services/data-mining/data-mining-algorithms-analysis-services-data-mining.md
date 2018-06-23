---
title: Algoritmos de mineração de dados (Analysis Services – mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- segmentation algorithms [Analysis Services]
- clustering [Data Mining]
- learning algorithms
- data mining [Analysis Services], models
- algorithms [data mining]
- mining models [Analysis Services], algorithms
- inductive learning
- mining models [Analysis Services], creating
- data mining [Analysis Services], algorithms
- machine learning algorithms [Analysis Services]
ms.assetid: ed1fc83b-b98c-437e-bf53-4ff001b92d64
caps.latest.revision: 72
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f0c797ed300d90416e92f3dd85f575db3a08aa8a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006022"
---
# <a name="data-mining-algorithms-analysis-services---data-mining"></a>Algoritmos de mineração de dados (Analysis Services – Mineração de Dados)
  Um *algoritmo de mineração de dados* é um conjunto de heurística e cálculos que cria um modelo de mineração de dados. Para criar um modelo, o algoritmo primeiro analisa os dados que você fornece, procurando tipos de padrões ou tendências específicos. O algoritmo usa os resultados dessa análise para definir os parâmetros ideais para criar o modelo de mineração. Esses parâmetros são aplicados pelo conjunto de dados inteiro para extrair padrões acionáveis e estatísticas detalhadas.  
  
 O modelo de mineração que um algoritmo cria a partir de seus dados pode assumir vários formatos, incluindo:  
  
-   Um conjunto de clusters que descreve como os casos em um conjunto de dados estão relacionados.  
  
-   Uma árvore de decisão que prevê um resultado e descreve como critérios diferentes afetam esse resultado.  
  
-   Um modelo matemático que prevê as vendas.  
  
-   Um conjunto de regras que descreve como são agrupados produtos em uma transação e as probabilidades de que os produtos sejam comprados juntos.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece vários algoritmos para uso em soluções de mineração de dados. Estes algoritmos são implementações de algumas das metodologias mais populares usadas em mineração de dados. Todos os algoritmos de mineração de dados da Microsoft podem ser personalizados e são completamente programáveis usando as APIs fornecidas, ou usando os componentes de mineração de dados no SQL Server Integration Services.  
  
 Você também pode usar algoritmos de terceiros compatíveis com OLE DB para mineração de dados ou desenvolver algoritmos personalizados que podem ser registrados como serviços e, em seguida, usados dentro da estrutura de mineração de dados do SQL Server.  
  
## <a name="choosing-the-right-algorithm"></a>Escolhendo o algoritmo certo  
 A escolha do melhor algoritmo para uma tarefa analítica específica pode ser um desafio. Embora você possa usar algoritmos diferentes para executar a mesma tarefa empresarial, cada algoritmo produz um resultado diferente e alguns podem produzir mais de um tipo de resultado. Por exemplo, você pode usar o algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] não apenas para previsão, mas também como uma maneira de reduzir o número de colunas em um conjunto dados uma vez que a árvore de decisão pode identificar colunas que não afetam o modelo de mineração final.  
  
### <a name="choosing-an-algorithm-by-type"></a>Escolhendo um algoritmo por tipo  
 O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] inclui os seguintes tipos de algoritmos:  
  
-   **Algoritmos de classificação** preveem uma ou mais variáveis discretas, com base nos outros atributos do conjunto de dados.  
  
-   **Algoritmos de regressão** preveem uma ou mais variáveis contínuas, como lucro ou perda, com base em outros atributos do conjunto de dados.  
  
-   **Algoritmos de segmentação** dividem dados em grupos ou clusters de itens que têm propriedades semelhantes.  
  
-   **Algoritmos de associação** encontram correlações entre atributos diferentes em um conjunto de dados. A aplicação mais comum desse tipo de algoritmo é para criar regras de associação, que podem ser usadas em uma análise da cesta de compras.  
  
-   **Algoritmos de análise de sequência** resumem sequências frequentes ou episódios em dados, como um fluxo de caminho da Web.  
  
 Porém, não há nenhuma razão para você ficar limitado a um algoritmo em suas soluções. Os analistas experientes às vezes usam um algoritmo para determinar as entradas mais efetivas (ou seja, variáveis) e então aplicam um algoritmo diferente para prever um resultado específico baseado naqueles dados. A mineração de dados do SQL Server permite que você compile vários modelos em uma única estrutura de mineração, de modo que, dentro de uma única solução de mineração de dados, você possa usar um algoritmo de clustering, um modelo de árvores de decisão e um modelo naïve Bayes para obter exibições diferentes de seus dados. Você também pode usar vários algoritmos em uma única solução para executar tarefas separadas, por exemplo, você pode usar regressão para obter previsões financeiras e um algoritmo de rede neural para executar uma análise de fatores que influenciam as vendas.  
  
### <a name="choosing-an-algorithm-by-task"></a>Escolhendo um algoritmo por tarefa  
 Para ajudar você a selecionar um algoritmo para usar com uma tarefa específica, a tabela a seguir fornece sugestões para os tipos de tarefas para as quais cada algoritmos é tradicionalmente usado.  
  
|Exemplos de tarefas|Algoritmos da Microsoft a serem usados|  
|-----------------------|---------------------------------|  
|**Prevendo um atributo discreto**<br /><br /> Sinalizar os clientes em uma lista de compradores potenciais como bons ou ruins.<br /><br /> Calcular a probabilidade de um servidor falhar dentro dos próximos 6 meses.<br /><br /> Categorizar resultados de pacientes e explore os fatores relacionados.|[Algoritmo Árvores de Decisão da Microsoft](microsoft-decision-trees-algorithm.md)<br /><br /> [Referência técnica do algoritmo Naive Bayes da Microsoft](microsoft-naive-bayes-algorithm.md)<br /><br /> [Algoritmo Microsoft Clustering](microsoft-clustering-algorithm.md)<br /><br /> [Algoritmo Rede Neural da Microsoft](microsoft-neural-network-algorithm.md)|  
|**Prevendo um atributo contínuo**<br /><br /> Prever as vendas do próximo ano.<br /><br /> Prever visitantes de site considerando as tendências históricas e sazonais.<br /><br /> Gerar uma contagem de risco considerando a demografia.|[Algoritmo Árvores de Decisão da Microsoft](microsoft-decision-trees-algorithm.md)<br /><br /> [Algoritmo Microsoft Time Series](microsoft-time-series-algorithm.md)<br /><br /> [Algoritmo Regressão Linear da Microsoft](microsoft-linear-regression-algorithm.md)|  
|**Prevendo uma sequência**<br /><br /> Executar uma análise de sequência de cliques no site da empresa.<br /><br /> Analisar os fatores que conduzem à falha do servidor.<br /><br /> Capturar e analisar sequências de atividades durante visitas de pacientes externos, formular práticas recomendadas para atividades comuns.|[Algoritmo Microsoft Sequence Clustering](microsoft-sequence-clustering-algorithm.md)|  
|**Localizando grupos de itens comuns em transações**<br /><br /> Usar análise da cesta de compras para determinar colocação de produto.<br /><br /> Sugerir produtos adicionais a um cliente para compra.<br /><br /> Analisar dados de pesquisa de visitantes para um evento, encontrar quais atividades estão correlacionadas, planejar atividades futuras.|[Algoritmo Associação da Microsoft](microsoft-association-algorithm.md)<br /><br /> [Algoritmo Árvores de Decisão da Microsoft](microsoft-decision-trees-algorithm.md)|  
|**Localizando grupos de itens semelhantes**<br /><br /> Criar grupos de perfis de risco de paciente em atributos como demografia e comportamentos.<br /><br /> Analisar usuários por padrões de navegação e compra.<br /><br /> Identificar servidores que têm características de uso semelhantes.|[Algoritmo Microsoft Clustering](microsoft-clustering-algorithm.md)<br /><br /> [Algoritmo Microsoft Sequence Clustering](microsoft-sequence-clustering-algorithm.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
 A tabela a seguir fornece links para recursos de aprendizado para cada algoritmo de mineração de dados fornecido no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
|||  
|-|-|  
|**Descrição básica do algoritmo**|Explica o que o algoritmo faz e como funciona, e descreve possíveis cenários comerciais onde o algoritmo poderia ser útil.|  
||[Algoritmo Associação da Microsoft](microsoft-association-algorithm.md)<br /><br /> [Algoritmo Microsoft Clustering](microsoft-clustering-algorithm.md)<br /><br /> [Algoritmo Árvores de Decisão da Microsoft](microsoft-decision-trees-algorithm.md)<br /><br /> [Algoritmo Regressão Linear da Microsoft](microsoft-linear-regression-algorithm.md)<br /><br /> [Algoritmo Regressão Logística da Microsoft](microsoft-logistic-regression-algorithm.md)<br /><br /> [Referência técnica do algoritmo Naive Bayes da Microsoft](microsoft-naive-bayes-algorithm.md)<br /><br /> [Algoritmo Rede Neural da Microsoft](microsoft-neural-network-algorithm.md)<br /><br /> [Algoritmo Microsoft Sequence Clustering](microsoft-sequence-clustering-algorithm.md)<br /><br /> [Algoritmo Microsoft Time Series](microsoft-time-series-algorithm.md)|  
|**Referência técnica**|Fornece detalhes técnicos sobre a implementação do algoritmo, com referências acadêmicas conforme o necessário. Lista os parâmetros que podem ser definidos para controlar o comportamento do algoritmo e personalizar os resultados no modelo. Descreve os requisitos de dados e fornece dicas de desempenho se possível.|  
||[Referência técnica do algoritmo de associação da Microsoft](microsoft-association-algorithm-technical-reference.md)<br /><br /> [Referência técnica do algoritmo Microsoft Clustering](microsoft-clustering-algorithm-technical-reference.md)<br /><br /> [Referência técnica do algoritmo Árvores de Decisão da Microsoft](microsoft-decision-trees-algorithm-technical-reference.md)<br /><br /> [Referência técnica do algoritmo de regressão linear da Microsoft](microsoft-linear-regression-algorithm-technical-reference.md)<br /><br /> [Referência técnica do algoritmo Regressão Logística da Microsoft](microsoft-logistic-regression-algorithm-technical-reference.md)<br /><br /> [Referência técnica do algoritmo Microsoft Naive Bayes](microsoft-naive-bayes-algorithm-technical-reference.md)<br /><br /> [Referência técnica do algoritmo Rede Neural da Microsoft](microsoft-neural-network-algorithm-technical-reference.md)<br /><br /> [Referência técnica do algoritmo Microsoft Sequence Clustering](microsoft-sequence-clustering-algorithm-technical-reference.md)<br /><br /> [Referência técnica do algoritmo Microsoft Time Series](microsoft-time-series-algorithm-technical-reference.md)|  
|**Conteúdo do modelo**|Explica como as informações são estruturadas dentro de cada tipo de modelo de mineração de dados, e explica como interpretar as informações armazenadas em cada um dos nós.|  
||[Conteúdo do modelo de associação de modelos de mineração &#40;Analysis Services – mineração de dados&#41;](mining-model-content-for-association-models-analysis-services-data-mining.md)<br /><br /> [Conteúdo do modelo de mineração para modelos de Clustering &#40;Analysis Services – mineração de dados&#41;](mining-model-content-for-clustering-models-analysis-services-data-mining.md)<br /><br /> [Conteúdo do modelo de árvore de decisão de mineração &#40;Analysis Services – mineração de dados&#41;](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)<br /><br /> [Conteúdo do modelo de regressão Linear modelos de mineração &#40;Analysis Services – mineração de dados&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)<br /><br /> [Conteúdo do modelo de regressão logística modelos de mineração &#40;Analysis Services – mineração de dados&#41;](mining-model-content-for-logistic-regression-models.md)<br /><br /> [Conteúdo do modelo para modelos Naive Bayes de mineração &#40;Analysis Services – mineração de dados&#41;](mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)<br /><br /> [Conteúdo do modelo de rede Neural modelos de mineração &#40;Analysis Services – mineração de dados&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)<br /><br /> [Conteúdo do modelo para modelos de Clustering de sequência de mineração &#40;Analysis Services – mineração de dados&#41;](mining-model-content-for-sequence-clustering-models.md)<br /><br /> [Conteúdo do modelo para modelos de série temporal mineração &#40;Analysis Services – mineração de dados&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md)|  
|**Consultas de mineração de dados**|Fornece diversas consultas que você pode usar com cada tipo modelo. Os exemplos incluem consultas de conteúdo que permitem que você saiba mais sobre os padrões no modelo e consultas de previsão que o ajudarão a criar previsões com base nesses padrões.|  
||[Exemplos de consulta de um modelo de associação](association-model-query-examples.md)<br /><br /> [Exemplos de consulta de modelo de clustering](clustering-model-query-examples.md)<br /><br /> [Exemplos de consulta de modelo de árvores de decisão](decision-trees-model-query-examples.md)<br /><br /> [Exemplos de consulta de modelo de regressão linear](linear-regression-model-query-examples.md)<br /><br /> [Exemplos de consulta de modelo de regressão logística](logistic-regression-model-query-examples.md)<br /><br /> [Exemplos de consulta do modelo Naive Bayes](naive-bayes-model-query-examples.md)<br /><br /> [Exemplos de consulta de modelos de rede neural](neural-network-model-query-examples.md)<br /><br /> [Exemplos de consulta dos modelos de clustering de sequências](sequence-clustering-model-query-examples.md)<br /><br /> [Exemplos de consulta de modelos de série temporal](time-series-model-query-examples.md)|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|**Tópico**|**Descrição**|  
|---------------|---------------------|  
|Determinar o algoritmo usado por um modelo de mineração de dados|[Consultar os parâmetros usados para criar um modelo de mineração](query-the-parameters-used-to-create-a-mining-model.md)|  
|Criar um algoritmo de plug-in personalizado|[Algoritmos de plug-in](plugin-algorithms.md)|  
|Explorar um modelo usando um visualizador específico de algoritmo|[Visualizadores do modelo de Mineração de dados](data-mining-model-viewers.md)|  
|Exibir o conteúdo de um modelo usando um formato de tabela genérico|[Procurar um modelo usando o Visualizador de Árvore de Conteúdo Genérica da Microsoft](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)|  
|Aprender sobre como configurar seus dados e usar algoritmos para criar modelos|[Estruturas de mineração &#40;Analysis Services – mineração de dados&#41;](mining-structures-analysis-services-data-mining.md)<br /><br /> [Modelos de mineração &#40;Analysis Services – mineração de dados&#41;](mining-models-analysis-services-data-mining.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas de mineração de dados](data-mining-tools.md)  
  
  