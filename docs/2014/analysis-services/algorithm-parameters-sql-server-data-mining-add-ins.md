---
title: Parâmetros de algoritmo (SQL Server Data Mining Add-ins) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- MAXIMUM_STATES
- FORCED_REGRESSOR
- PERIODICITY_HINT
- HOLDOUT_SEED
- MAXIMUM_ITEMSET_SIZE
- HIDDEN_NODE_RATIO
- CLUSTERING_METHOD
- FORECAST_METHOD
- STOPPING_TOLERANCE
- MISSING_VALUE_SUBSTITUTION
- MINIMUM_IMPORTANCE
- HISTORIC_MODEL_COUNT
- SPLIT_METHOD
- MAXIMUM_OUTPUT_ATTRIBUTES
- HOLDOUT_PERCENTAGE
- MINIMUM_PROBABILITY
- SAMPLE_SIZE
- HISTORICAL_MODEL_GAP
- CLUSTER_SEED
- SCORE_METHOD
- INSTABILITY_SENSITIVITY
- AUTO_DETECT_PERIODICITY
- MAXIMUM_SEQUENCE_STATES
- MINIMUM_DEPENDENCY_PROBABILITY
- MINIMUM_SUPPORT
- MAXIMUM_SUPPORT
- MINIMUM_ITEMSET_SIZE
- PREDICTION_SMOOTHING
- algorithm parameters
- MAXIMUM_SERIES_VALUE
- MODELLING_CARDINALITY
- MAXIMUM_INPUT_ATTRIBUTES
- MINIMUM_SERIES_VALUE
- MAXIMUM_ITEMSET_COUNT
- CLUSTER_COUNT
- COMPLEXITY_PENALTY
ms.assetid: fcdc3f85-813d-4279-90b0-16e26edd008d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e902272c58f1e841a3108199e53d51ac12f8ae4a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062595"
---
# <a name="algorithm-parameters-sql-server-data-mining-add-ins"></a>Parâmetros do Algoritmo (Suplementos de Mineração de Dados do SQL Server)
  Quando você executa mineração de dados usando as Ferramentas de Análise de Tabela para Excel, não precisa configurar o algoritmo ou os parâmetros de mineração de dados; cada ferramenta analisa os dados e seleciona automaticamente os parâmetros ideais. No entanto, se desejar modificar o modelo, ou criar um modelo de mineração do zero, o Cliente de Mineração de Dados para Excel oferece várias opções de personalização.  
  
-   Criar um modelo de mineração de dados manualmente, clicando em **Advanced** e, em seguida, clicando em **Adicionar modelo à estrutura**.  
  
