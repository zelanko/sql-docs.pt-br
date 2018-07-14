---
title: Elemento AllowedRowsExpression (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: ec24b11d-d11e-4369-a619-7e41a3c46159
caps.latest.revision: 7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7f335861084f86fa509b8c2bc3f977332d5e1da7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37291322"
---
# <a name="allowedrowsexpression-element-assl"></a>AllowedRowsExpression Element (ASSL)
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[CellPermission](../objects/cellpermission-element-assl.md), [StandardAction](../data-type/action-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Para o `CellPermission` elemento, o `Expression` elemento contém uma expressão MDX lógica que identifica células aplicáveis aos direitos indicados pelo [Access](access-element-assl.md) elemento do `CellPermission` elemento. Se o valor de um elemento `Expression` para um elemento `CellPermission` estiver vazio, o elemento `CellPermission` será ignorado.  
  
 Para o elemento `StandardAction`, o elemento `Expression` contém uma linguagem MDX que representa o conteúdo da ação. Se o valor de um elemento `Expression` para um elemento `StandardAction` estiver vazio, o elemento `StandardAction` será ignorado.  
  
 Os elementos que correspondem aos pais no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.CellPermission> e <xref:Microsoft.AnalysisServices.StandardAction>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
