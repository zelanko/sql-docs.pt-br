---
title: Elemento AttributePermission (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AttributePermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AttributePermission
helpviewer_keywords:
- AttributePermission element
ms.assetid: efc8aa63-3959-4b2e-98f8-2a9c424298c2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1da791fae7c8b802c8de0642f25025fe311155d4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074756"
---
# <a name="attributepermission-element-assl"></a>Elemento AttributePermission (ASSL)
  Define as permissões que os membros de um [função](role-element-assl.md) elemento têm nos atributos de uma dimensão individual em um [cubo](cube-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AttributePermissions>  
   <AttributePermission>  
      <AttributeID>...</AttributeID>  
      <Description>...</Description>  
      <DefaultMember>...</DefaultMember>  
            <VisualTotals>...</VisualTotals>  
      <AllowedSet>...</AllowedSet>  
            <DeniedSet>...</DeniedSet>  
      <Annotations>...</Annotations>  
   </AttributePermission>  
</AttributePermissions>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|None|  
|Valor padrão|None|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[AttributePermissions](../collections/attributepermissions-element-assl.md)|  
|Elementos filho|[AllowedSet](../properties/allowedset-element-assl.md), [anotações](../collections/annotations-element-assl.md), [AttributeID](../properties/id-element-assl.md), [DefaultMember](member-element-assl.md), [DeniedSet](../properties/deniedset-element-assl.md), [descrição ](../properties/description-element-assl.md), [VisualTotals](../properties/visualtotals-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.AttributePermission>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados CubeDimensionPermission &#40;ASSL&#41;](../data-type/permission-data-type-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
