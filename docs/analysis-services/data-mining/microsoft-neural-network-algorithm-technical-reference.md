---
title: Microsoft Neural Network Algorithm Technical Reference | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1e11579c4613b79af9b7c20887eecae1ee90cd93
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="microsoft-neural-network-algorithm-technical-reference"></a>Microsoft Neural Network Algorithm Technical Reference
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  A Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] usa uma rede *multicamadas Perceptron*, também denominada *rede Regra-Delta com Algoritmo Backpropagation*, composta de até três camadas de neurônios ou *perceptrons*. Essas camadas são uma camada de entrada, uma camada opcional oculta e uma camada de saída.  
  
 Uma descrição detalhada das redes neurais de multicamadas Perceptron está fora do escopo da presente documentação. Este tópico explica a implementação básica do algoritmo, incluindo o método usado para normalizar valores de entrada e saída, e os métodos de seleção de recursos utilizados para reduzir a cardinalidade do atributo. Este tópico descreve os parâmetros e outras configurações que podem ser usadas para personalizar o comportamento do algoritmo, além de fornecer links para informações adicionais sobre como consultar o modelo.  
  
## <a name="implementation-of-the-microsoft-neural-network-algorithm"></a>Implementação do algoritmo Rede Neural da Microsoft  
 Em uma rede neural multicamadas Perceptron, cada neurônio recebe uma ou mais entradas e produz uma ou mais saídas idênticas. Cada saída é uma função não linear simples da soma das entradas ao neurônio. As entradas só passam para frente a partir de nós na camada de entrada até nós na camada oculta, e passam da camada oculta para a camada de saída sem nenhuma conexão entre os neurônios na camada. Se não houver nenhuma camada oculta, como no modelo de regressão logística, as entradas passarão diretamente dos nós na camada de entrada para os nós na camada de saída.  
  
 Há três tipos de neurônios em uma rede neural que é criada com o algoritmo Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] :  
  
**Neurônios de entrada**  
  
 Neurônios de entrada fornecem valores de atributo de entrada para o modelo de mineração de dados. Para atributos de entrada discretos, um neurônio de entrada representa normalmente um único estado do atributo de entrada. Isso incluirá valores ausentes, se os dados de treinamento contiverem nulos para esse atributo. Um atributo de entrada discreto que tiver mais de dois estados gerará um neurônio de entrada para cada estado e um neurônio de entrada para o estado existente ou ausente, se houver nulos nos dados de treinamento. Um atributo de entrada contínuo gera dois neurônios de entrada: um para um estado ausente, e um para o valor do próprio atributo contínuo. Os neurônios de entrada fornecem entradas para um ou mais neurônios ocultos.  
  
**Hidden neurons**  
  
 Neurônios ocultos recebem entradas de neurônios de entrada e fornecem saídas para os neurônios de saída.  
  