-   Use qualquer um dos assistentes de modelagem no cliente de mineração de dados e, em seguida, clique em **parâmetros** para controlar o comportamento do [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmos de mineração de dados.  
  
-   Clique em **consulta** para abrir o Assistente de modelo de consulta e, em seguida, clique em **avançado** para abrir o **dados Editor avançada de mineração consulta**. Nesse editor, você pode criar modelos usando modelos DMX.  
  
 Também é possível modificar o comportamento dos modelos de mineração já criados ou você pode filtrar os resultados, definindo parâmetros no visualizador de modelo de mineração.  
  
## <a name="list-of-algorithm-parameters"></a>Lista de parâmetros de algoritmo  
 Todos os algoritmos da [!INCLUDE[msCoName](../includes/msconame-md.md)] podem ser personalizados com a configuração de parâmetros. Como as melhores configurações de parâmetro dependem da composição dos dados, uma explicação completa dos efeitos da alteração dos parâmetros está além do escopo deste tópico.  
  
 A tabela a seguir lista os parâmetros, descreve sua funcionalidade e fornece links para mais informações técnicas.  
  
|Nome do parâmetro|Usado em|Descrição|  
|--------------------|-------------|-----------------|  
|AUTO_DETECT_PERIODICITY|Algoritmo MTS|Especifica um valor numérico entre 0 e 1 usado para detectar periodicidade. Definir esse valor mais próximo a 1 favorece a descoberta de vários padrões quase periódicos e a geração automática de dicas de periodicidade. Lidar com muitas dicas de periodicidade provavelmente resultará em tempo de treinamento de modelos significativamente maior, mas também em modelos mais precisos. Se o valor for mais próximo a 0, a periodicidade será detectada somente para dados fortemente periódicos.<br /><br /> O padrão é 0.6.|  
|CLUSTER_COUNT|Algoritmo Microsoft Clustering<br /><br /> Microsoft Sequence Clustering Algorithm|Especifica o número aproximado de clusters a serem criados pelo algoritmo. Se o número aproximado de clusters não pode ser criado a partir dos dados, o algoritmo cria o máximo de clusters possível. Quando CLUSTER_COUNT é definido como 0, o algoritmo usa heurísticos para determinar melhor o número de clusters a serem criados.<br /><br /> O padrão é 10.|  
|CLUSTER_SEED|Algoritmo Microsoft Clustering|Especifica o número de propagação usado apenas para gerar clusters aleatoriamente para o estágio inicial de criação de modelo.<br /><br /> O padrão é 0.|  
|CLUSTERING_METHOD|Algoritmo Microsoft Clustering|Especifica o método de clustering para o algoritmo a ser usado. Os seguintes métodos de clustering estão disponíveis: EM evolutivo (1), EM não evolutivo (2), K-Means evolutivo (3) e K-Means não evolutivo (4).<br /><br /> O padrão é 1.|  
|COMPLEXITY_PENALTY|Algoritmo Árvores de Decisão da Microsoft<br /><br /> Algoritmo MTS|Controla o crescimento da árvore de decisão. Um valor baixo aumenta o número de divisões e um valor alto diminui o número de divisões. O valor padrão se baseia no número de atributos de um determinado modelo, conforme descrito na lista a seguir:<br /><br /> Para os atributos 1 a 9, o padrão é 0,5.<br /><br /> Para 10 a 99 atributos, o padrão é 0,9.<br /><br /> Para 100 ou mais atributos, o padrão é 0,99.<br /><br /> Observação: Em modelos de série temporal, esse parâmetro se aplica somente a modelos criados usando o algoritmo ARTxp ou a modelos combinados.|  
|FORCED_REGRESSOR|Algoritmo Árvores de Decisão da Microsoft<br /><br /> Algoritmo Regressão Linear da Microsoft|Força o algoritmo a usar as colunas indicadas como regressores, independentemente da sua importância quando calculadas pelo algoritmo.<br /><br /> Observação: Esse parâmetro é usado apenas para árvores de decisão que preveem um atributo contínuo. Por definição, um modelo de regressão linear é um caso especial de árvores de decisão que prevê atributos comuns. No entanto, qualquer modelo de árvore de decisão pode conter um nó que representa uma fórmula de regressão linear.|  
|FORECAST_METHOD|Algoritmo MTS|Indica se as previsões devem ser feitas com o uso do algoritmo ARTxp ou ARIMA ou uma combinação de ambos.<br /><br /> O padrão é MIXED.|  
|HIDDEN_NODE_RATIO|Microsoft Neural Network Algorithm|Especifica a proporção dos neurônios ocultos com os neurônios de entrada e saída. A fórmula a seguir determina o número inicial de neurônios na camada oculta:<br /><br /> HIDDEN_NODE_RATIO * SQRT (Total de neurônios de entrada \* Total de neurônios de saída)<br /><br /> O valor padrão é 4.0.|  
|HISTORIC_MODEL_COUNT|Algoritmo MTS|Especifica o número de modelos de histórico que será criado.<br /><br /> O padrão é 1.|  
|HISTORICAL_MODEL_GAP|Algoritmo MTS|Especifica o intervalo de tempo entre dois modelos de histórico consecutivos. Por exemplo, a configuração desse valor como g resulta na criação de modelos de histórico para dados truncados por frações de tempo em intervalos de g, 2*g, 3\*g e assim por diante.<br /><br /> O padrão é 10.|  
|HOLDOUT_PERCENTAGE|Algoritmo Regressão Logística da Microsoft<br /><br /> Microsoft Neural Network Algorithm|Especifica a porcentagem de casos nos dados de treinamento que são usados para calcular o erro de dados de controle e que é utilizada como parte do critério de interrupção durante o treinamento do modelo de mineração.<br /><br /> O valor padrão é 30.<br /><br /> Observação: Este parâmetro é diferente do valor da porcentagem de controle que se aplica a uma estrutura de mineração.|  
|HOLDOUT_SEED|Algoritmo Regressão Logística da Microsoft<br /><br /> Microsoft Neural Network Algorithm|Especifica um número que é usado para semear o gerador pseudoaleatório quando o algoritmo determinar os dados de controle aleatoriamente. Se esse parâmetro for definido como 0, o algoritmo gerará a semente com base no nome do modelo de mineração, para garantir que o conteúdo do modelo permaneça o mesmo durante um novo processamento.<br /><br /> O valor padrão é 0.<br /><br /> Observação: Esse parâmetro é diferente do valor de semente de controle que se aplica a uma estrutura de mineração.|  
|INSTABILITY_SENSITIVITY|Algoritmo MTS|Controla o ponto no qual a variância de previsão excede certo limite e o algoritmo ARTxp suprime previsões. O valor padrão é 1.<br /><br /> Observação: Esse parâmetro se aplica somente a modelos combinados ou que usam o algoritmo ARTxp.|  
|MAXIMUM_INPUT_ATTRIBUTES|Algoritmo Microsoft Clustering<br /><br /> Algoritmo Árvores de Decisão da Microsoft<br /><br /> Algoritmo Regressão Linear da Microsoft<br /><br /> Algoritmo Microsoft Naïve Bayes<br /><br /> Microsoft Neural Network Algorithm<br /><br /> Algoritmo Regressão Logística da Microsoft|Define o número de atributos de entrada que o algoritmo pode manipular antes de invocar a seleção de recurso. Defina este valor como 0 para desativar a seleção de recursos.<br /><br /> O padrão é 255.|  
|MAXIMUM_ITEMSET_COUNT|Algoritmo Associação da Microsoft|Especifica o número de máximo de conjuntos de itens que será produzido. Se nenhum número for especificado, o algoritmo gerará todos os conjuntos de itens possíveis.<br /><br /> O padrão é 200000.|  
|MAXIMUM_ITEMSET_SIZE|Algoritmo Associação da Microsoft|Especifica o número máximo de itens permitidos em um conjunto de itens. Definir esse valor como 0 especifica que não há limite para o tamanho do conjunto de itens.<br /><br /> O padrão é 3.|  
|MAXIMUM_OUTPUT_ATTRIBUTES|Algoritmo Árvores de Decisão da Microsoft<br /><br /> Algoritmo Regressão Linear da Microsoft<br /><br /> Algoritmo Regressão Logística da Microsoft<br /><br /> Algoritmo Microsoft Naïve Bayes<br /><br /> Microsoft Neural Network Algorithm|Define o número de atributos de saída que o algoritmo pode manipular antes de invocar a seleção de recurso. Defina este valor como 0 para desativar a seleção de recursos.<br /><br /> O padrão é 255.|  
|MAXIMUM_SEQUENCE_STATES|Microsoft Sequence Clustering Algorithm|Especifica o número de máximo de estados que uma sequência pode ter. A definição desse valor com um número maior que 100 pode fazer com que o algoritmo crie um modelo que não fornece informações significativas.<br /><br /> O padrão é 64.|  
|MAXIMUM_SERIES_VALUE|Algoritmo MTS|Especifica o valor máximo para usar em previsões. Esse parâmetro é usado, juntamente com MINIMUM_SERIES_VALUE, para restringir as previsões a algum intervalo esperado. Por exemplo, você pode especificar que a quantidade de vendas prevista para qualquer dia nunca deve exceder o número de produtos no inventário.|  
|MAXIMUM_STATES|Algoritmo Microsoft Clustering<br /><br /> Microsoft Neural Network Algorithm<br /><br /> Microsoft Sequence Clustering Algorithm|Especifica o número máximo de estados de atributo para os quais o algoritmo dá suporte. Se o número de estados que um atributo tiver for maior que o número máximo de estados, o algoritmo usa os estados do atributo mais populares e ignorará os demais estados.<br /><br /> O padrão é 100.|  
|MAXIMUM_SUPPORT|Algoritmo Associação da Microsoft|Especifica o número máximo de casos em que um conjunto de itens pode ter suporte. Se esse valor for menor que 1, o valor representará uma porcentagem do total de casos. Se esse valor for maior do que 1, ele representará o número absoluto de casos que podem conter o conjunto de itens.<br /><br /> O padrão é 1.|  
|MINIMUM_IMPORTANCE|Algoritmo Associação da Microsoft|Especifica o limite de importância para regras de associação. As regras com menos importância do que esse valor são filtradas.|  
|MINIMUM_ITEMSET_SIZE|Algoritmo Associação da Microsoft|Especifica o número mínimo de itens permitidos em um conjunto de itens.<br /><br /> O padrão é 1.|  
|MINIMUM_DEPENDENCY_PROBABILITY|Algoritmo Microsoft Naïve Bayes|Especifica a probabilidade mínima de dependência entre os atributos de entrada e de saída. Esse valor é usado para limitar o tamanho do conteúdo gerado pelo algoritmo. Essa propriedade pode ser definida de 0 a 1. Valores maiores reduzem o número de atributos no conteúdo do modelo.<br /><br /> O padrão é 0,5.|  
|MINIMUM_PROBABILITY|Algoritmo Associação da Microsoft|Especifica a probabilidade mínima de uma regra ser verdadeira. Por exemplo, configurar este valor como 0,5 especifica que nenhuma regra com menos de 50% de probabilidade será gerada.<br /><br /> O padrão é 0,4.|  
|MINIMUM_SERIES_VALUE|Algoritmo MTS|Especifica a restrição inferior para qualquer previsão de série temporal. Os valores previstos nunca serão menores do que essa restrição.|  
|MINIMUM_SUPPORT|Algoritmo Associação da Microsoft|Especifica o número mínimo de casos que devem conter o conjunto de itens antes de o algoritmo gerar uma regra. Se você definir esse valor como menos que 1, o número mínimo de casos será especificado como uma porcentagem do total de casos. Se você definir esse valor como um número inteiro maior que 1, o número mínimo de casos será especificado como o número absoluto de casos que devem conter o conjunto de itens. O algoritmo pode aumentar automaticamente o valor desse parâmetro se houver limite de memória.<br /><br /> O padrão é 0,03.|  
|MINIMUM_SUPPORT|Algoritmo Microsoft Clustering|Especifica o número mínimo de casos em cada cluster.<br /><br /> O padrão é 1.|  
|MINIMUM_SUPPORT|Algoritmo Árvores de Decisão da Microsoft|Determina o número mínimo de casos folha necessário para gerar uma divisão na árvore de decisão.<br /><br /> O padrão é 10.|  
|MINIMUM_SUPPORT|Microsoft Sequence Clustering Algorithm|Especifica o número mínimo de casos em cada cluster.<br /><br /> O padrão é 10.|  
|MINIMUM_SUPPORT|Algoritmo MTS|Especifica o número mínimo de intervalos de tempo necessário para gerar uma divisão em cada árvore de série temporal.<br /><br /> O padrão é 10.|  
|MISSING_VALUE_SUBSTITUTION|Algoritmo MTS|Especifica o método que será usado para preencher os intervalos nos dados históricos. Por padrão, intervalos irregulares ou bordas imperfeitas não são permitidos nos dados. Os métodos a seguir podem ser usados para preencher intervalos ou bordas irregulares: use o valor anterior, o valor médio ou uma constante numérica específica.|  
|MODELLING_CARDINALITY|Algoritmo Microsoft Clustering|Especifica o número de modelos de exemplo construídos durante o processo de clustering.<br /><br /> O padrão é 10.|  
|PERIODICITY_HINT|Algoritmo MTS|Fornece uma dica para o algoritmo sobre a periodicidade dos dados. Por exemplo, se as vendas variam de acordo com o ano e a unidade de medida da série são meses, a periodicidade é 12. O parâmetro assume o formato de {n [, n]}, em que n é qualquer número positivo. O n nos colchetes [] é opcional e pode ser repetido sempre que necessário.<br /><br /> O padrão é {1}.|  
|PREDICTION_SMOOTHING|Algoritmo MTS|Controla a combinação dos algoritmos de série temporal ARTxp e ARIMA. O valor especificado somente é válido quando o parâmetro FORECAST_METHOD é definido como MIXED. Os valores devem ficar entre 0 e 1. Se o valor for 0, o modelo usará apenas ARTXP. Se o valor for 1, o modelo usará apenas ARIMA. Um valor perto de 0 é ponderado com mais peso para ARTXP. Um valor perto de 1 é ponderado com mais peso para ARIMA.|  
|SAMPLE_SIZE|Algoritmo Microsoft Clustering|Especifica o número de casos que o algoritmo usará em cada passagem se o parâmetro CLUSTERING_METHOD for definido como um dos métodos de cluster evolutivo. A definição do parâmetro SAMPLE_SIZE como 0 fará com que todo o conjunto de dados seja clusterizado em uma única passagem. Isso pode causar problemas de memória e de desempenho.<br /><br /> O padrão é 50000.|  
|SAMPLE_SIZE|Algoritmo Regressão Logística da Microsoft<br /><br /> Microsoft Neural Network Algorithm|Especifica o número de casos a ser usado para treinar o modelo. O provedor de algoritmo usa esse número ou a porcentagem do total de casos não incluídos na porcentagem de controle conforme especificado pelo parâmetro HOLDOUT_PERCENTAGE, o que tiver menor valor.<br /><br /> Em outras palavras, se HOLDOUT_PERCENTAGE for definido como 30, o algoritmo usará o valor desse parâmetro ou um valor igual a 70 por cento do número total de casos, o que for menor.<br /><br /> O padrão é 10000.|  
|SCORE_METHOD|Algoritmo Árvores de Decisão da Microsoft|Determina o método usado para calcular a pontuação da divisão. As seguintes opções estão disponíveis: (1) entropia, (2) Bayesiano com K2 a priori ou (3) Bayesian Dirichlet equivalente (BDE) anterior.<br /><br /> O padrão é 3.|  
|SPLIT_METHOD|Algoritmo Árvores de Decisão da Microsoft|Determina o método usado para dividir o nó. As seguintes opções estão disponíveis: Binário (1), completo (2) ou ambos (3).<br /><br /> O padrão é 3.|  
|STOPPING_TOLERANCE|Referência técnica do algoritmo Microsoft Clustering|Especifica o valor usado para determinar quando a convergência é alcançada e o algoritmo terminou de criar o modelo. A convergência é alcançada quando a alteração geral nas probabilidades do cluster é menor do que a taxa do parâmetro STOPPING_TOLERANCE dividida pelo tamanho do modelo.<br /><br /> O padrão é 10.|  
  
### <a name="comments"></a>Comentários  
 Para obter mais detalhes sobre os algoritmos, consulte os Manuais Online do SQL Server.  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;suplementos de mineração de dados do SQL Server&#41;](data-mining-algorithms-sql-server-data-mining-add-ins.md)  
  
  
