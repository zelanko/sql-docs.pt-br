---
title: Algoritmo msc | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 273d1271d63ae8f4d40d604745cbe8c3f5eda6ee
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="microsoft-sequence-clustering-algorithm"></a>Algoritmo MSC
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  O algoritmo de Clustering de Sequência do [!INCLUDE[msCoName](../../includes/msconame-md.md)] é um algoritmo exclusivo que combina a análise de sequência com o cluster. Você pode usá-lo para explorar dados que contêm eventos que podem ser vinculados em uma *sequência*. O algoritmo localiza as sequências mais comuns e realiza clustering para encontrar sequências que são similares. Os exemplos a seguir ilustram os tipos de sequências das quais você pode capturar dados de aprendizado de máquina para fornecer informações sobre problemas comuns ou cenários comerciais:  
  
-   Fluxos ou caminhos de cliques gerados quando os usuários navegam em um site  
  
-   Logs que listam eventos que precedem um incidente, como falha de disco rígido ou deadlock de servidor  
  
-   Os registros de transação que descrevem a ordem em que um cliente adiciona itens a um carrinho de compras online  
  
-   Registros que seguem interações de cliente (ou paciente) com o passar do tempo, para prever cancelamentos de serviço ou outros resultados insatisfatórios  
  
 Sob vários aspectos, esse algoritmo é semelhante ao algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering. No entanto, em vez de localizar clusters de casos que contêm atributos semelhantes, o algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering localiza clusters de casos que contêm caminhos semelhantes em uma sequência.  
  
## <a name="example"></a>Exemplo  
 O site do [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] coleta informações sobre as páginas visitadas pelos usuários e sobre a ordem em que são visitadas. Como a empresa oferece a funcionalidade de encomendas online, os clientes devem fazer logon no site. Dessa maneira, a empresa obtém informações de clique relativas a cada perfil de cliente. Usando o algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering nesses dados, a empresa pode localizar grupos, ou clusters, de clientes que têm padrões ou sequências de clique semelhantes. A empresa então poderá usar esses clusters para analisar como os usuários navegam pelo site, identificar quais páginas estão mais intrinsecamente relacionadas à venda de um determinado produto e prever que páginas terão maiores probabilidades de acesso nas próximas visitas.  
  
## <a name="how-the-algorithm-works"></a>Como o algoritmo funciona  
 O [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering é um algoritmo híbrido que combina técnicas de clustering com a análise de cadeia Markov para identificar clusters e suas sequências.  Uma das marcas registradas do algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering é que ele usa dados de sequência. Esses dados normalmente representam uma série de eventos ou transições entre estados em um conjunto de dados, como uma série de compras de produtos ou cliques de um usuário específico. O algoritmo examina todas as probabilidades de transição e avalia as diferenças, ou distâncias, entre todas as sequências possíveis no conjunto de dados para determinar quais são as melhores sequências a usar como entradas para clustering. Depois que o algoritmo cria a lista de sequências candidatas, ele usa as informações das sequências como entrada para clustering usando EM (Maximização de expectativa).  
  
 Para obter uma descrição detalhada da implementação, consulte [Referência técnica do Algoritmo MSC](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md).  
  
## <a name="data-required-for-sequence-clustering-models"></a>Dados necessários para modelos de cluster de sequência  
 Quando você prepara dados para uso no treinamento de um modelo de clustering de sequência, é preciso conhecer os requisitos de um determinado algoritmo, inclusive a quantidade de dados necessários e como eles são usados.  
  
 Os requisitos de um modelo de clustering de sequência são os seguintes:  
  
-   **Uma única coluna chave** Um modelo de clustering de sequência requer uma chave que identifique registros.  
  
-   **Uma coluna de sequência** Para dados de sequência, o modelo deve ter uma tabela aninhada que contém uma coluna de ID de sequência. A ID de sequência pode ser qualquer tipo de dados classificável. Por exemplo, você pode usar um identificador de página da Web, um número inteiro ou uma cadeia de caracteres de texto, desde que a coluna identifique os eventos em uma sequência. Só é permitido um identificador de sequência para cada sequência, e cada modelo pode ter apenas um tipo de sequência.  
  
-   **Atributos não sequenciais opcionais** O algoritmo dá suporte à adição de outros atributos não relacionados a sequenciamento. Esses atributos podem incluir colunas aninhadas.  
  
 No exemplo do site do [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] , citado anteriormente, um modelo de clustering de sequências pode incluir informações de pedidos como a tabela de casos, dados demográficos do cliente específico de cada pedido como atributos não sequenciais e uma tabela aninhada contendo a sequência em que o cliente navegou pelo site ou colocou itens em um carrinho de compras como as informações de sequência.  
  
 Para obter informações mais detalhadas sobre os tipos de conteúdo e de dados com suporte pelos modelos de sequence clustering, consulte a seção Requisitos de [Referência técnica do algoritmo MSC](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md).  
  
## <a name="viewing-a-sequence-clustering-model"></a>Exibindo um modelo de cluster de sequências  
 O modelo de mineração criado por esse algoritmo contém descrições das sequências mais comuns nos dados. Para explorar o modelo, você pode usar o **Visualizador de Cluster de Sequência da Microsoft**. Quando você exibe um modelo de clustering de sequências, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mostra clusters que contêm várias transições. Também é possível exibir as estatísticas pertinentes. Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Cluster de Sequência da Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md).  
  
 Para obter mais detalhes, você pode navegar pelo modelo no [Visualizador de Árvore de Conteúdo Genérica da Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md). O conteúdo armazenado do modelo inclui a distribuição de todos os valores de cada nó, a probabilidade de cada cluster e detalhes sobre as transições. Para obter mais informações, consulte [Conteúdo do modelo de mineração para modelos de clustering de sequência &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md).  
  
## <a name="creating-predictions"></a>Criando previsões  
 Após o treinamento do modelo, os resultados são armazenados como um conjunto de padrões. Você pode usar as descrições das sequências mais comuns nos dados para prever a próxima etapa provável de uma nova sequência. Todavia, como o algoritmo inclui outras colunas, você pode usar o modelo resultante para identificar as relações entre os dados sequenciados e as entradas não sequenciais. Por exemplo, se você acrescentar dados demográficos ao modelo, poderá fazer previsões sobre grupos de clientes específicos. As consultas de previsão podem ser personalizadas para retornar um número variável de previsões ou para retornar estatísticas descritivas.  
  
 Para obter informações sobre como criar consultas com base em um modelo de mineração de dados, consulte [Consultas de mineração de dados](../../analysis-services/data-mining/data-mining-queries.md). Para obter exemplos de como usar consultas com um modelo de sequence clustering, consulte [Exemplos de consulta de modelo de sequence clustering](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md).  
  
## <a name="remarks"></a>Comentários  
  
-   Não dá suporte ao uso de PMML para criar modelos de mineração.  
  
-   Dá suporte ao detalhamento.  
  
-   Dá suporte ao uso de modelos de mineração OLAP e à criação de dimensões de mineração de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados e &#40; Analysis Services – Data Mining e &#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Referência técnica do algoritmo msc](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)   
 [Exemplos de consulta de modelo de Clustering de sequência](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)   
 [Procurar um modelo usando o Visualizador de Cluster de sequência da Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
  
