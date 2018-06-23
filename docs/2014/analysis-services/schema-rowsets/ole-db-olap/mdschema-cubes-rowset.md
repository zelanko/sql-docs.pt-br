---
title: Conjunto de linhas MDSCHEMA_CUBES | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MDSCHEMA_CUBES
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_CUBES rowset
ms.assetid: 5f1b63d4-aa3f-48c6-b866-7ffd91675044
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0044c9943b2f2819ea216c735f298b7e30de7a3a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118428"
---
# <a name="mdschemacubes-rowset"></a>Conjunto de linhas MDSCHEMA_CUBES
  Descreve a estrutura de cubos dentro de um banco de dados.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `MDSCHEMA_CUBES` linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||O nome do banco de dados.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||Sem suporte.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||O nome do cubo ou da dimensão. Nomes de dimensão são antecedidos por um símbolo de cifrão ($). **Observação:** somente administradores de servidor e banco de dados tem permissões para consultar cubos criados a partir de uma dimensão.|  
|`CUBE_TYPE`|`DBTYPE_WSTR`||O tipo do cubo. Os valores válidos são:<br /><br /> -   `CUBE`<br />-   `DIMENSION`|  
|`CUBE_GUID`|`DBTYPE_GUID`||Sem suporte.|  
|`CREATED_ON`|`DBTYPE_DBTIMESTAMP`||Sem suporte.|  
|`LAST_SCHEMA_UPDATE`|`DBTYPE_DBTIMESTAMP`||O horário do último processamento do cubo.|  
|`SCHEMA_UPDATED_BY`|`DBTYPE_WSTR`||Sem suporte.|  
|`LAST_DATA_UPDATE`|`DBTYPE_DBTIMESTAMP`||O horário do último processamento do cubo.|  
|`DATA_UPDATED_BY`|`DBTYPE_WSTR`||Sem suporte.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Uma descrição amigável do cubo.|  
|`IS_DRILLTHROUGH_ENABLED`|`DBTYPE_BOOL`||Um Booliano que sempre retorna true.|  
|`IS_LINKABLE`|`DBTYPE_BOOL`||Um Booliano isso indica se um cubo pode ser usado em um cubo vinculado.|  
|`IS_WRITE_ENABLED`|`DBTYPE_BOOL`||Um Booliano que indica se um cubo está habilitado para gravação.|  
|`IS_SQL_ENABLED`|`DBTYPE_BOOL`||Um Booliano que indica se um SQL pode ser usado no cubo.|  
|`CUBE_CAPTION`|`DBTYPE_WSTR`||A legenda do cubo.|  
|`BASE_CUBE_NAME`|`DBTYPE_WSTR`||O nome do cubo de origem se esse cubo for um cubo de perspectiva.|  
|`ANNOTATIONS`|`DBTYPE_WSTR`||(Opcional) Um conjunto de notas em formato XML.|  
  
 O conjunto de linhas é classificado em `CATALOG_NAME`, `SCHEMA_NAME`, `CUBE_NAME`.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `MDSCHEMA_CUBES` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(Opcional) Um bitmap com um destes valores válidos:<br /><br /> -CUBO DE 1<br />-DIMENSÃO DE 2<br /><br /> A restrição padrão tem valor 1.|  
|`Base Cube_Name`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema OLE DB para OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  