---
title: Elemento ScriptCacheProcessingMode (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f014ac1cbad00a077bee80ec6db32d623e155f9d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="scriptcacheprocessingmode-element-assl"></a>Elemento ScriptCacheProcessingMode (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Indica se o servidor deve criar o cache de scripts durante ou após o processamento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Cube>  
   ...  
      <ScriptCacheProcessingMode>...</ScriptCacheProcessingMode>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Regular*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Regular*|O servidor cria o cache de scripts durante o processamento.|  
|*Lento*|O servidor cria o cache de scripts após o processamento.|  
  
 A enumeração que corresponde aos valores permitidos para **ScriptCacheProcessingMode** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ScriptCacheProcessingMode>.  
  
 O elemento que corresponde ao pai do **ScriptCacheProcessingMode** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Cube>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
