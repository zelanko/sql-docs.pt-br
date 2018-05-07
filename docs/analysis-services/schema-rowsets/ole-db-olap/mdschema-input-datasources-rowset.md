---
title: Conjunto de linhas MDSCHEMA_INPUT_DATASOURCES | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6efa6baf40c41db7de09ebcb4e5c44990ff7e6ed
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="mdschemainputdatasources-rowset"></a>Conjunto de linhas MDSCHEMA_INPUT_DATASOURCES
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Descreve as fontes de dados definidas dentro do banco de dados.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **MDSCHEMA_INPUT_DATASOURCES** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||O nome do catálogo ao qual pertence essa fonte de dados.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||Sem suporte.|  
|**DATASOURCE_NAME**|**DBTYPE_WSTR**||O nome do objeto de fonte de dados.|  
|**DATASOURCE_TYPE**|**DBTYPE_WSTR**||O tipo da fonte de dados. Os valores válidos incluem:<br /><br /> **Relacional**<br /><br /> **OLAP**|  
|**CREATED_ON**|**DBTYPE_DBTIMESTAMP**||A data de criação da fonte de dados.|  
|**LAST_SCHEMA_UPDATE**|**DBTYPE_DBTIMESTAMP**||A data e a hora da última modificação na fonte de dados.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Uma descrição amigável da ação.|  
|**TEMPO LIMITE**|**DBTYPE_UI4**||O tempo limite da fonte de dados.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas **MDSCHEMA_INPUT_DATASOURCES** pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**DATASOURCE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**DATASOURCE_TYPE**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [OLE DB para OLAP Schema Rowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
