---
title: Elemento LNum (XMLA) | Microsoft Docs
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
- LNum Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.lnum
- urn:schemas-microsoft-com:xml-analysis#LNum
- http://schemas.microsoft.com/analysisservices/2003/engine#LNum
helpviewer_keywords:
- LNum element
ms.assetid: 7b9cc143-0c5e-4a8c-a288-8921bfcfd103
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: affdefb04b94d863faa9a9fb6a9eed8ea5b07606
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36005949"
---
# <a name="lnum-element-xmla"></a>Elemento LNum (XMLA)
  Contém informações sobre posições ordinais de nível pai [HierarchyInfo](hierarchyinfo-element-xmla.md) ou [membro](member-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<HierarchyInfo> <!-- or Member -->  
   ...  
   <LNum>...</LNum>  
   ...  
</HierarchyInfo>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|INT|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[HierarchyInfo](hierarchyinfo-element-xmla.md), [Member](member-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Para elementos `HierarchyInfo`, o elemento `LNum` contém o nome da propriedade que fornece as posições ordinais de nível da hierarquia. O valor é equivalente à propriedade LEVEL_NUMBER definida para conjuntos de linhas de eixo no comando OLE DB para a especificação OLAP.  
  
 Para `Member` elementos, o `LNum` elemento contém a com base em zero posição ordinal do nível raiz da hierarquia do membro representado pelo pai [membro](member-element-xmla.md) elemento. Um valor zero representa o nível raiz da hierarquia.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  