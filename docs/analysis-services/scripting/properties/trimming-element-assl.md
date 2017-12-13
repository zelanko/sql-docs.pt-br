---
title: Elemento Trimming (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Trimming Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Trimming
helpviewer_keywords: Trimming element
ms.assetid: 8b3bbf89-8309-4d00-9aea-a5918f0c7027
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a7b5388a374511010c299576ec864056e165e5fa
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="trimming-element-assl"></a>Elemento Trimming (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Especifica como os dados da fonte de dados são cortados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DataItem>  
   ...  
   <Trimming>...</Trimming>  
   ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Certo*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[O item de dados](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*À esquerda*|Os dados são fragmentados à esquerda.|  
|*Certo*|Os dados são fragmentados à direita.|  
|*LeftRight*|Os dados são fragmentados à esquerda e à direita.|  
|*Nenhuma*|Os dados não são fragmentados.|  
  
 A enumeração que corresponde aos valores permitidos para **cortar** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Trimming>.  
  
 O elemento que corresponde ao pai do **cortar** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DataItem>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
