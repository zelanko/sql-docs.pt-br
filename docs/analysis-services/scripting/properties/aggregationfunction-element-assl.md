---
title: Elemento AggregationFunction (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
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
manager: kfile
ms.openlocfilehash: c7c9aedc12abbeb5ab805e0d85cfe1421857749b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="aggregationfunction-element-assl"></a>Elemento AggregationFunction (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres a seguir:  
  
|Value|Description|  
|-----------|-----------------|  
|*Sum*|A medida é agregada usando a função **Sum** .|  
|*Count*|A medida é agregada usando a função **Count** .|  
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
 [Contas de elemento &#40;ASSL&#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)   
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
