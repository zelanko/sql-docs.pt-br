---
title: Conjunto de linhas MDSCHEMA_MEASURES | Microsoft Docs
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
- MDSCHEMA_MEASURES
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_MEASURES rowset
ms.assetid: 6ff5bd1a-aad0-49b8-9f8d-7df2637caacf
caps.latest.revision: 30
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 84ea2ceeaef0c6431f3860f3b23da07f43ee6c5a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37237466"
---
# <a name="mdschemameasures-rowset"></a>Conjunto de linhas MDSCHEMA_MEASURES
  Descreve cada medida dentro de um cubo.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `MDSCHEMA_MEASURES` linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||O nome do catálogo ao qual essa medida pertence. `NULL` se o provedor não oferecer suporte a catálogos.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||O nome do esquema ao qual esta medida pertence. `NULL` se o provedor não oferecer suporte a esquemas.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||O nome do cubo ao qual pertence essa medida.|  
|`MEASURE_NAME`|`DBTYPE_WSTR`||O nome da medida.|  
|`MEASURE_UNIQUE_NAME`|`DBTYPE_WSTR`||O nome exclusivo da medida. Para provedores que geram nomes exclusivos por qualificação, cada componente desse nome é delimitado.|  
|`MEASURE_CAPTION`|`DBTYPE_WSTR`||Um rótulo ou legenda associado à medida. Usado principalmente para fins de exibição. Se não houver uma legenda, `MEASURE_NAME` será retornado.|  
|`MEASURE_GUID`|`DBTYPE_GUID`||Sem suporte.|  
|`MEASURE_AGGREGATOR`|`DBTYPE_I4`||Uma enumeração que identifica como uma medida foi derivada. Pode ser um dos seguintes valores:<br /><br /> -   `MDMEASURE_AGGR_SUM` (`1`) identifica que a medida é agregada de `SUM`.<br />-   `MDMEASURE_AGGR_COUNT` (`2`) identifica que a medida é agregada de `COUNT`.<br />-   **MDMEASURE_AGGR_MIN** (`3`) identifica que a medida é agregada de `MIN`.<br />-   **MDMEASURE_AGGR_MAX** (`4`) identifica que a medida é agregada de `MAX`.<br />-   `MDMEASURE_AGGR_AVG` (`5`) identifica que a medida é agregada de `AVG`.<br />-   `MDMEASURE_AGGR_VAR` (`6`) identifica que a medida é agregada de `VAR`.<br />-   `MDMEASURE_AGGR_STD` (`7`) identifica que a medida é agregada de `STDEV`.<br />-   `MDMEASURE_AGGR_DST` (`8`) identifica que a medida é agregada de `DISTINCT COUNT`.<br />-   `MDMEASURE_AGGR_NONE` (`9`) identifica que a medida é agregada de `NONE`.<br />-   `MDMEASURE_AGGR_AVGCHILDREN` (`10`) identifica que a medida é agregada de `AVERAGEOFCHILDREN`.<br />-   `MDMEASURE_AGGR_FIRSTCHILD` (`11`) identifica que a medida é agregada de `FIRSTCHILD`.<br />-   `MDMEASURE_AGGR_LASTCHILD` (`12`) identifica que a medida é agregada de `LASTCHILD`.<br />-   `MDMEASURE_AGGR_FIRSTNONEMPTY` (`13`) identifica que a medida é agregada de `FIRSTNONEMPTY`,<br />-   `MDMEASURE_AGGR_LASTNONEMPTY` (`14`) identifica que a medida é agregada de `LASTNONEMPTY`.<br />-   `MDMEASURE_AGGR_BYACCOUNT` (`15`) identifica que a medida é agregada de `BYACCOUNT`.<br />-   `MDMEASURE_AGGR_CALCULATED` (`127`) identifica que a medida foi derivada de uma fórmula que não era nenhuma das funções anteriores.<br />-   `MDMEASURE_AGGR_UNKNOWN` (`0`) identifica que a medida foi derivada de uma função de agregação desconhecida ou a fórmula.|  
|`DATA_TYPE`|`DBTYPE_UI2`||O tipo de dados da medida.|  
|`NUMERIC_PRECISION`|`DBTYPE_UI2`||A precisão máxima da propriedade se o tipo de dados do objeto da medida é um número exato. Será `NULL` para todos os outros tipos de propriedades.|  
|`NUMERIC_SCALE`|`DBTYPE_I2`||O número de dígitos à direita do separador decimal quando o indicador de tipo do objeto de medida é `DBTYPE_NUMERIC` ou `DBTYPE_DECIMAL`. Caso contrário, esse valor será `NULL`.|  
|`MEASURE_UNITS`|`DBTYPE_WSTR`||Sem suporte|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Uma descrição humanamente legível da medida. `NULL` quando não existe descrição.|  
|`EXPRESSION`|`DBTYPE_WSTR`||Uma expressão para o membro.|  
|`MEASURE_IS_VISIBLE`|`DBTYPE_BOOL`||Um Booliano que sempre retorna Verdadeiro. Se a medida não for visível, ela não será incluída no conjunto de linhas de esquema.|  
|`LEVELS_LIST`|`DBTYPE_WSTR`||Uma cadeia de caracteres que sempre retorna `NULL`.|  
|`MEASURE_NAME_SQL_COLUMN_NAME`|`DBTYPE_WSTR`||O nome da coluna na consulta de SQL que corresponde ao nome da medida.|  
|`MEASURE_UNQUALIFIED_CAPTION`|`DBTYPE_WSTR`||O nome da medida, não qualificado com o nome do grupo de medidas.|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`||O nome do grupo de medidas ao qual pertence a medida.|  
|`MEASURE_DISPLAY_FOLDER`|`DBTYPE_WSTR`||O caminho a ser usado ao exibir a medida na interface do usuário. Os nomes de pastas serão separados por ponto-e-vírgula. Pastas aninhadas são indicadas por uma barra invertida (\\).|  
|`DEFAULT_FORMAT_STRING`|`DBTYPE_WSTR`||A cadeia de caracteres de formato padrão da medida.|  
  
 O conjunto de linhas é classificado em `CATALOG_NAME`, `SCHEMA_NAME`, `CUBE_NAME`, `MEASURE_NAME`.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `MDSCHEMA_MEASURES` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`MEASURE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`MEASURE_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(Opcional) Um bitmap com um dos seguintes valores válidos:<br /><br /> -CUBO DE 1<br />-DIMENSÃO DE 2<br /><br /> A restrição padrão tem valor 1.|  
|`MEASURE_VISIBILITY`|`DBTYPE_UI2`|(Opcional) Um bitmap com um dos seguintes valores válidos:<br /><br /> -Visible 1<br />-2 não é visível<br /><br /> A restrição padrão tem valor 1.|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema OLE DB para OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  
