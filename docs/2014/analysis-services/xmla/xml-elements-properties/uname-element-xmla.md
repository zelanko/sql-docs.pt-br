---
title: Elemento UName (XMLA) | Microsoft Docs
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
- UName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#UName
- urn:schemas-microsoft-com:xml-analysis#UName
- microsoft.xml.analysis.uname
helpviewer_keywords:
- UName element
ms.assetid: b4916d44-cf77-4d4c-b4e5-a0a98192d057
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fa8df2d964db3c8131b9566e04b05c106638d62e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185123"
---
# <a name="uname-element-xmla"></a>Elemento UName (XMLA)
  Contém o nome exclusivo do pai [HierarchyInfo](hierarchyinfo-element-xmla.md) ou [membro](member-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<HierarchyInfo> <!-- or Member -->  
   ...  
   <UName>...</UName>  
   ...  
</HierarchyInfo>  
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
|Elementos pai|[HierarchyInfo](hierarchyinfo-element-xmla.md), [Member](member-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Para elementos `HierarchyInfo`, o elemento `UName` contém o nome da propriedade que fornece os nomes do membro exclusivo da hierarquia. O valor é equivalente à propriedade MEMBER_UNIQUE_NAME definida para conjuntos de linhas de eixo no comando OLE DB para a especificação OLAP.  
  
 Para os elementos `Member`, o elemento `UName` contém o nome exclusivo do elemento pai `Member`.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
