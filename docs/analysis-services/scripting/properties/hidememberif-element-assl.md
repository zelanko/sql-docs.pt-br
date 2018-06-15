---
title: Elemento HideMemberIf (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 7c2e76ae7cd667327f2eaf464ba790a34d0b253c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34032417"
---
# <a name="hidememberif-element-assl"></a>Elemento HideMemberIf (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Indica se, e quando, um membro em um nível ficará oculto pelos aplicativos cliente.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Level>  
   ...  
   <HideMemberIf>...</HideMemberIf>  
   ...  
</Level>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Nunca*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Nível](../../../analysis-services/scripting/objects/level-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Nunca*|Membros nunca são ocultados.|  
|*OnlyChildWithNoName*|Um membro é ocultado quando ele for o único filho de seu pai e seu nome estiver vazio.|  
|*OnlyChildWithParentName*|Um membro é ocultado quando ele for o único filho de seu pai e seu nome for idêntico ao de seu pai.|  
|*Sem nome*|Um membro é ocultado quando seu nome estiver vazio.|  
|*ParentName*|Um membro é ocultado quando seu nome for idêntico ao de seu pai.|  
  
## <a name="remarks"></a>Remarks  
 A enumeração que corresponde aos valores permitidos para **HideMemberIf** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.HideIfValue>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
