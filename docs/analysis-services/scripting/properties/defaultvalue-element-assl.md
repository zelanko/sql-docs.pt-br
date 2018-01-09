---
title: Elemento DefaultValue (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DefaultValue Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DefaultValue
helpviewer_keywords: DefaultValue element
ms.assetid: 87e964a3-f317-46c3-98c7-b3621765c77b
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1843aba22fa964ebfdca96ed02a0a07348139074
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="defaultvalue-element-assl"></a>Elemento DefaultValue (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém o valor padrão de somente leitura associado [ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ServerProperty>  
   ...  
   <DefaultValue>   </DefaultValue>  
   ...  
</ServerProperty>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Qualquer simpleType|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Esse elemento contém o valor padrão de instalação somente de leitura do **ServerProperty** para a instância atual do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. O valor padrão é fornecido pela instância e normalmente não pode ser alterado.  
  
 O elemento que corresponde ao pai do **DefaultValue** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ServerProperty>.  
  
## <a name="see-also"></a>Consulte Também  
 [Elemento ServerProperties &#40; ASSL &#41;](../../../analysis-services/scripting/collections/serverproperties-element-assl.md)   
 [Elemento Server &#40; ASSL &#41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
