---
title: Conjunto de linhas MDSCHEMA_CUBES | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: MDSCHEMA_CUBES
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_CUBES rowset
ms.assetid: 5f1b63d4-aa3f-48c6-b866-7ffd91675044
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3ff85f0461a9ca0abc7c9acdfdd4cb2b23722c41
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="mdschemacubes-rowset"></a>Conjunto de linhas MDSCHEMA_CUBES
  Descreve a estrutura de cubos dentro de um banco de dados.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **MDSCHEMA_CUBES** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|O nome do banco de dados.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Sem suporte.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|O nome do cubo ou da dimensão. Nomes de dimensão são antecedidos por um símbolo de cifrão ($).<br /><br /> Observação: Somente servidores e administradores de banco de dados tem permissões para consultar cubos criados a partir de uma dimensão.|  
|**CUBE_TYPE**|**DBTYPE_WSTR**|O tipo do cubo. Os valores válidos são:<br /><br /> **CUBO**<br /><br /> **DIMENSÃO**|  
|**CUBE_GUID**|**DBTYPE_GUID**|Sem suporte.|  
|**CREATED_ON**|**DBTYPE_DBTIMESTAMP**|Sem suporte.|  
|**LAST_SCHEMA_UPDATE**|**DBTYPE_DBTIMESTAMP**|O horário do último processamento do cubo.|  
|**SCHEMA_UPDATED_BY**|**DBTYPE_WSTR**|Sem suporte.|  
|**LAST_DATA_UPDATE**|**DBTYPE_DBTIMESTAMP**|O horário do último processamento do cubo.|  
|**DATA_UPDATED_BY**|**DBTYPE_WSTR**|Sem suporte.|  
|**DESCRIPTION**|**DBTYPE_WSTR**|Uma descrição amigável do cubo.|  
|**IS_DRILLTHROUGH_ENABLED**|**DBTYPE_BOOL**|Um Booliano que sempre retorna true.|  
|**IS_LINKABLE**|**DBTYPE_BOOL**|Um Booliano isso indica se um cubo pode ser usado em um cubo vinculado.|  
|**IS_WRITE_ENABLED**|**DBTYPE_BOOL**|Um Booliano que indica se um cubo está habilitado para gravação.|  
|**IS_SQL_ENABLED**|**DBTYPE_BOOL**|Um Booliano que indica se um SQL pode ser usado no cubo.|  
|**CUBE_CAPTION**|**DBTYPE_WSTR**|A legenda do cubo.|  
|**BASE_CUBE_NAME**|**DBTYPE_WSTR**|O nome do cubo de origem se esse cubo for um cubo de perspectiva.|  
|**ANOTAÇÕES**|**DBTYPE_WSTR**|(Opcional) Um conjunto de notas em formato XML.|  
  
 O conjunto de linhas é classificado em **CATALOG_NAME**, **SCHEMA_NAME**, **CUBE_NAME**.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas **MDSCHEMA_CUBES** pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(Opcional) A restrição padrão é um valor de 1. Um bitmap com um destes valores válidos:<br /><br /> 1 CUBO<br /><br /> 2 DIMENSÃO|  
|**Cube_Name base**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema OLE DB para OLAP](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
