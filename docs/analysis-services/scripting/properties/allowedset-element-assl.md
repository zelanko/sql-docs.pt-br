---
title: Elemento AllowedSet (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- AllowedSet Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AllowedSet
helpviewer_keywords:
- AllowedSet element
ms.assetid: 4aff2e03-6e1f-4f1a-b99d-d86bba25ab9b
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1cd5a490c8a5d0edf78c3071f9ea118602132f18
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="allowedset-element-assl"></a>Elemento AllowedSet (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contém uma expressão de conjunto que define o conjunto de permissões permitidas para um [função](../../../analysis-services/scripting/objects/role-element-assl.md) elemento em um atributo.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<AttributePermission>  
      ...  
   <AllowedSet>...</AllowedSet>  
   ...  
</AttributePermission>  
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
|Elementos pai|[AttributePermission](../../../analysis-services/scripting/objects/attributepermission-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 O elemento que corresponde ao pai do **AllowedSet** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.AttributePermission>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
