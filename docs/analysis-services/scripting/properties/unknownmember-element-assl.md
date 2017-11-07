---
title: Elemento UnknownMember (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- UnknownMember Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- UnknownMember
helpviewer_keywords:
- UnknownMember element
ms.assetid: 5558961e-e3c6-4f4e-817d-5b12b0734c03
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5da9cdc237512a47a27b21691864b3da523ce70a
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="unknownmember-element-assl"></a>Elemento UnknownMember (ASSL)
  Indica se o membro desconhecido é visível.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Dimension>  
      ...  
   <UnknownMember>...</UnknownMember>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Nenhuma*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Visível*|O membro desconhecido existe e é exibido.|  
|*Oculto*|O membro desconhecido existe, mas não é exibido.|  
|*Nenhuma*|O membro desconhecido não é usado.|  
  
 A enumeração que corresponde aos valores permitidos para **UnknownMember** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.UnknownMemberBehavior>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento UnknownMemberName &#40; ASSL &#41;](../../../analysis-services/scripting/properties/unknownmembername-element-assl.md)   
 [Elemento UnknownMemberTranslation &#40; ASSL &#41;](../../../analysis-services/scripting/objects/unknownmembertranslation-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

