---
title: Conjunto de linhas DISCOVER_LITERALS | Microsoft Docs
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
- DISCOVER_LITERALS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_LITERALS rowset
ms.assetid: 1bf0a2e2-a419-4c25-b271-37dfa44de2ea
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: dc239de2abb609aa035880c0cf9dd9217343c08c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="discoverliterals-rowset"></a>Conjunto de linhas DISCOVER_LITERALS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Retorna informações sobre literais, incluindo tipos de dados e valores, com suporte do provedor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XMLA (XML for Analysis).  
  
 Se você chamar o [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método com o **DISCOVER_LITERALS** valor de enumeração no [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) elemento, o **Discover** método retorna o **DISCOVER_LITERALS** conjunto de linhas.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O **DISCOVER_LITERALS** linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**LiteralName**|**DBTYPE_WSTR**||O nome do literal descrito na linha.<br /><br /> Por exemplo: **DBLITERAL_LIKE_PERCENT**|  
|**LiteralValue**|**DBTYPE_WSTR**||Um valor literal real.<br /><br /> Por exemplo, se **LiteralName** é **DBLITERAL_LIKE_PERCENT** e o caractere de porcentagem (**%**) corresponde a zero ou mais caracteres em uma cláusula LIKE, o valor do **LiteralValue** coluna é "**%**".|  
|**LiteralInvalidChars**|**DBTYPE_WSTR**||Os caracteres que não são válidos no literal.<br /><br /> Por exemplo, se os nomes de tabela podem conter qualquer coisa diferente de um caractere numérico, essa cadeia de caracteres é "**0123456789**".|  
|**LiteralInvalidStartingChars**|**DBTYPE_WSTR**||Os caracteres que não são válidos, como o primeiro caractere do literal. Se o literal puder iniciar com qualquer caractere válido, isso é **nulo**.|  
|**LiteralMaxLength**|**DBTYPE_I4**||O número máximo de caracteres no literal. Se não houver um valor máximo ou o máximo for desconhecido, o valor será –1.|  
|**LiteralNameEnumValue**|**DBTYPE_I4**|||  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O **DISCOVER_LITERALS** linhas pode ser restringido nas colunas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**LiteralName**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis conjuntos de linhas de esquema](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)   
 [Conjunto de linhas DISCOVER_KEYWORDS & #40; XMLA & #41;](../../../analysis-services/schema-rowsets/xml/discover-keywords-rowset-xmla.md)  
  
  
