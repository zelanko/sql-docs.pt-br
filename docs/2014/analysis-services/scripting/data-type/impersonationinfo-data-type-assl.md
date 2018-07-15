---
title: Tipo de dados ImpersonationInfo (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ImpersonationInfo Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ImpersonationInfo data type
ms.assetid: 8a6b55fe-1f02-4519-bdc2-4553b576b2f3
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 25321c491db72fb61770b48a3d75743cf50276bd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37310726"
---
# <a name="impersonationinfo-data-type-assl"></a>Tipo de dados ImpersonationInfo (ASSL)
  Define um tipo de dados primitivo que representa as informações usadas para representar um usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ImpersonationInfo>  
   <ImpersonationMode>...</ImpersonationMode>  
   <Account>...</Account>  
   <Password>   </Password>  
   <ImpersonationInfoSecurity>...</ImpersonationInfoSecurity>  
</ImpersonationInfo>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipo de dados base|Nenhum|  
|Tipos de dados derivados|Nenhum|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhum|  
|Elementos filho|[Account](../properties/account-element-impersonationinfo-assl.md), [ImpersonationInfoSecurity](../properties/impersonationinfosecurity-element-assl.md), [ImpersonationMode](../properties/impersonationmode-element-assl.md), [Password](../properties/password-element-assl.md)|  
|Elementos derivados|[DataSourceImpersonationInfo](../properties/impersonationinfo-element-assl.md), [ImpersonationInfo](../properties/impersonationinfo-element-assl.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
