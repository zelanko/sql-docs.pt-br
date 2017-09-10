---
title: "Seleção (mineração de dados) de recursos | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6ae50c18dab1894b42e209d2a37762e0fa9e0d57
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="feature-selection-data-mining"></a>Seleção de recursos (mineração de dados)
  A*seleção de recursos* é uma parte importante do aprendizado de máquina. Seleção de recursos refere-se ao processo de reduzir as entradas para a análise e processamento ou de localizar as entradas mais significativas. Um termo relacionado, a *engenharia de recursos* (ou *extração de recursos*), refere-se ao processo de extração de informações úteis ou recursos dos dados existentes.  
  
## <a name="why-do-feature-selection"></a>O que significa a seleção de recursos?  
 A seleção de recursos é essencial para a criação de um bom modelo por vários motivos. Um deles é que a seleção de recursos implica um certo grau de *redução de cardinalidade*para impor um corte no número de atributos que podem ser considerados ao criar um modelo. Os dados quase sempre contém mais informações do que o necessário para criar o modelo ou o tipo errado de informações. Por exemplo, você pode ter um conjunto de dados com 500 colunas que descrevem as características dos clientes; no entanto, se os dados de algumas das colunas forem muito esparsos, não será muito benéfico adicioná-los ao modelo, e se algumas das colunas forem duplicatas de outras, usar as duas colunas poderá afetar o modelo.  
  
 Não apenas a seleção de recursos melhora a qualidade do modelo, mas também torna o processo de modelagem mais eficiente. Se você usar colunas desnecessárias quando criar um modelo, precisará de mais CPU e memória durante o processo de treinamento e de mais espaço de armazenamento para o modelo completo. Mesmo se os recursos não forem um problema, ainda convém executar a seleção de recursos e identificar as melhores colunas, pois colunas desnecessárias podem prejudicar a qualidade do modelo de várias maneiras:  
  
-   Dados com ruído ou redundantes dificultam a descoberta de padrões significativos.  
  
-   Se o conjunto de dados for de grande dimensão, a maioria que algoritmos de mineração de dados exigirá um conjunto de dados de treinamento muito maior.  
  
 Durante o processo de seleção de recursos, o analista, a ferramenta de modelagem ou o algoritmo seleciona ou descarta ativamente atributos com base em sua utilidade para análise.  O analista pode realizar engenharia de recursos para adicionar recursos e remover ou modificar dados existentes, enquanto o algoritmo de aprendizado de máquina normalmente pontua as colunas e valida sua utilidade no modelo.  
  
 ![Recurso de seleção e o processo de engenharia](../../analysis-services/data-mining/media/ssdm-featureselectionprocess.png "seleção e o processo de engenharia de recurso")  
  
 Em suma, a seleção de recursos ajuda a resolver dois problemas: ter dados de pouco valor em excesso ou de ter poucos dados de alto valor. Seu objetivo na seleção de recursos deve ser identificar o número mínimo de colunas da fonte de dados significativo para a criação de um modelo.  
  
## <a name="how-feature-selection-works-in-sql-server-data-mining"></a>Como a seleção de recursos funciona no SQL Server Data Mining  
 A seleção de recursos sempre é executada antes do modelo ser treinado. Com alguns algoritmos, as técnicas de seleção de recursos são "internas" para que as colunas irrelevantes sejam excluídas e os melhores recursos sejam descobertos automaticamente. Cada algoritmo tem seu próprio conjunto de técnicas padrão para aplicar a redução de recursos de forma inteligente.  Porém, você também pode definir manualmente parâmetros para influenciar o comportamento de seleção de recursos.  
  
 Durante a seleção automática de recursos, a pontuação é calculada para cada atributo, e somente os atributos que têm as melhores classificações são selecionados para o modelo. Também é possível ajustar o limiar para os pontos mais altos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Data Mining fornece vários métodos para calcular estas pontuações e o método exato aplicado em qualquer modelo depende destes fatores:  
  
-   O algoritmo usado em seu modelo  
  
-   O tipo de dados do atributo  
  
