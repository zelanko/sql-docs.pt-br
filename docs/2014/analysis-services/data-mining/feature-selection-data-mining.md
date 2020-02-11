---
title: Seleção de recursos (mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], feature selections
- attributes [data mining]
- feature selection algorithms [Analysis Services]
- data mining [Analysis Services], feature selections
- neural network algorithms [Analysis Services]
- naive bayes algorithms [Analysis Services]
- decision tree algorithms [Analysis Services]
- datasets [Analysis Services]
- clustering algorithms [Analysis Services]
- coding [Data Mining]
ms.assetid: b044e785-4875-45ab-8ae4-cd3b4e3033bb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a1d79bb3810a56e8a1769845131312eab306f223
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084422"
---
# <a name="feature-selection-data-mining"></a>Seleção de recursos (mineração de dados)
  A *seleção de recursos* é um termo normalmente usado em Data Mining para descrever as ferramentas e as técnicas disponíveis para reduzir as entradas para um tamanho gerenciável para processamento e análise. A seleção de recursos implica não apenas *redução de cardinalidade*, o que significa a imposição de um corte arbitrário ou predefinido no número de atributos que podem ser considerados ao criar um modelo, mas também à escolha de atributos, o que significa que o analista ou a ferramenta de modelagem seleciona ou descarta os atributos de forma ativa com base em sua utilidade para análise.  
  
 A capacidade para aplicar seleção de recursos é crítica para análise efetiva, porque os conjuntos de dados frequentemente contêm muito mais informações do que é necessário para criar o modelo. Por exemplo, um conjunto de dados pode conter 500 colunas que descrevem as características de clientes, mas se os dados em algumas das colunas forem muito esparsos, você ganharia um benefício muito pequeno por acrescentá-los ao modelo. Se você mantiver colunas desnecessárias quando criar o modelo, precisará de mais CPU e memória durante o processo de treinamento e de mais espaço de armazenamento para o modelo completo.  
  
 Ainda que recursos não sejam um problema, normalmente você remove colunas desnecessárias porque elas podem diminuir a qualidade dos padrões descobertos, pelos seguintes motivos:  
  
-   Algumas colunas são ruidosas ou redundantes. Esse ruído dificulta a descoberta de padrões significantes a partir dos dados;  
  
-   Para descobrir padrões de qualidade, a maioria que algoritmos de mineração de dados requer um conjunto de dados de treinamento muito maior no conjunto de dados de grande dimensão. Mas os dados de treinamento são muito pequenos em alguns aplicativos de mineração de dados.  
  
 Se somente 50 das 500 colunas na fonte de dados tiverem informações úteis para criar um modelo, você poderá apenas omiti-las do modelo ou pode usar técnicas de seleção de recursos para descobrir automaticamente os melhores recursos e excluir valores que são estatisticamente insignificantes. A seleção de recursos ajuda a resolver os problemas de ter dados demais de pouco valor, ou de ter pouquíssimos dados de alto valor.  
  
## <a name="feature-selection-in-analysis-services-data-mining"></a>Seleção de recursos na mineração de dados do Analysis Services  
 Normalmente, a seleção de recursos é executada automaticamente no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e cada algoritmo tem um conjunto de técnicas padrão para aplicar redução de recursos de maneira inteligente. A seleção de recursos sempre é feita antes do treinamento do modelo, para que os atributos de um conjunto de dados com maior probabilidade de uso no modelo sejam escolhidos de forma automática. Porém, você também pode definir manualmente parâmetros para influenciar o comportamento de seleção de recursos.  
  
 Em geral, ela funciona calculando uma pontuação para cada atributo e, em seguida, selecionando apenas os atributos com a pontuação mais alta. Também é possível ajustar o limiar para os pontos mais altos. O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece vários métodos para calcular estas pontuações e o método exato que é aplicado em qualquer modelo depende destes fatores:  
  
-   O algoritmo usado em seu modelo  
  
-   O tipo de dados do atributo  
  
