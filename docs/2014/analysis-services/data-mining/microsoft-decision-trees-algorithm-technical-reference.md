---
title: Referência técnica do algoritmo de árvores de decisão da Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MAXIMUM_INPUT_ATTRIBUTES parameter
- SPLIT_METHOD parameter
- MINIMUM_SUPPORT parameter
- MAXIMUM_OUTPUT_ATTRIBUTES parameter
- FORCED_REGRESSOR parameter
- decision tree algorithms [Analysis Services]
- decision trees [Analysis Services]
- COMPLEXITY_PENALTY parameter
- SCORE_METHOD parameter
ms.assetid: 1e9f7969-0aa6-465a-b3ea-57b8d1c7a1fd
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: edb2b9790ac2294f53c26b65e9897064f4050083
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019752"
---
# <a name="microsoft-decision-trees-algorithm-technical-reference"></a>Referência técnica do algoritmo Árvores de Decisão da Microsoft
  O algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] é um híbrido que incorpora métodos diferentes para a criação de uma árvore e dá suporte a várias tarefas analíticas, incluindo regressão, classificação e associação. O algoritmo Árvores de Decisão da Microsoft é dá suporte à modelagem de atributos discretos e contínuos.  
  
 Este tópico explica a implementação do algoritmo, descreve como personalizar o comportamento do algoritmo para tarefas diferentes e fornece links para informações adicionais sobre como consultar modelos de árvore de decisão.  
  
