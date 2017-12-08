---
title: Comandos do elemento (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
apiname: Commands Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Commands
helpviewer_keywords: Commands element
ms.assetid: c9f69fe8-2221-469b-b5b0-08563aaa01dc
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f5061f5508e878905408d5b0c210e6513ab4ff37
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="commands-element-assl"></a>Elemento Commands (ASSL)
  Contém a coleção de elementos [Command](../../../analysis-services/scripting/objects/command-element-assl.md) associados a um elemento [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<MdxScript>  
   ...  
   <Commands>  
      <Command>...</Command>  
...</Commands>  
   ...  
</MdxScript>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)|  
|Elementos filho|[Comando](../../../analysis-services/scripting/objects/command-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.CommandCollection>.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
