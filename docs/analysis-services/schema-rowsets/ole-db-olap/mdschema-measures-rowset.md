---
title: Conjunto de linhas MDSCHEMA_MEASURES | Microsoft Docs
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
apiname:
- MDSCHEMA_MEASURES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_MEASURES rowset
ms.assetid: 6ff5bd1a-aad0-49b8-9f8d-7df2637caacf
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c77b91b179e360f539549cda05d0a17f0697ee56
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="mdschemameasures-rowset"></a>Conjunto de linhas MDSCHEMA_MEASURES
  Descreve cada medida dentro de um cubo.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O **MDSCHEMA_MEASURES** linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||O nome do catálogo ao qual essa medida pertence. **NULL** se o provedor não oferecer suporte a catálogos.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||O nome do esquema ao qual esta medida pertence. **NULO** se o provedor não dá suporte a esquemas.|  
|**CUBE_NAME**|**DBTYPE_WSTR**||O nome do cubo ao qual pertence essa medida.|  
|**MEASURE_NAME**|**DBTYPE_WSTR**||O nome da medida.|  
|**MEASURE_UNIQUE_NAME**|**DBTYPE_WSTR**||O nome exclusivo da medida. Para provedores que geram nomes exclusivos por qualificação, cada componente desse nome é delimitado.|  
|**MEASURE_CAPTION**|**DBTYPE_WSTR**||Um rótulo ou legenda associado à medida. Usado principalmente para fins de exibição. Se não houver uma legenda, **MEASURE_NAME** é retornado.|  
|**MEASURE_GUID**|**DBTYPE_GUID**||Sem suporte.|  
|**MEASURE_AGGREGATOR**|**DBTYPE_I4**||Uma enumeração que identifica como uma medida foi derivada. Pode ser um dos seguintes valores:<br /><br /> **MDMEASURE_AGGR_SUM** (**1**) identifica que a medida é agregada de **soma**.<br /><br /> **MDMEASURE_AGGR_COUNT** (**2**) identifica que a medida é agregada de **contagem**.<br /><br /> **MDMEASURE_AGGR_MIN** (**3**) identifica que a medida é agregada de **MIN**.<br /><br /> **MDMEASURE_AGGR_MAX** (**4**) identifica que a medida é agregada de **MAX**.<br /><br /> **MDMEASURE_AGGR_AVG** (**5**) identifica que a medida é agregada de **AVG**.<br /><br /> **MDMEASURE_AGGR_VAR** (**6**) identifica que a medida é agregada de **VAR**.<br /><br /> **MDMEASURE_AGGR_STD** (**7**) identifica que a medida é agregada de **STDEV**.<br /><br /> **MDMEASURE_AGGR_DST** (**8**) identifica que a medida é agregada de **contagem DISTINTA**.<br /><br /> **MDMEASURE_AGGR_NONE** (**9**) identifica que a medida é agregada de **NONE**.<br /><br /> **MDMEASURE_AGGR_AVGCHILDREN** (**10**) identifica que a medida é agregada de **AVERAGEOFCHILDREN**.<br /><br /> **MDMEASURE_AGGR_FIRSTCHILD** (**11**) identifica que a medida é agregada de **FIRSTCHILD**.<br /><br /> **MDMEASURE_AGGR_LASTCHILD** (**12**) identifica que a medida é agregada de **LASTCHILD**.<br /><br /> **MDMEASURE_AGGR_FIRSTNONEMPTY** (**13**) identifica que a medida é agregada de **FIRSTNONEMPTY**,<br /><br /> **MDMEASURE_AGGR_LASTNONEMPTY** (**14**) identifica que a medida é agregada de **LASTNONEMPTY**.<br /><br /> **MDMEASURE_AGGR_BYACCOUNT** (**15**) identifica que a medida é agregada de **BYACCOUNT**.<br /><br /> **MDMEASURE_AGGR_CALCULATED** (**127**) identifica que a medida foi derivada de uma fórmula que não era nenhuma das funções anteriores.<br /><br /> **MDMEASURE_AGGR_UNKNOWN** (**0**) identifica que a medida foi derivada de uma fórmula ou uma função de agregação desconhecida.|  
|**DATA_TYPE**|**DBTYPE_UI2**||O tipo de dados da medida.|  
|**NUMERIC_PRECISION**|**DBTYPE_UI2**||A precisão máxima da propriedade se o tipo de dados do objeto da medida é um número exato. **NULO** para todos os outros tipos de propriedade.|  
|**NUMERIC_SCALE**|**DBTYPE_I2**||O número de dígitos à direita da vírgula decimal se o indicador de tipo do objeto de medida é **DBTYPE_NUMERIC** ou **DBTYPE_DECIMAL**. Caso contrário, esse valor é **nulo**.|  
|**MEASURE_UNITS**|**DBTYPE_WSTR**||Sem suporte|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Uma descrição humanamente legível da medida. **NULO** se não existir descrição.|  
|**EXPRESSÃO**|**DBTYPE_WSTR**||Uma expressão para o membro.|  
|**MEASURE_IS_VISIBLE**|**DBTYPE_BOOL**||Um Booliano que sempre retorna Verdadeiro. Se a medida não for visível, ela não será incluída no conjunto de linhas de esquema.|  
|**LEVELS_LIST**|**DBTYPE_WSTR**||Uma cadeia de caracteres que sempre retorna **nulo**.|  
|**MEASURE_NAME_SQL_COLUMN_NAME**|**DBTYPE_WSTR**||O nome da coluna na consulta de SQL que corresponde ao nome da medida.|  
|**MEASURE_UNQUALIFIED_CAPTION**|**DBTYPE_WSTR**||O nome da medida, não qualificado com o nome do grupo de medidas.|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**||O nome do grupo de medidas ao qual pertence a medida.|  
|**MEASURE_DISPLAY_FOLDER**|**DBTYPE_WSTR**||O caminho a ser usado ao exibir a medida na interface do usuário. Os nomes de pastas serão separados por ponto-e-vírgula. Pastas aninhadas são indicadas por uma barra invertida (\\).|  
|**DEFAULT_FORMAT_STRING**|**DBTYPE_WSTR**||A cadeia de caracteres de formato padrão da medida.|  
  
 O conjunto de linhas é classificado em **CATALOG_NAME**, **SCHEMA_NAME**, **CUBE_NAME**, **MEASURE_NAME**.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O **MDSCHEMA_MEASURES** linhas pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**MEASURE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**MEASURE_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(Opcional) A restrição padrão é um valor de 1. Um bitmap com um dos seguintes valores válidos:<br /><br /> 1 CUBO<br /><br /> 2 DIMENSÃO|  
|**MEASURE_VISIBILITY**|**DBTYPE_UI2**|(Opcional) A restrição padrão é um valor de 1. Um bitmap com um dos seguintes valores válidos:<br /><br /> 1 Visível<br /><br /> 2 Não visível|  
  
## <a name="see-also"></a>Consulte também  
 [OLE DB para OLAP Schema Rowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  

