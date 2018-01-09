---
title: Elemento Role (ASSL) | Microsoft Docs
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
apiname: Role Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ROLE
helpviewer_keywords: Role element
ms.assetid: 56f52462-a7fd-4b51-a7fb-4311134439e9
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7511f1a9aaccf31112685521f20dbe2c69002f31
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="role-element-assl"></a>Elemento Role (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém informações sobre uma função de segurança.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Roles>  
      <Role>  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreateTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Description>...</Description>  
      <Members>...</Members>  
      <Annotations>...</Annotations>  
   </Role>  
</Roles>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Roles](../../../analysis-services/scripting/collections/roles-element-assl.md)|  
|Elementos filho|[Anotações](../../../analysis-services/scripting/collections/annotations-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [descrição](../../../analysis-services/scripting/properties/description-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [ Membros](../../../analysis-services/scripting/collections/members-element-assl.md), [nome](../../../analysis-services/scripting/properties/name-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 A definição da função inclui os usuários que são membros da função.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Role>.  
  
## <a name="see-also"></a>Consulte Também  
 [Elemento de banco de dados &#40; ASSL &#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Elemento Server &#40; ASSL &#41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
