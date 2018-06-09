---
title: IsTrainingCase (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 00344eeb38f3aae5cae7ac25c1b65b403cc85cb9
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34842339"
---
# <a name="istrainingcase-dmx"></a>IsTrainingCase (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Indica se um caso é usado como um caso de treinamento para o modelo de mineração de dados ou a estrutura de mineração especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IsTrainingCase()  
```  
  
## <a name="result-type"></a>Tipo de Resultado  
 Retorna **true** se o caso fizer parte do conjunto de dados de treinamento; caso contrário, **false**.  
  
## <a name="remarks"></a>Remarks  
 Se você usar o Assistente de Mineração de Dados para criar uma estrutura de mineração e o modelo de mineração relacionado, por padrão, 30% dos casos serão separados para serem usados como um conjunto de dados de teste. Os casos restantes especificados na fonte de dados serão usados para treinar o modelo. No entanto, se você usar DMX para criar o modelo de mineração, por padrão, todos os dados serão usados para treinar o modelo e nenhum conjunto de teste será criado. Para permitir a criação de um conjunto de dados de teste, defina os parâmetros da cláusula WITH HOLDOUT.  
  
 É possível determinar se os dados de uma estrutura de mineração de dados específica foram particionados em conjuntos de teste e de treinamento exibindo um valor das propriedades <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> e <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A>.  
  
> [!NOTE]  
>  Detalhamento deve ser habilitado no modelo, se você quiser usar as funções IsTrainingCase ou IsTestCase para retornar detalhes sobre os casos no modelo. Para obter mais informações,consulte [Habilitar drillthrough para um modelo de mineração](../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md).  
  
 Para retornar casos que fazem parte do conjunto de dados de teste, use a função [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa o modelo de mineração de dados clustering do cenário de mala direta no [Tutorial básico de mineração de dados](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). A consulta retorna somente os casos que foram usados para treinar o modelo de mineração. Além disso, os casos de treinamento são restritos a clientes com menos de 40 anos.  
  
```  
SELECT *  
FROM [TM Clustering].CASES  
WHERE IsTrainingCase()  
AND [Age] <40  
```  
  
 Para obter outros exemplos de como consultar os casos usados na mineração de dados, consulte [SELECT FROM &#60;modelo&#62;. CASOS &#40;DMX&#41; ](../dmx/select-from-model-cases-dmx.md) e [SELECT FROM &#60;estrutura&#62;. CASOS](../dmx/select-from-structure-cases.md).  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de dados de treinamento e teste](../analysis-services/data-mining/training-and-testing-data-sets.md)   
 [Funções &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Consultas de mineração de dados](../analysis-services/data-mining/data-mining-queries.md)  
  
  
