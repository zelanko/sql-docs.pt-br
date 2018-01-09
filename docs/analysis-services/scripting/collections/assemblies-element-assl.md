---
title: Elemento assemblies (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Assemblies Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Assemblies
helpviewer_keywords: Assemblies element
ms.assetid: 8c9be991-0717-4fcf-97d9-13df0f27da05
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9ac91c9fdec23334538c4464fad2bfe736e1b708
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="assemblies-element-assl"></a>Elemento Assemblies (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém a coleção de [Assembly](../../../analysis-services/scripting/objects/assembly-element-assl.md) elementos associados a um [servidor](../../../analysis-services/scripting/objects/server-element-assl.md) ou [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Server> <!-- or Database -->  
   ...  
   <Assemblies>  
      <Assembly xsi:type="ClrAssembly">...</Assembly>  
            <Assembly xsi:type="ComAssembly">...</Assembly>  
   </Assemblies>  
   ...  
</Server>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Database](../../../analysis-services/scripting/objects/database-element-assl.md), [Server](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|Elementos filho|[Assembly](../../../analysis-services/scripting/objects/assembly-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.AssemblyCollection>.  
  
## <a name="see-also"></a>Consulte Também  
 [Coleções de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
