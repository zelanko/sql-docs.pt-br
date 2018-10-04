---
title: Conjunto de linhas DISCOVER_SCHEMA_ROWSETS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DISCOVER_SCHEMA_ROWSETS
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_SCHEMA_ROWSETS rowset
ms.assetid: e5012aa0-6ef8-497f-96c1-2772e2394f62
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 951914dd810b3f9ec9fca52790510541a1cca604
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48124216"
---
# <a name="discoverschemarowsets-rowset"></a>Conjunto de linhas DISCOVER_SCHEMA_ROWSETS
  Retorna os nomes, as restrições, a descrição e outras informações para todos os valores de enumeração e quaisquer valores adicionais de enumeração específica de provedor que recebem suporte do provedor do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA).  
  
 Se você chamar o [Discover](../../xmla/xml-elements-methods-discover.md) método com o `DISCOVER_SCHEMA_ROWSETS` valor de enumeração no [RequestType](../../xmla/xml-elements-properties/type-element-xmla.md) elemento, o `Discover` método retorna o `DISCOVER_SCHEMA_ROWSETS` conjunto de linhas.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas DISCOVER_SCHEMA_ROWSETS contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`SchemaName`|`DBTYPE_WSTR`||O nome do esquema ou solicitação. Essa solicitação retorna os valores na enumeração *RequestTypes* .|  
|`SchemaGuid`|`DBTYPE_GUID`||O GUID do esquema.|  
|`Restrictions`|`DBTYPE_HCHAPTER`||Uma matriz das restrições suportadas pelo provedor.|  
|`Description`|`DBTYPE_WSTR`||Uma descrição localizável do esquema.|  
|`RestrictionsMask`|`DBTYPE_UI8`|||  
  
 Este conjunto de linhas do esquema não é classificado.  
  
 Para um provedor que dá suporte a três restrições para o conjunto de linhas de esquema de DBSCHEMA_MEMBERS, a matriz `Restrictions` deve retornar o resultado a seguir. Os elementos no resultado se referem a nomes de colunas no esquema.  
  
```  
<Restrictions>  
      <CATALOG_NAME type="string" />   
      <SCHEMA_NAME type="string" />   
      <CUBE_NAME type="string" />   
</Restrictions>  
```  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `DISCOVER_SCHEMA_ROWSETS` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`SchemaName`|`DBTYPE_WSTR`||  
  
## <a name="see-also"></a>Consulte também  
 [Conjunto de linhas de esquema do XML](xml-for-analysis-schema-rowsets.md)  
  
  
