---
description: IsTestCase (DMX)
title: IsTestCase (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 11795005d0a2a7cf97a515278a30a586ff640ef0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88352272"
---
# <a name="istestcase-dmx"></a>IsTestCase (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Indica se um caso é usado como um caso de teste para o modelo de mineração de dados ou a estrutura de mineração especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IsTestCase()  
```  
  
## <a name="result-type"></a>Tipo de resultado  
 Retornará **true** se o caso for uma parte do conjunto de dados de teste; caso contrário, **false**.  
  
## <a name="remarks"></a>Comentários  
 Se você usar o Assistente de Mineração de Dados para criar uma estrutura de mineração e o modelo de mineração relacionado, por padrão, 30% dos casos serão separados para serem usados como um conjunto de dados de teste. Os casos restantes serão utilizados para treinar o modelo de mineração de dados. O mesmo conjunto de dados de teste pode ser usado com todos os modelos baseados nessa estrutura. No entanto, se você usar DMX para criar o modelo de mineração, por padrão, todos os dados serão usados para treinar o modelo e nenhum conjunto de testes será criado. Para habilitar a criação de um conjunto de dados de teste, você deve definir os parâmetros da cláusula WITH de validação.  
  
 É possível determinar se um conjunto de teste foi criado em uma estrutura de mineração específica exibindo o valor das propriedades <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> e <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A>.  
  
> [!NOTE]  
>  O detalhamento deve ser habilitado no modelo se você quiser usar as funções IsTrainingCase ou IsTestCase para retornar detalhes sobre os casos em um modelo específico. Para obter mais informações,consulte [Habilitar drillthrough para um modelo de mineração](https://docs.microsoft.com/analysis-services/data-mining/enable-drillthrough-for-a-mining-model).  
  
 Para retornar casos que fazem parte do conjunto de dados de treinamento, use a função [IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa a `Targeted Mailing` estrutura de mineração criada no [tutorial de mineração de dados básico](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). A consulta retorna todos os casos da estrutura que são usados para teste.  
  
```  
SELECT *  
FROM [Targeted Mailing].CASES  
WHERE IsTestCase()  
```  
  
 Para obter mais informações sobre como consultar os casos usados em Data Mining, consulte [selecionar do modelo de &#60;&#62;. CASOS &#40;&#41;DMX ](../dmx/select-from-model-cases-dmx.md) e [selecionar entre &#60;estrutura&#62;. CASOS](../dmx/select-from-structure-cases.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Funções &#40;&#41;DMX ](../dmx/functions-dmx.md)   
 [Consultas de mineração de dados](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries)   
 [Conjuntos de dados de teste e treinamento](https://docs.microsoft.com/analysis-services/data-mining/training-and-testing-data-sets)  
  
  
