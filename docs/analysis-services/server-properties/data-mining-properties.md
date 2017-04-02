---
title: "Propriedades de minera&#231;&#227;o de dados | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "propriedade ClusterCount"
  - "propriedade AllowedProvidersInOpenRowset"
  - "propriedade MinimumSeriesValue"
  - "propriedade ScoreMethod"
  - "propriedade MinimumImportance"
  - "propriedade ModellingCardinality"
  - "propriedade BrentTolerance"
  - "propriedade ComplexityPenalty"
  - "propriedade MaximumItemsetCount"
  - "propriedade MinimumSupport"
  - "propriedade AllowSessionMiningModels"
  - "propriedade HoldoutPercentage"
  - "propriedade ClusterCountPrior"
  - "propriedade MaximumSequenceStates"
  - "propriedade OptimizedPredictionCount"
  - "mineração de dados [Analysis Services], propriedades"
  - "propriedade MaximumSales"
  - "propriedade MaximumContinuousInputAttributes"
  - "propriedade MaximumOutputAttributes"
  - "propriedade AllowAdHocOpenRowsetQueries"
  - "propriedade Enabled"
  - "propriedade HistoricModelGap"
  - "propriedade SampleSize"
  - "propriedade MaximumInputAttributes"
  - "propriedade PeriodicityHint"
  - "propriedade MissingValueSubstitution"
  - "propriedade ScoreMethod"
  - "propriedade ForceRegressor"
  - "propriedade MaximumBucketsForContinuousSplit"
  - "propriedade MaxConcurrentPredictionQueries"
  - "propriedade MinimumItemsetSize"
  - "propriedade AcyclicGraph"
  - "propriedade HoldoutMethod"
  - "propriedade StoppingTolerance"
  - "propriedades [mineração de dados]"
  - "propriedade AutoDetectPeriodicity"
  - "propriedade HoldoutTolerance"
  - "propriedade MinimumLeafCases"
  - "propriedade HoldoutSeed"
  - "propriedade MinimumClusterCases"
  - "propriedade ClusterCountDeviation"
  - "propriedade MinimumDependencyProbability"
  - "propriedade ClusteringMethod"
  - "propriedade MaximumItemsetSize"
  - "propriedade HiddenNodeRatio"
  - "propriedade MaximumSeriesValue"
ms.assetid: 9bc9abed-180a-4bd8-b2eb-89c62fa88110
caps.latest.revision: 19
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 19
---
# Propriedades de minera&#231;&#227;o de dados
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oferece suporte às propriedades do servidor de mineração de dados listadas nas tabelas a seguir. Para obter mais informações sobre propriedades adicionais do servidor e como defini-las, consulte [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Aplica-se a:** somente modo de servidor multidimensional  
  
## Categoria não específica  
 **AllowSessionMiningModels**  
 Uma propriedade Booleana que indica se podem ser criados modelos de mineração de sessão.  
  
 O valor padrão para essa propriedade é false, o que indica que modelos de mineração de sessão não podem ser criados.  
  
 **AllowAdHocOpenRowsetQueries**  
 Uma propriedade Booleana que indica se consultas ad hoc abertas de conjunto de linhas são permitidas.  
  
 O valor padrão para essa propriedade é false, o que indica que as consultas abertas de conjuntos de linhas não são permitidas durante uma sessão.  
  
 **AllowedProvidersInOpenRowset**  
 Uma propriedade de cadeia de caracteres que identifica quais fornecedores são permitidos em um conjunto de linhas aberto, consistindo de uma lista de ProgIDs ou [All] de fornecedores separada por vírgula/ponto-e-vírgula.  
  
 **MaxConcurrentPredictionQueries**  
 Uma propriedade de inteiro de 32 bits assinada que define o número máximo de consultas de previsão simultâneas.  
  
## Categoria de algoritmos  
 **Microsoft_Association_Rules\ Enabled**  
 Uma propriedade Booleana que indica se o algoritmo Microsoft_Association_Rules está habilitado.  
  
 **Microsoft_Clustering\ Enabled**  
 Uma propriedade Booleana que indica se o algoritmo Microsoft_Clustering está habilitado.  
  
 **Microsoft_Decision_Trees\ Enabled**  
 Uma propriedade Booleana que indica se o algoritmo Microsoft_ DecisionTrees está habilitado.  
  
 **Microsoft_Naive_Bayes\ Enabled**  
 Uma propriedade Booleana que indica se o algoritmo Microsoft_ Naive_Bayes está habilitado.  
  
 **Microsoft_Neural_Network\ Enabled**  
 Uma propriedade Booleana que indica se o algoritmo Microsoft_Neural_Network está habilitado.  
  
 **Microsoft_Sequence_Clustering\ Enabled**  
 Uma propriedade Booleana que indica se o algoritmo Microsoft_ Sequence_Clustering está habilitado.  
  
 **Microsoft_Time_Series\ Enabled**  
 Uma propriedade Booleana que indica se o algoritmo Microsoft_Time_Series está habilitado.  
  
 **Microsoft_Linear_Regression\ Enabled**  
 Uma propriedade Booleana que indica se o algoritmo Microsoft_Linear_Regression está habilitado.  
  
 **Microsoft_Logistic_Regression\ Enabled**  
 Uma propriedade Booleana que indica se o algoritmo Microsoft_Logistic_Regression está habilitado.  
  
> [!NOTE]  
>  Além das propriedades que definem os serviços mineração de dados disponíveis no servidor, há propriedades de mineração de dados que definem o comportamento de algoritmos específicos. Essas propriedades são configuradas quando você criar um modelo de mineração de dados individual, não ao nível do servidor. Para obter mais informações, consulte [Algoritmos de mineração de dados &#40;Analysis Services – Mineração de Dados&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
## Consulte também  
 [Arquitetura física &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/physical-architecture-analysis-services-data-mining.md)   
 [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determina o Modo de Servidor de uma instância do Analysis Services.](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  