**Neurônios de saída**  
  
 Os neurônios de saída representam valores de atributos previsíveis para o modelo de mineração de dados. Para atributos de entrada discretos, um neurônio de saída representa normalmente um único estado previsto para um atributo previsível, inclusive valores ausentes. Por exemplo, um atributo previsível binário produz um nó de saída que descreve um estado existente ou ausente, para indicar se existe um valor para aquele atributo. Uma coluna booliana usada como atributo previsível gera três neurônios de saída: um para um valor verdadeiro, um para um valor falso e um para um estado existente ou ausente. Um atributo predicável discreto que tiver mais de dois estados gerará um neurônio de saída para cada estado e um neurônio de saída para o estado existente ou ausente. Colunas previsíveis contínuas geram dois neurônios de saída: um para um estado existente ou ausente e um para o valor do próprio atributo contínuo. Se mais de 500 neurônios de saída forem gerados por meio da revisão do conjunto de colunas previsíveis, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gerará uma nova rede no modelo de mineração para representar os neurônios de saída adicionais.  
  
 Um neurônio recebe entrada de outros neurônios ou de outros dados, dependendo de qual camada da rede ele está. Um neurônio de entrada recebe entradas dos dados originais. Os neurônios ocultos e os neurônios de saída recebem entradas da saída de outros neurônios na rede neural. As entradas estabelecem relações entre neurônios e as relações servem como caminho de análise para um conjunto específico de casos.  
  
 Cada entrada tem um valor atribuído a ele, denominado *peso*, que descreve a relevância ou a importância de uma entrada específica para um neurônio oculto ou para um neurônio de saída. Quanto maior o peso atribuído a uma entrada, mais relevante ou importante será o valor dessa entrada. Os pesos podem ser negativos, o que implica que a entrada pode inibir, em vez de ativar, um neurônio específico. O valor de cada entrada é multiplicado pelo peso para enfatizar a importância de uma entrada para um determinado neurônio. Para pesos negativos, o efeito de multiplicar o valor pelo peso é remover a importância.  
  
 Cada neurônio tem atribuído a ele uma função não linear simples, denominada *função de ativação*, que descreve a relevância ou a importância de um neurônio específico para a camada da rede neural. Neurônios ocultos usam uma função *tangente hiperbólica* (tanh) como sua função de ativação, enquanto os neurônios de saída utilizam uma função *sigmoide* para ativação. Ambas as funções, são funções não lineares, contínuas e que fazem com que a rede neural modele relações não lineares entre os neurônios de entrada e de saída.  
  
### <a name="training-neural-networks"></a>Treinando Redes Neurais  
 Várias etapas são envolvidas no treinamento de um modelo de mineração de dados que usa o algoritmo Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Essas etapas são amplamente influenciadas pelos valores especificados para os parâmetros do algoritmo.  
  
 O algoritmo primeiro avalia e depois extrai dados de treinamento da fonte de dados. A porcentagem dos dados de treinamento, chamados *dados de validação*, é reservada para o uso na avaliação da precisão da rede. Durante o processo de treinamento, a rede é avaliada imediatamente após cada iteração pelos dados de treinamento. Quando a precisão não aumentar mais, o processo de treinamento será interrompido.  
  
 Os valores dos parâmetros *SAMPLE_SIZE* e *HOLDOUT_PERCENTAGE* são usados para definir o número de casos a serem amostrados dos dados de treinamento e o número de casos a serem deixados de lado para os dados de controle. O valor do parâmetro *HOLDOUT_SEED* é usado para definir aleatoriamente os casos individuais a serem deixados de lado para os dados de controle.  
  
> [!NOTE]  
>  Esses parâmetros de algoritmo são diferentes das propriedades HOLDOUT_SIZE e HOLDOUT_SEED, que são aplicadas a uma estrutura de mineração para definir um conjunto de dados de teste.  
  
 O algoritmo seguinte define o número e a complexidade das redes que o modelo de mineração tem suporte. Se o modelo de mineração contém um ou mais atributos usados apenas para previsão, o algoritmo cria uma única rede que representa todos esses atributos. Se o modelo de mineração contém um ou mais atributos usados para entrada e previsão, o provedor do algoritmo construirá uma rede para cada atributo.  
  
 Para atributos de entrada e previsíveis com valores discretos, cada neurônio de entrada ou de saída representa respectivamente um único estado. Para atributos de entrada e previsíveis com valores contínuos, cada neurônio de entrada ou de saída representa respectivamente o intervalo e a distribuição de valores para o atributo. O número máximo de estados com suporte em ambos os casos depende do valor do parâmetro do algoritmo *MAXIMUM_STATES* . Se o número de estados para um atributo específico exceder o valor do parâmetro do algoritmo *MAXIMUM_STATES* , os estados mais populares ou relevantes para esse atributo serão escolhidos, até o máximo de estados permitidos, e os demais estados serão agrupados como valores ausentes para efeito de análise.  
  
 Então, o algoritmo usará o valor do parâmetro *HIDDEN_NODE_RATIO* quando for determinar o número inicial de neurônios a serem criados para a camada oculta. Você pode definir *HIDDEN_NODE_RATIO* como 0 para impedir a criação de camada oculta nas redes que o algoritmo gera para o modelo de mineração, a fim de tratar a rede neural como uma regressão lógica.  
  
 O provedor de algoritmos avalia iterativamente o peso de todas as entradas na rede ao mesmo tempo, selecionando o conjunto de dados de treinamento que foi reservado anteriormente e, comparando o valor atual conhecido de cada caso nos dados de validação com a previsão da rede em um processo definido como *aprendizado em lotes*. Após o algoritmo avaliar o conjunto inteiro dos dados de treinamento, ele revisa o valor atual e previsto para cada neurônio. O algoritmo calcula o grau do erro, se houver, e ajusta os pesos associados com as entradas daquele neurônio, funcionando em direção oposta, dos neurônios de saída para os neurônios de entrada, em um processo conhecimento como *backpropagation*. O algoritmo repete então o processo em todo o conjunto dos dados de treinamento. Devido ao fato do algoritmo ter suporte para vários pesos e neurônios de saída, o algoritmo gradiente conjugado é usado para guiar o processo de treinamento a fim de atribuir e avaliar os pesos para as entradas. Uma descrição do algoritmo gradiente conjugado está fora do escopo desta documentação.  
  
