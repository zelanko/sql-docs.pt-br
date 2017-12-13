---
title: Elemento AllowedRowsExpression (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: ec24b11d-d11e-4369-a619-7e41a3c46159
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b4431e5c770f2948ae1c246cd05980737d39c005
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="allowedrowsexpression-element-assl"></a>AllowedRowsExpression Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contém uma expressão de análise de dados (DAX), do tipo booliano, que define o conteúdo do elemento pai.  
  
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
  
## <a name="remarks"></a>Comentários  
 Para o **CellPermission** elemento, o **expressão** elemento contém uma expressão MDX lógica que identifica células aplicáveis aos direitos indicados pelo [acesso](../../../analysis-services/scripting/properties/access-element-assl.md) elemento do **CellPermission** elemento. Se o valor de um **expressão** elemento para uma **CellPermission** elemento está vazio, o **CellPermission** elemento será ignorado.  
  
 Para o **StandardAction** elemento, o **expressão** elemento contém uma expressão MDX que representa o conteúdo da ação. Se o valor de um **expressão** elemento para uma **StandardAction** elemento está vazio, o **StandardAction** elemento será ignorado.  
  
 Os elementos que correspondem aos pais no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.CellPermission> e <xref:Microsoft.AnalysisServices.StandardAction>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