## <a name="implementation-of-the-decision-trees-algorithm"></a>Implementação do algoritmo Árvores de Decisão  
 O algoritmo Árvores de Decisão da Microsoft aplica a abordagem Bayesiana para aprender os modelos de interação causal obtendo distribuições posteriores aproximadas dos modelos. Para obter uma explicação detalhada dessa abordagem, consulte o documento no site do Microsoft Research, por [Estrutura e aprendizado de parâmetro](http://go.microsoft.com/fwlink/?LinkId=237640&clcid=0x409).  
  
 A metodologia para avaliar o valor das informações *a priori* necessárias para o aprendizado se baseia na suposição da *equivalência de probabilidade*. Essa pressuposição afirma que os dados não devem ajudar a discriminar estruturas de rede que de outra forma representam as mesmas asserções de independência condicional. Pressupõe-se que cada caso tenha uma única rede Bayesiana a priori e uma única medida de confiança para essa rede.  
  
 Com o uso dessas redes a priori, o algoritmo calcula as *probabilidades posteriores* relativas das estruturas de rede, de acordo com os dados de treinamento atuais, e identifica as estruturas de rede que têm as probabilidades posteriores mais altas.  
  
 O algoritmo Árvores de Decisão da Microsoft usa métodos diferentes para calcular a melhor árvore. O método usado depende da tarefa que pode ser regressão linear, classificação ou análise de associação. Um único modelo pode conter várias árvores para atributos previsíveis diferentes. Além disso, cada árvore pode conter várias ramificações, de acordo com a quantidade de atributos e valores nos dados. A forma e a intensidade da árvore criada em um determinado modelo dependem do método de pontuação e de outros parâmetros utilizados. Alterações aos parâmetros também podem afetar o local em que os nós são divididos.  
  
### <a name="building-the-tree"></a>Criando a árvore  
 Quando o algoritmo Árvores de Decisão da Microsoft cria o conjunto de valores de entrada possíveis, ele executa *feature selection* para identificar os atributos e os valores que fornecem a maioria das informações e remove da consideração os valores que são muito raros. O algoritmo também agrupa valores em *compartimentos*, para criar agrupamentos de valores que podem ser processados como uma unidade para otimizar o desempenho.  
  
 Uma árvore é criada com a determinação das correlações entre uma entrada e o resultado pretendido. Depois que todos os atributos tiverem sido correlacionados, o algoritmo identificará o único atributo que separa mais claramente os resultados. Este ponto da melhor separação é medido com o uso de uma equação que calcula o ganho de informações. o atributo com a melhor pontuação de ganho de informações é usado para dividir os casos em subconjuntos, que são analisados recursivamente pelo mesmo processo, até que não seja mais possível dividir a árvore.  
  
 A equação exata usada para avaliar o ganho de informações depende dos parâmetros definidos quando você criou o algoritmo, do tipo de dados da coluna previsível e do tipo de dados da entrada.  
  
### <a name="discrete-and-continuous-inputs"></a>Entradas discretas e contínuas  
 Quando o atributo previsível é discreto e as entradas previsíveis também, contar os resultados por entrada é uma questão de criar uma matriz e gerar pontuações para cada célula na matriz.  
  
 No entanto, quando o atributo previsível é discreto e as entradas são contínuas, a entrada das colunas contínuas é discreta automaticamente. Você pode aceitar o padrão e fazer com que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] encontre o número ideal de compartimentos ou pode controlar a maneira pela qual as entradas contínuas são discretizadas definindo as propriedades <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> e <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> . Para obter mais informações, consulte [Alterar a discretização de uma coluna em um modelo de mineração](change-the-discretization-of-a-column-in-a-mining-model.md).  
  
 No caso de atributos contínuos, o algoritmo usa a regressão linear para determinar onde uma árvore de decisão se divide.  
  
 Quando o atributo previsível é um tipo de dados numérico contínuo, a seleção de recursos é aplicada às saídas também, para reduzir o número possível de resultados e criar o modelo mais rapidamente. Você pode alterar o limite de seleção de recursos e, portanto, aumentar ou diminuir o número de valores possíveis configurando o parâmetro MAXIMUM_OUTPUT_ATTRIBUTES.  
  
 Para obter uma explicação mais detalhada sobre como o algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] funciona com colunas previsíveis distintas, consulte [Aprendendo sobre redes Bayesianas: A combinação de dados de conhecimento e estatísticos](http://go.microsoft.com/fwlink/?LinkId=45963). Para obter mais informações sobre como o algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] funciona com uma coluna previsível contínua, consulte o apêndice de [Modelos de árvore de regressão automática para análise de série temporal](http://go.microsoft.com/fwlink/?LinkId=45966).  
  
### <a name="scoring-methods-and-feature-selection"></a>Métodos de pontuação e seleção de recursos  
 O algoritmo Árvores de Decisão da Microsoft oferece três fórmulas para ganho de informações de pontuação: entropia de Shannon, rede Bayesiana com K2 a priori e rede Bayesiana com uma distribuição Dirichlet uniforme a priori. Todos os três métodos são bem-estabelecidos no campo de mineração de dados. É recomendável fazer experiências com parâmetros e métodos de pontuação diferentes para determinar aqueles que fornecem os melhores resultados. Para obter mais informações sobre esses métodos de pontuação, consulte [Feature Selection](../../sql-server/install/feature-selection.md).  
  
 Todos os algoritmos de mineração de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usam seleção de recursos automaticamente para melhorar a análise e reduzir a carga de processamento. O método usado para seleção de recursos depende do algoritmo utilizado para criar o modelo. Os parâmetros de algoritmo que controlam seleção de recursos para um modelo de árvores de decisão são MAXIMUM_INPUT_ATTRIBUTES e MAXIMUM_OUTPUT.  
  
|Algoritmo|Método de análise|Comentários|  
|---------------|------------------------|--------------|  
|Árvores de decisão|Pontuação de interesse<br /><br /> Entropia de Shannon<br /><br /> Bayesian com K2 a priori<br /><br /> Bayesian Dirichlet com uniforme a priori (padrão)|Se qualquer coluna contiver valores contínuos não binários, a pontuação de interesse será usada em todas as colunas para garantir a consistência. Caso contrário, será usado o método padrão ou o especificado.|  
|Regressão Linear|Pontuação de interesse|A Regressão Linear usa apenas o interesse, pois suporta apenas colunas contínuas.|  
  
### <a name="scalability-and-performance"></a>Escalabilidade e desempenho  
 A classificação é uma estratégia de mineração de dados importante. Em geral, a quantidade de informações necessária para classificar os casos aumenta em proporção direta ao número de registros de entrada. Isso limita o tamanho dos dados que podem ser classificados. O algoritmo Árvores de Decisão da Microsoft usa os seguintes métodos para resolver esses problemas, melhorar o desempenho e eliminar as restrições de memória:  
  
-   Seleção de recursos para otimizar a seleção dos atributos.  
  
-   Pontuação Bayesiana para controlar o crescimento da árvore.  
  
-   Otimização de compartimentos para atributos contínuos.  
  
-   Agrupamento dinâmico de valores de entrada para determinar os valores mais importantes.  
  
 O algoritmo Árvores de Decisão da Microsoft é rápido e escalonável, e foi projetado para paralelização fácil, o que significa que todos os processadores funcionam em conjunto para criar um único modelo consistente. A combinação dessas características torna o classificador de árvore de decisão uma ferramenta ideal para mineração de dados.  
  
 Se as restrições de desempenho forem graves, talvez você possa melhorar o tempo de processamento durante o treinamento de um modelo de árvore de decisão usando os métodos a seguir. No entanto, se você fizer isso, saiba que eliminar atributos para melhorar o desempenho de processamento alterará os resultados do modelo e possivelmente o tornará menos representativo da população total.  
  
-   Aumente o valor do parâmetro COMPLEXITY_PENALTY para limitar o crescimento de árvore.  
  
-   Limite o número de itens em modelos de associação para limitar o número de árvores criadas.  
  
-   Aumente o valor do parâmetro MINIMUM_SUPPORT para evitar sobreajuste.  
  
-   Restrinja o número de valores discretos de qualquer atributo para 10 ou menos. Você pode tentar agrupar valores de modos diferentes em modelos diferentes.  
  
    > [!NOTE]  
    >  É possível usar as ferramentas de exploração de dados disponíveis no  [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] para visualizar a distribuição de valores nos dados e agrupar os valores apropriadamente antes de iniciar a mineração de dados. Para obter mais informações, consulte [Tarefa e Visualizador de Criação de Perfil de Dados](../../integration-services/control-flow/data-profiling-task-and-viewer.md). Também é possível usar os [Suplementos de Mineração de Dados para Excel 2007](http://www.microsoft.com/downloads/details.aspx?FamilyID=7C76E8DF-8674-4C3B-A99B-55B17F3C4C51)para explorar, agrupar e rotular novamente os dados no Microsoft Excel.  
  
## <a name="customizing-the-decision-trees-algorithm"></a>Personalizando o algoritmo Árvores de Decisão  
 O algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] tem suporte para parâmetros que afetam o desempenho e a precisão do modelo de mineração resultante. Também é possível definir sinalizadores de modelagem nas colunas do modelo de mineração ou da estrutura de mineração para controlar a maneira como os dados são processados.  
  
> [!NOTE]  
>  O algoritmo Árvores de Decisão da Microsoft está disponível em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; no entanto, alguns parâmetros avançados para personalizar o comportamento do algoritmo Árvores de Decisão da Microsoft estão disponíveis para uso apenas em edições específicas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Recursos com suporte nas edições do SQL Server 2012](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473).  
  
