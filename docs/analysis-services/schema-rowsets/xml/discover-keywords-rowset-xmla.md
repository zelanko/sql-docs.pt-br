---
title: Conjunto de linhas DISCOVER_KEYWORDS (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DISCOVER_KEYWORDS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_KEYWORDS rowset
ms.assetid: 99945e53-3a1b-4d7b-9aff-712977db8b2d
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 232bbcfb4d5cf1dfc181a0c6d8879e4390f61a9e
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="discoverkeywords-rowset-xmla"></a>Conjunto de linhas DISCOVER_KEYWORDS (XMLA)
  Retorna informações sobre palavras-chave reservadas pelo provedor do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA).  
  
 Se você chamar o método [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) com o valor de enumeração **DISCOVER_KEYWORDS** no elemento [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) , o método **Discover** retornará o conjunto de linhas **DISCOVER_KEYWORDS** .  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DISCOVER_KEYWORDS** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**Palavra-chave**|**DBTYPE_WSTR**||Uma lista de todas as palavras-chaves reservadas por um provedor.<br /><br /> Exemplo: **AND**|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas **DISCOVER_KEYWORDS** pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**Palavra-chave**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis conjuntos de linhas de esquema](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)   
 [Conjunto de linhas DISCOVER_LITERALS](../../../analysis-services/schema-rowsets/xml/discover-literals-rowset.md)  
  
  

