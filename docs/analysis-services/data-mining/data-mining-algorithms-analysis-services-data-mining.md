---
title: Algoritmos de mineração de dados (Analysis Services - mineração de dados) | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 55b46feab1170d5db9689e9347a37f7353263791
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68183801"
---
# <a name="data-mining-algorithms-analysis-services---data-mining"></a>Algoritmos de mineração de dados (Analysis Services – Mineração de Dados)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Um *algoritmo* na mineração de dados (ou aprendizado de máquina) é um conjunto de heurística e cálculos que cria um modelo com base nos dados. Para criar um modelo, o algoritmo primeiro analisa os dados que você fornece, procurando tipos de padrões ou tendências específicos. O algoritmo usa os resultados dessa análise em muitas iterações para definir os parâmetros ideais para criar o modelo de mineração. Esses parâmetros são aplicados pelo conjunto de dados inteiro para extrair padrões acionáveis e estatísticas detalhadas.  
  
 O modelo de mineração que um algoritmo cria a partir de seus dados pode assumir vários formatos, incluindo:  
  
-   Um conjunto de clusters que descreve como os casos em um conjunto de dados estão relacionados.  
  
-   Uma árvore de decisão que prevê um resultado e descreve como critérios diferentes afetam esse resultado.  
  
-   Um modelo matemático que prevê as vendas.  
  
-   Um conjunto de regras que descreve como são agrupados produtos em uma transação e as probabilidades de que os produtos sejam comprados juntos.  
  
 Os algoritmos fornecidos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining são os métodos mais populares e bem conhecidos de derivar padrões dos dados. Por exemplo, clustering de K-means é um dos algoritmos de clustering mais antigos e está disponível amplamente em muitas ferramentas e com muitas opções e implementações diferentes. No entanto, a implementação de clustering de K-means específica usada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining foi desenvolvida pela Microsoft Research e então otimizada para melhor desempenho com o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Todos os algoritmos de mineração de dados da Microsoft podem ser amplamente personalizados e são totalmente programáveis usando as APIs fornecidas. Você também pode automatizar a criação, treinamento e retreinamento de modelos usando os componentes de mineração de dados no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Você também pode usar algoritmos de terceiros que estão em conformidade com a especificação do OLE DB para Data Mining ou desenvolver algoritmos personalizados que podem ser registrados como serviços e usados da estrutura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining.  
  
## <a name="choosing-the-right-algorithm"></a>Escolhendo o algoritmo certo  
 A escolha do melhor algoritmo para uma tarefa analítica específica pode ser um desafio. Embora você possa usar algoritmos diferentes para executar a mesma tarefa empresarial, cada algoritmo produz um resultado diferente e alguns podem produzir mais de um tipo de resultado. Por exemplo, você pode usar o algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] não apenas para previsão, mas também como uma maneira de reduzir o número de colunas em um conjunto dados uma vez que a árvore de decisão pode identificar colunas que não afetam o modelo de mineração final.  
  
### <a name="choosing-an-algorithm-by-type"></a>Escolhendo um algoritmo por tipo  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Data Mining inclui os seguintes tipos de algoritmos:  
  
-   **Algoritmos de classificação** preveem uma ou mais variáveis discretas, com base nos outros atributos do conjunto de dados.  
  
-   **Algoritmos de regressão** preveem uma ou mais variáveis numéricas contínuas, como lucro ou perda, com base nos outros atributos do conjunto de dados.  
  
-   **Algoritmos de segmentação** dividem dados em grupos ou clusters de itens que têm propriedades semelhantes.  
  
-   **Algoritmos de associação** encontram correlações entre atributos diferentes em um conjunto de dados. A aplicação mais comum desse tipo de algoritmo é para criar regras de associação, que podem ser usadas em uma análise da cesta de compras.  
  
-   **Algoritmos de análise de sequência** resumem sequências ou episódios frequentes em dados, como uma série de cliques em um site da Web ou uma série de eventos de log de manutenção de computador anteriores.  
  
 Porém, não há nenhuma razão para você ficar limitado a um algoritmo em suas soluções. Os analistas experientes às vezes usam um algoritmo para determinar as entradas mais efetivas (ou seja, variáveis) e então aplicam um algoritmo diferente para prever um resultado específico baseado naqueles dados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Data Mining permite que você crie vários modelos em uma única estrutura de mineração, de modo que, dentro de uma única solução de mineração de dados, você possa usar um algoritmo de clustering, um modelo de árvores de decisão e um modelo Naïve Bayes para obter exibições diferentes de seus dados. Você também pode usar vários algoritmos em uma única solução para executar tarefas separadas, por exemplo, você pode usar regressão para obter previsões financeiras e um algoritmo de rede neural para executar uma análise de fatores que influenciam as previsões.  
  