### <a name="setting-algorithm-parameters"></a>Definindo parâmetros de algoritmo  
 A tabela a seguir descreve os parâmetros que você pode usar com o algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 *COMPLEXITY_PENALTY*  
 Controla o crescimento da árvore de decisão. Um valor baixo aumenta o número de divisões e um valor alto diminui o número de divisões. O valor padrão se baseia no número de atributos de um determinado modelo, conforme descrito na lista a seguir:  
  
-   Para os atributos 1 a 9, o padrão é 0,5.  
  
-   Para 10 a 99 atributos, o padrão é 0,9.  
  
-   Para 100 ou mais atributos, o padrão é 0,99.  
  
 *FORCE_REGRESSOR*  
 Força o algoritmo a usar as colunas especificadas como regressores, independentemente da sua importância quando calculadas pelo algoritmo. Esse parâmetro é usado apenas para árvores de decisão que preveem um atributo contínuo.  
  
> [!NOTE]  
>  Ao definir esse parâmetro, você força o algoritmo a tentar usar o atributo como um regressor. No entanto, se o atributo será realmente usado como um regressor no modelo final dependerá dos resultados da análise. Você pode descobrir quais colunas foram usadas como regressores consultando o conteúdo do modelo.  
  
 [Disponível somente em algumas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ]  
  
 *MAXIMUM_INPUT_ATTRIBUTES*  
 Define o número de atributos de entrada que o algoritmo pode manipular antes de invocar a seleção de recurso.  
  
 O padrão é 255.  
  
 Defina este valor como 0 para desativar a seleção de recursos.  
  
 [Disponível somente em algumas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
  
 *MAXIMUM_OUTPUT_ATTRIBUTES*  
 Define o número de atributos de saída que o algoritmo pode manipular antes de invocar a seleção de recurso.  
  
 O padrão é 255.  
  
 Defina este valor como 0 para desativar a seleção de recursos.  
  
 [Disponível somente em algumas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
  
 *MINIMUM_SUPPORT*  
 Determina o número mínimo de casos folha necessário para gerar uma divisão na árvore de decisão.  
  
 O padrão é 10.  
  
 Talvez seja necessário aumentar esse valor se o conjunto de dados for muito grande, para evitar treinamento excessivo.  
  
 *SCORE_METHOD*  
 Determina o método usado para calcular a pontuação da divisão. As seguintes opções estão disponíveis:  
  
|ID|Nome|  
|--------|----------|  
|1|Entropia|  
|3|Bayesian com K2 a priori|  
|4|Bayesiano Dirichlet Equivalente (BDE) com uniforme a priori<br /><br /> (padrão)|  
  
 O padrão é 4 ou BDE.  
  
 Para obter uma explicação desses métodos de pontuação, consulte [Feature Selection](../../sql-server/install/feature-selection.md).  
  
 *SPLIT_METHOD*  
 Determina o método usado para dividir o nó. As seguintes opções estão disponíveis:  
  
|ID|Nome|  
|--------|----------|  
|1|**Binary:** Indica que, independentemente do número real de valores do atributo, a árvore deverá ser dividida em duas ramificações.|  
|2|**Complete:** Indica que a árvore pode criar tantas divisões quanto há valores de atributo.|  
|3|**Both:** Especifica que o Analysis Services pode determinar se uma divisão binária ou completa deve ser usada para produzir os melhores resultados.|  
  
 O padrão é 3.  
  
### <a name="modeling-flags"></a>Sinalizadores de modelagem  
 O algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] oferece suporte aos seguintes sinalizadores de modelagem. Ao criar um modelo ou uma estrutura de mineração, você define sinalizadores de modelagem para especificar como os valores em cada coluna são manipulados durante a análise. Para obter mais informações, consulte [Sinalizadores de modelagem &#40;Mineração de dados&#41;](modeling-flags-data-mining.md).  
  
|Sinalizador de modelagem|Description|  
|-------------------|-----------------|  
|MODEL_EXISTENCE_ONLY|Significa que a coluna será tratada como tendo dois estados possíveis: `Missing` e `Existing`. Nulo é um valor ausente.<br /><br /> Aplica-se às colunas de modelo de mineração.|  
|NOT NULL|Indica que a coluna não pode conter um nulo. Um erro ocorrerá se o Analysis Services encontrar um valor nulo durante o treinamento do modelo.<br /><br /> Aplica-se às colunas de estrutura de mineração.|  
  
### <a name="regressors-in-decision-tree-models"></a>Regressores em modelos de árvore de decisão  
 Mesmo que você não use o algoritmo Regressão Linear da [!INCLUDE[msCoName](../../includes/msconame-md.md)] , qualquer modelo de árvore de decisão que tenha entradas e saídas numéricas contínuas poderá incluir nós que representem uma regressão em um atributo contínuo.  
  
 Não é necessário especificar que uma coluna de dados numéricos contínuos representa um regressor. O algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] usará automaticamente a coluna como um regressor potencial e particionará o conjunto de dados em regiões com padrões significativos, mesmo que você não defina o sinalizador REGRESSOR na coluna.  
  
 No entanto, você pode usar o parâmetro FORCE_REGRESSOR para garantir que o algoritmo utilizará um determinado regressor. Esse parâmetro só pode ser usado com os algoritmos Árvores de decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] e Regressão Linear da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Quando você define o sinalizador de modelagem, o algoritmo tenta encontrar equações de regressão de forma um * C1 + b\*C2 +... para ajustar os padrões em nós da árvore. A soma dos restos é calculada e, se o desvio for muito grande, será forçada uma divisão da árvore.  
  
 Por exemplo, se você estiver prevendo o comportamento de compra dos clientes usando a **Renda** como um atributo e definir o sinalizador de modelagem REGRESSOR na coluna, o algoritmo primeiro tentará adequar os valores de **Renda** usando uma fórmula de regressão padrão. Se o desvio for muito grande, a fórmula de regressão será abandonada e a árvore será dividida em outro atributo. O algoritmo de árvore de decisão tentará ajustar um regressor para renda em cada uma das ramificações após a divisão.  
  
