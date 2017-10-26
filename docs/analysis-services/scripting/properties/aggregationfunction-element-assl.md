---
title: Elemento AggregationFunction (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- AggregationFunction Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AggregationFunction
helpviewer_keywords:
- AggregationFunction element
ms.assetid: 40cfc7f9-1089-45f9-be90-a29770ed9682
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e14f744b35fc1d48ba2a96b15bd8bc3ec46e8e20
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Sum*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Conta](../../../analysis-services/scripting/objects/account-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres a seguir:  
  
|Valor|Description|  
|-----------|-----------------|  
|*Sum*|A medida é agregada usando a função **Sum** .|  
|*Contagem*|A medida é agregada usando a função **Count** .|  
|*Min*|A medida é agregada usando a função **Min** .|  
|*Max*|A medida é agregada usando a função **Max** .|  
|*DistinctCount*|A medida é agregada usando a função **DistinctCount** .|  
|*Nenhuma*|A medida não é agregada.|  
|*AverageOfChildren*|A medida é agregada retornando a média de seus filhos.|  
|*FirstChild*|A medida é agregada retornando seu primeiro membro filho.|  
|*LastChild*|A medida é agregada retornando seu último membro filho.|  
|*FirstNonEmpty*|A medida é agregada retornando seu primeiro membro não vazio.|  
|*LastNonEmpty*|A medida é agregada retornando seu último membro não vazio.|  
  
 A enumeração que corresponde aos valores permitidos para **AggregationFunction** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.AggregationFunction>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Accounts &#40; ASSL &#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