### <a name="choosing-an-algorithm-by-task"></a>Escolhendo um algoritmo por tarefa  
 Para ajudar você a selecionar um algoritmo para usar com uma tarefa específica, a tabela a seguir fornece sugestões para os tipos de tarefas para as quais cada algoritmos é tradicionalmente usado.  
  
|Exemplos de tarefas|Algoritmos da Microsoft a serem usados|  
|-----------------------|---------------------------------|  
|**Prevendo um atributo discreto:**<br /><br /> Sinalizar os clientes em uma lista de compradores potenciais como bons ou ruins.<br /><br /> Calcular a probabilidade de um servidor falhar dentro dos próximos 6 meses.<br /><br /> Categorizar resultados de pacientes e explore os fatores relacionados.|[Algoritmo Árvores de Decisão da Microsoft](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)<br /><br /> [Referência técnica do algoritmo Naive Bayes da Microsoft](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)<br /><br /> [Algoritmo Microsoft Clustering](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)<br /><br /> [Algoritmo Rede Neural da Microsoft](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)|  
|**Prevendo um atributo contínuo:**<br /><br /> Prever as vendas do próximo ano.<br /><br /> Prever visitantes de site considerando as tendências históricas e sazonais.<br /><br /> Gerar uma contagem de risco considerando a demografia.|[Algoritmo Árvores de Decisão da Microsoft](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)<br /><br /> [Algoritmo Microsoft Time Series](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)<br /><br /> [Algoritmo Regressão Linear da Microsoft](../../analysis-services/data-mining/microsoft-linear-regression-algorithm.md)|  
|**Prevendo uma sequência:**<br /><br /> Executar uma análise de sequência de cliques no site da empresa.<br /><br /> Analisar os fatores que conduzem à falha do servidor.<br /><br /> Capturar e analisar sequências de atividades durante visitas de pacientes externos, formular práticas recomendadas para atividades comuns.|[Algoritmo Microsoft Sequence Clustering](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)|  
|**Localizando grupos de itens comuns em transações:**<br /><br /> Usar análise da cesta de compras para determinar colocação de produto.<br /><br /> Sugerir produtos adicionais a um cliente para compra.<br /><br /> Analisar dados de pesquisa de visitantes para um evento, encontrar quais atividades estão correlacionadas, planejar atividades futuras.|[Algoritmo Associação da Microsoft](../../analysis-services/data-mining/microsoft-association-algorithm.md)<br /><br /> [Algoritmo Árvores de Decisão da Microsoft](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)|  
|**Localizando grupos de itens semelhantes:**<br /><br /> Criar grupos de perfis de risco de paciente em atributos como demografia e comportamentos.<br /><br /> Analisar usuários por padrões de navegação e compra.<br /><br /> Identificar servidores que têm características de uso semelhantes.|[Algoritmo Microsoft Clustering](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)<br /><br /> [Algoritmo Microsoft Sequence Clustering](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
 A tabela a seguir fornece links para recursos de aprendizado para cada algoritmo de mineração de dados fornecido no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining:  
  
|||  
|-|-|  
|**Descrição básica do algoritmo**|Explica o que o algoritmo faz e como funciona, e descreve possíveis cenários comerciais onde o algoritmo poderia ser útil.|  
||[Algoritmo Associação da Microsoft](../../analysis-services/data-mining/microsoft-association-algorithm.md)<br /><br /> [Algoritmo Microsoft Clustering](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)<br /><br /> [Algoritmo Árvores de Decisão da Microsoft](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)<br /><br /> [Algoritmo Regressão Linear da Microsoft](../../analysis-services/data-mining/microsoft-linear-regression-algorithm.md)<br /><br /> [Algoritmo Regressão Logística da Microsoft](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)<br /><br /> [Referência técnica do algoritmo Naive Bayes da Microsoft](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)<br /><br /> [Algoritmo Rede Neural da Microsoft](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)<br /><br /> [Algoritmo Microsoft Sequence Clustering](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)<br /><br /> [Algoritmo MTS](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)|  
|**Referência técnica**|Fornece detalhes técnicos sobre a implementação do algoritmo, com referências acadêmicas conforme o necessário. Lista os parâmetros que podem ser definidos para controlar o comportamento do algoritmo e personalizar os resultados no modelo. Descreve os requisitos de dados e fornece dicas de desempenho se possível.|  
||[Referência técnica do algoritmo de associação da Microsoft](../../analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md)<br /><br /> [Referência técnica do algoritmo Microsoft Clustering](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md)<br /><br /> [Referência técnica do algoritmo Árvores de Decisão da Microsoft](../../analysis-services/data-mining/microsoft-decision-trees-algorithm-technical-reference.md)<br /><br /> [Referência Técnica do Algoritmo de Regressão Linear da Microsoft](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md)<br /><br /> [Referência técnica do algoritmo Regressão Logística da Microsoft](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)<br /><br /> [Referência técnica do algoritmo Microsoft Naive Bayes](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm-technical-reference.md)<br /><br /> [Referência técnica do algoritmo Rede Neural da Microsoft](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)<br /><br /> [Referência técnica do algoritmo Microsoft Sequence Clustering](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)<br /><br /> [Referência técnica do algoritmo Microsoft Time Series](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)|  
|**Conteúdo do modelo**|Explica como as informações são estruturadas dentro de cada tipo de modelo de mineração de dados, e explica como interpretar as informações armazenadas em cada um dos nós.|  
||[Conteúdo do modelo de mineração para modelos de associação &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)<br /><br /> [Conteúdo do modelo de mineração para modelos de clustering &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md)<br /><br /> [Conteúdo do modelo de mineração para modelos de árvore de decisão &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)<br /><br /> [Conteúdo do modelo de mineração para modelos de regressão linear &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)<br /><br /> [Conteúdo do modelo de mineração para modelos de regressão logística &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)<br /><br /> [Conteúdo do modelo de mineração para modelos Naive Bayes &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)<br /><br /> [Conteúdo do modelo de mineração para modelos de rede neural &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)<br /><br /> [Conteúdo do modelo de mineração para modelos de clustering de sequência &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)<br /><br /> [Conteúdo do modelo de mineração para modelos de série temporal &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)|  
|**Consultas de mineração de dados**|Fornece diversas consultas que você pode usar com cada tipo modelo. Os exemplos incluem consultas de conteúdo que permitem que você saiba mais sobre os padrões no modelo e consultas de previsão que o ajudarão a criar previsões com base nesses padrões.|  
||[Exemplos de consulta de um modelo de associação](../../analysis-services/data-mining/association-model-query-examples.md)<br /><br /> [Exemplos de consulta de modelo de clustering](../../analysis-services/data-mining/clustering-model-query-examples.md)<br /><br /> [Exemplos de consulta de modelo de árvores de decisão](../../analysis-services/data-mining/decision-trees-model-query-examples.md)<br /><br /> [Exemplos de consulta de modelo de regressão linear](../../analysis-services/data-mining/linear-regression-model-query-examples.md)<br /><br /> [Exemplos de consulta de modelo de regressão logística](../../analysis-services/data-mining/logistic-regression-model-query-examples.md)<br /><br /> [Exemplos de consulta do modelo Naive Bayes](../../analysis-services/data-mining/naive-bayes-model-query-examples.md)<br /><br /> [Exemplos de consulta de modelos de rede neural](../../analysis-services/data-mining/neural-network-model-query-examples.md)<br /><br /> [Exemplos de consulta dos modelos de clustering de sequências](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)<br /><br /> [Exemplos de consulta de um modelo de série temporal](../../analysis-services/data-mining/time-series-model-query-examples.md)|  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|**Tópico**|**Descrição**|  
|---------------|---------------------|  
|Determinar o algoritmo usado por um modelo de mineração de dados|[Consultar os parâmetros usados para criar um modelo de mineração](../../analysis-services/data-mining/query-the-parameters-used-to-create-a-mining-model.md)|  
|Criar um algoritmo de plug-in personalizado|[Algoritmos de plug-in](../../analysis-services/data-mining/plugin-algorithms.md)|  
|Explorar um modelo usando um visualizador específico de algoritmo|[Visualizadores do modelo de Mineração de dados](../../analysis-services/data-mining/data-mining-model-viewers.md)|  
|Exibir o conteúdo de um modelo usando um formato de tabela genérico|[Procurar um modelo usando o Visualizador de Árvore de Conteúdo Genérica da Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)|  
|Aprender sobre como configurar seus dados e usar algoritmos para criar modelos|[Estruturas de Mineração &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)<br /><br /> [Modelos de mineração &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas de mineração de dados](../../analysis-services/data-mining/data-mining-tools.md)  
  
  
