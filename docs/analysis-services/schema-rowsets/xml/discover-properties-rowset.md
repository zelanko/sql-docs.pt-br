---
title: Conjunto de linhas DISCOVER_PROPERTIES | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
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
manager: kfile
ms.openlocfilehash: f37cf116c4d31dbd63ba13b575a91fa042350863
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
  
  
