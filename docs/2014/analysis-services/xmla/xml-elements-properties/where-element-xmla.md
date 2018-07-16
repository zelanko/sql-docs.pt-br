---
title: Em que o elemento (XMLA) | Microsoft Docs
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
- Where Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Where
- microsoft.xml.analysis.where
- http://schemas.microsoft.com/analysisservices/2003/engine#Where
helpviewer_keywords:
- Where element
ms.assetid: 81fb4190-3379-4ddf-8795-a0772f3b92bb
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 44d6242d0c815ee8ec150936a5e41ad12de4a59d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37218066"
---
# <a name="where-element-xmla"></a>Elemento Where (XMLA)
  Define uma condição de filtro usada pelo comando pai [Drop](../xml-elements-commands/drop-element-xmla.md) ou [Update](../xml-elements-commands/update-element-xmla.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Drop> <!-- or Update -->  
   ...  
   <Where>  
      <Attributes>...</Attributes>  
   </Where>  
   ...  
</Insert>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Drop](../xml-elements-commands/drop-element-xmla.md), [Update](../xml-elements-commands/update-element-xmla.md)|  
|Elementos filho|[Atributos](attributes-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 Para `Drop` comandos, o `Where` elemento, combinado com o [DeleteWithDescendants](deletewithdescendants-element-xmla.md) elemento, identifica o escopo dos membros de atributo a ser removido.  
  
 Para comandos `Update`, o elemento `Where` identifica o escopo dos membros de atributo a serem atualizados. Vários membros de atributo podem ser atualizados com uma combinação de atributos incluídos na coleção `Attributes` do comando pai `Update` e na coleção `Attributes` do elemento `Where`.  
  
 Para obter mais informações sobre a exclusão e atualização de membros de atributo, consulte [Inserindo, atualizando e descartando membros &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
