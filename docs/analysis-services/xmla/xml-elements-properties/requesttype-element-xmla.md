---
title: Elemento RequestType (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 63c1a838d74745b5ef51f73b51e34c95e08a81ff
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37994788"
---
# <a name="requesttype-element-xmla"></a>Elemento RequestType (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Determina o tipo de metadados retornados pela [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método.  
  
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
|Elementos pai|[Descobrir](../../../analysis-services/xmla/xml-elements-methods-discover.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O **RequestType** elemento determina o conjunto de linhas de esquema do qual o **Discover** método retorna dados. Essa enumeração é limitada aos nomes dos conjuntos de linhas de esquema com suporte pelo Analysis Services. Para obter mais informações sobre conjuntos de linhas de esquema, consulte [conjuntos de linhas de esquema do Analysis Services](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md).  
  
> [!NOTE]  
>  O **RequestType** elemento enumera apenas os nomes de conjunto de linhas do esquema. Ocorre um erro se for usado o conjunto de linhas de esquema GUID.  
  
## <a name="see-also"></a>Confira também
 [Propriedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
