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
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 99a340f2bbeb1e5d61a20b4031beeade9fbcc5c7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006925"
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
 Para o `CellPermission` elemento, o `Expression` elemento contém uma expressão MDX lógica que identifica células aplicáveis aos direitos indicados pelo [acesso](access-element-assl.md) elemento o `CellPermission` elemento. Se o valor de um elemento `Expression` para um elemento `CellPermission` estiver vazio, o elemento `CellPermission` será ignorado.  
  
 Para o elemento `StandardAction`, o elemento `Expression` contém uma linguagem MDX que representa o conteúdo da ação. Se o valor de um elemento `Expression` para um elemento `StandardAction` estiver vazio, o elemento `StandardAction` será ignorado.  
  
 Os elementos que correspondem aos pais no modelo de objeto AMO (Objetos de Gerenciamento de Análise) são <xref:Microsoft.AnalysisServices.CellPermission> e <xref:Microsoft.AnalysisServices.StandardAction>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  