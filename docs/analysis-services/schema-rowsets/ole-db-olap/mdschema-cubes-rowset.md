---
title: Conjunto de linhas MDSCHEMA_CUBES | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 82a07fda14984582ae9461d861df0fa47920b527
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="mdschemacubes-rowset"></a>Conjunto de linhas MDSCHEMA_CUBES
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 [OLE DB para OLAP Schema Rowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
