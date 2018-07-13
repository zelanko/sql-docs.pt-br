---
title: Criar um modelo de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data mining models, creating
- forecasting [data mining]
- mining models, creating
- clustering [data mining]
- association [data mining]
- data modeling [data mining]
- estimation
- classification [data mining]
ms.assetid: 804b7db3-1f6a-4f73-a81d-bbe02520d7c6
caps.latest.revision: 16
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c2bb6c2b6ada95816cc45288c68bc784eb0ef2a0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37239916"
---
# <a name="creating-a-data-mining-model"></a>Criando um modelo de mineração de dados
  Modelagem de dados é a etapa de mineração de dados em que você cria padrões e tendências, aplicando *algoritmos* aos dados. Posteriormente, você poderá usar esses padrões para análise ou para fazer previsões.  
  
 Os Suplementos de Mineração de Dados para Office oferecem suporte a mineração de dados por meio de assistentes que facilitam a criação de modelos. Os assistentes analisam os dados, identificam correlações, calculam o significado estatístico de todas as variáveis e selecionam automaticamente o melhor modelo.  
  
 Embora essa funcionalidade seja tão avançada como as ferramentas fornecidas de mineração de dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], a combinação de assistentes e a interface familiar do Excel torna fácil criar, modificar e usar a mineração de dados.  
  
## <a name="advanced-data-mining"></a>Avançados (mineração de dados)  
 Os assistentes avançados permitem que você crie novos modelos de mineração de dados, com base nos dados armazenados no Excel, usando um dos algoritmos de mineração de dados no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
