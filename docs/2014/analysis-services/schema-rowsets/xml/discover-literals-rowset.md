---
title: Conjunto de linhas DISCOVER_LITERALS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DISCOVER_LITERALS
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_LITERALS rowset
ms.assetid: 1bf0a2e2-a419-4c25-b271-37dfa44de2ea
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: a4643ab803f3e6a7d63c4172423e909b6badd64b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012087"
---
# <a name="discoverliterals-rowset"></a>Conjunto de linhas DISCOVER_LITERALS
  Retorna informações sobre literais, incluindo tipos de dados e valores, com suporte do provedor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XMLA (XML for Analysis).  
  
 Se você chamar o [Discover](../../xmla/xml-elements-methods-discover.md) método com o `DISCOVER_LITERALS` valor de enumeração no [RequestType](../../xmla/xml-elements-properties/type-element-xmla.md) elemento, o `Discover` método retorna o `DISCOVER_LITERALS` conjunto de linhas.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DISCOVER_LITERALS` linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`LiteralName`|`DBTYPE_WSTR`||O nome do literal descrito na linha.<br /><br /> Por exemplo: `DBLITERAL_LIKE_PERCENT`|  
|`LiteralValue`|`DBTYPE_WSTR`||Um valor literal real.<br /><br /> Por exemplo, se `LiteralName` for `DBLITERAL_LIKE_PERCENT` e o caractere de percentual (`%`) corresponder a zero ou mais caracteres em uma cláusula LIKE, o valor da coluna `LiteralValue` será "`%`".|  
|`LiteralInvalidChars`|`DBTYPE_WSTR`||Os caracteres que não são válidos no literal.<br /><br /> Por exemplo, se nomes de tabela puderem conter qualquer coisa que não seja um caractere numérico, essa cadeia de caracteres será "`0123456789`".|  
|`LiteralInvalidStartingChars`|`DBTYPE_WSTR`||Os caracteres que não são válidos, como o primeiro caractere do literal. Se o literal puder iniciar com qualquer caractere válido, ele será `null`.|  
|`LiteralMaxLength`|`DBTYPE_I4`||O número máximo de caracteres no literal. Se não houver um valor máximo ou o máximo for desconhecido, o valor será –1.|  
|`LiteralNameEnumValue`|`DBTYPE_I4`|||  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `DISCOVER_LITERALS` pode ser restringido nas colunas da tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`LiteralName`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis conjuntos de linhas de esquema](xml-for-analysis-schema-rowsets.md)   
 [Conjunto de linhas DISCOVER_KEYWORDS &#40;XMLA&#41;](discover-keywords-rowset-xmla.md)  
  
  