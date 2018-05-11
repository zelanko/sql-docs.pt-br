---
title: Elemento AllowedRowsExpression (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7bca46eeaafa4f0e028b08d9f70903f1e6e84b9f
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="allowedrowsexpression-element-assl"></a>AllowedRowsExpression Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contém uma expressão DAX, do tipo booliano, que define o conteúdo do elemento pai.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<CellPermission> <!-- or StandardAction -->  
   ...  
   <Expression>...</Expression>  
   ...  
</CellPermission>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CellPermission](../../../analysis-services/scripting/objects/cellpermission-element-assl.md), [StandardAction](../../../analysis-services/scripting/data-type/standardaction-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 Para o **CellPermission** elemento, o **expressão** elemento contém uma expressão MDX lógica que identifica células aplicáveis aos direitos indicados pelo [acesso](../../../analysis-services/scripting/properties/access-element-assl.md) elemento do **CellPermission** elemento. Se o valor de um **expressão** elemento para uma **CellPermission** elemento está vazio, o **CellPermission** elemento será ignorado.  
  
 Para o **StandardAction** elemento, o **expressão** elemento contém uma expressão MDX que representa o conteúdo da ação. Se o valor de um **expressão** elemento para uma **StandardAction** elemento está vazio, o **StandardAction** elemento será ignorado.  
  
 Os elementos que correspondem aos pais no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.CellPermission> e <xref:Microsoft.AnalysisServices.StandardAction>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
