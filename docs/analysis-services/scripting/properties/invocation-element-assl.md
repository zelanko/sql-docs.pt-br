---
title: Elemento Invocation (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- Invocation Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Invocation
helpviewer_keywords:
- Invocation element
ms.assetid: f6bf64ad-ae57-4d46-bf92-1d07a65378bb
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d48dedecabb385ebacd752fff75d6ccec2e1489c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="invocation-element-assl"></a>Elemento Invocation (ASSL)
  Especifica como um [ação](../../../analysis-services/scripting/objects/action-element-assl.md) deve ser chamado.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Action>  
   ...  
   <Invocation>...</Invocation>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Interativo*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Ação](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 A invocação de uma ação depende do aplicativo cliente. O **invocação** elemento sugere a um aplicativo cliente como uma ação deve ser tratada e não indica à instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] como invocar uma ação.  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Interativo*|Chamado interativamente pelo usuário.|  
|*AoAbrir*|Chamado quando um aplicativo cliente abre o objeto.|  
|*Lote*|Chamado por um comando de processamento em lote.|  
  
 A enumeração que corresponde aos valores permitidos para **invocação** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Action>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