-   Os parâmetros que você pode ter definido em seu modelo  
  
 A seleção de recursos é aplicada a entradas, atributos previsíveis ou estados em uma coluna. Quando a pontuação para a seleção de recursos estiver concluída, somente os atributos e os estados que o algoritmo selecionar serão incluídos no processo de criação de modelo e poderão ser usados para previsão. Se você escolher um atributo previsível que não atende o limite para seleção de recursos, o atributo ainda poderá ser usado para previsão, mas as previsões serão baseadas somente nas estatísticas globais que existem no modelo.  
  
> [!NOTE]  
>  A seleção de recursos afeta apenas as colunas usadas no modelo e não o armazenamento da estrutura de mineração. As colunas que ficarem fora do modelo de mineração continuarão disponíveis na estrutura, e os dados das colunas da estrutura de mineração serão armazenados em cache.  
  
### <a name="definition-of-feature-selection-methods"></a>Definição de métodos de seleção de recursos  
 Há várias formas de implementar a seleção de recursos, dependendo do tipo de dados com que você está trabalhando e do algoritmo escolhido para a análise. O SQL Server Analysis Services fornece vários métodos populares e bem-estabelecidos para pontuar atributos. O método aplicado em qualquer algoritmo ou conjunto de dados depende dos tipos de dados e do uso de coluna.  
  
 A pontuação de *interesse* é usada para classificar e ordenar atributos em colunas que contêm dados numéricos contínuos não binários.  
  
 A *entropia de Shannon* e duas pontuações de *Bayesiana* estão disponíveis para colunas que contêm dados discretos e discretizado. No entanto, se o modelo contiver colunas contínuas, a pontuação de interesse será usada para avaliar todas as colunas de entrada para garantir a consistência.  
  
 A seção a seguir descreve cada método de seleção de recursos.  
  
#### <a name="interestingness-score"></a>Pontuação de interesse  
 Um recurso será interessante se ele transmitir alguma informação útil. Como a definição do que é útil varia dependendo do cenário, a Data Mining setor desenvolveu várias maneiras de medir a *curiosaidade*. Por exemplo, *novidade* pode ser interessante na detecção de exceção, mas a capacidade de discriminar várias entre itens relacionados ou o *peso de discriminamento*pode ser mais interessante para classificação.  
  
 A medida de interesse usada em SQL Server Analysis Services é *baseada em entropia*, o que significa que os atributos com distribuições aleatórias têm maior entropia e menor lucro de informações; Portanto, esses atributos são menos interessantes. A entropia de qualquer atributo em particular é comparada à entropia de todos os outros atributos, como segue:  
  
 Interestingness(Attribute) = - (m - Entropy(Attribute)) * (m - Entropy(Attribute))  
  
 Entropia central ou m, significa a entropia de todo o conjunto de recursos. Ao subtrair a entropia do atributo de destino da entropia central, é possível avaliar a quantidade de informações fornecida pelo atributo.  
  
 Por padrão, essa pontuação será usada sempre que a coluna contiver dados numéricos contínuos não binários.  
  
#### <a name="shannons-entropy"></a>entropia de Shannon  
 A entropia de Shannon mede a incerteza de uma variável aleatória para um resultado em particular. Por exemplo, a entropia do lançamento de uma moeda pode ser representada como uma função da probabilidade de o resultado ser cara.  
  
 O Analysis Services usa a seguinte fórmula para calcular a entropia de Shannon:  
  
 H(X) = -∑ P(xi) log(P(xi))  
  
 Esse método de pontuação está disponível para atributos discretos e diferenciados.  
  
