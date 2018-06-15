---
title: Conjunto de linhas mdschema_measuresgroups | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: df2bfe8aecc32c8f046d18fff4e72cd15409fdc8
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34029037"
---
# <a name="mdschemameasuregroups-rowset"></a>Conjunto de linhas MDSCHEMA_MEASURESGROUPS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Descreve os grupos de medidas dentro de um banco de dados.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **MDSCHEMA_MEASUREGROUPS** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||O nome do catálogo ao qual pertence esse grupo de medidas. **NULL** se o provedor não oferecer suporte a catálogos.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||Sem suporte.|  
|**CUBE_NAME**|**DBTYPE_WSTR**||O nome do cubo ao qual pertence esse grupo de medidas.|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**||O nome do grupo de medidas.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Uma descrição legível do membro.|  
|**IS_WRITE_ENABLED**|**DBTYPE_BOOL**||Um Booliano que indica se um grupo de medidas está habilitado para gravação.<br /><br /> Retornará **true** se o grupo de medidas estiver habilitado para gravação.|  
|**MEASUREGROUP_CAPTION**|**DBTYPE_WSTR**||A legenda de exibição do grupo de medidas.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas **MDSCHEMA_MEASUREGROUPS** pode ser restringido nas colunas da tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [OLE DB para OLAP Schema Rowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
