---
title: Elemento aliases (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Aliases Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Aliases
helpviewer_keywords:
- Aliases element
ms.assetid: 9de9e683-d30d-4d61-b32d-c5a946825742
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 677434b5ea6383e5905a703225edb5e56e3fb4e7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37267682"
---
# <a name="aliases-element-assl"></a>Elemento Aliases (ASSL)
  Contém a coleção de [Alias](../properties/alias-element-assl.md) elementos associados a um [conta](../objects/account-element-assl.md) elemento  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Account>  
      ...  
   <Aliases>  
      <Alias>...</Alias>  
      </Aliases>  
      ...  
</Account>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum (coleção)|  
|Valor padrão|Nenhum (coleção)|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Conta](../objects/account-element-assl.md)|  
|Elementos filho|[Alias](../properties/alias-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 O elemento que corresponde ao pai de `Aliases` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Account>.  
  
## <a name="see-also"></a>Consulte também  
 [Contas de elemento &#40;ASSL&#41;](accounts-element-assl.md)   
 [Elemento de banco de dados &#40;ASSL&#41;](../objects/database-element-assl.md)   
 [Coleções &#40;ASSL&#41;](collections-assl.md)  
  
  
