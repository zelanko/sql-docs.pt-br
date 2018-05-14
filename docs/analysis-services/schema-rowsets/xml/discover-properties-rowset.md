---
title: Conjunto de linhas DISCOVER_PROPERTIES | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8752af7b67b69659ec3d9a348b4ec7c647f41c55
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="discoverproperties-rowset"></a>Conjunto de linhas DISCOVER_PROPERTIES
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Retorna uma lista de informações e valores sobre o padrão e propriedades específicas do provedor que recebem suporte do provedor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) para a fonte de dados especificada. Propriedades sem-suporte não são listadas no conjunto de resultados retornado.  
  
 Se você chamar o [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método com o **DISCOVER_PROPERTIES** valor de enumeração no [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) elemento, o **Discover** método retorna o **DISCOVER_PROPERTIES** conjunto de linhas.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DISCOVER_PROPERTIES** contém as colunas a seguir.  
  
|Nome da coluna|Tipo|Comprimento|Description|  
|-----------------|----------|------------|-----------------|  
|**propertyName**|**DBTYPE_WSTR**||O nome da propriedade.|  
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
|**propertyName**|**DBTYPE_WSTR**||  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis conjuntos de linhas de esquema](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
