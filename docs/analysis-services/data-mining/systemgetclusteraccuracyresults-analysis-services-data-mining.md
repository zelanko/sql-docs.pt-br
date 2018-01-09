---
title: "SystemGetClusterAccuracyResults (Analysis Services – mineração de dados) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- stored procedures [Analysis Services], data mining
- SystemGetClusterAccuracyResults
- cross-validation [data mining]
ms.assetid: e1701738-50d5-46b4-b406-f1e800545abb
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 47272107eea7905a1e0414f42ff450e7a1ebbdb9
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="systemgetclusteraccuracyresults-analysis-services---data-mining"></a>SystemGetClusterAccuracyResults (Analysis Services - Data Mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Retorna as métricas de precisão de validação cruzada para uma estrutura de mineração e modelos de clusters relacionados.  
  
 Esse procedimento armazenado retorna métrica para todo o conjunto de dados como uma única partição. Para dividir o conjunto de dados em seções cruzadas e retornar métricas para cada partição, use [SystemGetClusterCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  Esse procedimento armazenado só funciona para modelos de clustering. Para modelos não clustering, use [SystemGetAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SystemGetClusterAccuracyResults(  
<mining structure>   
[,<mining model list>]  
,<data set>  
,<test list>])  
```  
  
## <a name="arguments"></a>Argumentos  
 *estrutura de mineração*  
 Nome de uma estrutura de mineração no banco de dados atual.  
  
 (Obrigatória)  
  
 *lista do modelo de mineração*  
 Lista separada por vírgulas de modelos para validar.  
  
 O padrão é **null**, ou seja, todos os modelos aplicáveis são usados. Quando o padrão é usado, modelos que não são de clustering são excluídos automaticamente da lista de candidatos para processamento.  
  
 (opcional)  
  
 *conjunto de dados*  
 Um valor inteiro que indica qual partição na estrutura de mineração será usada para teste. O valor é derivado de uma máscara de bits que representa a soma dos valores seguintes, onde qualquer valor único é opcional:  
  
|||  
|-|-|  
|Casos de treinamento|0x0001|  
|Casos de teste|0x0002|  
|Filtro do modelo|0x0004|  
  
 Para obter uma lista completa de valores possíveis, consulte a seção Comentários mais adiante neste tópico.  
  
 (Obrigatória)  
  
 *test list*  
 Uma cadeia de caracteres que especifica opções de teste. Esse parâmetro é reservado para uso futuro.  
  
 (opcional)  
  
## <a name="return-type"></a>Tipo de retorno  
 Uma tabela que contém pontuações para cada partição individual e agrega para todos os modelos.  
  
 A tabela a seguir lista as colunas retornadas por **SystemGetClusterAccuracyResults**. Para aprender como interpretar as informações retornadas pelo procedimento armazenado, consulte [Medidas no relatório de validação cruzada](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).  
  
|Nome da coluna|Description|  
|-----------------|-----------------|  
|ModelName|O nome do modelo que foi testado. **Tudo** indica que o resultado é uma agregação para todos os modelos.|  
|AttributeName|Não aplicável a modelos de clustering.|  
|AttributeState|Não aplicável a modelos de clustering.|  
|PartitionIndex|Um número que indica a partição.<br /><br /> Para esse procedimento armazenado, o número é sempre 0.|  
|PartitionCases|Um inteiro que indica quantos casos foram testados.|  
|Teste|O tipo de teste que foi executado.|  
|Measure|Nome da medida retornada pelo teste. Medidas para cada modelo dependem do tipo modelo e do tipo do valor previsível.<br /><br /> Para obter uma lista de medidas retornadas para cada tipo previsível, consulte [Medidas no relatório de validação cruzada](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).<br /><br /> Para obter uma definição de cada medida, consulte [Validação cruzada &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md).|  
|Valor|Uma pontuação de probabilidade que indica a probabilidade de caso de cluster.|  
  
## <a name="remarks"></a>Remarks  
 A tabela a seguir fornece exemplos dos valores que você pode usar para especificar os dados na estrutura de mineração usados para validação cruzada. Se você desejar usar casos de teste para validação cruzada, a estrutura de mineração já deverá conter um conjunto de dados para teste. Para obter informações sobre como definir um conjunto de dados de teste ao criar uma estrutura de mineração, consulte [Conjuntos de dados de treinamento e teste](../../analysis-services/data-mining/training-and-testing-data-sets.md).  
  
|Valor inteiro|Description|  
|-------------------|-----------------|  
|1|Somente casos de treinamento são usados.|  
|2|Somente os casos de teste são usados.|  
|3|Somente os casos de teste e de treinamento são usados.|  
|4|Combinação inválida.|  
|5|Somente casos de teste são usados e o filtro de modelo é aplicado.|  
|6|Somente casos de teste são usados e o filtro de modelo é aplicado.|  
|7|Os casos de teste e de treinamento são usados e o filtro de modelo é aplicado.|  
  
 Para obter mais informações sobre os cenários nos quais você usaria validação cruzada, consulte [Teste e validação &#40;Data Mining&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md).  
  
## <a name="examples"></a>Exemplos  
 Esse exemplo retorna medidas de precisão para dois modelos de clustering, denominados `Cluster 1` e `Cluster 2`, que são associados à estrutura de mineração vTargetMail. O código da linha quatro indica que os resultados devem ser baseados nos casos de testes sozinhos, sem usar filtros que possam ser associados a cada modelo.  
  
```  
CALL SystemGetClusterAccuracyResults (  
[vTargetMail],  
[Cluster 1], [Cluster 2],  
2  
)  
```  
  
 Resultados do exemplo:  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|Teste|Medida|Valor|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|Cluster 1|||0|5545|Clustering|Probabilidade de caso|0.796514342249313|  
|Cluster 2|||0|5545|Clustering|Probabilidade de caso|0.732122471228572|  
  
## <a name="requirements"></a>Requisitos  
 A validação cruzada só está disponível no [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] a partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [SystemGetCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults &#40; Analysis Services – mineração de dados &#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults &#40; Analysis Services – mineração de dados &#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemClusterGetAccuracyResults](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  