-   Os parâmetros que você pode ter definido em seu modelo  
  
 A seleção de recursos é aplicada a entradas, atributos previsíveis ou estados em uma coluna. Quando a pontuação para a seleção de recursos estiver concluída, somente os atributos e os estados que o algoritmo selecionar serão incluídos no processo de criação de modelo e poderão ser usados para previsão. Se você escolher um atributo previsível que não atende o limite para seleção de recursos, o atributo ainda poderá ser usado para previsão, mas as previsões serão baseadas somente nas estatísticas globais que existem no modelo.  
  
> [!NOTE]  
>  A seleção de recursos afeta apenas as colunas usadas no modelo e não o armazenamento da estrutura de mineração. As colunas que ficarem fora do modelo de mineração continuarão disponíveis na estrutura, e os dados das colunas da estrutura de mineração serão armazenados em cache.  
  
### <a name="feature-selection-scores"></a>Pontuações de seleção de recursos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Data Mining dá suporte a esses métodos populares e bem-estabelecidos para pontuar atributos. O método específico usado em qualquer algoritmo ou conjunto de dados específico depende dos tipos de dados e do uso de coluna.  
  
-   A pontuação de *interesse* é usada para classificar e ordenar atributos em colunas que contêm dados numéricos contínuos não binários.  
  
-   A*entropia de Shannon* e duas pontuações *Bayesiana* estão disponíveis para colunas que contêm dados discretos e diferenciados. No entanto, se o modelo contiver colunas contínuas, a pontuação de interesse será usada para avaliar todas as colunas de entrada para garantir a consistência.  
  
#### <a name="interestingness-score"></a>Pontuação de interesse  
 Um recurso será interessante se ele transmitir alguma informação útil. No entanto, o *interesse* pode ser medido de muitas formas.  *Novidade* seria valiosa para detectar uma exceção, mas a capacidade de diferenciar itens intimamente relacionados, ou *peso discriminatório*, seria mais interessante para a classificação.  
  
 A medida de interesse usada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining *baseia-se em entropia*, ou seja, os atributos com distribuições aleatórias têm maior entropia e menor ganho de informações; sendo assim, esses atributos são menos interessantes. A entropia de qualquer atributo em particular é comparada à entropia de todos os outros atributos, como segue:  
  
 Interestingness(Attribute) = - (m - Entropy(Attribute)) * (m - Entropy(Attribute))  
  
 Entropia central ou m, significa a entropia de todo o conjunto de recursos. Ao subtrair a entropia do atributo de destino da entropia central, é possível avaliar a quantidade de informações fornecida pelo atributo.  
  
 Por padrão, essa pontuação será usada sempre que a coluna contiver dados numéricos contínuos não binários.  
  
#### <a name="shannons-entropy"></a>entropia de Shannon  
 A entropia de Shannon mede a incerteza de uma variável aleatória para um resultado em particular. Por exemplo, a entropia do lançamento de uma moeda pode ser representada como uma função da probabilidade de o resultado ser cara.  
  
 O Analysis Services usa a seguinte fórmula para calcular a entropia de Shannon:  
  
 H(X) = -∑ P(xi) log(P(xi))  
  
 Esse método de pontuação está disponível para atributos discretos e diferenciados.  
  