## <a name="requirements"></a>Requisitos  
 Um modelo de árvore de decisão deve conter uma coluna de chave, colunas de entrada e pelo menos uma coluna previsível.  
  
### <a name="input-and-predictable-columns"></a>Colunas de entrada e colunas previsíveis  
 O algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] oferece suporte a colunas de entrada e colunas previsíveis específicas que são listadas na tabela a seguir. Para obter mais informações sobre o significado dos tipos de conteúdo quando usados em um modelo de mineração, consulte [Tipos de conteúdo &#40;Mineração de dados&#41;](content-types-data-mining.md).  
  
|coluna|Tipos de conteúdo|  
|------------|-------------------|  
|Atributo de entrada|Contínuo, cíclico, discreto, diferenciado, chave, ordenado, tabela|  
|Atributo previsível|Contínuo, cíclico, discreto, diferenciado, ordenado, tabela|  
  
> [!NOTE]  
>  Os tipos de conteúdo Cíclico e Ordenado têm suporte, mas o algoritmo os trata como valores discretos e não executa processamento especial.  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmo de árvores de decisão da Microsoft](microsoft-decision-trees-algorithm.md)   
 [Exemplos de consulta de modelo de árvores de decisão](decision-trees-model-query-examples.md)   
 [Conteúdo do modelo de árvore de decisão de mineração &#40;Analysis Services – mineração de dados&#41;](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)  
  
  