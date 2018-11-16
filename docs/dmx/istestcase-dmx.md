---
title: IsTestCase (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b7e80f8a9dfb82f13350b94b310690a081fae1de
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606636"
---
# <a name="istestcase-dmx"></a>IsTestCase (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Indica se um caso é usado como um caso de teste para o modelo de mineração de dados ou a estrutura de mineração especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IsTestCase()  
```  
  
## <a name="result-type"></a>Tipo de Resultado  
 Retorna **verdadeira** se o caso fizer parte do conjunto de dados de teste; caso contrário **falso**.  
  
## <a name="remarks"></a>Comentários  
 Se você usar o Assistente de Mineração de Dados para criar uma estrutura de mineração e o modelo de mineração relacionado, por padrão, 30% dos casos serão separados para serem usados como um conjunto de dados de teste. Os casos restantes serão utilizados para treinar o modelo de mineração de dados. O mesmo conjunto de dados de teste pode ser usado com todos os modelos baseados nessa estrutura. No entanto, se você usar DMX para criar o modelo de mineração, por padrão, todos os dados são usados para treinar o modelo, e nenhum conjunto de teste é criado. Para habilitar a criação de um conjunto de dados de teste, você deve definir os parâmetros da cláusula WITH HOLDOUT.  
  
 É possível determinar se um conjunto de teste foi criado em uma estrutura de mineração específica exibindo o valor das propriedades <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> e <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A>.  
  
> [!NOTE]  
>  Detalhamento deve ser habilitado no modelo, se você quiser usar as funções IsTrainingCase ou IsTestCase para retornar detalhes sobre os casos em um modelo específico. Para obter mais informações,consulte [Habilitar drillthrough para um modelo de mineração](../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md).  
  
 Para retornar casos que fazem parte do conjunto de dados de treinamento, use a função [IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa o `Targeted Mailing` estrutura de mineração que é criada na [Basic Data Mining Tutorial](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). A consulta retorna todos os casos da estrutura que são usados para teste.  
  
```  
SELECT *  
FROM [Targeted Mailing].CASES  
WHERE IsTestCase()  
```  
  
 Para obter mais informações sobre como consultar casos usados na mineração de dados, consulte [SELECT FROM &#60;modelo&#62;. CASOS de &#40;DMX&#41; ](../dmx/select-from-model-cases-dmx.md) e [SELECT FROM &#60;estrutura&#62;. CASOS](../dmx/select-from-structure-cases.md).  
  
## <a name="see-also"></a>Consulte também  
 [Funções &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Consultas de mineração de dados](../analysis-services/data-mining/data-mining-queries.md)   
 [Conjuntos de dados de teste e treinamento](../analysis-services/data-mining/training-and-testing-data-sets.md)  
  
  
