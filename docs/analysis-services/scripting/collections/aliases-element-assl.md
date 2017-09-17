---
title: Elemento aliases (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Aliases Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Aliases
helpviewer_keywords:
- Aliases element
ms.assetid: 9de9e683-d30d-4d61-b32d-c5a946825742
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a2c0b1eb29df31046b0cb8175be382af50a920a3
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="aliases-element-assl"></a>Elemento Aliases (ASSL)
  Contém a coleção de [Alias](../../../analysis-services/scripting/properties/alias-element-assl.md) elementos associados a um [conta](../../../analysis-services/scripting/objects/account-element-assl.md) elemento  
  
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum (coleção)|  
|Valor padrão|Nenhum (coleção)|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Conta](../../../analysis-services/scripting/objects/account-element-assl.md)|  
|Elementos filho|[Alias](../../../analysis-services/scripting/properties/alias-element-assl.md)|  
  
## <a name="remarks"></a>Comentários  
 O elemento correspondente para o pai do **Aliases** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Account>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Accounts &#40; ASSL &#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)   
 [Elemento de banco de dados &#40; ASSL &#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Coleções de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