### <a name="create-mining-structure"></a>Criar a Estrutura de Mineração  
 O Assistente para Criar Estrutura de Mineração o ajuda a criar uma nova estrutura de mineração de dados, que você pode usar como a base para vários modelos de mineração. O assistente lhe oferece a opção de separar parte dos dados para usar como um conjunto de testes, para que você possa avaliar todos os modelos que utilizam os mesmos dados de acordo com um padrão de teste consistente.  
  
 [Criar estrutura de mineração &#40;suplementos de mineração de dados do SQL Server&#41;](create-mining-structure-sql-server-data-mining-add-ins.md)  
  
### <a name="add-model-to-structure"></a>Adicionar modelo à estrutura  
 O assistente para Adicionar Modelo à Estrutura lhe permite escolher uma estrutura de mineração de dados existente e criar um novo modelo de mineração de dados para ela. Você pode adicionar vários modelos de mineração a uma estrutura, alterar os parâmetros ou escolher algoritmos de mineração de dados diferentes e personalizar a saída.  
  
 [Adicionar modelo à estrutura &#40;Data Mining Add-ins para Excel&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md)  
  
## <a name="analyze-key-influencers-analyze"></a>Analisar os Influenciadores Principais (Analisar)  
 Você escolhe uma coluna ou um valor de saída e então o algoritmo analisa todos os dados de saída para identificar os fatores com mais influência no destino. Opcionalmente, você pode criar um relatório que compara quaisquer dois valores, de forma que você possa ver como os influenciadores são alterados.  
  
 O **analisar os influenciadores principais** ferramenta usa o algoritmo Microsoft Naïve Bayes.  
  
 [Analisar os influenciadores principais &#40;ferramentas de análise de tabela para Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
  
## <a name="associate-data-mining"></a>Associação (mineração de dados)  
 O **associar** assistente cria um modelo de associação que detecta associações entre os itens que aparecem em várias transações: por exemplo, na análise de cesta de compras.  
  
 [Assistente para associação &#40;cliente de mineração de dados para Excel&#41;](associate-wizard-data-mining-client-for-excel.md)  
  
## <a name="classify-data-mining"></a>Classificar (mineração de dados)  
 O **classificar** assistente cria um modelo de classificação que analisa os fatores que contribuíram para um resultado de destino. Você pode usar vários algoritmos com este assistente, incluindo Árvores de Decisão, Naïve Bayes e Redes Neurais.  
  
 [Assistente para classificar &#40;Data Mining Add-ins para Excel&#41;](classify-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="cluster-data-mining"></a>Cluster (mineração de dados)  
 O **Cluster** assistente cria um modelo de clustering que detecta grupos de linhas que compartilham características semelhantes. Clustering (às vezes chamado de *segmentação*) é uma técnica de aprendizado sem supervisão é muito útil ao tentar entender os padrões e agrupamentos em dados novos.  
  
 O algoritmo Clustering da Microsoft dá suporte a diversas variedades do clustering K-means e de Maximização de expectativa (EM).  
  
 [Assistente de cluster &#40;Data Mining Add-ins para Excel&#41;](cluster-wizard-data-mining-add-ins-for-excel.md).  
  
## <a name="detect-categories-analyze"></a>Detectar categorias (Analisar)  
 O **detectar categorias** ferramenta permite que você adicione qualquer conjunto de dados e aplique clustering para localizar agrupamentos de dados. É útil para encontrar semelhanças e para criar grupos para mais análise.  
  
 O **detectar categorias** ferramenta usa o algoritmo Microsoft Clustering.  
  
 [Detectar categorias &#40;ferramentas de análise de tabela para Excel&#41;](detect-categories-table-analysis-tools-for-excel.md)  
  
## <a name="estimate-data-mining"></a>Estimar (mineração de dados)  
 O assistente para Estimar cria um modelo de estimativa que extrai padrões de dados e usa esses padrões para prever valores numéricos contínuos, de data ou de hora. Usa o algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
 [Assistente de estimativa &#40;Data Mining Add-ins para Excel&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="fill-from-example-analyze"></a>Preencher com Base no Exemplo (Analisar)  
 O **preencher do exemplo** ferramenta o ajuda a imputar valores ausentes. Você fornece alguns exemplos de como deverão ser os valores ausentes e a ferramenta cria padrões com base em todos os dados da tabela, e então recomenda novos valores com base em padrões dos dados.  
  
 O **preencher do exemplo** ferramenta usa o algoritmo de regressão logística da Microsoft.  
  
 [Preencher com base no exemplo &#40;ferramentas de análise de tabela para Excel&#41;](fill-from-example-table-analysis-tools-for-excel.md)  
  
## <a name="forecast-analyze"></a>Previsão (Analisar)  
 O **previsão** ferramenta usa dados que são alterados ao longo do tempo e prevê valores futuros.  
  
 O **previsão** ferramenta usa o algoritmo Microsoft Time Series.  
  
 [Previsão &#40;ferramentas de análise de tabela para Excel&#41;](forecast-table-analysis-tools-for-excel.md)  
  
## <a name="forecast-data-mining"></a>Previsão (mineração de dados)  
 O **previsão** assistente cria um modelo de previsão que detecta padrões em uma série de células e depois prevê valores adicionais.  
  
 [Assistente de previsão &#40;Data Mining Add-ins para Excel&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="highlight-exceptions-analyze"></a>Realçar Exceções (Analisar)  
 O **realçar exceções** ferramenta analisa padrões em uma tabela de dados e localiza linhas e valores que não se ajustam ao padrão. Então, você poderá examiná-los e corrigi-los e executar o modelo novamente, ou sinalizar valores para ação posterior.  
  
 O **realçar exceções** ferramenta usa o algoritmo Microsoft Clustering.  
  
 [Realçar exceções &#40;ferramentas de análise de tabela para Excel&#41;](highlight-exceptions-table-analysis-tools-for-excel.md)  
  
## <a name="prediction-calculator-analyze"></a>Cálculo de Previsão (Analisar)  
 Essa ferramenta cria um modelo que analisa os fatores que levam a resultados de destino e então prevê um resultado para qualquer nova entrada, com base em critérios derivados desses padrões. Também gera uma planilha de tomada de decisão interativa que permite a você a criar pontuação de novas entradas com facilidade. Você também pode criar uma versão impressa da planilha de pontuação para uso offline.  
  
 O **cálculo de previsão** ferramenta usa o algoritmo de regressão logística da Microsoft.  
  
 [Cálculo de previsão &#40;ferramentas de análise de tabela para Excel&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
  
## <a name="scenario-goal-seek-analyze"></a>Cenário: Metas a Atingir (Analisar)  
 No **meta a atingir** ferramenta, você especifica um valor de destino e a ferramenta identificará os fatores subjacentes que devem ser alterados para alcançar a meta. Por exemplo, se você sabe que deve aumentar a satisfação da chamada em 20%, poderá solicitar ao modelo que preveja os fatores que devem mudar para que essa meta seja produzida.  
  
 O **meta a atingir** ferramenta usa o algoritmo de regressão logística da Microsoft.  
  
 detalhes  
  
 [Cenário de metas a atingir &#40;ferramentas de análise de tabela para Excel&#41;](goal-seek-scenario-table-analysis-tools-for-excel.md)  
  
## <a name="scenario-what-if-scenario-analyze"></a>Cenário: cenário E-Se (Analisar)  
 O **hipóteses** ferramenta complementa o **meta a atingir** ferramenta. Com essa ferramenta, você inseriu o valor que deseja alterar, e o modelo prevê se essa alteração será suficiente para obtenção do resultado desejado. Por exemplo, você poderia perguntar ao modelo para inferir se a adição de um operador de chamada extra poderia aumentar a satisfação do cliente em um ponto.  
  
 O **hipotética** ferramenta usa o algoritmo de regressão logística da Microsoft.  
  
 [Cenário e-se &#40;ferramentas de análise de tabela para Excel&#41;](what-if-scenario-table-analysis-tools-for-excel.md)  
  
## <a name="shopping-basket-analysis-analyze"></a>Análise da Cesta de Compras (Analisar)  
 O **análise da cesta de compras** ferramenta cria grupos de produtos frequentemente adquiridos juntos, para identificar padrões que podem ser usados na venda cruzada ou especial. Também gera relatórios com base no preço e no custo de pacotes de produto relacionados, para auxiliar a tomada de decisão.  
  
 Você também pode usar essa ferramenta para eventos que ocorrem juntos com frequência, fatores que levam a um diagnóstico ou qualquer outro conjunto de causas e resultados potenciais.  
  
 O **análise da cesta de compras** ferramenta usa o algoritmo Microsoft Association.  
  
 [Análise da cesta de compras &#40;ferramentas de análise de tabela para Excel&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)  
  
## <a name="see-also"></a>Consulte também  
 [Explorando e limpando dados](exploring-and-cleaning-data.md)   
 [Validando modelos e usando modelos para previsão &#40;Data Mining Add-ins para Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [Implantando e dimensionando modelos de mineração &#40;Data Mining Add-ins para Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
