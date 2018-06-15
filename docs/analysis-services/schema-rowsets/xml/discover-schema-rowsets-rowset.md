---
title: Conjunto de linhas DISCOVER_SCHEMA_ROWSETS | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7349a3e4877813003212b125de31e7b98343313d
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34031907"
---
# <a name="discoverschemarowsets-rowset"></a>Conjunto de linhas DISCOVER_SCHEMA_ROWSETS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Retorna os nomes, as restrições, a descrição e outras informações para todos os valores de enumeração e quaisquer valores adicionais de enumeração específica de provedor que recebem suporte do provedor do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA).  
  
 Se você chamar o [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método com o **DISCOVER_SCHEMA_ROWSETS** valor de enumeração no [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) elemento, o **Discover**método retorna o **DISCOVER_SCHEMA_ROWSETS** conjunto de linhas.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas DISCOVER_SCHEMA_ROWSETS contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**schemaName**|**DBTYPE_WSTR**||O nome do esquema ou solicitação. Essa solicitação retorna os valores na enumeração *RequestTypes* .|  
|**SchemaGuid**|**DBTYPE_GUID**||O GUID do esquema.|  
|**Restrições**|**DBTYPE_HCHAPTER**||Uma matriz das restrições suportadas pelo provedor.|  
|**Descrição**|**DBTYPE_WSTR**||Uma descrição localizável do esquema.|  
|**RestrictionsMask**|**DBTYPE_UI8**|||  
  
 Este conjunto de linhas do esquema não é classificado.  
  
 Para um provedor que dá suporte a três restrições para o conjunto de linhas de esquema de DBSCHEMA_MEMBERS, a matriz **Restrictions** deve retornar o resultado a seguir. Os elementos no resultado se referem a nomes de colunas no esquema.  
  
```  
<Restrictions>  
      <CATALOG_NAME type="string" />   
      <SCHEMA_NAME type="string" />   
      <CUBE_NAME type="string" />   
</Restrictions>  
```  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas **DISCOVER_SCHEMA_ROWSETS** pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**schemaName**|**DBTYPE_WSTR**||  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis conjuntos de linhas de esquema](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