#### <a name="bayesian-with-k2-prior"></a>Bayesian com K2 a priori  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Data Mining fornece duas pontuações para seleção de recursos que se baseiam em redes Bayesianas. Uma rede Bayesiana é um gráfico *direcionado* ou *acíclico* de estados e transições entre estados, ou seja, alguns estados vêm sempre antes do estado atual, alguns ocorrem depois, e o gráfico não se repete nem gera um loop. Por definição, as redes Bayesianas permitem o uso do conhecimento prévio. No entanto, a questão de qual estado anterior usar no cálculo de probabilidades de estados posteriores é importante para o design, o desempenho e a precisão do algoritmo.  
  
 O algoritmo K2 para aprender com a rede Bayesiana foi desenvolvido por Cooper e Herskovits e é usado com frequência na mineração de dados. Ele é escalável e analisa diversas variáveis, mas requer ordenação das variáveis usadas como entrada. Para obter mais informações, consulte [Learning Bayesian Networks](http://research.microsoft.com/en-us/um/people/heckerman/hgc94uai.pdf) (em inglês) de Chickering, Geiger e Heckerman.  
  
 Esse método de pontuação está disponível para atributos discretos e diferenciados.  
  
#### <a name="bayesian-dirichlet-equivalent-with-uniform-prior"></a>Bayesiano Dirichlet Equivalente com Uniforme a priori  
 A pontuação BDE (Bayesiano Dirichlet Equivalente) também usa análise Bayesiana para avaliar uma rede dado um conjunto de dados. O método de pontuação do BDE foi desenvolvido por Heckerman e se baseia na métrica de BD desenvolvida por Cooper e Herskovits. A distribuição Dirichlet é uma distribuição multinomial que descreve a probabilidade condicional de cada variável da rede e possui muitas propriedades que devemos conhecer.  
  
 O método BDEU (Bayesiano Dirichlet Equivalente com Uniforme a priori) assume um caso especial da distribuição Dirichlet, na qual uma constante matemática é usada para criar uma distribuição fixa ou uniforme de estados anteriores. A pontuação do BDE também assume equivalência de probabilidade, o que significa que não se pode esperar que os dados separem estruturas equivalentes. Em outras palavras, se a pontuação de Se A Então B for igual à pontuação de Se B Então A, não será possível distinguir as estruturas com base nos dados nem deduzir a causa.  
  
 Para obter mais informações sobre redes Bayesianas e a implementação desses métodos de pontuação, consulte [Learning Bayesian Networks](http://research.microsoft.com/en-us/um/people/heckerman/hgc94uai.pdf)(em inglês).  
  
### <a name="feature-selection-methods-per-algorithm"></a>Métodos de seleção de recursos por algoritmo  
 A tabela a seguir lista os algoritmos que suportam a seleção de recursos, os métodos de seleção de recursos usados por eles e os parâmetros que você define para controlar o comportamento da seleção de recursos:  
  
|Algoritmo|Método de análise|Comentários|  
|---------------|------------------------|--------------|  
|Naive Bayes|entropia de Shannon<br /><br /> Bayesian com K2 a priori<br /><br /> Bayesian Dirichlet com uniforme a priori (padrão)|O algoritmo Microsoft Naïve Bayes aceita somente atributos discretos ou diferenciados; portanto, não pode usar a pontuação de interesse.<br /><br /> Para obter mais informações sobre esse algoritmo, consulte [Microsoft Naive Bayes Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm-technical-reference.md).|  
|Árvores de decisão|Pontuação de interesse<br /><br /> Entropia de Shannon<br /><br /> Bayesian com K2 a priori<br /><br /> Bayesian Dirichlet com uniforme a priori (padrão)|Se qualquer coluna contiver valores contínuos não binários, a pontuação de interesse será usada em todas as colunas para garantir a consistência. Caso contrário, será usado o método de seleção de recursos padrão ou o método que você especificou quando criou o modelo.<br /><br /> Para obter mais informações sobre esse algoritmo, consulte [Microsoft Decision Trees Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-decision-trees-algorithm-technical-reference.md).|  
|Rede neural|Pontuação de interesse<br /><br /> Entropia de Shannon<br /><br /> Bayesian com K2 a priori<br /><br /> Bayesian Dirichlet com uniforme a priori (padrão)|O algoritmo Redes Neurais da Microsoft pode usar ambos os métodos Bayesiano e baseado em entropia, desde que os dados contenham colunas contínuas.<br /><br /> Para obter mais informações sobre esse algoritmo, consulte [Microsoft Neural Network Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md).|  
|Regressão logística|Pontuação de interesse<br /><br /> Entropia de Shannon<br /><br /> Bayesian com K2 a priori<br /><br /> Bayesian Dirichlet com uniforme a priori (padrão)|Embora o algoritmo de Regressão Logística da Microsoft se baseie no algoritmo Rede Neural da Microsoft, você não pode personalizar modelos de regressão logística para controlar o comportamento de seleção de recursos; portanto, a seleção de recursos sempre usa o método mais apropriado para o atributo por padrão.<br /><br /> Se todos os atributos forem discretos ou diferenciados, o padrão será BDEU.<br /><br /> Para obter mais informações sobre esse algoritmo, consulte [Microsoft Logistic Regression Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md).|  
|Clustering|Pontuação de interesse|O algoritmo Microsoft Clustering pode usar dados discretos ou diferenciados. No entanto, como a pontuação de cada atributo é calculada como uma distância e representada como um número contínuo, a pontuação de interesse deve ser usada.<br /><br /> Para obter mais informações sobre esse algoritmo, consulte [Microsoft Clustering Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md).|  
|Regressão linear|Pontuação de interesse|O algoritmo de Regressão Linear da Microsoft pode usar somente a pontuação de interesse, pois suporta apenas colunas contínuas.<br /><br /> Para obter mais informações sobre esse algoritmo, consulte [Microsoft Linear Regression Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md).|  
|Regras de associação<br /><br /> Clustering de sequências|Não usado|A seleção de recursos não é invocada com esses algoritmos.<br /><br /> No entanto, você poderá controlar o comportamento do algoritmo e reduzir o tamanho dos dados de entrada se necessário, configurando o valor dos parâmetros MINIMUM_SUPPORT e MINIMUM_PROBABILIITY.<br /><br /> Para obter mais informações, consulte [Microsoft Association Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md) e [Microsoft Sequence Clustering Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md).|  
|Série temporal|Não usado|A seleção de recursos não se aplica a modelos de série temporal.<br /><br /> Para obter mais informações sobre esse algoritmo, consulte [Microsoft Time Series Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md).|  
  
## <a name="feature-selection-parameters"></a>Parâmetros de seleção de recursos  
 Nos algoritmos que suportam a seleção de recursos, é possível controlar quando a seleção de recursos é ativada usando os parâmetros a seguir. Cada algoritmo tem um valor padrão para o número de entradas permitidas, mas você pode substituir esse padrão e especificar o número de atributos. Esta seção lista os parâmetros que são fornecidos para gerenciar a seleção de recursos.  
  
#### <a name="maximuminputattributes"></a>MAXIMUM_INPUT_ATTRIBUTES  
 Se o modelo tiver mais colunas do que o número especificado no parâmetro *MAXIMUM_INPUT_ATTRIBUTES* , o algoritmo ignorará as colunas calculadas como não interessantes.  
  
#### <a name="maximumoutputattributes"></a>MAXIMUM_OUTPUT_ATTRIBUTES  
 Da mesma forma, se o modelo tiver mais colunas previsíveis do que o número especificado no parâmetro *MAXIMUM_OUTPUT_ATTRIBUTES* , o algoritmo ignorará as colunas calculadas como não interessantes.  
  
#### <a name="maximumstates"></a>MAXIMUM_STATES  
 Se um modelo tiver mais casos que os especificado no parâmetro *MAXIMUM_STATES* , os estados menos populares serão agrupados para tratados como ausentes. Se qualquer um desses parâmetros for definido como 0, a seleção de recursos será desativada, o que afeta o tempo de processamento e o desempenho.  
  
 Além destes métodos para seleção de recursos, você pode melhorar a capacidade de o algoritmo identificar ou promover atributos significativos definindo *sinalizadores de modelagem* no modelo ou definindo *sinalizadores de distribuição* na estrutura. Para obter mais informações sobre esses conceitos, consulte [Sinalizadores de modelagem &#40;Data Mining&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md) e [Distribuições de colunas &#40;Data Mining&#41;](../../analysis-services/data-mining/column-distributions-data-mining.md).  
  
## <a name="see-also"></a>Consulte também  
 [Personalizar os modelos de mineração e a estrutura](../../analysis-services/data-mining/customize-mining-models-and-structure.md)  
  
  

