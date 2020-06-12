---
title: Criando um modelo de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
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
author: minewiskan
ms.author: owend
ms.openlocfilehash: cce03fab2757b366fbe67dc6c68cb3be1c075e3c
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84526422"
---
# <a name="creating-a-data-mining-model"></a>Criando um modelo de mineração de dados
  A modelagem de dados é a etapa de Data Mining em que você cria padrões e tendências aplicando *algoritmos* aos dados. Posteriormente, você poderá usar esses padrões para análise ou para fazer previsões.  
  
 Os Suplementos de Mineração de Dados para Office oferecem suporte a mineração de dados por meio de assistentes que facilitam a criação de modelos. Os assistentes analisam os dados, identificam correlações, calculam o significado estatístico de todas as variáveis e selecionam automaticamente o melhor modelo.  
  
 Embora essa funcionalidade seja cada vez mais potente que as ferramentas de Data Mining fornecidas pelo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] , a combinação de assistentes e a interface familiar do Excel facilita a criação, a modificação e o uso de data mining.  
  
## <a name="advanced-data-mining"></a>Avançados (mineração de dados)  
 Os assistentes avançados permitem criar novos modelos de Data Mining, com base nos dados armazenados no Excel, usando um dos algoritmos de Data Mining no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
### <a name="create-mining-structure"></a>Criar a Estrutura de Mineração  
 O Assistente para Criar Estrutura de Mineração o ajuda a criar uma nova estrutura de mineração de dados, que você pode usar como a base para vários modelos de mineração. O assistente lhe oferece a opção de separar parte dos dados para usar como um conjunto de testes, para que você possa avaliar todos os modelos que utilizam os mesmos dados de acordo com um padrão de teste consistente.  
  
 [Crie &#40;de estrutura de mineração SQL Server suplementos de mineração de dados&#41;](create-mining-structure-sql-server-data-mining-add-ins.md)  
  
### <a name="add-model-to-structure"></a>Adicionar modelo à estrutura  
 O assistente para Adicionar Modelo à Estrutura lhe permite escolher uma estrutura de mineração de dados existente e criar um novo modelo de mineração de dados para ela. Você pode adicionar vários modelos de mineração a uma estrutura, alterar os parâmetros ou escolher algoritmos de mineração de dados diferentes e personalizar a saída.  
  
 [Adicionar modelo à estrutura &#40;suplementos de mineração de dados para Excel&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md)  
  
## <a name="analyze-key-influencers-analyze"></a>Analisar os Influenciadores Principais (Analisar)  
 Você escolhe uma coluna ou um valor de saída e então o algoritmo analisa todos os dados de saída para identificar os fatores com mais influência no destino. Opcionalmente, você pode criar um relatório que compara quaisquer dois valores, de forma que você possa ver como os influenciadores são alterados.  
  
 A ferramenta **analisar influenciadores principais** usa o algoritmo Bayes simples da Microsoft.  
  
 [Analisar os influenciadores principais &#40;ferramentas de análise de tabela para Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
  
## <a name="associate-data-mining"></a>Associação (mineração de dados)  
 O assistente para **associar** cria um modelo de associação que detecta associações entre itens que aparecem em várias transações: por exemplo, na análise de cesta de mercado.  
  
 [Assistente para associar &#40;cliente de mineração de dados para Excel&#41;](associate-wizard-data-mining-client-for-excel.md)  
  
## <a name="classify-data-mining"></a>Classificar (mineração de dados)  
 O **Assistente de classificação cria** um modelo de classificação que analisa os fatores que contribuíram para um resultado de destino. Você pode usar vários algoritmos com este assistente, incluindo Árvores de Decisão, Naïve Bayes e Redes Neurais.  
  
 [Assistente de classificação &#40;suplementos de mineração de dados para Excel&#41;](classify-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="cluster-data-mining"></a>Cluster (mineração de dados)  
 O assistente de **cluster** cria um modelo de clustering que detecta grupos de linhas que compartilham características semelhantes. O clustering (às vezes chamado de *segmentação*) é uma técnica de aprendizado não supervisionada que é muito útil ao tentar entender os padrões e agrupamentos em novos dados.  
  
 O algoritmo Clustering da Microsoft dá suporte a diversas variedades do clustering K-means e de Maximização de expectativa (EM).  
  
 O [Assistente de Cluster &#40;suplementos de mineração de dados para&#41;do Excel ](cluster-wizard-data-mining-add-ins-for-excel.md).  
  
## <a name="detect-categories-analyze"></a>Detectar categorias (Analisar)  
 A ferramenta **detectar categorias** permite que você adicione qualquer conjunto de dados e aplique clustering para localizar agrupamentos de dados. É útil para encontrar semelhanças e para criar grupos para analisar ainda mais.  
  
 A ferramenta **detectar categorias** usa o algoritmo Microsoft Clustering.  
  
 [Detectar categorias &#40;ferramentas de análise de tabela para Excel&#41;](detect-categories-table-analysis-tools-for-excel.md)  
  
## <a name="estimate-data-mining"></a>Estimar (mineração de dados)  
 O assistente para Estimar cria um modelo de estimativa que extrai padrões de dados e usa esses padrões para prever valores numéricos contínuos, de data ou de hora. Usa o algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
 [Assistente de estimativa &#40;suplementos de mineração de dados para Excel&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="fill-from-example-analyze"></a>Preencher com Base no Exemplo (Analisar)  
 A ferramenta **preencher de exemplo** ajuda a imputar valores ausentes. Você fornece alguns exemplos de como deverão ser os valores ausentes e a ferramenta cria padrões com base em todos os dados da tabela, e então recomenda novos valores com base em padrões dos dados.  
  
 A ferramenta **preencher com exemplo** usa o algoritmo regressão logística da Microsoft.  
  
 [Preencha com o exemplo &#40;ferramentas de análise de tabela para Excel&#41;](fill-from-example-table-analysis-tools-for-excel.md)  
  
## <a name="forecast-analyze"></a>Previsão (Analisar)  
 A ferramenta de **previsão** usa dados que mudam ao longo do tempo e prevê valores futuros.  
  
 A ferramenta de **previsão** usa o algoritmo Microsoft Time Series.  
  
 [Previsão de &#40;ferramentas de análise de tabela para Excel&#41;](forecast-table-analysis-tools-for-excel.md)  
  
## <a name="forecast-data-mining"></a>Previsão (mineração de dados)  
 O assistente de **previsão** cria um modelo de previsão que detecta padrões em uma série de células e, em seguida, prevê valores adicionais.  
  
 [Assistente de previsão &#40;suplementos de mineração de dados para Excel&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="highlight-exceptions-analyze"></a>Realçar Exceções (Analisar)  
 A ferramenta **realçar exceções** analisa os padrões em uma tabela de dados e localiza linhas e valores que não se ajustam ao padrão. Então, você poderá examiná-los e corrigi-los e executar o modelo novamente, ou sinalizar valores para ação posterior.  
  
 A ferramenta **realçar exceções** usa o algoritmo Microsoft Clustering.  
  
 [Realçar exceções &#40;ferramentas de análise de tabela para Excel&#41;](highlight-exceptions-table-analysis-tools-for-excel.md)  
  
## <a name="prediction-calculator-analyze"></a>Cálculo de Previsão (Analisar)  
 Essa ferramenta cria um modelo que analisa os fatores que levam a resultados de destino e então prevê um resultado para qualquer nova entrada, com base em critérios derivados desses padrões. Também gera uma planilha de tomada de decisão interativa que permite a você a criar pontuação de novas entradas com facilidade. Você também pode criar uma versão impressa da planilha de pontuação para uso offline.  
  
 A ferramenta de **cálculo de previsão** usa o algoritmo regressão logística da Microsoft.  
  
 [Cálculo de Previsão &#40;ferramentas de análise de tabela para Excel&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
  
## <a name="scenario-goal-seek-analyze"></a>Cenário: Metas a Atingir (Analisar)  
 Na ferramenta **meta Seek** , você especifica um valor de destino e a ferramenta identifica os fatores subjacentes que devem ser alterados para atender a esse destino. Por exemplo, se você sabe que deve aumentar a satisfação da chamada em 20%, poderá solicitar ao modelo que preveja os fatores que devem mudar para que essa meta seja produzida.  
  
 A ferramenta **meta Seek** usa o algoritmo regressão logística da Microsoft.  
  
 detalhes  
  
 [Cenário de busca de meta &#40;ferramentas de análise de tabela para Excel&#41;](goal-seek-scenario-table-analysis-tools-for-excel.md)  
  
## <a name="scenario-what-if-scenario-analyze"></a>Cenário: cenário E-Se (Analisar)  
 A ferramenta de **análise** de hipóteses complementa a ferramenta de **meta Seek** . Com essa ferramenta, você inseriu o valor que deseja alterar, e o modelo prevê se essa alteração será suficiente para obtenção do resultado desejado. Por exemplo, você poderia perguntar ao modelo para inferir se a adição de um operador de chamada extra poderia aumentar a satisfação do cliente em um ponto.  
  
 A ferramenta **What-If** usa o algoritmo de regressão logística da Microsoft.  
  
 [Cenário de hipóteses &#40;ferramentas de análise de tabela para Excel&#41;](what-if-scenario-table-analysis-tools-for-excel.md)  
  
## <a name="shopping-basket-analysis-analyze"></a>Análise da Cesta de Compras (Analisar)  
 A ferramenta de **análise de cesta de compras** cria grupos de produtos que são frequentemente comprados juntos, para identificar padrões que podem ser usados na venda cruzada ou venda vertical. Também gera relatórios com base no preço e no custo de pacotes de produto relacionados, para auxiliar a tomada de decisão.  
  
 Você também pode usar essa ferramenta para eventos que ocorrem juntos com frequência, fatores que levam a um diagnóstico ou qualquer outro conjunto de causas e resultados potenciais.  
  
 A ferramenta de **análise de cesta de compras** usa o algoritmo de associação da Microsoft.  
  
 [Análise de cesta de compras &#40;tabela AnalysisTools para Excel&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Explorando e limpando dados](exploring-and-cleaning-data.md)   
 [Validando modelos e usando modelos para previsão &#40;suplementos de mineração de dados para Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [Implantando e dimensionando modelos de mineração &#40;suplementos de mineração de dados para Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
