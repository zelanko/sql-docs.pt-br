---
title: Onde o elemento (XMLA) | Microsoft Docs
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
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 4e63d2ecd6f20d374c6746c7d3bc77ad455f1ef6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122923"
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
 Para `Drop` comandos, o `Where` elemento, combinado com o [DeleteWithDescendants](deletewithdescendants-element-xmla.md) elemento, identifica o escopo de membros de atributo a ser removido.  
  
 Para comandos `Update`, o elemento `Where` identifica o escopo dos membros de atributo a serem atualizados. Vários membros de atributo podem ser atualizados com uma combinação de atributos incluídos na coleção `Attributes` do comando pai `Update` e na coleção `Attributes` do elemento `Where`.  
  
 Para obter mais informações sobre a exclusão e atualização de membros de atributo, consulte [Inserindo, atualizando e descartando membros &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  