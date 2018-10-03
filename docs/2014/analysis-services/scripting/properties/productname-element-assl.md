---
title: Elemento ProductName (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ProductName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ProductName
helpviewer_keywords:
- ProductName element
ms.assetid: f8129bb2-55c9-44e1-8857-82dc01c04a7f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 959f6624e0ce22647f724279042f5cd6ab6ba2f3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48149886"
---
# <a name="productname-element-assl"></a>Elemento ProductName (ASSL)
  Contém o nome de produto somente leitura da instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que está associado com um [servidor](../objects/server-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Server>  
      ...  
      <ProductName>...</ProductName>  
   ...  
</Server>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|None|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Servidor](../objects/server-element-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O elemento `ProductName` provê acesso somente leitura ao nome do produto associado a uma instância de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 O elemento que corresponde ao pai de `ProductName` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Server>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