#### <a name="bayesian-with-k2-prior"></a>Bayesian com K2 a priori  
 O Analysis Services fornece duas pontuações para seleção de recursos que se baseiam em redes Bayesianas. Uma rede Bayesiana é um gráfico *direcionado* ou *acíclico* de estados e transições entre estados, ou seja, alguns estados vêm sempre antes do estado atual, alguns ocorrem depois, e o gráfico não se repete nem gera um loop. Por definição, as redes Bayesianas permitem o uso do conhecimento prévio. No entanto, a questão de qual estado anterior usar no cálculo de probabilidades de estados posteriores é importante para o design, o desempenho e a precisão do algoritmo.  
  
 O algoritmo K2 para aprender com a rede Bayesiana foi desenvolvido por Cooper e Herskovits e é usado com frequência na mineração de dados. Ele é escalável e analisa diversas variáveis, mas requer ordenação das variáveis usadas como entrada. Para obter mais informações, consulte [Learning Bayesian Networks](https://go.microsoft.com/fwlink/?LinkId=105885) (em inglês) de Chickering, Geiger e Heckerman.  
  
 Esse método de pontuação está disponível para atributos discretos e diferenciados.  
  
#### <a name="bayesian-dirichlet-equivalent-with-uniform-prior"></a>Bayesiano Dirichlet Equivalente com Uniforme a priori  
 A pontuação BDE (Bayesiano Dirichlet Equivalente) também usa análise Bayesiana para avaliar uma rede dado um conjunto de dados. O método de pontuação do BDE foi desenvolvido por Heckerman e se baseia na métrica de BD desenvolvida por Cooper e Herskovits. A distribuição Dirichlet é uma distribuição multinomial que descreve a probabilidade condicional de cada variável da rede e possui muitas propriedades que devemos conhecer.  
  
 O método BDEU (Bayesiano Dirichlet Equivalente com Uniforme a priori) assume um caso especial da distribuição Dirichlet, na qual uma constante matemática é usada para criar uma distribuição fixa ou uniforme de estados anteriores. A pontuação do BDE também assume equivalência de probabilidade, o que significa que não se pode esperar que os dados separem estruturas equivalentes. Em outras palavras, se a pontuação de Se A Então B for igual à pontuação de Se B Então A, não será possível distinguir as estruturas com base nos dados nem deduzir a causa.  
  
 Para obter mais informações sobre redes Bayesianas e a implementação desses métodos de pontuação, consulte [Learning Bayesian Networks](https://go.microsoft.com/fwlink/?LinkId=105885)(em inglês).  
  
### <a name="feature-selection-methods-used-by-analysis-services-algorithms"></a>Métodos de seleção de recursos usados pelos algoritmos do Analysis Services  
 A tabela a seguir lista os algoritmos que suportam a seleção de recursos, os métodos de seleção de recursos usados por eles e os parâmetros que você define para controlar o comportamento da seleção de recursos:  
  
|Algoritmo|Método de análise|Comentários|  
|---------------|------------------------|--------------|  
|Naive Bayes|entropia de Shannon<br /><br /> Bayesian com K2 a priori<br /><br /> Bayesian Dirichlet com uniforme a priori (padrão)|O algoritmo Microsoft Naïve Bayes aceita somente atributos discretos ou diferenciados; portanto, não pode usar a pontuação de interesse.<br /><br /> Para obter mais informações sobre esse algoritmo, consulte [Microsoft Naive Bayes Algorithm Technical Reference](microsoft-naive-bayes-algorithm-technical-reference.md).|  
|Árvores de decisão|Pontuação de interesse<br /><br /> entropia de Shannon<br /><br /> Bayesian com K2 a priori<br /><br /> Bayesian Dirichlet com uniforme a priori (padrão)|Se qualquer coluna contiver valores contínuos não binários, a pontuação de interesse será usada em todas as colunas para garantir a consistência. Caso contrário, será usado o método de seleção de recursos padrão ou o método que você especificou quando criou o modelo.<br /><br /> Para obter mais informações sobre esse algoritmo, consulte [Microsoft Decision Trees Algorithm Technical Reference](microsoft-decision-trees-algorithm-technical-reference.md).|  
|Rede neural|Pontuação de interesse<br /><br /> entropia de Shannon<br /><br /> Bayesian com K2 a priori<br /><br /> Bayesian Dirichlet com uniforme a priori (padrão)|O algoritmo Redes Neurais da Microsoft pode usar ambos os métodos Bayesiano e baseado em entropia, desde que os dados contenham colunas contínuas.<br /><br /> Para obter mais informações sobre esse algoritmo, consulte [Microsoft Neural Network Algorithm Technical Reference](microsoft-neural-network-algorithm-technical-reference.md).|  
|Regressão logística|Pontuação de interesse<br /><br /> entropia de Shannon<br /><br /> Bayesian com K2 a priori<br /><br /> Bayesian Dirichlet com uniforme a priori (padrão)|Embora o algoritmo de Regressão Logística da Microsoft se baseie no algoritmo Rede Neural da Microsoft, você não pode personalizar modelos de regressão logística para controlar o comportamento de seleção de recursos; portanto, a seleção de recursos sempre usa o método mais apropriado para o atributo por padrão.<br /><br /> Se todos os atributos forem discretos ou diferenciados, o padrão será BDEU.<br /><br /> Para obter mais informações sobre esse algoritmo, consulte [Microsoft Logistic Regression Algorithm Technical Reference](microsoft-logistic-regression-algorithm-technical-reference.md).|  
|Clustering|Pontuação de interesse|O algoritmo Microsoft Clustering pode usar dados discretos ou diferenciados. No entanto, como a pontuação de cada atributo é calculada como uma distância e representada como um número contínuo, a pontuação de interesse deve ser usada.<br /><br /> Para obter mais informações sobre esse algoritmo, consulte [Microsoft Clustering Algorithm Technical Reference](microsoft-clustering-algorithm-technical-reference.md).|  
|Regressão linear|Pontuação de interesse|O algoritmo de Regressão Linear da Microsoft pode usar somente a pontuação de interesse, pois suporta apenas colunas contínuas.<br /><br /> Para obter mais informações sobre esse algoritmo, consulte [Microsoft Linear Regression Algorithm Technical Reference](microsoft-linear-regression-algorithm-technical-reference.md).|  
|Regras da associação<br /><br /> Clustering de sequências|Não usado|A seleção de recursos não é invocada com esses algoritmos.<br /><br /> No entanto, você poderá controlar o comportamento do algoritmo e reduzir o tamanho dos dados de entrada se necessário, configurando o valor dos parâmetros MINIMUM_SUPPORT e MINIMUM_PROBABILIITY.<br /><br /> Para obter mais informações, consulte [Microsoft Association Algorithm Technical Reference](microsoft-association-algorithm-technical-reference.md) e [Microsoft Sequence Clustering Algorithm Technical Reference](microsoft-sequence-clustering-algorithm-technical-reference.md).|  
|Série temporal|Não usado|A seleção de recursos não se aplica a modelos de série temporal.<br /><br /> Para obter mais informações sobre esse algoritmo, consulte [Microsoft Time Series Algorithm Technical Reference](microsoft-time-series-algorithm-technical-reference.md).|  
  
## <a name="feature-selection-parameters"></a>Parâmetros de seleção de recursos  
 Nos algoritmos que suportam a seleção de recursos, é possível controlar quando a seleção de recursos é ativada usando os parâmetros a seguir. Cada algoritmo tem um valor padrão para o número de entradas permitidas, mas você pode substituir esse padrão e especificar o número de atributos. Esta seção lista os parâmetros que são fornecidos para gerenciar a seleção de recursos.  
  
#### <a name="maximum_input_attributes"></a>MAXIMUM_INPUT_ATTRIBUTES  
 Se o modelo tiver mais colunas do que o número especificado no parâmetro *MAXIMUM_INPUT_ATTRIBUTES* , o algoritmo ignorará as colunas calculadas como não interessantes.  
  
#### <a name="maximum_output_attributes"></a>MAXIMUM_OUTPUT_ATTRIBUTES  
 Da mesma forma, se o modelo tiver mais colunas previsíveis do que o número especificado no parâmetro *MAXIMUM_OUTPUT_ATTRIBUTES* , o algoritmo ignorará as colunas calculadas como não interessantes.  
  
#### <a name="maximum_states"></a>MAXIMUM_STATES  
 Se um modelo tiver mais casos que os especificado no parâmetro *MAXIMUM_STATES* , os estados menos populares serão agrupados para tratados como ausentes. Se qualquer um desses parâmetros for definido como 0, a seleção de recursos será desativada, o que afeta o tempo de processamento e o desempenho.  
  
 Além destes métodos para seleção de recursos, você pode melhorar a capacidade de o algoritmo identificar ou promover atributos significativos definindo *sinalizadores de modelagem* no modelo ou definindo *sinalizadores de distribuição* na estrutura. Para obter mais informações sobre esses conceitos, consulte [Sinalizadores de modelagem &#40;Data Mining&#41;](modeling-flags-data-mining.md) e [Distribuições de colunas &#40;Data Mining&#41;](column-distributions-data-mining.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Personalizar os modelos de mineração e a estrutura](customize-mining-models-and-structure.md)  
  
  