### <a name="feature-selection"></a>Seleção de recursos  
 Se o número de atributos de entrada for maior do que o valor do parâmetro *MAXIMUM_INPUT_ATTRIBUTES* ou se o número de atributos previsíveis for maior do que o valor do parâmetro *MAXIMUM_OUTPUT_ATTRIBUTES* , um algoritmo de seleção de recursos será usado para reduzir a complexidade das redes incluídas no modelo de mineração. A seleção de recursos reduz o número de atributos de entrada e previsíveis para deixar apenas aqueles que são estatisticamente relevantes para o modelo.  
  
 A seleção de recursos é usada automaticamente por todos os algoritmos de mineração de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para melhorar a análise e reduzir a carga de processamento. O método usado para seleção de recursos em modelos de rede neural depende do tipo de dados do atributo. Para referência, a tabela a seguir mostra os métodos de seleção de recursos usados para modelos de rede neural e os métodos de seleção de recursos usados para o algoritmo de Regressão Logística, que se baseia no algoritmo Rede Neural.  
  
|Algoritmo|Método de análise|Comentários|  
|---------------|------------------------|--------------|  
|Rede Neural|Pontuação de interesse<br /><br /> Entropia de Shannon<br /><br /> Bayesian com K2 a priori<br /><br /> Bayesian Dirichlet com uniforme a priori (padrão)|O algoritmo Redes Neurais pode usar ambos os métodos de pontuação Bayesiano e baseado em entropia, desde que os dados contenham colunas contínuas.<br /><br /> Padrão.|  
|Regressão Logística|Pontuação de interesse<br /><br /> Entropia de Shannon<br /><br /> Bayesian com K2 a priori<br /><br /> Bayesian Dirichlet com uniforme a priori (padrão)|Como não é possível indicar um parâmetro para esse algoritmo controlar o comportamento de seleção de recursos, os padrões são usados. Sendo assim, se todos os atributos forem discretos ou diferenciados, o padrão será BDEU.|  
  
 Os parâmetros de algoritmo que controlam a seleção de recursos para um modelo de rede neural são MAXIMUM_INPUT_ATTRIBUTES, MAXIMUM_OUTPUT_ATTRIBUTES e MAXIMUM_STATES. Você também pode controlar o número de camadas ocultas definindo o parâmetro HIDDEN_NODE_RATIO.  
  
