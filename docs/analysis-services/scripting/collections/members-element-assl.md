---
title: Elemento Members (ASSL) | Microsoft Docs
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
- Members Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Members
helpviewer_keywords:
- Members element
ms.assetid: 4bf585a3-b681-486d-852b-1244c5658a04
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 223618d552b1bd0277697c53505ac32c089f3ded
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="members-element-assl"></a>Elemento Members (ASSL)
  Contém a coleção de elementos [Member](../../../analysis-services/scripting/objects/member-element-assl.md) do elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Group> <!-- or Role --<  
   ...  
   <Members>  
      <Member>...</Member>  
   </Members>  
   ...  
</Group>  
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
|Elementos pai|[Group](../../../analysis-services/scripting/objects/group-element-assl.md), [Role](../../../analysis-services/scripting/objects/role-element-assl.md)|  
|Elementos filho|[Membro](../../../analysis-services/scripting/objects/member-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 Os elementos que correspondem aos pais de **membros** no modelo de objeto de Analysis Management Objects (AMO) são <xref:Microsoft.AnalysisServices.Group> e <xref:Microsoft.AnalysisServices.Role>.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
