---
title: Conjunto de linhas MDSCHEMA_MEASUREGROUP_DIMENSIONS | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4be854b72c773300115e49551ceaf0ddc4d7db81
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="mdschemameasuregroupdimensions-rowset"></a>Conjunto de linhas MDSCHEMA_MEASUREGROUP_DIMENSIONS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Enumera as dimensões de grupos de medidas.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **MDSCHEMA_MEASUREGROUP_DIMENSIONS** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||O nome do catálogo ao qual pertence esse grupo de medidas. **NULL** se o provedor não oferecer suporte a catálogos.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||Sem suporte.|  
|**CUBE_NAME**|**DBTYPE_WSTR**||O nome do cubo ao qual pertence esse grupo de medidas.|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**||O nome do grupo de medidas.|  
|**MEASUREGROUP_CARDINALITY**|**DBTYPE_WSTR**||O número de instâncias que uma medida do grupo de medidas pode ter para um único membro de dimensão. Os valores possíveis incluem:<br /><br /> **UM**<br /><br /> **MUITOS**|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**||O nome exclusivo da dimensão.|  
|**DIMENSION_CARDINALITY**|**DBTYPE_WSTR**||O número de instâncias que um membro da dimensão pode ter para uma única instância de uma medida do grupo de medidas. Os valores possíveis incluem:<br /><br /> **UM**<br /><br /> **MUITOS**|  
|**DIMENSION_IS_VISIBLE**|**DBTYPE_BOOL**||Um Booliano que indica se as hierarquias da dimensão estão visíveis.<br /><br /> Retornará **TRUE** se uma ou mais hierarquias da dimensão estiverem visíveis; caso contrário, **FALSE**.|  
|**DIMENSION_IS_FACT_DIMENSION**|**DBTYPE_BOOL**||Um Booliano que indica se a dimensão é uma dimensão de fatos.<br /><br /> Retornará **TRUE** se a dimensão for uma dimensão de fatos; caso contrário, **FALSE**.|  
|**DIMENSION_PATH**|**DBTYPE_HCHAPTER**||Uma lista de dimensões para a dimensão de referência.|  
|**DIMENSION_GRANULARITY**|**DBTYPE_WSTR**||O nome exclusivo da hierarquia de granularidade.|  
  
 O conjunto de linhas dá suporte à classificação em **CATALOG_NAME**, **SCHEMA_NAME**, **CUBE_NAME**, **MEASUREGROUP_NAME**, **DIMENSION_UNIQUE_NAME**.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas **MDSCHEMA_MEASUREGROUP_DIMENSIONS** pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**DIMENSION_VISIBILITY**|**DBTYPE_UI2**|(Opcional) Um bitmap com um dos seguintes valores válidos:<br /><br /> 1 Visível<br /><br /> 2 não visível<br /><br /> A restrição padrão tem valor 1.|  
  
## <a name="see-also"></a>Consulte também  
 [OLE DB para OLAP Schema Rowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