### <a name="scoring-methods"></a>Métodos de pontuação  
 A*Pontuação* é um tipo de normalização que, no contexto de treinamento de um modelo de rede neural, significa o processo de converter um valor, como uma etiqueta de texto discreta, em um valor que possa ser comparado com outros tipos de entradas e ponderado na rede. Por exemplo, se um atributo de entrada for Sexo e os valores possíveis forem Masculino e Feminino, e outro atributo de entrada for Renda, com um intervalo variável de valores, os valores de cada atributo não serão diretamente comparáveis e, portanto, deverão ser codificados para uma escala comum para que os pesos possam ser calculados. A pontuação é o processo de normalizar essas entradas para valores numéricos: especificamente para um intervalo de probabilidade. As funções usadas para normalização também ajudam a distribuir o valor de entrada mais uniformemente em uma escala uniforme, para que valores extremos não distorçam os resultados da análise.  
  
 As saídas da rede neural também são codificadas. Quando há um único destino para a saída (isto é, previsão), ou vários destinos que são usados apenas para previsão e não para entrada, o modelo cria uma única rede e talvez não seja necessário para normalizar os valores. No entanto, se vários atributos forem usados para entrada e previsão, o modelo deverá criar várias redes; portanto, todos os valores deverão ser normalizados e as saídas também deverão ser codificadas, à medida que deixarem a rede.  
  
 A codificação de entradas se baseia em somar cada valor discreto nos casos de treinamento e multiplicar esse valor por seu peso. Esse processo é denominado *soma ponderada*, que é passada à função de ativação na camada oculta. Uma pontuação z é usada para codificação, da seguinte forma:  
  
 **Valores discretos**  
  
 `μ = p` – a probabilidade anterior de um estado  
  
 `StdDev  = sqrt(p(1-p))`  
  
 **Valores contínuos**  
  
 Valor presente= `1 - μ/σ`  
  
 Valor inexistente= `-μ/σ`  
  
 Após a codificação dos valores, as entradas passam pela soma ponderada, com as margens de rede como pesos.  
  
 A codificação de saídas usa a função sigmoide que tem propriedades que a tornam muito útil para previsão. Uma dessas propriedades é que, independentemente do modo como os valores originais são escalonados e independentemente se os valores são negativos ou positivos, a saída dessa função sempre é um valor entre 0 e 1, o que é adequado para estimar probabilidades. Outra propriedade útil é que a função sigmoide tem um efeito de atenuação, de modo que à medida que o valor se afasta do ponto de inflexão, a probabilidade de o valor avançar é de 0 ou 1, mas lentamente.  
  
## <a name="customizing-the-neural-network-algorithm"></a>Personalizando o algoritmo Rede Neural  
 O algoritmo Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] tem suporte a vários parâmetros que afetam o comportamento, o desempenho e a precisão do modelo de mineração resultante. Também é possível modificar o modo como o modelo processa dados definindo sinalizadores de modelagem nas colunas ou definindo sinalizadores de distribuição para especificar o modo como os valores na coluna são manipulados.  
  
### <a name="setting-algorithm-parameters"></a>Definindo parâmetros de algoritmo  
 A tabela a seguir descreve os parâmetros que podem ser usados com o algoritmo Rede Neural da Microsoft.  
  
 HIDDEN_NODE_RATIO  
 Especifica a proporção dos neurônios ocultos com os neurônios de entrada e saída. A fórmula a seguir determina o número inicial de neurônios na camada oculta:  
  
 HIDDEN_NODE_RATIO * SQRT (Total de neurônios de entrada \* Total de neurônios de saída)  
  
 O valor padrão é 4.0.  
  
 HOLDOUT_PERCENTAGE  
 Especifica a porcentagem de casos nos dados de treinamento que são usados para calcular o erro de dados de controle e que é utilizada como parte do critério de interrupção durante o treinamento do modelo de mineração.  
  
 O valor padrão é 30.  
  
 HOLDOUT_SEED  
 Especifica um número que é usado para semear o gerador pseudoaleatório quando o algoritmo determinar os dados de controle aleatoriamente. Se esse parâmetro for definido como 0, o algoritmo gerará a semente com base no nome do modelo de mineração, para garantir que o conteúdo do modelo permaneça o mesmo durante um novo processamento.  
  
 O valor padrão é 0.  
  
 MAXIMUM_INPUT_ATTRIBUTES  
 Define o número máximo de atributos de entrada que podem ser fornecidos ao algoritmo antes que a seleção de recursos seja empregada. Definir esse valor como 0 desabilita a seleção do recurso para os atributos de entrada.  
  
 O valor padrão é 255.  
  
 MAXIMUM_OUTPUT_ATTRIBUTES  
 Define o número máximo de atributos de saída que podem ser fornecidos ao algoritmo antes que a seleção de recursos seja empregada. Definir esse valor como 0 desabilita a seleção do recurso para os atributos de saída.  
  
 O valor padrão é 255.  
  
 MAXIMUM_STATES  
 Especifica o número máximo de estados discreto por atributo para os quais o algoritmo dá suporte. Se o número de estados para um atributo específico for maior do que o número especificado para esse parâmetro, o algoritmo usará os estados mais populares do atributo e tratará os demais estados como ausentes.  
  
 O valor padrão é 100.  
  
 SAMPLE_SIZE  
 Especifica o número de casos a ser usado para treinar o modelo. O algoritmo usa esse número ou a porcentagem do total de casos não incluídos nos dados de validação conforme especificado pelo parâmetro HOLDOUT_PERCENTAGE, o que tiver menor valor.  
  
 Em outras palavras, se HOLDOUT_PERCENTAGE for definido como 30, o algoritmo usará o valor desse parâmetro ou um valor igual a 70 por cento do número total de casos, o que for menor.  
  
 O valor padrão é 10000.  
  
