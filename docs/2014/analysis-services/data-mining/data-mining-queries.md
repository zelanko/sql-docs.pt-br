---
title: Consultas de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- prediction queries [Analysis Services]
- queries [DMX], creating
- prediction queries [DMX]
- Prediction Query Builder
- mining models [Analysis Services], querying
ms.assetid: 802806a6-69bb-4c3c-b9aa-d1a1ddfc7fc2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 71704480c6c3258c2d6553c3328535ff4ea4a9cd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48197706"
---
# <a name="data-mining-queries"></a>Consultas de mineração de dados
  Consultas de mineração de dados são úteis para muitos propósitos. Você pode:  
  
-   Aplicar o modelo a novos dados, para fazer previsões únicas ou várias. Você pode fornecer valores de entrada como parâmetros, ou em um lote.  
  
-   Obter um resumo estatístico dos dados usados para treinar.  
  
-   Extrair padrões e regras ou gerar um perfil do caso típico que representa um padrão no modelo.  
  
-   Extrair fórmulas de regressão e outros cálculos que explicam padrões.  
  
-   Obter os casos que se ajustem a um padrão específico.  
  
-   Recuperar detalhes sobre casos individuais usados no modelo, incluindo dados não usados na análise.  
  
-   Treinar novamente um modelo adicionando novos dados ou executar previsão cruzada.  
  
 Esta seção fornece uma visão geral das informações necessárias para você começar a trabalhar com consultas de mineração de dados. Descreve os tipos de consultas que você pode criar em objetos de mineração de dados, introduz as ferramentas de consulta e linguagens de consulta, e fornece links para exemplos de consultas que você pode criar em modelos que foram criados usando os algoritmos fornecidos no SQL Server Data Mining.  
  
 [Entendendo as consultas de mineração de dados](#bkmk_Understand)  
  
 [Ferramentas de consulta e interfaces](#bkmk_Interfaces)  
  
 [Consultas para tipos de modelo diferentes](#bkmk_ModelTypes)  
  
 [Requisitos](#bkmk_Reqs)  
  
##  <a name="bkmk_Understand"></a> Entendendo as consultas de mineração de dados  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Data Mining dá suporte aos seguintes tipos de consultas:  
  
-   [Consultas de previsão &#40;mineração de dados&#41;](prediction-queries-data-mining.md)  
  
     Consultas que fazem inferências com base em padrões no modelo, e de dados de entrada.  
  
-   [Consultas de conteúdo &#40;mineração de dados&#41;](content-queries-data-mining.md)  
  
     Consultas que retornam metadados, estatísticas e outras informações sobre o próprio modelo.  
  
-   [Consultas de detalhamento &#40;mineração de dados&#41;](drillthrough-queries-data-mining.md)  
  
     Consultas que podem recuperar os dados de caso subjacentes para o modelo, ou até mesmo dados da estrutura que não foi usada no modelo.  
  
-   [Consultas de definição de dados &#40;mineração de dados&#41;](data-definition-queries-data-mining.md)  
  
     Consultas que não retornam informações do modelo, mas são usadas para compilar modelos e estruturas ou atualizar os dados em um modelo ou estrutura.  
  
 Antes de criar consultas, nós recomendamos que você se acostume com as diferenças entre modelos criados com cada algoritmo de mineração de dados fornecido pelo SQL Server.  
  
-   Navegue e explore cada tipo de modelo usando os visualizadores de mineração de dados personalizados que são fornecidos para cada tipo de algoritmo. Para obter mais informações, consulte [Tarefas e instruções do visualizador do modelo de mineração](mining-model-viewer-tasks-and-how-tos.md).  
  
-   Analise o conteúdo do modelo para cada tipo de modelo, usando o **Visualizador de Árvore de Conteúdo Genérica da Microsoft**. Para interpretar essas informações, consulte [Mining Model Content &#40;Analysis Services - Data Mining&#41;](mining-model-content-analysis-services-data-mining.md).  
  
##  <a name="bkmk_Interfaces"></a> Ferramentas de consulta e interfaces  
 Você pode criar consultas de mineração de dados interativamente usando uma das ferramentas de consulta fornecidas pelo SQL Server. O Construtor de Consultas de Previsão gráfica é fornecido no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Se você não usou o Construtor de Consultas de Previsão antes, nós recomendamos que você siga as etapas no [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md) para se acostumar com a interface. Para uma rápida visão geral das etapas, consulte Criar uma Consulta usando [Criar uma consulta de previsão usando o construtor de consultas de previsão](create-a-prediction-query-using-the-prediction-query-builder.md).  
  
 O Construtor de Consultas de Previsão é útil para iniciar consultas que você personalizará posteriormente. Você pode adicionar fontes de dados facilmente e mapeá-los para colunas e, em seguida, alternar a exibição de DMX e personalizar a consulta adicionando uma cláusula WHERE ou outras funções.  
  
 Quando você estiver familiarizado com modelos de mineração de dados e como criar consultas, você também poderá escrever consultas diretamente usando extensões DMX. O DMX é uma linguagem de consulta semelhante ao Transact-SQL, e que você pode usar de muitos clientes diferentes. O DMX é a ferramenta ideal para criar previsões personalizadas e consultas complexas. Para obter uma introdução ao DMX, consulte [Criando e consultando modelos de mineração de dados com DMX: Tutoriais &#40;Analysis Services – Mineração de dados&#41;](../../tutorials/create-query-data-mining-models-dmx-tutorials.md).  
  
 Os editores de DMX são fornecidos no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você também pode usar o Construtor de Consultas de Previsão para iniciar suas consultas e, em seguida, alterar a exibição para o editor de texto e copiar a instrução DMX para outro cliente. Para obter mais informações, consulte [Interfaces de consulta de mineração de dados](data-mining-query-tools.md).  
  
 Você pode compor instruções DMX programaticamente e enviá-las de seu cliente para o servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando AMO ou XMLA. Porém, o DMX é a linguagem que você deve usar para criar consultas em um modelo de mineração.  
  
 Você também pode consultar os metadados, estatísticas e conteúdo do modelo usando DMVs (Exibições de Gerenciamento Dinâmico) que são baseados nos conjuntos de linhas de esquema de mineração de dados. Estes DMVs facilitam a recuperação de informações sobre o modelo digitando instruções SELECT; no entanto, você não pode criar previsões. Para obter mais informações sobre os DMVs com suporte pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Usar DMVs &#40;Exibições de Gerenciamento Dinâmico&#41; para monitorar o Analysis Services](../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md).  
  
 Finalmente, você também pode criar consultas de mineração de dados para uso em pacotes de Integration Services, usando a [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md), ou a [Data Mining Query Transformation](../../integration-services/data-flow/transformations/data-mining-query-transformation.md). A tarefa de fluxo de controle dá suporte a vários tipos de consultas de DMX, enquanto a transformação de fluxo de dados só dá suporte a consultas que trabalham com dados no fluxo de dados, ou seja, consultas que usam a sintaxe PREDICTION JOIN.  
  
##  <a name="bkmk_ModelTypes"></a> Consultas para tipos de modelo diferentes  
 O algoritmo que foi usado quando o modelo foi criado influencia muito o tipo de informações que você pode obter de uma consulta de mineração de dados. A razão para as diferenças é que cada algoritmo processa os dados de um modo diferente, e armazena tipos diferentes de padrões. Por exemplo, alguns algoritmos criam clusters; outros criam árvores. Portanto, você pode precisar usar previsão especializada e funções de consulta, dependendo do tipo de modelo com o qual você está trabalhando.  
  
 A lista a seguir fornece um resumo das funções que você pode usar nas consultas:  
  
-   **Funções de previsão gerais:** o `Predict` função é polimórfica, ou seja, ele funciona com todos os tipos de modelo. Esta função automaticamente detectará o tipo de modelo com o qual você está trabalhando e solicita parâmetros adicionais. Para obter mais informações, consulte [Prever &#40;DMX&#41;](/sql/dmx/predict-dmx).  
  
    > [!WARNING]  
    >  Nem todos os modelos são usados para fazer previsões. Por exemplo, você pode criar um modelo de clustering que não tem um atributo previsível. Porém, mesmo que um modelo não tenha um atributo previsível, você poderá criar consultas de previsão que retornam outros tipos de informações úteis do modelo.  
  
-   **Funções de previsão personalizadas:** cada tipo de modelo fornece um conjunto de funções de previsão criado para trabalhar com os padrões criados por aquele algoritmo.  
  
     Por exemplo, a função `Lag` é fornecida para modelos de série temporal, para permitir que você exiba os dados históricos usados para o modelo. Para modelos de clustering, funções como `ClusterDistance` são mais significativas.  
  
     Para obter mais informações sobre as funções que têm suporte para cada tipo de modelo, consulte os links a seguir:  
  
    |||  
    |-|-|  
    |[Exemplos de consulta de um modelo de associação](association-model-query-examples.md)|[Referência técnica do algoritmo Naive Bayes da Microsoft](microsoft-naive-bayes-algorithm.md)|  
    |[Exemplos de consulta de modelo de clustering](clustering-model-query-examples.md)|[Exemplos de consulta de modelos de rede neural](neural-network-model-query-examples.md)|  
    |[Exemplos de consulta de modelo de árvores de decisão](decision-trees-model-query-examples.md)|[Exemplos de consulta dos modelos de clustering de sequências](sequence-clustering-model-query-examples.md)|  
    |[Exemplos de consulta de modelo de regressão linear](linear-regression-model-query-examples.md)|[Exemplos de consulta de modelos de série temporal](time-series-model-query-examples.md)|  
    |[Exemplos de consulta de modelo de regressão logística](logistic-regression-model-query-examples.md)||  
  
     Você também pode chamar funções VBA ou criar suas próprias funções. Para obter mais informações, consulte [Funções &#40;DMX&#41;](/sql/dmx/functions-dmx).  
  
-   **Estatísticas gerais:** há várias funções que podem ser usadas com quase qualquer tipo de modelo, que retornam um conjunto padrão de estatísticas descritivas, como desvio padrão.  
  
     Por exemplo, o `PredictHistogram` função retorna uma tabela que lista todos os estados da coluna especificada.  
  
     Para obter mais informações, consulte [Funções de previsão gerais &#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx).  
  
-   **Estatísticas personalizadas:** funções adicionais de suporte são fornecidas para cada tipo de modelo, para gerar estatísticas que sejam pertinentes à tarefa analítica específica.  
  
     Por exemplo, quando você estiver trabalhando com um modelo de clustering, você pode usar a função `PredictCaseLikelihood`, para retornar a pontuação de probabilidade associada a um determinado caso e cluster. Porém, se você criou um modelo de regressão linear, é mais interessante recuperar o coeficiente e interceptar, o que você pode fazer usando uma consulta de conteúdo.  
  
-   **Funções de conteúdo de modelo:** o *conteúdo* de todos os modelos é representado em um formato de tabela padronizado que permite recuperar as informações com uma simples consulta. Você cria consultas no conteúdo do modelo usando o DMX. Você também pode obter um tipo de conteúdo do modelo de mineração usando os conjuntos de linhas de esquema de mineração de dados.  
  
     No conteúdo do modelo, o significado de cada linha ou nó da tabela que é retornada difere dependendo do tipo de algoritmo que foi usado para criar o modelo, assim como do tipo de dados da coluna. Para obter mais informações, consulte [Content Queries &#40;Data Mining&#41;](content-queries-data-mining.md).  
  
##  <a name="bkmk_Reqs"></a> Requisitos  
 Antes de poder criar uma consulta em relação a um modelo, o modelo de mineração de dados deve ter sido processado. O processamento de objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] exige permissões especiais. Para obter mais informações sobre os modelos de mineração de processamento, consulte [Requisitos e considerações sobre processamento &#40;Mineração de Dados&#41;](processing-requirements-and-considerations-data-mining.md).  
  
 Executar consultas em um modelo de mineração de dados exige níveis diferentes de permissões, dependendo do tipo de consulta que você executar. Por exemplo, o detalhamento para dados de estrutura ou caso normalmente exige permissões adicionais que podem ser definidas no objeto de estrutura de mineração ou objeto de modelo de mineração.  
  
 No entanto, se sua consulta usar dados externos e incluir instruções como OPENROWSET ou OPENQUERY, o banco de dados que você estiver consultando deverá habilitar estas instruções e você deverá ter permissão nos objetos de banco de dados subjacentes.  
  
 Para obter mais informações sobre os contextos de segurança exigidas para executar consultas de mineração de dados, consulte [Visão geral de segurança &#40;Mineração de Dados&#41;](security-overview-data-mining.md)  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos nesta seção introduzem cada tipo de consulta de mineração de dados em mais detalhes e fornecem links para exemplos detalhados de como criar consultas em modelos de mineração de dados.  
  
 [Consultas de previsão &#40;mineração de dados&#41;](prediction-queries-data-mining.md)  
  
 [Consultas de conteúdo &#40;mineração de dados&#41;](content-queries-data-mining.md)  
  
 [Consultas de detalhamento &#40;mineração de dados&#41;](drillthrough-queries-data-mining.md)  
  
 [Consultas de definição de dados &#40;mineração de dados&#41;](data-definition-queries-data-mining.md)  
  
 [Interfaces de Consulta de Mineração de Dados](data-mining-query-tools.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Use estes links para aprender a criar e trabalhar com consultas de mineração de dados.  
  
|Tarefas|Links|  
|-----------|-----------|  
|Exiba tutoriais e passo a passo em consultas de mineração de dados|[Lição 6: Criando e trabalhando com previsões &#40;Tutorial de mineração de dados básicos&#41;](../../tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)<br /><br /> [Tutorial DMX de previsão de série temporal](../../tutorials/time-series-prediction-dmx-tutorial.md)|  
|Use ferramentas de consulta de mineração de dados no SQL Server Management Studio e no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]|[Criar uma consulta DMX no SQL Server Management Studio](create-a-dmx-query-in-sql-server-management-studio.md)<br /><br /> [Criar uma consulta de previsão usando o Construtor de Consultas de previsão](create-a-prediction-query-using-the-prediction-query-builder.md)<br /><br /> [Aplicar funções de previsão a um modelo](apply-prediction-functions-to-a-model.md)<br /><br /> [Editar manualmente uma consulta de previsão](manually-edit-a-prediction-query.md)|  
|Trabalhe com dados externos usados em consultas de previsão|[Escolher e mapear dados de entrada para uma consulta de previsão](choose-and-map-input-data-for-a-prediction-query.md)<br /><br /> [Escolher e mapear dados de entrada para uma consulta de previsão](choose-and-map-input-data-for-a-prediction-query.md)|  
|Trabalhe com os resultados de consultas|[Exibir e salvar os resultados de uma consulta de previsão](view-and-save-the-results-of-a-prediction-query.md)|  
|Use DMX e modelos de consulta de XMLA fornecidos no Management Studio|[Criar uma consulta de previsão Singleton a partir de um modelo](create-a-singleton-prediction-query-from-a-template.md)<br /><br /> [Criar uma consulta de mineração de dados usando XML/A](create-a-data-mining-query-by-using-xmla.md)<br /><br /> [Usar modelos do Analysis Services no SQL Server Management Studio](../instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|Saiba mais sobre consultas de conteúdo e veja exemplos|[Criar uma consulta de conteúdo em um modelo de mineração](create-a-content-query-on-a-mining-model.md)<br /><br /> [Consultar os parâmetros usados para criar um modelo de mineração](query-the-parameters-used-to-create-a-mining-model.md)<br /><br /> [Consultas de conteúdo &#40;mineração de dados&#41;](content-queries-data-mining.md)|  
|Defina opções de consulta e solucione permissões de consulta e problemas|[Alterar o valor do tempo limite de consultas de mineração de dados](data-mining-queries.md)|  
|Use os componentes de mineração de dados no Integration Services|[Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md)<br /><br /> [Data Mining Query Transformation](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services - mineração de dados&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [Conteúdo do modelo de mineração &#40;Analysis Services - mineração de dados&#41;](mining-model-content-analysis-services-data-mining.md)  
  
  
