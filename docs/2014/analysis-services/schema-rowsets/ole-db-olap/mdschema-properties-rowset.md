---
title: Conjunto de linhas MDSCHEMA_PROPERTIES | Microsoft Docs
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
- MDSCHEMA_PROPERTIES
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_PROPERTIES rowset
ms.assetid: 95c480f7-c525-44ba-a59b-cd36f5855a4f
caps.latest.revision: 30
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f62a6e4f77053c1aec69fc2e16b8049193249466
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37189213"
---
# <a name="mdschemaproperties-rowset"></a>Conjunto de linhas MDSCHEMA_PROPERTIES
  Descreve as propriedades de membros dentro de um banco de dados.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `MDSCHEMA_PROPERTIES` linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||O nome do banco de dados.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||O nome do esquema ao qual essa propriedade pertence. `NULL` se o provedor não oferecer suporte a esquemas.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||O nome do cubo.|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`||O nome exclusivo da dimensão. Para provedores que geram nomes exclusivos por qualificação, cada componente desse nome é delimitado.|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`||O nome exclusivo da hierarquia. Para provedores que geram nomes exclusivos por qualificação, cada componente desse nome é delimitado.|  
|`LEVEL_UNIQUE_NAME`|`DBTYPE_WSTR`||O nome exclusivo do nível ao qual pertence essa propriedade. Se o provedor não der suporte a níveis nomeados, ele deverá retornar o valor `DIMENSION_UNIQUE_NAME` para este campo. Para provedores que geram nomes exclusivos por qualificação, cada componente desse nome é delimitado.|  
|`MEMBER_UNIQUE_NAME`|`DBTYPE_WSTR`||O nome exclusivo do membro ao qual pertence essa propriedade. Usado para repositórios de dados que não dão suporte a níveis nomeados ou que têm propriedades para cada membro. Se a propriedade se aplicar a todos os membros de um nível, essa coluna será `NULL`. Para provedores que geram nomes exclusivos por qualificação, cada componente desse nome é delimitado.|  
|`PROPERTY_TYPE`|`DBTYPE_I2`||Um bitmap que especifica o tipo da propriedade:<br /><br /> -   `MDPROP_MEMBER` (`1`) identifica uma propriedade de membro. Essa propriedade pode ser usada na cláusula DIMENSION PROPERTIES da instrução SELECT.<br />-   `MDPROP_CELL` (`2`) identifica uma propriedade de uma célula. Essa propriedade pode ser usada na cláusula CELL PROPERTIES que ocorre no final da instrução SELECT.<br />-   `MDPROP_SYSTEM` (`4`) identifica uma propriedade interna.<br />-   `MDPROP_BLOB` (`8`) identifica uma propriedade que contém um objeto binário grande (blob).|  
|`PROPERTY_NAME`|`DBTYPE_WSTR`||O nome da propriedade. Se a chave da propriedade for igual ao nome da propriedade, `PROPERTY_NAME` ficará em branco.|  
|`PROPERTY_CAPTION`|`DBTYPE_WSTR`||Um rótulo ou uma legenda associada à propriedade, usada principalmente para fins de exibição. Retorna `PROPERTY_NAME` quando não há uma legenda.|  
|`DATA_TYPE`|`DBTYPE_UI2`||O tipo de dados da propriedade.|  
|`CHARACTER_MAXIMUM_LENGTH`|`DBTYPE_UI4`||O comprimento máximo possível da propriedade, se o seu tipo for caractere, binário ou bit.<br /><br /> Zero indica que não há um comprimento máximo definido.<br /><br /> Retorna `NULL` para todos os outros tipos de dados.|  
|`CHARACTER_OCTET_LENGTH`|`DBTYPE_UI4`||O comprimento máximo possível (em bytes) da propriedade, se o seu tipo for caractere ou binário.<br /><br /> Zero indica que não há um comprimento máximo definido.<br /><br /> Retorna `NULL` para todos os outros tipos de dados.|  
|`NUMERIC_PRECISION`|`DBTYPE_UI2`||A precisão máxima da propriedade, se for um tipo de dados numérico.<br /><br /> Retorna `NULL` para todos os outros tipos de dados.|  
|`NUMERIC_SCALE`|`DBTYPE_I2`||O número de dígitos à direita do separador decimal, se o tipo for `DBTYPE_NUMERIC` ou `DBTYPE_DECIMAL`.<br /><br /> Retorna `NULL` para todos os outros tipos de dados.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Uma descrição legível da propriedade. `NULL` quando não existe descrição.|  
|`PROPERTY_CONTENT_TYPE`|`DBTYPE_I2`||O tipo da propriedade. Pode ser uma das seguintes enumerações:<br /><br /> -   **MD_PROPTYPE_REGULAR** (`0x00`)<br />-   **MD_PROPTYPE_ID** (`0x01`)<br />-   **MD_PROPTYPE_RELATION_TO_PARENT** (`0x02`)<br />-   **MD_PROPTYPE_ROLLUP_OPERATOR** (`0x03`)<br />-   **MD_PROPTYPE_ORG_TITLE** (`0x11`)<br />-   **MD_PROPTYPE_CAPTION** (`0x21`)<br />-   **MD_PROPTYPE_CAPTION_SHORT** (`0x22`)<br />-   **MD_PROPTYPE_CAPTION_DESCRIPTION** (`0x23`)<br />-   **MD_PROPTYPE_CAPTION_ABREVIATION** (`0x24`)<br />-   **MD_PROPTYPE_WEB_URL** (`0x31`)<br />-   **MD_PROPTYPE_WEB_HTML** (`0x32`)<br />-   **MD_PROPTYPE_WEB_XML_OR_XSL** (`0x33`)<br />-   **MD_PROPTYPE_WEB_MAIL_ALIAS** (`0x34`)<br />-   **MD_PROPTYPE_ADDRESS** (`0x41`)<br />-   **MD_PROPTYPE_ADDRESS_STREET** (`0x42`)<br />-   **MD_PROPTYPE_ADDRESS_HOUSE** (`0x43`)<br />-   **MD_PROPTYPE_ADDRESS_CITY** (`0x44`)<br />-   **MD_PROPTYPE_ADDRESS_STATE_OR_PROVINCE** (`0x45`)<br />-   **MD_PROPTYPE_ADDRESS_ZIP** (`0x46`)<br />-   **MD_PROPTYPE_ADDRESS_QUARTER** (`0x47`)<br />-   **MD_PROPTYPE_ADDRESS_COUNTRY** (`0x48`)<br />-   **MD_PROPTYPE_ADDRESS_BUILDING** (`0x49`)<br />-   **MD_PROPTYPE_ADDRESS_ROOM** (`0x4A`)<br />-   **MD_PROPTYPE_ADDRESS_FLOOR** (`0x4B`)<br />-   **MD_PROPTYPE_ADDRESS_FAX** (`0x4C`)<br />-   **MD_PROPTYPE_ADDRESS_PHONE** (`0x4D`)<br />-   **MD_PROPTYPE_GEO_CENTROID_X** (`0x61`)<br />-   **MD_PROPTYPE_GEO_CENTROID_Y** (`0x62`)<br />-   **MD_PROPTYPE_GEO_CENTROID_Z** (`0x63`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_TOP** (`0x64`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_LEFT** (`0x65`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_BOTTOM** (`0x66`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_RIGHT** (`0x67`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_FRONT** (`0x68`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_REAR** (`0x69`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_POLYGON** (`0x6A`)<br />-   **MD_PROPTYPE_PHYSICAL_SIZE** (`0x71`)<br />-   **MD_PROPTYPE_PHYSICAL_COLOR** (`0x72`)<br />-   **MD_PROPTYPE_PHYSICAL_WEIGHT** (`0x73`)<br />-   **MD_PROPTYPE_PHYSICAL_HEIGHT** (`0x74`)<br />-   **MD_PROPTYPE_PHYSICAL_WIDTH** (`0x75`)<br />-   **MD_PROPTYPE_PHYSICAL_DEPTH** (`0x76`)<br />-   **MD_PROPTYPE_PHYSICAL_VOLUME** (`0x77`)<br />-   **MD_PROPTYPE_PHYSICAL_DENSITY** (`0x78`)<br />-   **MD_PROPTYPE_PERSON_FULL_NAME** (`0x82`)<br />-   **MD_PROPTYPE_PERSON_FIRST_NAME** (`0x83`)<br />-   **MD_PROPTYPE_PERSON_LAST_NAME** (`0x84`)<br />-   **MD_PROPTYPE_PERSON_MIDDLE_NAME** (`0x85`)<br />-   **MD_PROPTYPE_PERSON_DEMOGRAPHIC** (`0x86`)<br />-   **MD_PROPTYPE_PERSON_CONTACT** (`0x87`)<br />-   **MD_PROPTYPE_QTY_RANGE_LOW** (`0x91`)<br />-   **MD_PROPTYPE_QTY_RANGE_HIGH** (`0x92`)<br />-   **MD_PROPTYPE_FORMATTING_COLOR** (`0xA1`)<br />-   **MD_PROPTYPE_FORMATTING_ORDER** (`0xA2`)<br />-   **MD_PROPTYPE_FORMATTING_FONT** (`0xA3`)<br />-   **MD_PROPTYPE_FORMATTING_FONT_EFFECTS** (`0xA4`)<br />-   **MD_PROPTYPE_FORMATTING_FONT_SIZE** (`0xA5`)<br />-   **MD_PROPTYPE_FORMATTING_SUB_TOTAL** (`0xA6`)<br />-   **MD_PROPTYPE_DATE** (`0xB1`)<br />-   **MD_PROPTYPE_DATE_START** (`0xB2`)<br />-   **MD_PROPTYPE_DATE_ENDED** (`0xB3`)<br />-   **MD_PROPTYPE_DATE_CANCELED** (`0xB4`)<br />-   **MD_PROPTYPE_DATE_MODIFIED** (`0xB5`)<br />-   **MD_PROPTYPE_DATE_DURATION** (`0xB6`)<br />-   **MD_PROPTYPE_VERSION** (`0xC1`)|  
|`SQL_COLUMN_NAME`|`DBTYPE_WSTR`||O nome da propriedade usada em consultas SQL da dimensão de cubo ou dimensão de banco de dados.|  
|`LANGUAGE`|`DBTYPE_UI2`||A conversão expressa como um `LCID`. Só é válido para conversões de propriedade.|  
|`PROPERTY_ORIGIN`|`DBTYPE_UI2`||Identifica o tipo de hierarquia à qual a propriedade se aplica:<br /><br /> -   `MD_USER_DEFINED` (`1`) indica que a propriedade está em uma hierarquia definida pelo usuário<br />-   `MD_SYSTEM_ENABLED` (`2`) indica que a propriedade está em uma hierarquia de atributo<br />-   `MD_SYSTEM_DISABLED` (`4`) indica que a propriedade está em uma hierarquia de atributo que não está habilitada.|  
|`PROPERTY_ATTRIBUTE_HIERARCHY_NAME`|`DBTYPE_WSTR`||O nome da hierarquia de atributo que deu origem a essa propriedade.|  
|`PROPERTY_CARDINALITY`|`DBTYPE_WSTR`||A cardinalidade da propriedade. Os possíveis valores incluem as seguintes cadeias de caracteres:<br /><br /> -   `ONE`<br />-   `MANY`|  
|`MIME_TYPE`|`DBTYPE_WSTR`||O tipo mime para BLOBs (objetos binários grandes).|  
|`PROPERTY_IS_VISIBLE`|`DBTYPE_BOOL`||Um Booliano que indica se a propriedade está visível.<br /><br /> Retornará `TRUE` se a propriedade estiver visível; caso contrário, `FALSE`.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `MDSCHEMA_PROPERTIES` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Obrigatório|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Opcional|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional|  
|`LEVEL_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional|  
|`MEMBER_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional|  
|`PROPERTY_TYPE`|`DBTYPE_I2`|Opcional|  
|`PROPERTY_NAME`|`DBTYPE_WSTR`|Opcional|  
|`PROPERTY_CONTENT_TYPE`|`DBTYPE_I2`|(Opcional) Uma restrição padrão é estabelecida em `MDPROP_MEMBER` ou `MDPROP_CELL`.|  
|`PROPERTY_ORIGIN`|`DBTYPE_UI2`|(Opcional) Uma restrição padrão é estabelecida em `MD_USER_DEFINED` ou `MD_SYSTEM_ENABLED`.|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(Opcional) Um bitmap com um dos seguintes valores válidos:<br /><br /> -CUBO DE 1<br />-DIMENSÃO DE 2<br /><br /> A restrição padrão tem valor 1.|  
|`PROPERTY_VISIBILITY`|`DBTYPE_UI2`|(Opcional) Um bitmap com um dos seguintes valores válidos:<br /><br /> -Visible 1<br />-2 não visível<br /><br /> A restrição padrão tem valor 1.|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema OLE DB para OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  
