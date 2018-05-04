---
title: Conjunto de linhas DBSCHEMA_TABLES | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DBSCHEMA_TABLES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DBSCHEMA_TABLES rowset
ms.assetid: 14c16e6b-0aff-4ad1-b98f-cdb7df0f8d73
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1e6117a2a17457a919e202a6dfeef411a766e0f3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="dbschematables-rowset"></a>Conjunto de linhas DBSCHEMA_TABLES
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Identifica os grupos de medidas e dimensões expostos como tabelas no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O **DBSCHEMA_TABLES** linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**TABLE_CATALOG**|**DBTYPE_WSTR**|255|O nome do catálogo ao qual esse objeto pertence.|  
|**TABLE_SCHEMA**|**DBTYPE_WSTR**|255|O nome do cubo ao qual esse objeto pertence.|  
|**TABLE_NAME**|**DBTYPE_WSTR**|255|O nome do objeto, se **TABLE_TYPE** é **tabela**.|  
|**TABLE_TYPE**|**DBTYPE_WSTR**||O tipo da tabela.<br /><br /> **TABELA** indica o objeto é um grupo de medidas.<br /><br /> **TABELA do sistema** indica o objeto é uma dimensão.|  
|**TABLE_GUID**|**DBTYPE_GUID**||Sem suporte.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Uma descrição legível do objeto.|  
|**TABLE_PROPID**|**DBTYPE_UI4**||Sem suporte.|  
|**DATE_CREATED**|**DBTYPE_DBTIMESTAMP**||Sem suporte.|  
|**DATE_MODIFIED**|**DBTYPE_DBTIMESTAMP**||A data da última modificação do objeto.|  
|**TABLE_OLAP_TYPE**|**DBTYPE_WSTR**||O tipo OLAP do objeto.<br /><br /> **Grupo_de_medidas** indica que o objeto é um grupo de medidas.<br /><br /> **CUBE_DIMENSION** indicado que o objeto é uma dimensão.|  
  
 O conjunto de linhas é classificado em **TABLE_TYPE**, **TABLE_CATALOG**, **TABLE_SCHEMA**, e **TABLE_NAME**.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O **DBSCHEMA_TABLES** linhas pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**TABLE_CATALOG**|**DBTYPE_WSTR**|Opcional|  
|**TABLE_SCHEMA**|**DBTYPE_WSTR**|Opcional|  
|**TABLE_NAME**|**DBTYPE_WSTR**|Opcional|  
|**TABLE_TYPE**|**DBTYPE_WSTR**|Opcional|  
|**TABLE_OLAP_TYPE**|**DBTYPE_WSTR**|Opcional|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas do esquema OLE DB](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  
