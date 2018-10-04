---
title: Elemento AggregationFunction (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AggregationFunction Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationFunction
helpviewer_keywords:
- AggregationFunction element
ms.assetid: 40cfc7f9-1089-45f9-be90-a29770ed9682
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 453d51d678a8e721eaa7fa280e23248c66019b5b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48153201"
---
# <a name="aggregationfunction-element-assl"></a>Elemento AggregationFunction (ASSL)
  Contém a função de agregação a ser usada para o tipo de conta.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Account>  
   ...  
   <AggregationFunction>...</AggregationFunction>  
   ...  
</Account>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Sum*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[conta](../objects/account-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres a seguir:  
  
|Valor|Description|  
|-----------|-----------------|  
|*Sum*|A medida é agregada usando a função `Sum`.|  
|*Contagem*|A medida é agregada usando a função `Count`.|  
|*Min*|A medida é agregada usando a função `Min`.|  
|*Max*|A medida é agregada usando a função `Max`.|  
|*DistinctCount*|A medida é agregada usando a função `DistinctCount`.|  
|*Nenhuma*|A medida não é agregada.|  
|*AverageOfChildren*|A medida é agregada retornando a média de seus filhos.|  
|*FirstChild*|A medida é agregada retornando seu primeiro membro filho.|  
|*LastChild*|A medida é agregada retornando seu último membro filho.|  
|*FirstNonEmpty*|A medida é agregada retornando seu primeiro membro não vazio.|  
|*LastNonEmpty*|A medida é agregada retornando seu último membro não vazio.|  
  
 A enumeração que corresponde aos valores permitidos para `AggregationFunction` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.AggregationFunction>.  
  
## <a name="see-also"></a>Consulte também  
 [Contas de elemento &#40;ASSL&#41;](../collections/accounts-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
