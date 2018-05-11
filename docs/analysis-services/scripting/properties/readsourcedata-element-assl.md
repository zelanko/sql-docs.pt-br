---
title: Elemento ReadSourceData (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 5f492f8334e9ff2c79e760549e493e5d66022bc7
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="readsourcedata-element-assl"></a>Elemento ReadSourceData (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Determina como nomes exclusivos são gerados para hierarquias que estão contidas dentro do [CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CubePermission>  
   ...  
   <ReadSourceData>...</ReadSourceData>  
   ...  
</CubePermission>  
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
|Elemento pai|[CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Nenhuma*|Nenhum acesso é permitido aos dados disponíveis na fase de cálculo 0.|  
|*Permitido*|O acesso é permitido aos dados disponíveis na fase de cálculo 0.|  
  
## <a name="remarks"></a>Remarks  
 O elemento que corresponde ao pai do **ReadSourceData** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.CubePermission>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Cube & #40; ASSL & #41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [Elemento Dimension & #40; ASSL & #41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
