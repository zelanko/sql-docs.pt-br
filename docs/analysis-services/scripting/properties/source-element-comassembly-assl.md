---
title: Fonte do elemento (ComAssembly) (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Source Element (ComAssembly)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Source
helpviewer_keywords:
- Source element
ms.assetid: 5c9209e8-ace6-4688-a64d-4987a7648ab9
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 29749505f76b06b8facab1895067177b19a6d534
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="source-element-comassembly-assl"></a>Elemento Source (ComAssembly) (ASSL)
  Contém o nome de arquivo ou identificador programático (ProgID) para um componente COM (Component Object Model).  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ComAssembly>  
   ...  
   <Source>...</Source>  
   ...  
</ComAssembly>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[ComAssembly](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O elemento que corresponde ao pai do **fonte** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ComAssembly>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento assembly & #40; ASSL & #41;](../../../analysis-services/scripting/objects/assembly-element-assl.md)   
 [Tipo de dados ClrAssembly & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)   
 [Elemento assemblies & #40; ASSL & #41;](../../../analysis-services/scripting/collections/assemblies-element-assl.md)   
 [Elemento de banco de dados & #40; ASSL & #41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Elemento Server & #40; ASSL & #41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

