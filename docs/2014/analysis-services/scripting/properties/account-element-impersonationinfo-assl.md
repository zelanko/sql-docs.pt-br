---
title: Elemento (ImpersonationInfo) (ASSL) de conta | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Account Element (ImpersonationInfo)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Account element
ms.assetid: aa3a1281-e42a-4926-875b-e6b81f4599c3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f454e39a7c4ec4911f38ff070f94fcbe50a34c74
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48190366"
---
# <a name="account-element-impersonationinfo-assl"></a>Elemento Account (ImpersonationInfo) (ASSL)
  Contém o nome da conta de usuário para o [ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md) tipo de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ImpersonationInfo  
   ...  
  <Account>...</Account>  
   ...  
</Action>  
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
|Elementos pai|[ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O valor da `Account` elemento, bem como o valor da [senha](password-element-assl.md) elemento, será usado para fins de representação se o valor da [ImpersonationMode](impersonationmode-element-assl.md) elemento para qualquer elemento derivado do `ImpersonationInfo` tipo de dados é definido como *ImpersonateAccount*.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento DataSourceImpersonationInfo &#40;ASSL&#41;](impersonationinfo-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
