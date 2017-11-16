---
title: Elemento PendingValue (ASSL) | Microsoft Docs
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
- PendingValue Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- PendingValue
helpviewer_keywords:
- PendingValue element
ms.assetid: 386b2ec6-3d83-42d2-b83a-83e375fbdcbd
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5f52fd24820bf616cf82fb6e322329a9bdeb5bea
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="pendingvalue-element-assl"></a>Elemento PendingValue (ASSL)
  Contém somente leitura pendentes valor associado [ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ServerProperty>  
   ...  
   <PendingValue>...</PendingValue>  
   ...  
</ServerProperty>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Qualquer simpleType|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Esse elemento contém o valor de **ServerProperty** que será usado na próxima vez que a instância atual do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] é iniciado. Esse valor normalmente é recuperado de qualquer lugar onde o valor da propriedade de servidor está armazenado, em um arquivo de inicialização, no registro do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows ou em outro mecanismo de armazenamento.  
  
 O elemento que corresponde ao pai do **PendingValue** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ServerProperty>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento ServerProperties &#40; ASSL &#41;](../../../analysis-services/scripting/collections/serverproperties-element-assl.md)   
 [Elemento Server &#40; ASSL &#41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

