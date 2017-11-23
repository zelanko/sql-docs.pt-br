---
title: "SystemGetClusterCrossValidationResults (Analysis Services – mineração de dados) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SystemGetClusterCrossValidationResults
- stored procedures [Analysis Services], data mining
- cross-validation [data mining]
ms.assetid: 79de9b81-9f2e-4f20-ace9-e3b19d6a9759
caps.latest.revision: "21"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a741805b22296232bffdc881ba4105243ea92506
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="systemgetclustercrossvalidationresults-analysis-services---data-mining"></a>SystemGetClusterCrossValidationResults (Analysis Services - Data Mining)
  Particiona a estrutura de mineração em um número especificado de seções cruzadas, treina um modelo para cada partição e retorna métricas de precisão para cada partição.  
  
 **Observação** : esse procedimento armazenado só pode ser usado com uma estrutura de mineração que contém pelo menos um modelo de clustering. Para validação cruzada de modelos que não são de clustering, você deve usar [SystemGetCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SystemGetClusterCrossValidationResults(  
<structure name>,   
[,<mining model list>]  
,<fold count>}  
,<max cases>  
<test list>])  
```  
  
## <a name="arguments"></a>Argumentos  
 *estrutura de mineração*  
 Nome de uma estrutura de mineração no banco de dados atual.  
  
 (obrigatório)  
  
 *lista do modelo de mineração*  
 Lista separada por vírgulas de modelos de mineração para validar.  
  
 Se uma lista de modelos de mineração não for especificada, a validação cruzada será executada em todos os modelos de clustering associados com a estrutura especificada.  
  
> [!NOTE]  
>  Para validação cruzada de modelos que não são de clustering, você deve usar um procedimento armazenado separado, [SystemGetCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md).  
  
 (opcional)  
  
 *número de partições*  
 Inteiro que especifica o número de partições nas quais separar o conjunto de dados. O valor mínimo é 2. O número máximo de dobras é **maximum integer** ou o número de casos, o que for inferior.  
  
 Cada partição conterá este número de casos, aproximadamente: *máximo de casos*/*contagem de dobras*.  
  
 Não há valor padrão.  
  
> [!NOTE]  
>  O número de dobras afeta grandemente o tempo necessário para realizar a validação cruzada. Se você selecionar um número que seja muito alto, a consulta poderá ser executada por muito tempo e, em alguns casos, o servidor poderá ficar sem-resposta ou expirar.  
  
 (obrigatório)  
  
 *máximo de casos*  
 Inteiro que especifica o número de máximo de caixas que podem ser testadas.  
  
 Um valor de 0 indica que serão usadas todas as caixas na fonte de dados.  
  
 Se for especificado um número maior que o de casos reais no conjunto de dados, todos os casos serão da fonte de dados serão usados.  
  
 (obrigatório)  
  
 *test list*  
 Uma cadeia de caracteres que especifica opções de teste.  
  
 **Observação** : esse parâmetro é reservado para uso futuro.  
  
 (opcional)  
  
## <a name="return-type"></a>Tipo de retorno  
 A tabela Tipo de retorno contém pontuações para cada partição específica e agregações para todos os modelos.  
  
 A tabela a seguir descreve as colunas retornadas.  
  
|Nome da coluna|Description|  
|-----------------|-----------------|  
|ModelName|O nome do modelo que foi testado.|  
|AttributeName|O nome da coluna previsível. Para modelos de cluster, sempre **null**.|  
|AttributeState|Um valor de destino especificado na coluna previsível. Para modelos de cluster, sempre **null.**|  
|PartitionIndex|Um índice de base 1 que identifica a qual partição os resultados se aplicam.|  
|PartitionSize|Um inteiro que indica quantos casos foram incluídos em cada partição.|  
|Teste|O tipo de teste que foi executado.|  
|Measure|Nome da medida retornada pelo teste. Medidas para cada modelo dependem do tipo do valor previsível. Para obter uma definição de cada medida, consulte [Validação cruzada &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md).<br /><br /> Para obter uma lista de medidas retornadas para cada tipo previsível, consulte [Medidas no relatório de validação cruzada](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).|  
|Value|O valor da medida de teste especificada.|  
  
## <a name="remarks"></a>Comentários  
 Para retornar métricas de precisão para o conjunto de dados completo, use [SystemGetClusterAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md).  
  
 Além disso, se o modelo de mineração já tiver sido dividido em dobras, você poderá ignorar o processamento e retornar somente os resultados da validação cruzada usando [SystemGetClusterAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir demonstra como particionar uma estrutura de mineração em três dobras e, em seguida, testar dois modelos de clustering associados com a estrutura de mineração.  
  
 A linha três do código lista os modelos de mineração específicos que você deseja testar. Se você não especificar a lista, todos os modelos de clustering associados com a estrutura serão usados.  
  
 A linha quatro do código especifica o número de dobras e a linha cinco especifica o número máximo de casos a usar.  
  
 Como esses são modelos de clustering, não é necessário especificar um atributo ou valor previsível.  
  
```  
CALL SystemGetClusterCrossValidationResults(  
[v Target Mail],  
[Cluster 1], [Cluster 2],  
3,  
10000  
)  
```  
  
 Resultados do exemplo:  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|Teste|Measure|Value|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|Cluster 1|||1|3025|Clustering|Probabilidade de caso|0.930524511864121|  
|Cluster 1|||2|3025|Clustering|Probabilidade de caso|0.919184178430778|  
|Cluster 1|||3|3024|Clustering|Probabilidade de caso|0.929651120490248|  
|Cluster 2|||1|1289|Clustering|Probabilidade de caso|0.922789726933607|  
|Cluster 2|||2|1288|Clustering|Probabilidade de caso|0.934865535691068|  
|Cluster 2|||3|1288|Clustering|Probabilidade de caso|0.924724595688798|  
  
## <a name="requirements"></a>Requisitos  
 A validação cruzada só está disponível no [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] a partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [SystemGetCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults &#40; Analysis Services – mineração de dados &#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetClusterAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  