### <a name="modeling-flags"></a>Sinalizadores de modelagem  
 Os sinalizadores de modelagem a seguir têm suporte para uso com o algoritmo Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 NOT NULL  
 Indica que a coluna não pode conter um nulo. Um erro ocorrerá se o Analysis Services encontrar um valor nulo durante o treinamento do modelo.  
  
 Aplica-se às colunas de estrutura de mineração.  
  
 MODEL_EXISTENCE_ONLY  
 Indica que o modelo deve considerar apenas se um valor existe para o atributo ou se um valor está ausente. O valor exato não importa.  
  
 Aplica-se às colunas de modelo de mineração.  
  
### <a name="distribution-flags"></a>Sinalizadores de distribuição  
 Os sinalizadores de distribuição a seguir têm suporte para uso com o algoritmo Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Os sinalizadores são usados como dicas para o modelo apenas; se o algoritmo detectar uma distribuição diferente, ele usará a distribuição encontrada, não aquela fornecida na dica.  
  
 Normal  
 Indica que os valores dentro da coluna devem ser tratados como se representam a distribuição normal ou gaussiana.  
  
 Uniforme  
 Indica que os valores dentro da coluna devem ser tratados como se fossem distribuídos uniformemente; ou seja, a probabilidade de qualquer valor é aproximadamente igual e é uma função do número total de valores.  
  
 Log Normal  
 Indica que os valores na coluna devem ser tratados como se estivessem distribuídos de acordo com a curva *log normal* , o que significa que o logaritmo dos valores será distribuído normalmente.  
  
## <a name="requirements"></a>Requisitos  
 Um modelo de rede neural deve conter pelo menos uma coluna de entrada e uma coluna de saída.  
  
### <a name="input-and-predictable-columns"></a>Colunas de entrada e colunas previsíveis  
 O algoritmo Rede Neural da [!INCLUDE[msCoName](../../includes/msconame-md.md)] dá suporte a colunas de entrada e colunas previsíveis específicas que são listadas na tabela a seguir.  
  
|Coluna|Tipos de conteúdo|  
|------------|-------------------|  
|Atributo de entrada|Contínuo, cíclico, discreto, diferenciado, chave, tabela, e ordenado|  
|Atributo previsível|Contínuo, cíclico, discreto, diferenciado, e ordenado|  
  
> [!NOTE]  
>  Os tipos de conteúdo Cíclico e Ordenado têm suporte, mas o algoritmo os trata como valores discretos e não executa processamento especial.  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmo rede Neural da Microsoft](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)   
 [Conteúdo do modelo de mineração para modelos de rede Neural & #40; Analysis Services – mineração de dados & #41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [Exemplos de consulta de modelo de rede neural](../../analysis-services/data-mining/neural-network-model-query-examples.md)  
  
  
