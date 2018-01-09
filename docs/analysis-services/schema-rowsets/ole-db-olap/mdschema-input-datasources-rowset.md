---
title: Conjunto de linhas MDSCHEMA_INPUT_DATASOURCES | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: MDSCHEMA_INPUT_DATASOURCES
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_INPUT_DATASOURCES rowset
ms.assetid: 12482fd5-16e3-4171-9cb0-76d0d4f5308e
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a810fef41d402cb35d9e6e3c62120f09b0c6bae4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="mdschemainputdatasources-rowset"></a>Conjunto de linhas MDSCHEMA_INPUT_DATASOURCES
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Descreve as fontes de dados definidas no banco de dados.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Conjuntos de linhas de esquema OLE DB para OLAP](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
