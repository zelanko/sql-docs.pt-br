---
title: Conjunto de linhas DISCOVER_PROPERTIES | Microsoft Docs
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
- DISCOVER_PROPERTIES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_PROPERTIES rowset
ms.assetid: 3e2b50e2-3855-4091-8b02-4968e8e57d4c
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 374ca8fc9ce17f7da659a9718e8a7a531e8c3ca5
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="discoverproperties-rowset"></a>Conjunto de linhas DISCOVER_PROPERTIES
  Retorna uma lista de informações e valores sobre o padrão e propriedades específicas do provedor que recebem suporte do provedor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) para a fonte de dados especificada. Propriedades sem-suporte não são listadas no conjunto de resultados retornado.  
  
 Se você chamar o [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método com o **DISCOVER_PROPERTIES** valor de enumeração no [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) elemento, o **Discover** método retorna o **DISCOVER_PROPERTIES** conjunto de linhas.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DISCOVER_PROPERTIES** contém as colunas a seguir.  
  
|Nome da coluna|Tipo|Comprimento|Description|  
|-----------------|----------|------------|-----------------|  
|**PropertyName**|**DBTYPE_WSTR**||O nome da propriedade.|  
|**PropertyDescription**|**DBTYPE_WSTR**||Uma descrição de texto localizável da propriedade. Pode retornar **NULL**.|  
|**PropertyType**|**DBTYPE_WSTR**||O tipo de dados XML da propriedade.<br /><br /> Pode retornar **NULL**.|  
|**PropertyAccessType**|**DBTYPE_WSTR**||O acesso da propriedade. O valor pode ser **Read**, **Write**ou **ReadWrite**.|  
|**IsRequired**|**DBTYPE_BOOL**||Um Booliano que indica se uma propriedade é necessária.<br /><br /> True se uma propriedade for necessária; false se ela não for necessária.<br /><br /> Pode retornar **NULL**.|  
|**Value**|**DBTYPE_WSTR**||O valor atual da propriedade.<br /><br /> Pode retornar **NULL**.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas **DISCOVER_PROPERTIES** pode ser restringido na coluna listada na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**PropertyName**|**DBTYPE_WSTR**||  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis conjuntos de linhas de esquema](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

