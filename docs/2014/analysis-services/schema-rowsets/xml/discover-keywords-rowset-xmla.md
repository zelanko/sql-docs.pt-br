---
title: Conjunto de linhas DISCOVER_KEYWORDS (XMLA) | Microsoft Docs
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
- DISCOVER_KEYWORDS
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_KEYWORDS rowset
ms.assetid: 99945e53-3a1b-4d7b-9aff-712977db8b2d
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a8be22c5132ed85ecb515ccadce20ecd593818a2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37241546"
---
# <a name="discoverkeywords-rowset-xmla"></a>Conjunto de linhas DISCOVER_KEYWORDS (XMLA)
  Retorna informações sobre palavras-chave reservadas pelo provedor do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA).  
  
 Se você chamar o [Discover](../../xmla/xml-elements-methods-discover.md) método com o `DISCOVER_KEYWORDS` valor de enumeração no [RequestType](../../xmla/xml-elements-properties/type-element-xmla.md) elemento, o `Discover` método retorna o `DISCOVER_KEYWORDS` conjunto de linhas.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DISCOVER_KEYWORDS` linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`Keyword`|`DBTYPE_WSTR`||Uma lista de todas as palavras-chaves reservadas por um provedor.<br /><br /> Exemplo: `AND`|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `DISCOVER_KEYWORDS` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`Keyword`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis Schema Rowsets](xml-for-analysis-schema-rowsets.md)   
 [Conjunto de linhas DISCOVER_LITERALS](discover-literals-rowset.md)  
  
  
