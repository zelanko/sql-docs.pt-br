---
title: Conjunto de linhas MDSCHEMA_DIMENSIONS | Microsoft Docs
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
apiname: MDSCHEMA_DIMENSIONS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_DIMENSIONS rowset
ms.assetid: a0fd94bb-359a-4df6-93a6-d60d50223944
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d6e6179a6d3538282dbbc125f8e8865ad3c560a6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="mdschemadimensions-rowset"></a>Conjunto de linhas MDSCHEMA_DIMENSIONS
  Descreve as dimensões compartilhadas e privadas dentro de um banco de dados.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O **MDSCHEMA_DIMENSIONS** linhas contém as seguintes colunas:  
  
|Nome da coluna|Indicador de tipo|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|O nome do banco de dados.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Sem suporte.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|O nome do cubo.|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**|O nome da dimensão. Se uma dimensão fizer parte de mais de um cubo ou grupo de medidas, haverá uma linha para cada combinação exclusiva de dimensão, grupo de medidas e cubo.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|O nome exclusivo da dimensão.|  
|**DIMENSION_GUID**|**DBTYPE_GUID**|Sem suporte.|  
|**DIMENSION_CAPTION**|**DBTYPE_WSTR**|A legenda da dimensão. Isso deve ser usado durante a exibição do nome da dimensão para o usuário, como na interface do usuário ou em relatórios.|  
|**DIMENSION_ORDINAL**|**DBTYPE_UI4**|A posição da dimensão dentro do cubo.|  
|**DIMENSION_TYPE**|**DBTYPE_I2**|O tipo da dimensão. Os valores válidos incluem:<br /><br /> **MD_DIMTYPE_UNKNOWN** (**0**)<br /><br /> **MD_DIMTYPE_TIME** (**1**)<br /><br /> **MD_DIMTYPE_MEASURE** (**2**)<br /><br /> **MD_DIMTYPE_OTHER** (**3**)<br /><br /> **MD_DIMTYPE_QUANTITATIVE** (**5**)<br /><br /> **MD_DIMTYPE_ACCOUNTS** (**6**)<br /><br /> **MD_DIMTYPE_CUSTOMERS** (**7**)<br /><br /> **MD_DIMTYPE_PRODUCTS** (**8**)<br /><br /> **MD_DIMTYPE_SCENARIO** (**9**)<br /><br /> **MD_DIMTYPE_UTILIY** (**10**)<br /><br /> **MD_DIMTYPE_CURRENCY** (**11**)<br /><br /> **MD_DIMTYPE_RATES** (**12**)<br /><br /> **MD_DIMTYPE_CHANNEL** (**13**)<br /><br /> **MD_DIMTYPE_PROMOTION** (**14**)<br /><br /> **MD_DIMTYPE_ORGANIZATION** (**15**)<br /><br /> **MD_DIMTYPE_BILL_OF_MATERIALS** (**16**)<br /><br /> **MD_DIMTYPE_GEOGRAPHY** (**17**)|  
|**DIMENSION_CARDINALITY**|**DBTYPE_UI4**|O número de membros no atributo de chave.|  
|**DEFAULT_HIERARCHY**|**DBTYPE_WSTR**|Uma hierarquia da dimensão. Preservada para compatibilidade com versões anteriores.|  
|**DESCRIPTION**|**DBTYPE_WSTR**|Uma descrição amigável da dimensão.|  
|**IS_VIRTUAL**|**DBTYPE_BOOL**|Sempre **FALSE**.|  
|**IS_READWRITE**|**DBTYPE_BOOL**|Um Booliano que indica se a dimensão está habilitada para gravação.<br /><br /> **TRUE** se a dimensão está habilitada para gravação.|  
|**DIMENSION_UNIQUE_SETTINGS**|**DBTYPE_I4**|Um bitmap que especifica quais colunas contêm valores exclusivos se a dimensão contém apenas os membros com nomes exclusivos. As seguintes constantes de valor de bit são definidas no Msmd.h para este bitmap:<br /><br /> **MDDIMENSIONS_MEMBER_KEY_UNIQUE**|  
|**DIMENSION_MASTER_UNIQUE_NAME**|**DBTYPE_WSTR**|Sempre **nulo**.|  
|**DIMENSION_IS_VISIBLE**|**DBTYPE_BOOL**|Sempre **TRUE**.<br /><br /> Observação: Uma dimensão não estiver visível, a menos que uma ou mais hierarquias da dimensão estão visíveis.|  
  
 O conjunto de linhas é classificado em **CATALOG_NAME**, **SCHEMA_NAME**, **CUBE_NAME**, **DIMENSION_NAME**.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O **MDSCHEMA_DIMENSIONS** linhas pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(Opcional) A restrição padrão é um valor de 1. Um bitmap com um dos seguintes valores válidos:<br /><br /> 1 CUBO<br /><br /> 2 DIMENSÃO|  
|**DIMENSION_VISIBILITY**|**DBTYPE_UI2**|(Opcional) A restrição padrão é um valor de 1. Um bitmap com um dos seguintes valores válidos:<br /><br /> 1 Visível<br /><br /> 2 não visível|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema OLE DB para OLAP](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
