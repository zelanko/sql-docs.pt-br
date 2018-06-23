---
title: Elemento Password (ASSL) | Microsoft Docs
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
- Password Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Password element
ms.assetid: ee756b01-fb08-4a9a-8c2a-7c04af0f8658
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e702e7307e11c506652e91ca4cdc8f02ca06318d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006429"
---
# <a name="password-element-assl"></a>Elemento Password (ASSL)
  Contém a senha da conta de usuário para o [ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ImpersonationInfo  
   ...  
  <Password>...</Password>  
   ...  
</ImpersonationInfo>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor da `Password` elemento, bem como o valor da [conta](account-element-impersonationinfo-assl.md) elemento, será usado para fins de representação se o valor da [ImpersonationMode](impersonationmode-element-assl.md) de qualquer elemento derivado do `ImpersonationInfo` tipo de dados é definido como *ImpersonateAccount*.  
  
 Apenas os membros da função do administrador do servidor da instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] pode fornecer um valor em branco para o elemento `Password`  
  
## <a name="see-also"></a>Consulte também  
 [Elemento DataSourceImpersonationInfo &#40;ASSL&#41;](impersonationinfo-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  