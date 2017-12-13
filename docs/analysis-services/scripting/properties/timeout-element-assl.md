---
title: Elemento Timeout (ASSL) | Microsoft Docs
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
apiname: Timeout Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Timeout
helpviewer_keywords: Timeout element
ms.assetid: 7694872b-bd05-459f-b5dc-3cfbd92a9664
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 77211dad8880244574aa0a3bf1765d89df8013ee
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="timeout-element-assl"></a>Elemento Timeout (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Especifica o tempo, em segundos, depois que uma tentativa de recuperar dados relata um tempo limite.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DataSource>  
   ...  
   <Timeout>...</Timeout>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Duração|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Fonte de dados](../../../analysis-services/scripting/objects/datasource-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O elemento que corresponde ao pai do **Timeout** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DataSource>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
