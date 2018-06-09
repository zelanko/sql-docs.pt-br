---
title: PredictCaseLikelihood (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d8159af8ac4b3c9bf21dcdc68a0cfb30c46e33e5
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34841769"
---
# <a name="predictcaselikelihood-dmx"></a>PredictCaseLikelihood (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Esta função retorna a probabilidade de um caso de entrada se ajustar no modelo existente. Usado somente com modelos de cluster.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PredictCaseLikelihood([NORMALIZED|NONNORMALIZED])  
```  
  
## <a name="arguments"></a>Argumentos  
 NORMALIZED  
 O valor de retorno contém a probabilidade do caso com o modelo dividido pela probabilidade do caso sem o modelo.   
  
 NONNORMALIZED  
 O valor de retorno contém a probabilidade bruta do caso, que é o produto das probabilidades dos atributos de caso.  
  
## <a name="applies-to"></a>Aplica-se a  
 Modelos que são criados usando o [!INCLUDE[msCoName](../includes/msconame-md.md)] Clustering e [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmos de Clustering de sequência.  
  
## <a name="return-type"></a>Tipo de retorno  
 Número de ponto flutuante da dupla precisão entre 0 e 1. Um número próximo de 1 indica que o caso tem uma alta probabilidade de ocorrer neste modelo. Um número próximo de 0 indica que o caso tem pouca probabilidade de ocorrer neste modelo.  
  
## <a name="remarks"></a>Remarks  
 Por padrão, o resultado da **PredictCaseLikelihood** função é normalizada. Em geral, os valores normalizados são mais úteis à medida que o número de atributos de um caso aumenta e as diferenças entre as probabilidades brutas de quaisquer dois casos tornam-se muito menores.  
  
 A seguinte equação é usada para calcular os valores normalizados, determinados x e y:  
  
-   x = probabilidade do caso baseada no modelo de cluster  
  
-   y = probabilidade de caso marginal, calculada como a probabilidade de log do caso com base na contagem dos casos de treinamento  
  
-   Z = Exp( log(x) – Log(Y))  
  
 Normalizado = (z / (1 + z))  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a probabilidade de o caso específico ocorrer no modelo de cluster, que é baseado no banco de dados [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW.  
  
```  
SELECT  
  PredictCaseLikelihood() AS Default_Likelihood,  
  PredictCaseLikelihood(NORMALIZED) AS Normalized_Likelihood,  
  PredictCaseLikelihood(NONNORMALIZED) AS Raw_Likelihood,  
FROM  
  [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
 Resultados esperados:  
  
|Default_Likelihood|Normalized_Likelihood|Raw_Likelihood|  
|-------------------------|----------------------------|---------------------|  
|6.30672792729321E-08|6.30672792729321E-08|9.5824454056846E-48|  
  
 A diferença entre esses resultados demonstra o efeito da normalização. O valor bruto para **CaseLikelihood** sugere que a probabilidade do caso é aproximadamente 20 por cento; no entanto, quando você normaliza os resultados, ele se torna aparente que a probabilidade do caso é muito baixa.  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services – mineração de dados&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funções de previsão geral &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
