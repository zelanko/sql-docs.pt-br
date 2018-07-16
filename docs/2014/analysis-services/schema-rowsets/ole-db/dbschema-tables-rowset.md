---
title: Conjunto de linhas DBSCHEMA_TABLES | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DBSCHEMA_TABLES
topic_type:
- apiref
helpviewer_keywords:
- DBSCHEMA_TABLES rowset
ms.assetid: 14c16e6b-0aff-4ad1-b98f-cdb7df0f8d73
caps.latest.revision: 31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 83537dc9159331342ae344e5003d9c04fd8980eb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37211826"
---
# <a name="dbschematables-rowset"></a>Conjunto de linhas DBSCHEMA_TABLES
  Identifica os grupos de medidas e dimensões expostas como tabelas no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DBSCHEMA_TABLES` linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`TABLE_CATALOG`|`DBTYPE_WSTR`|255|O nome do catálogo ao qual esse objeto pertence.|  
|`TABLE_SCHEMA`|`DBTYPE_WSTR`|255|O nome do cubo ao qual esse objeto pertence.|  
|`TABLE_NAME`|`DBTYPE_WSTR`|255|O nome do objeto, se `TABLE_TYPE` for `TABLE`.|  
|`TABLE_TYPE`|`DBTYPE_WSTR`||O tipo da tabela.<br /><br /> `TABLE` Indica se que o objeto é um grupo de medidas.<br /><br /> `SYSTEM TABLE` Indica se que o objeto é uma dimensão.|  
|`TABLE_GUID`|`DBTYPE_GUID`||Sem suporte.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Uma descrição legível do objeto.|  
|`TABLE_PROPID`|`DBTYPE_UI4`||Sem suporte.|  
|`DATE_CREATED`|`DBTYPE_DBTIMESTAMP`||Sem suporte.|  
|`DATE_MODIFIED`|`DBTYPE_DBTIMESTAMP`||A data da última modificação do objeto.|  
|`TABLE_OLAP_TYPE`|`DBTYPE_WSTR`||O tipo OLAP do objeto.<br /><br /> **Grupo_de_medidas** indica o objeto é um grupo de medidas.<br /><br /> `CUBE_DIMENSION` indica que o objeto é uma dimensão.|  
  
 O conjunto de linhas é classificado em `TABLE_TYPE`, `TABLE_CATALOG`, `TABLE_SCHEMA` e `TABLE_NAME`.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `DBSCHEMA_TABLES` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`TABLE_CATALOG`|`DBTYPE_WSTR`|Opcional|  
|`TABLE_SCHEMA`|`DBTYPE_WSTR`|Opcional|  
|`TABLE_NAME`|`DBTYPE_WSTR`|Opcional|  
|`TABLE_TYPE`|`DBTYPE_WSTR`|Opcional|  
|`TABLE_OLAP_TYPE`|`DBTYPE_WSTR`|Opcional|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas do esquema OLE DB](ole-db-schema-rowsets.md)  
  
  
