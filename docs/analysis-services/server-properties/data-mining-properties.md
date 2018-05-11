---
title: Propriedades de mineração de dados | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 17a0f6259524e40b2c2f6b22655c1ebe9feb2c1b
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="data-mining-properties"></a>Propriedades de mineração de dados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
 [Determina o Modo de Servidor de uma instância do Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
