---
title: Conteúdo do modelo de mineração (Analysis Services – mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- algorithms [data mining]
- standard deviation
- confidence scores [data mining]
- mining models [Analysis Services]
- variance
- machine learning algorithms [Analysis Services]
- model content
- support [data mining]
- node distribution
ms.assetid: e7c039f6-3266-4d84-bfbd-f99b6858acf4
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1b7932b90770b7217944beaf1d4cb0d826ee853b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mining-model-content-analysis-services---data-mining"></a>Mining Model Content (Analysis Services - Data Mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Depois de projetar e processar um modelo de mineração usando dados da estrutura de mineração subjacente, o modelo de mineração é concluído e contém o *conteúdo do modelo de mineração*. Você pode usar este conteúdo para fazer previsões ou analisar seus dados.  
  
 O conteúdo do modelo de mineração inclui metadados sobre o modelo, estatísticas sobre os dados e padrões descobertos pelo algoritmo de mineração. Dependendo do algoritmo usado, o conteúdo do modelo pode incluir fórmulas de regressão, as definições das regras e dos conjuntos de itens ou pesos e outras estatísticas.  
  
 Independentemente do algoritmo que foi usado, o conteúdo do modelo de mineração é apresentado em uma estrutura padrão. Você pode navegar pela estrutura no Visualizador de Árvore de Conteúdo Genérica da Microsoft, fornecido no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]e, em seguida, alternar para um dos visualizadores personalizados e ver como as informações são interpretadas e exibidas graficamente para cada tipo de modelo. Você também pode criar consultas relacionadas ao conteúdo do modelo de mineração usando qualquer cliente que dê suporte ao conjunto de linhas de esquema MINING_MODEL_CONTENT. Para obter mais informações, consulte [Tarefas e instruções de consulta de Data Mining](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md).  
  
 Esta seção descreve a estrutura básica do conteúdo fornecida para todos os tipos de modelos de mineração. Descreve os tipos de nós que são comuns a todos os conteúdos de modelo de mineração e fornece orientação para interpretar as informações.  
  
 [Estrutura do conteúdo do modelo de mineração](#bkmk_Structure)  
  
 [Nós no conteúdo do modelo](#bkmk_Nodes)  
  
 [Conteúdo do modelo de mineração por tipo de algoritmo](#bkmk_AlgoType)  
  
 [Ferramentas para exibir o conteúdo do modelo de mineração](#bkmk_Viewing)  
  
 [Ferramentas para consultar o conteúdo do modelo de mineração](#bkmk_Querying)  
  
##  <a name="bkmk_Structure"></a> Estrutura do conteúdo do modelo de mineração  
 O conteúdo de cada modelo é apresentado como uma série de *nós*. Um nó é um objeto dentro de um modelo de mineração que contém metadados e informações sobre uma parte do modelo. Os nós são organizados em uma hierarquia. A organização exata de nós na hierarquia e o significado da hierarquia dependem do algoritmo utilizado. Por exemplo, se você criar um modelo de árvores de decisão, esse modelo pode conter várias árvores, todas conectadas à raiz do modelo; se você criar um modelo de rede neural, esse modelo pode conter uma ou mais redes, além de um nó de estatísticas.  
  
 O primeiro nó de cada modelo é chamado de *nó raiz*ou nó *pai do modelo* . Todo modelo tem um nó raiz (NODE_TYPE = 1). O nó raiz normalmente contém alguns metadados sobre o modelo e o número de nós filho, além de algumas outras informações sobre os padrões identificadas pelo modelo.  
  
 Dependendo do algoritmo usado para criar o modelo, o nó raiz tem um número variado de nós filho. Nós filho têm significados diferentes e contêm conteúdo diferente, dependendo do algoritmo e da profundidade e complexidade dos dados.  
  
##  <a name="bkmk_Nodes"></a> Nós no conteúdo do modelo de mineração  
 Em um modelo de mineração, um nó é um contêiner de uso general que armazena algumas informações sobre todo ou parte do modelo. A estrutura de cada nó sempre é a mesma e contém as colunas definidas pelo conjunto de linhas de esquema de mineração de dados. Para obter mais informações, consulte [Conjunto de linhas DMSCHEMA_MINING_MODEL_CONTENT](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md).  
  
 Cada nó inclui metadados sobre o nó, incluindo um identificador que é exclusivo de cada modelo, a ID do nó pai e o número de nós filho que o nó tem. Os metadados identificam o modelo ao qual o nó pertence e o catálogo de banco de dados onde aquele modelo específico é armazenado. O conteúdo adicional fornecido no nó é diferente, dependendo do tipo de algoritmo usado para criar o modelo e poderia incluir o seguinte:  
  
-   Contagem de casos nos dados de treinamento que dá suporte a um valor específico previsto.  
  
-   Estatísticas, como média, desvio padrão ou variância.  
  
-   Coeficientes e fórmulas.  
  
-   Definição de regras e ponteiros laterais.  
  
-   Fragmentos XML que descrevem uma parte do modelo.  
  
### <a name="list-of-mining-content-node-types"></a>Lista dos tipos de nó do conteúdo de mineração  
 A tabela seguinte lista os tipos diferentes de nós que são produzidos em modelos de mineração de dados. Como cada algoritmo processa informações de modo diferente, cada modelo gera só alguns tipos específicos de nós. Se você alterar o algoritmo, o tipo de nós poderá ser alterado. Além disso, se você reprocessar o modelo, o conteúdo de cada nó poderá ser alterado.  
  
> [!NOTE]  
>  Se você usar um serviço de mineração de dados diferente, ou se você criar seus próprios algoritmos de plug-in, tipos de nós personalizados adicionais podem estar disponíveis.  
  
|ID DE NODE_TYPE|Rótulo do nó|Conteúdo do nó|  
|-------------------|----------------|-------------------|  
|1|Modelo|Metadados e nó raiz de conteúdo. Aplica-se a todos os tipos de modelo.|  
|2|trEE|Nó raiz de uma árvore de classificação. Aplica-se a modelos de árvore de decisão.|  
|3|Interior|Nó interno dividido em uma árvore. Aplica-se a modelos de árvore de decisão.|  
|4|Distribuição|Nó terminal de uma árvore. Aplica-se a modelos de árvore de decisão.|  
|5|Cluster|Cluster detectado pelo algoritmo. Aplica-se a modelos de clustering e a modelos de clustering de sequências.|  
|6|Unknown (desconhecido)|Tipo de nó desconhecido.|  
|7|Conjunto de itens|Conjunto de itens detectado pelo algoritmo. Aplica-se a modelos de associação ou a modelos de clustering de sequências.|  
|8|AssociationRule|Regra de associação detectada pelo algoritmo. Aplica-se a modelos de associação ou a modelos de clustering de sequências.|  
|9|PredictableAttribute|Atributo previsível. Aplica-se a todos os tipos de modelo.|  
|10|InputAttribute|Atributo de entrada. Aplica-se a árvores de decisão e a modelos Naïve Bayes.|  
|11|InputAttributeState|Estatísticas sobre os estados de um atributo de entrada. Aplica-se a árvores de decisão e a modelos Naïve Bayes.|  
|13|Sequência|Nó superior para um componente do modelo Markov de um clustering de sequências. Aplica-se a modelos de clustering de sequências.|  
|14|Transição|Matriz de transição Markov. Aplica-se a modelos de clustering de sequências.|  
|15|TimeSeries|Nó não raiz de uma árvore de série temporal. Aplica-se somente a modelos de série temporal.|  
|16|TsTree|Nó raiz de uma árvore de série temporal que corresponde a uma série temporal previsível. Aplica-se a modelos de série temporal e só se o modelo tiver sido criado com o parâmetro MIXED.|  
|17|NNetSubnetwork|Uma sub-rede. Aplica-se a modelos de rede neural.|  
|18|NNetInputLayer|Grupo que contém os nós da camada de entrada. Aplica-se a modelos de rede neural.|  
|19|NNetHiddenLayer|Grupos que contêm os nós que descrevem a camada oculta. Aplica-se a modelos de rede neural.|  
|21|NNetOutputLayer|Grupos que contêm os nós da camada de saída. Aplica-se a modelos de rede neural.|  
|21|NNetInputNode|Nó na camada de entrada que corresponde a um atributo de entrada com os estados correspondentes. Aplica-se a modelos de rede neural.|  
|22|NNetHiddenNode|Nó na camada oculta. Aplica-se a modelos de rede neural.|  
|23|NNetOutputNode|Nó na camada de saída. Este nó normalmente corresponde a um atributo de saída e aos estados correspondentes. Aplica-se a modelos de rede neural.|  
|24|NNetMarginalNode|Estatísticas marginais sobre o conjuntos de treinamento. Aplica-se a modelos de rede neural.|  
|25|RegressionTreeRoot|Raiz de uma árvore de regressão. Aplica-se a modelos de regressão linear e a modelos de árvore de decisão que contêm atributos de entrada contínuos.|  
|26|NaiveBayesMarginalStatNode|Estatísticas marginais sobre o conjuntos de treinamento. Aplica-se a modelos Naïve Bayes.|  
|27|ArimaRoot|Nó raiz de um modelo ARIMA. Aplica-se apenas a modelos de série temporal que usam o algoritmo ARIMA.|  
|28|ArimaPeriodicStructure|Uma estrutura periódica em um modelo ARIMA. Aplica-se apenas a modelos de série temporal que usam o algoritmo ARIMA.|  
|29|ArimaAutoRegressive|Coeficiente de regressão automática para um único termo em um modelo ARIMA.<br /><br /> Aplica-se apenas a modelos de série temporal que usam o algoritmo ARIMA.|  
|30|ArimaMovingAverage|Coeficiente de média de movimentação para um único termo em um modelo ARIMA. Aplica-se apenas a modelos de série temporal que usam o algoritmo ARIMA.|  
|1.000|CustomBase|Ponto de partida para tipos de nós personalizados. Os tipos de nós personalizados devem ser inteiros maiores do que esta constante. Aplica-se a modelos criados com algoritmos de plug-in personalizados.|  
  
### <a name="node-id-name-caption-and-description"></a>ID, nome, legenda e descrição do nó  
 O nó raiz de qualquer modelo sempre tem a ID exclusiva (**NODE_UNIQUE_NAME**) igual a 0. Todas as IDs de nó são atribuídas automaticamente pelo Analysis Services e não podem ser modificadas.  
  
 O nó raiz de cada modelo também contém alguns metadados básicos sobre o modelo. Estes metadados incluem o banco de dados do Analysis Services em que o modelo é armazenado (**MODEL_CATALOG**), o esquema (**MODEL_SCHEMA)** e o nome do modelo (**MODEL_NAME)**. No entanto, essas informações são repetidas em todos os nós do modelo, de modo que não é necessário consultar o nó raiz para obter esses metadados.  
  
 Além de um nome usado como o identificador exclusivo, cada nó tem um *nome* (**NODE_NAME**). Este nome é criado automaticamente pelo algoritmo para propósitos de exibição e não pode ser editado.  
  
> [!NOTE]  
>  O algoritmo Microsoft Clustering permite que os usuários atribuam nomes amigáveis a cada cluster. Porém, estes nomes amigáveis não são persistidos no servidor e, se você reprocessar o modelo, o algoritmo vai gerar novos nomes de cluster.  
  
 A *legenda* e a *descrição* de cada nó são geradas automaticamente pelo algoritmo e servem como rótulos para ajudar você a entender o conteúdo do nó. O texto gerado para cada campo depende do tipo de modelo. Em alguns casos, o nome, a legenda e a descrição podem conter exatamente a mesma cadeia de caracteres, mas em alguns modelos, a descrição pode conter informações adicionais. Consulte o tópico do tipo de modelo específico para obter detalhes da implementação.  
  
> [!NOTE]  
>  O servidor do Analysis Services só dá suporte à mudança de nomes de nós se você criar modelos usando um algoritmo de plug-in personalizado que implementa a mudança de nome. Para habilitar a mudança de nome, você deve substituir os métodos ao criar o algoritmo de plug-in.  
  
### <a name="node-parents-node-children-and-node-cardinality"></a>Pais, filhos e cardinalidade de nó  
 A relação entre nós pai e filhos em uma estrutura de árvore é determinada pelo valor da coluna PARENT_UNIQUE_NAME. Este valor é armazenado no nó filho e informa a ID do nó pai. Alguns exemplos a seguir mostram como essas informações poderiam ser usadas:  
  
-   Um PARENT_UNIQUE_NAME que é NULL indica que o nó é o nó superior do modelo.  
  
-   Se o valor de PARENT_UNIQUE_NAME for 0, o nó deve ser um descendente direto do nó superior no modelo. Isto porque a ID do nó raiz sempre é 0.  
  
-   Você pode usar funções em uma consulta DMX para localizar descendentes ou pais de um nó específico. Para obter mais informações sobre como usar funções em consultas, consulte [Consultas de Data Mining](../../analysis-services/data-mining/data-mining-queries.md).  
  
 *Cardinalidade* refere-se ao número de itens em um conjunto. No contexto de um modelo de mineração processado, a cardinalidade informa o número de filhos em um nó específico. Por exemplo, se um modelo de árvore de decisão tiver um nó para [Renda Anual] e esse nó tiver dois filhos, um para a condição [Renda Anual] = Alta e outro para a condição [Renda Anual] = Baixa, o valor de CHILDREN_CARDINALITY para o nó [Renda Anual] seria 2.  
  
> [!NOTE]  
>  No [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], somente os nós filho imediatos são contados ao calcular a cardinalidade de um nó. Porém, se você criar um algoritmo de plug-in personalizado, poderá sobrecarregar CHILDREN_CARDINALITY para contar a cardinalidade de modo diferente. Por exemplo, isto pode ser útil se você desejar contar o número total de descendentes, não apenas os filhos imediatos.  
  
 Embora a cardinalidade seja contada do mesmo modo para todos os modelos, a interpretação e o uso do valor de cardinalidade variam de acordo com o tipo de modelo. Por exemplo, em um modelo de clustering, a cardinalidade do nó superior informa o número total de clusters que foram localizados. Em outros tipos de modelos, a cardinalidade pode ter sempre um valor fixo dependendo do tipo de nó. Para obter mais informações sobre como interpretar a cardinalidade, consulte o tópico sobre o tipo de modelo específico.  
  
> [!NOTE]  
>  Além disso, alguns modelos, como os criados pelo algoritmo Rede Neural da Microsoft, contêm um tipo de nó especial que fornece estatísticas descritivas sobre os dados de treinamento do modelo inteiro. Por definição, esses nós nunca têm nós filho.  
  
### <a name="node-distribution"></a>node distribution  
 A coluna NODE_DISTRIBUTION contém uma tabela aninhada que em muitos nós fornece informações importantes e detalhadas sobre os padrões identificados pelo algoritmo. As estatísticas exatas fornecidas nesta tabela variam de acordo com o tipo de modelo, a posição do nó na árvore e o tipo de atributo previsível (um valor numérico contínuo ou um valor discreto); no entanto, essas estatísticas podem incluir os valores mínimo e máximo de um atributo, os pesos atribuídos aos valores, o número de casos em um nó, os coeficientes usados em uma fórmula de regressão e medidas estatísticas como desvio padrão e variância. Para obter mais informações sobre como interpretar a distribuição de nós, consulte o tópico do tipo específico de modelo com o qual você está trabalhando.  
  
> [!NOTE]  
>  A tabela NODE_DISTRIBUTION pode ser vazia, dependendo do tipo de nó. Por exemplo, alguns nós só servem para organizar uma coleção de nós filho e são os nós filho que contêm as estatísticas detalhadas.  
  
 A tabela aninhada, NODE_DISTRIBUTION, sempre contém as colunas seguintes. O conteúdo de cada coluna varia, dependendo do tipo de modelo. Para obter mais informações sobre tipos de modelo específicos, consulte [Conteúdo do modelo de mineração por tipo de algoritmo](#bkmk_AlgoType).  
  
 ATTRIBUTE_NAME  
 O conteúdo varia conforme o algoritmo. Pode ser o nome de uma coluna, como um atributo previsível, uma regra, um conjunto de itens ou uma parte das informações internas do algoritmo (por exemplo, parte de uma fórmula).  
  
 Esta coluna também pode conter um par de valores de atributo.  
  
 ATTRIBUTE_VALUE  
 Valor do atributo nomeado em ATTRIBUTE_NAME.  
  
 Se o nome do atributo for uma coluna, então, no caso mais simples, ATTRIBUTE_VALUE conterá um dos valores discretos para aquela coluna.  
  
 Dependendo do modo como o algoritmo processa os valores, ATTRIBUTE_VALUE também pode conter um sinalizador que informa se um valor existe para o atributo (**Existente**) ou se o valor é nulo (**Ausente**).  
  
 Por exemplo, se o seu modelo estiver configurado para encontrar clientes que adquiriram um item específico pelo menos uma vez, a coluna ATTRIBUTE_NAME poderá conter o par de valores de atributo que define o item de interesse, como `Model = 'Water bottle'`, e a coluna ATTRIBUTE_VALUE conterá somente a palavra-chave **Existente** ou **Ausente**.  
  
 SUPPORT  
 Contagem dos casos que têm este par de valores de atributo ou este conjunto de itens ou regra.  
  
 Em geral, para cada nó, o valor de suporte informa quantos casos no conjunto de treinamento estão incluídos no nó atual. Na maioria dos tipos de modelo, o suporte representa uma contagem exata de casos. Valores de suporte são úteis porque você pode exibir a distribuição de dados dentro dos casos de treinamento sem precisar consultar os dados de treinamento. O servidor do Analysis Services também usa estes valores armazenados para calcular a probabilidade armazenada versus a probabilidade anterior e determinar se a inferência é forte ou fraca.  
  
 Por exemplo, em uma árvore de classificação, o valor de suporte indica o número de casos que têm a combinação descrita de atributos.  
  
 Em uma árvore de decisão, a soma de suporte em cada nível de uma árvore é somada ao suporte do nó pai. Por exemplo, se um modelo com 1200 casos for dividido igualmente por sexo e, em seguida, subdividido igualmente por três valores de Renda (Baixa, Média e Alta), os nós filho do nó (2), que são os nós (4), (5) e (6), sempre serão somados ao mesmo número de casos do nó (2).  
  
|ID e atributos de nó|Contagem de suporte|  
|---------------------------------|-------------------|  
|(1) Raiz do modelo|1200|  
|(2) Sexo = Masculino<br /><br /> (3) Sexo = Feminino|600<br /><br /> 600|  
|(4) Sexo = Masculino e Renda = Alta<br /><br /> (5) Sexo = Masculino e Renda = Média<br /><br /> (6) Sexo = Masculino e Renda = Baixo|200<br /><br /> 200<br /><br /> 200|  
|(7) Sexo = Feminino e Renda = Alta<br /><br /> (8) Sexo = Feminino e Renda = Média<br /><br /> (9) Sexo = Feminino e Renda = Baixo|200<br /><br /> 200<br /><br /> 200|  
  
 Para um modelo de clustering, o número de suporte pode ser ponderado para incluir as probabilidades de pertencer a vários clusters. A associação de vários clusters é o método de clustering padrão. Neste cenário, como cada caso não pertence necessariamente a um único cluster, o suporte nesses modelos talvez não chegue a 100% em todos os clusters.  
  
 PROBABILITY  
 Indica a probabilidade para este nó específico dentro do modelo inteiro.  
  
 Geralmente, a probabilidade representa o suporte para este valor específico, dividido pela contagem total de casos dentro do nó (NODE_SUPPORT).  
  
 Porém, a probabilidade é ligeiramente ajustada para eliminar a polarização causada por valores ausentes nos dados.  
  
 Por exemplo, se os valores atuais para [Total de Filhos] forem “Um” e “Dois”, você talvez queira evitar a criação de um modelo que prevê a impossibilidade de ter filhos ou ter três filhos. Para assegurar que valores ausentes sejam improváveis, mas não impossíveis, o algoritmo sempre adiciona 1 à contagem de valores reais para qualquer atributo.  
  
 Exemplo:  
  
 Probabilidade de [Total de Filhos = Um] = [Contagem de casos onde Total de Filhos = Um] + 1/[Contagem de todos os casos] + 3  
  
 Probabilidade de [Total de Filhos = Dois] = [Contagem de casos onde Total de Filhos = Dois] + 1/[Contagem de todos os casos] + 3  
  
> [!NOTE]  
>  O ajuste de 3 é calculado somando-se 1 ao número total de valores existentes, n.  
  
 Depois do ajuste, a soma das probabilidades para obter todos os valores ainda é 1. A probabilidade do valor sem-dados (neste exemplo, [Total de Filhos = “Zero”, “Três” ou algum outro valor]), começa em um nível muito baixo diferente de zero e aumenta lentamente conforme mais casos são adicionados.  
  
 variance  
 Indica a variância dos valores dentro do nó. Por definição, a variância é sempre 0 para valores discretos. Se o modelo der suporte a valores contínuos, a variância será calculada como σ (sigma), usando o denominador n ou o número de casos no nó.  
  
 Há, em geral, duas definições para representar o desvio padrão (**StDev**). Um método para calcular o desvio padrão leva em conta a polarização e o outro método calcula o desvio padrão sem usar a polarização. Em geral, os algoritmos de mineração de dados da Microsoft não usam a polarização ao calcular o desvio padrão.  
  
 O valor que aparece na tabela NODE_DISTRIBUTION é o valor real para todos os atributos discretos e diferenciados e a média para valores contínuos.  
  
 VALUE_TYPE  
 Indica o tipo de dados do valor ou um atributo e o uso do valor. Certos tipos de valor só se aplicam a certos tipos de modelo:  
  
|ID de VALUE_TYPE|Rótulo do valor|Nome do tipo de valor|  
|--------------------|-----------------|---------------------|  
|1|Ausente|Indica que os dados do caso não tinham um valor para este atributo. O estado **Ausente** é calculado separadamente dos atributos que têm valores.|  
|2|Existente|Indica que os dados do caso contêm um valor para este atributo.|  
|3|Contínuo|Indica que o valor do atributo é um valor numérico contínuo e, portanto, pode ser representado por uma média, juntamente com a variância e o desvio padrão.|  
|4|Discreto|Indica um valor, numérico ou texto, que é tratado como discreto.<br /><br /> **Observação** Os valores discretos também podem ser ausentes; no entanto, eles são tratados de modo diferente durante os cálculos. Para obter mais informações, consulte [Valores ausentes&#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md).|  
|5|Discretizado|Indica que o atributo contém valores numéricos que foram diferenciados. O valor será uma cadeia de caracteres formatada que descreve os recipientes de diferenciação.|  
|6|Existente|Indica que o atributo tem valores numéricos contínuos e que os valores foram fornecidos nos dados, em comparação com os valores ausentes ou inferidos.|  
|7|Coeficiente|Indica um valor numérico que representa um coeficiente.<br /><br /> Um coeficiente é um valor que é aplicado ao calcular o valor da variável dependente. Por exemplo, se o seu modelo cria uma fórmula de regressão que prevê a renda com base na idade, o coeficiente é usado na fórmula que relaciona idade e renda.|  
|8|Ganho de pontos|Indica um valor numérico que representa o ganho de pontos para um atributo.|  
|9|Estatísticas|Indica um valor numérico que representa uma estatística para um regressor.|  
|10|Nome exclusivo do nó|Indica que o valor não deve ser tratado como numérico ou cadeia de caracteres, mas como o identificador exclusivo de outro nó de conteúdo em um modelo.<br /><br /> Por exemplo, em um modelo de rede neural, as IDs fornecem ponteiros de nós na camada de saída aos nós na camada oculta e ponteiros de nós na camada oculta aos nós na camada de entrada.|  
|11|Interceptação|Indica um valor numérico que representa a interceptação em uma fórmula de regressão.|  
|12|Periodicidade|Indica que o valor denota uma estrutura periódica em um modelo.<br /><br /> Aplica-se somente a modelos de série temporal que contêm um modelo ARIMA.<br /><br /> Observação: o algoritmo MTS detecta estruturas periódicas automaticamente com base nos dados de treinamento. Devido a isso, as periodicidades no modelo final podem incluir valores de periodicidade que não foram fornecidos como parâmetros durante a criação do modelo.|  
|13|Ordem regressiva automática|Indica que o valor representa o número de séries regressivas automáticas.<br /><br /> Aplica-se a modelos de série temporal que usam o algoritmo ARIMA.|  
|14|Ordem de média de movimentação|Representa um valor que representa o número de médias de movimentação em uma série.<br /><br /> Aplica-se a modelos de série temporal que usam o algoritmo ARIMA.|  
|15|Ordem de diferença|Indica que o valor representa um valor que indica quantas vezes a série é diferenciada.<br /><br /> Aplica-se a modelos de série temporal que usam o algoritmo ARIMA.|  
|16|Booliano|Representa um tipo Booleano.|  
|17|Outro|Representa um valor personalizado definido pelo algoritmo.|  
|18|Cadeia de caracteres pré-processada|Representa um valor personalizado que o algoritmo processa como uma cadeia de caracteres. Nenhuma formatação foi aplicada pelo modelo de objeto.|  
  
 Os tipos de valor são derivados da enumeração ADMOMD.NET. Para obter mais informações, consulte <xref:Microsoft.AnalysisServices.AdomdServer.MiningValueType>.  
  
### <a name="node-score"></a>Pontuação de nó  
 O significado da pontuação de nó varia dependendo do tipo de modelo e pode ser específico do tipo de nó. Para obter informações sobre como NODE_SCORE é calculado para cada modelo e tipo de nó, consulte [Conteúdo do modelo de mineração por tipo de algoritmo](#bkmk_AlgoType).  
  
### <a name="node-probability-and-marginal-probability"></a>Probabilidade de nó e probabilidade marginal  
 O conjunto de linhas de esquema do modelo de mineração inclui as colunas NODE_PROBABILITY e MARGINAL_PROBABILITY para todos os tipos de modelo. Essas colunas só contêm valores em nós onde um valor de probabilidade é significativo. Por exemplo, o nó raiz de um modelo nunca contém uma pontuação de probabilidade.  
  
 Nesses nós que fornecem pontuações de probabilidade, a probabilidade de nó e as probabilidades marginais representam cálculos diferentes.  
  
-   **Probabilidade marginal** é a probabilidade de alcançar o nó a partir de seu pai.  
  
-   **Probabilidade de nó** é a probabilidade de alcançar o nó a partir da raiz.  
  
-   A**probabilidade de nó** sempre é menor ou igual à **probabilidade marginal**.  
  
 Por exemplo, se a população de todos os clientes em uma árvore de decisão for dividida igualmente por sexo (e nenhum valor estiver ausente) a probabilidade dos nós filho deve ser 0,5. Porém, suponha que cada um dos nós para gênero seja dividido igualmente pelos níveis de renda (Alta, Média e Baixa). Nesse caso, a pontuação de MARGINAL_PROBABILITY para cada nó filho sempre deve ser 0,33, mas o valor de NODE_PROBABILTY será o produto de todas as probabilidades que levam a esse nó e, assim, sempre será menor que o valor de MARGINAL_PROBABILITY.  
  
|Nível de nó/atributo e valor|Probabilidade marginal|Probabilidade de nó|  
|----------------------------------------|--------------------------|----------------------|  
|Raiz do modelo<br /><br /> Todos os clientes de destino|1|1|  
|Clientes de destino divididos por sexo|.5|.5|  
|Clientes de destino divididos por sexo e divididos novamente três vezes por renda|.33|.5 * .33 = .165|  
  
### <a name="node-rule-and-marginal-rule"></a>Regra de nó e regra marginal  
 O conjunto de linhas de esquema do modelo de mineração também inclui as colunas NODE_RULE e MARGINAL_RULE para todos os tipos de modelo. Essas colunas contêm fragmentos XML que podem ser usados para serializar um modelo ou representar alguma parte da estrutura do modelo. Essas colunas podem ficar em branco para alguns nós, se um valor não for significativo.  
  
 São fornecidos dois tipos de regras XML, similares aos dois tipos de valores de probabilidade. O fragmento XML em MARGINAL_RULE define o atributo e o valor para o nó atual, enquanto o fragmento XML em NODE_RULE descreve o caminho para o nó atual da raiz do modelo.  
  
##  <a name="bkmk_AlgoType"></a> Conteúdo do modelo de mineração por tipo de algoritmo  
 Cada algoritmo armazena tipos diferentes de informações como parte de seu esquema de conteúdo. Por exemplo, o algoritmo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering gera muitos nós filho, cada um representando um possível cluster. Cada nó do cluster contém regras que descrevem características compartilhadas por itens no cluster. Em contraste, o algoritmo Regressão Linear da [!INCLUDE[msCoName](../../includes/msconame-md.md)] não contém nenhum nó filho; em vez disso, o nó pai do modelo contém a equação que descreve a relação linear identificada pela análise.  
  
 A tabela a seguir fornece links para tópicos de cada tipo de algoritmo.  
  
-   **Tópicos de conteúdo de modelo:** explicam o significado de cada tipo de nó para cada tipo de algoritmo e fornece orientações sobre quais nós são mais adequados em um determinado tipo de modelo.  
  
-   **Tópicos de consulta:** fornecem exemplos de consultas de um tipo de modelo específico e orientação para interpretar os resultados.  
  
|Algoritmo ou tipo de modelo|model content|Consultando modelos de mineração|  
|-----------------------------|-------------------|----------------------------|  
|Modelos de regras de associação|[Conteúdo do modelo de mineração para modelos de associação &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)|[Exemplos de consulta de modelo de associação](../../analysis-services/data-mining/association-model-query-examples.md)|  
|Modelos de clustering|[Conteúdo do modelo de mineração para modelos de árvore de decisão & #40; Analysis Services – mineração de dados & #41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)|[Exemplos de consulta de modelo de clustering](../../analysis-services/data-mining/clustering-model-query-examples.md)|  
|Modelo de árvores de decisão|[Conteúdo do modelo de mineração para modelos de árvore de decisão & #40; Analysis Services – mineração de dados & #41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)|[Exemplos de consulta de modelo de árvores de decisão](../../analysis-services/data-mining/decision-trees-model-query-examples.md)|  
|Modelos de regressão linear|[Conteúdo do modelo de mineração para modelos de regressão linear &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)|[Exemplos de consulta de modelo de regressão linear](../../analysis-services/data-mining/linear-regression-model-query-examples.md)|  
|Modelos de regressão logística|[Conteúdo do modelo de mineração para modelos de regressão logística &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)|[Exemplos de consulta de modelo de regressão linear](../../analysis-services/data-mining/linear-regression-model-query-examples.md)|  
|Modelos Naïve Bayes|[Conteúdo do modelo de mineração para modelos Naive Bayes & #40; Analysis Services – mineração de dados & #41;](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)|[Naive Bayes Model Query Examples](../../analysis-services/data-mining/naive-bayes-model-query-examples.md)|  
|Modelos de rede neural|[Conteúdo do modelo de mineração para modelos de rede neural &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)|[Neural Network Model Query Examples](../../analysis-services/data-mining/neural-network-model-query-examples.md)|  
|Clustering de sequências|[Conteúdo do modelo de mineração para modelos de clustering de sequência &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)|[Sequence Clustering Model Query Examples](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)|  
|Modelos de série temporal|[Conteúdo do modelo de mineração para modelos de série temporal & #40; Analysis Services – mineração de dados & #41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)|[Exemplos de consulta de modelo de série temporal](../../analysis-services/data-mining/time-series-model-query-examples.md)|  
  
##  <a name="bkmk_Viewing"></a> Ferramentas para exibir o conteúdo do modelo de mineração  
 Ao procurar ou explorar um modelo no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você poderá exibir as informações no **Visualizador de Árvore de Conteúdo Genérica da Microsoft**, disponível no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 O Visualizador de Conteúdo Genérico da [!INCLUDE[msCoName](../../includes/msconame-md.md)] exibe colunas, regras, propriedades, atributos, nós e outros conteúdos do modelo usando as mesmas informações que estão disponíveis no conjunto de linhas de esquema de conteúdo do modelo de mineração. O conjunto de linhas de esquema de conteúdo é uma estrutura genérica de apresentação de informações detalhadas sobre o conteúdo de um modelo de mineração de dados. Você pode exibir o conteúdo do modelo em qualquer cliente que dê suporte a conjuntos de linhas hierárquicos. O visualizador no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] apresenta essas informações em um visualizador de tabela HTML que representa todos os modelos em um formato consistente, facilitando a compreensão da estrutura dos modelos criados. Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Árvore de Conteúdo Genérico da Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md).  
  
##  <a name="bkmk_Querying"></a> Ferramentas para consultar o conteúdo do modelo de mineração  
 Para recuperar o conteúdo do modelo de mineração, você deve criar uma consulta do modelo de mineração de dados.  
  
 O modo mais fácil de criar uma consulta de conteúdo é executar seguinte instrução DMX no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:  
  
```  
SELECT * FROM [<mining model name>].CONTENT  
```  
  
 Para obter mais informações, consulte [Consultas de mineração de dados](../../analysis-services/data-mining/data-mining-queries.md).  
  
 Você também pode consultar o conteúdo do modelo de mineração usando os conjuntos de linhas de esquema de mineração de dados. Um conjunto de linhas de esquema é uma estrutura padrão que os clientes usam para identificar, procurar e consultar informações sobre estruturas e modelos de mineração. Você pode consultar os conjuntos de linhas de esquema usando instruções XMLA, Transact-SQL ou DMX.  
  
 No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], você também pode acessar as informações nos conjuntos de linhas de esquema de mineração de dados estabelecendo uma conexão com a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e consultando as tabelas do sistema. Para obter mais informações, consulte [Conjuntos de linhas de esquema de Data Mining &#40;SSAs&#41;](../../analysis-services/data-mining/data-mining-schema-rowsets-ssas.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visualizador de árvore de conteúdo genérica da Microsoft & #40; mineração de dados & #41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)   
 [Algoritmos de mineração de dados & #40; Analysis Services – mineração de dados & #41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
  
