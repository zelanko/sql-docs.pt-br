---
title: Elemento RequestType (XMLA) | Microsoft Docs
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
- RequestType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#RequestType
- urn:schemas-microsoft-com:xml-analysis#RequestType
- microsoft.xml.analysis.requesttype
helpviewer_keywords:
- RequestType element
ms.assetid: 54270a57-e327-4233-b4b2-d85b44652ac5
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d73bcac80918bc79064e0b6e1a4eabf315cdcd9a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37171187"
---
# <a name="requesttype-element-xmla"></a>Elemento RequestType (XMLA)
  Determina o tipo de metadados retornados pela [Discover](../xml-elements-methods-discover.md) método.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Discover>  
   ...  
   <RequestType>...</RequestType>  
   ...  
</Discover>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Descobrir](../xml-elements-methods-discover.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O elemento `RequestType` determina o conjunto de linhas de esquema a partir do qual o método `Discover` retorna dados. Essa enumeração é limitada aos nomes dos conjuntos de linhas de esquema com suporte pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Para obter mais informações sobre conjuntos de linhas de esquema, consulte [conjuntos de linhas de esquema do Analysis Services](../../schema-rowsets/analysis-services-schema-rowsets.md).  
  
> [!NOTE]  
>  O elemento `RequestType` só enumera nomes de conjunto de linhas de esquema. Ocorre um erro se for usado o conjunto de linhas de esquema GUID.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
