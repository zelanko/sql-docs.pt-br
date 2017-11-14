---
title: "Propriedades de mineração de dados | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: server-properties
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ClusterCount property
- AllowedProvidersInOpenRowset property
- MinimumSeriesValue property
- ScoreMethod property
- MinimumImportance property
- ModellingCardinality property
- BrentTolerance property
- ComplexityPenalty property
- MaximumItemsetCount property
- MinimumSupport property
- AllowSessionMiningModels property
- HoldoutPercentage property
- ClusterCountPrior property
- MaximumSequenceStates property
- OptimizedPredictionCount property
- data mining [Analysis Services], properties
- MaximumStates property
- MaximumContinuousInputAttributes property
- MaximumOutputAttributes property
- AllowAdHocOpenRowsetQueries property
- Enabled property
- HistoricModelGap property
- SampleSize property
- MaximumInputAttributes property
- PeriodicityHint property
- MissingValueSubstitution property
- SplitMethod property
- ForceRegressor property
- MaximumBucketsForContinuousSplit property
- MaxConcurrentPredictionQueries property
- MinimumItemsetSize property
- AcyclicGraph property
- HoldoutMethod property
- StoppingTolerance property
- properties [data mining]
- AutoDetectPeriodicity property
- HoldoutTolerance property
- MinimumLeafCases property
- HoldoutSeed property
- MinimumClusterCases property
- ClusterCountDeviation property
- MinimumDependencyProbability property
- ClusteringMethod property
- MaximumItemsetSize property
- HiddenNodeRatio property
- MaximumSeriesValue property
ms.assetid: 9bc9abed-180a-4bd8-b2eb-89c62fa88110
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9d8dfbc8391518ff1375cf47102d4cb607992338
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="data-mining-properties"></a>Propriedades de mineração de dados
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oferece suporte às propriedades do servidor de mineração de dados listadas nas tabelas a seguir. Para obter mais informações sobre propriedades adicionais do servidor e como defini-las, consulte [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Aplica-se a:** somente modo de servidor multidimensional  
  
## <a name="non-specific-category"></a>Categoria não específica  
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
  
## <a name="algorithms-category"></a>Categoria de algoritmos  
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
  
## <a name="see-also"></a>Consulte também  
 [Arquitetura física &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/physical-architecture-analysis-services-data-mining.md)   
 [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determina o Modo de Servidor de uma instância do Analysis Services.](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  

