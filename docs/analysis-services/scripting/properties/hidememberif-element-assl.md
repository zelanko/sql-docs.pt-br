---
title: Elemento HideMemberIf (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0e01cbbf403636bf42a806ba516f9947eaab20e4
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
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
  
  
