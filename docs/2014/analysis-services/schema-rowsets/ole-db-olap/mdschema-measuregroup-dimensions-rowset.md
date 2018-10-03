---
title: Conjunto de linhas MDSCHEMA_MEASUREGROUP_DIMENSIONS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MDSCHEMA_MEASUREGROUP_DIMENSIONS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_MEASUREGROUP_DIMENSIONS rowset
ms.assetid: c731c06a-7382-4e50-ba0e-d8cee3ab4f28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: be9e28aefd3170f8db73f21ae5f3f021be61c34c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48062662"
---
# <a name="mdschemameasuregroupdimensions-rowset"></a>Conjunto de linhas MDSCHEMA_MEASUREGROUP_DIMENSIONS
  Enumera as dimensões de grupos de medidas.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `MDSCHEMA_MEASUREGROUP_DIMENSIONS` linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||O nome do catálogo ao qual pertence esse grupo de medidas. `NULL` se o provedor não oferecer suporte a catálogos.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||Sem suporte.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||O nome do cubo ao qual pertence esse grupo de medidas.|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`||O nome do grupo de medidas.|  
|`MEASUREGROUP_CARDINALITY`|`DBTYPE_WSTR`||O número de instâncias que uma medida do grupo de medidas pode ter para um único membro de dimensão. Os valores possíveis incluem:<br /><br /> -   `ONE`<br />-   `MANY`|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`||O nome exclusivo da dimensão.|  
|`DIMENSION_CARDINALITY`|`DBTYPE_WSTR`||O número de instâncias que um membro da dimensão pode ter para uma única instância de uma medida do grupo de medidas.<br /><br /> Os valores possíveis incluem:<br /><br /> -   `ONE`<br />-   `MANY`|  
|`DIMENSION_IS_VISIBLE`|`DBTYPE_BOOL`||Um Booliano que indica se as hierarquias da dimensão estão visíveis.<br /><br /> Retornará `TRUE` se uma ou mais hierarquias da dimensão estiverem visíveis; caso contrário, `FALSE`.|  
|`DIMENSION_IS_FACT_DIMENSION`|`DBTYPE_BOOL`||Um Booliano que indica se a dimensão é uma dimensão de fatos.<br /><br /> Retornará `TRUE` se a dimensão for uma dimensão de fatos; caso contrário, `FALSE`.|  
|`DIMENSION_PATH`|`DBTYPE_HCHAPTER`||Uma lista de dimensões para a dimensão de referência.|  
|`DIMENSION_GRANULARITY`|`DBTYPE_WSTR`||O nome exclusivo da hierarquia de granularidade.|  
  
 O conjunto de linhas dá suporte à classificação em `CATALOG_NAME`, `SCHEMA_NAME`, `CUBE_NAME`, `MEASUREGROUP_NAME`, `DIMENSION_UNIQUE_NAME`.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `MDSCHEMA_MEASUREGROUP_DIMENSIONS` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`DIMENSION_VISIBILITY`|`DBTYPE_UI2`|(Opcional) Um bitmap com um dos seguintes valores válidos:<br /><br /> -Visible 1<br />-2 não visível<br />-Restrição de padrão é um valor de 1.|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema OLE DB para OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  
