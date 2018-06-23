---
title: Conjunto de linhas MDSCHEMA_INPUT_DATASOURCES | Microsoft Docs
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
- MDSCHEMA_INPUT_DATASOURCES
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_INPUT_DATASOURCES rowset
ms.assetid: 12482fd5-16e3-4171-9cb0-76d0d4f5308e
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ba789133cddb1d8b074a58e36ee2018359ae504e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119206"
---
# <a name="mdschemainputdatasources-rowset"></a>Conjunto de linhas MDSCHEMA_INPUT_DATASOURCES
  Descreve as fontes de dados definidas dentro do banco de dados.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `MDSCHEMA_INPUT_DATASOURCES` linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||O nome do catálogo ao qual pertence essa fonte de dados.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||Sem suporte.|  
|`DATASOURCE_NAME`|`DBTYPE_WSTR`||O nome do objeto de fonte de dados.|  
|`DATASOURCE_TYPE`|`DBTYPE_WSTR`||O tipo da fonte de dados. Os valores válidos incluem:<br /><br /> -   `Relational`<br />-   `Olap`|  
|`CREATED_ON`|`DBTYPE_DBTIMESTAMP`||A data de criação da fonte de dados.|  
|`LAST_SCHEMA_UPDATE`|`DBTYPE_DBTIMESTAMP`||A data e a hora da última modificação na fonte de dados.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Uma descrição amigável da ação.|  
|`TIMEOUT`|`DBTYPE_UI4`||O tempo limite da fonte de dados.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `MDSCHEMA_INPUT_DATASOURCES` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`DATASOURCE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`DATASOURCE_TYPE`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema OLE DB para OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  