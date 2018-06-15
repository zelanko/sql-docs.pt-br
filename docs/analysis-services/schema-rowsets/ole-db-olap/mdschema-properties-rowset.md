---
title: Conjunto de linhas MDSCHEMA_PROPERTIES | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7cccd5d28d3f4d2675229929a2bf3d35b383a032
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34036817"
---
# <a name="mdschemaproperties-rowset"></a>Conjunto de linhas MDSCHEMA_PROPERTIES
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Descreve as propriedades de membros dentro de um banco de dados.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O **MDSCHEMA_PROPERTIES** linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||O nome do banco de dados.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||O nome do esquema ao qual essa propriedade pertence. **NULO** se o provedor não dá suporte a esquemas.|  
|**CUBE_NAME**|**DBTYPE_WSTR**||O nome do cubo.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**||O nome exclusivo da dimensão. Para provedores que geram nomes exclusivos por qualificação, cada componente desse nome é delimitado.|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**||O nome exclusivo da hierarquia. Para provedores que geram nomes exclusivos por qualificação, cada componente desse nome é delimitado.|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**||O nome exclusivo do nível ao qual pertence essa propriedade. Se o provedor não oferece suporte a níveis nomeados, ele deve retornar o **DIMENSION_UNIQUE_NAME** valor desse campo. Para provedores que geram nomes exclusivos por qualificação, cada componente desse nome é delimitado.|  
|**MEMBER_UNIQUE_NAME**|**DBTYPE_WSTR**||O nome exclusivo do membro ao qual pertence essa propriedade. Usado para repositórios de dados que não dão suporte a níveis nomeados ou que têm propriedades para cada membro. Se a propriedade se aplica a todos os membros em um nível, essa coluna será **nulo**. Para provedores que geram nomes exclusivos por qualificação, cada componente desse nome é delimitado.|  
|**PROPERTY_TYPE**|**DBTYPE_I2**||Um bitmap que especifica o tipo da propriedade:<br /><br /> **MDPROP_MEMBER** (**1**) identifica uma propriedade de membro. Essa propriedade pode ser usada na cláusula DIMENSION PROPERTIES da instrução SELECT.<br /><br /> **MDPROP_CELL** (**2**) identifica uma propriedade de uma célula. Essa propriedade pode ser usada na cláusula CELL PROPERTIES que ocorre no final da instrução SELECT.<br /><br /> **MDPROP_SYSTEM** (**4**) identifica uma propriedade interna.<br /><br /> **MDPROP_BLOB** (**8**) identifica uma propriedade que contém um objeto binário grande (blob).|  
|**PROPERTY_NAME**|**DBTYPE_WSTR**||O nome da propriedade. Se a chave para a propriedade é igual ao nome da propriedade **PROPERTY_NAME** ficará em branco.|  
|**PROPERTY_CAPTION**|**DBTYPE_WSTR**||Um rótulo ou uma legenda associada à propriedade, usada principalmente para fins de exibição. Retorna **PROPERTY_NAME** se não houver uma legenda.|  
|**DATA_TYPE**|**DBTYPE_UI2**||O tipo de dados da propriedade.|  
|**CHARACTER_MAXIMUM_LENGTH**|**DBTYPE_UI4**||O comprimento máximo possível da propriedade, se o seu tipo for caractere, binário ou bit.<br /><br /> Zero indica que não há um comprimento máximo definido.<br /><br /> Retorna **nulo** para todos os outros tipos de dados.|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**||O comprimento máximo possível (em bytes) da propriedade, se o seu tipo for caractere ou binário.<br /><br /> Zero indica que não há um comprimento máximo definido.<br /><br /> Retorna **nulo** para todos os outros tipos de dados.|  
|**NUMERIC_PRECISION**|**DBTYPE_UI2**||A precisão máxima da propriedade, se for um tipo de dados numérico.<br /><br /> Retorna **nulo** para todos os outros tipos de dados.|  
|**NUMERIC_SCALE**|**DBTYPE_I2**||O número de dígitos à direita da vírgula decimal, se ele for um **DBTYPE_NUMERIC** ou **DBTYPE_DECIMAL** tipo.<br /><br /> Retorna **nulo** para todos os outros tipos de dados.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Uma descrição legível da propriedade. **NULO** se não existir descrição.|  
|**PROPERTY_CONTENT_TYPE**|**DBTYPE_I2**||O tipo da propriedade. Pode ser uma das seguintes enumerações:<br /><br /> **MD_PROPTYPE_REGULAR** (**0x00**)<br /><br /> **MD_PROPTYPE_ID** (**0x01**)<br /><br /> **MD_PROPTYPE_RELATION_TO_PARENT** (**0x02**)<br /><br /> **MD_PROPTYPE_ROLLUP_OPERATOR** (**0x03**)<br /><br /> **MD_PROPTYPE_ORG_TITLE** (**0x11**)<br /><br /> **MD_PROPTYPE_CAPTION** (**0x21**)<br /><br /> **MD_PROPTYPE_CAPTION_SHORT** (**0x22**)<br /><br /> **MD_PROPTYPE_CAPTION_DESCRIPTION** (**0x23**)<br /><br /> **MD_PROPTYPE_CAPTION_ABREVIATION** (**0x24**)<br /><br /> **MD_PROPTYPE_WEB_URL** (**0x31**)<br /><br /> **MD_PROPTYPE_WEB_HTML** (**0x32**)<br /><br /> **MD_PROPTYPE_WEB_XML_OR_XSL** (**0x33**)<br /><br /> **MD_PROPTYPE_WEB_MAIL_ALIAS** (**0x34**)<br /><br /> **MD_PROPTYPE_ADDRESS** (**0x41**)<br /><br /> **MD_PROPTYPE_ADDRESS_STREET** (**0x42**)<br /><br /> **MD_PROPTYPE_ADDRESS_HOUSE** (**0x43**)<br /><br /> **MD_PROPTYPE_ADDRESS_CITY** (**0x44**)<br /><br /> **MD_PROPTYPE_ADDRESS_STATE_OR_PROVINCE** (**0x45**)<br /><br /> **MD_PROPTYPE_ADDRESS_ZIP** (**0x46**)<br /><br /> **MD_PROPTYPE_ADDRESS_QUARTER** (**0x47**)<br /><br /> **MD_PROPTYPE_ADDRESS_COUNTRY** (**0x48**)<br /><br /> **MD_PROPTYPE_ADDRESS_BUILDING** (**0x49**)<br /><br /> **MD_PROPTYPE_ADDRESS_ROOM** (**0x4A**)<br /><br /> **MD_PROPTYPE_ADDRESS_FLOOR** (**0x4B**)<br /><br /> **MD_PROPTYPE_ADDRESS_FAX** (**0x4C**)<br /><br /> **MD_PROPTYPE_ADDRESS_PHONE** (**0x4D**)<br /><br /> **MD_PROPTYPE_GEO_CENTROID_X** (**0x61**)<br /><br /> **MD_PROPTYPE_GEO_CENTROID_Y** (**0x62**)<br /><br /> **MD_PROPTYPE_GEO_CENTROID_Z** (**0x63**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_TOP** (**0x64**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_LEFT** (**0x65**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_BOTTOM** (**0x66**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_RIGHT** (**0x67**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_FRONT** (**0x68**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_REAR** (**0x69**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_POLYGON** (**0x6A**)<br /><br /> **MD_PROPTYPE_PHYSICAL_SIZE** (**0x71**)<br /><br /> **MD_PROPTYPE_PHYSICAL_COLOR** (**0x72**)<br /><br /> **MD_PROPTYPE_PHYSICAL_WEIGHT** (**0x73**)<br /><br /> **MD_PROPTYPE_PHYSICAL_HEIGHT** (**0x74**)<br /><br /> **MD_PROPTYPE_PHYSICAL_WIDTH** (**0x75**)<br /><br /> **MD_PROPTYPE_PHYSICAL_DEPTH** (**0x76**)<br /><br /> **MD_PROPTYPE_PHYSICAL_VOLUME** (**0x77**)<br /><br /> **MD_PROPTYPE_PHYSICAL_DENSITY** (**0x78**)<br /><br /> **MD_PROPTYPE_PERSON_FULL_NAME** (**0x82**)<br /><br /> **MD_PROPTYPE_PERSON_FIRST_NAME** (**0x83**)<br /><br /> **MD_PROPTYPE_PERSON_LAST_NAME** (**0x84**)<br /><br /> **MD_PROPTYPE_PERSON_MIDDLE_NAME** (**0x85**)<br /><br /> **MD_PROPTYPE_PERSON_DEMOGRAPHIC** (**0x86**)<br /><br /> **MD_PROPTYPE_PERSON_CONTACT** (**0x87**)<br /><br /> **MD_PROPTYPE_QTY_RANGE_LOW** (**0x91**)<br /><br /> **MD_PROPTYPE_QTY_RANGE_HIGH** (**0x92**)<br /><br /> **MD_PROPTYPE_FORMATTING_COLOR** (**0xA1**)<br /><br /> **MD_PROPTYPE_FORMATTING_ORDER** (**0xA2**)<br /><br /> **MD_PROPTYPE_FORMATTING_FONT** (**0xA3**)<br /><br /> **MD_PROPTYPE_FORMATTING_FONT_EFFECTS** (**0xA4**)<br /><br /> **MD_PROPTYPE_FORMATTING_FONT_SIZE** (**0xA5**)<br /><br /> **MD_PROPTYPE_FORMATTING_SUB_TOTAL** (**0xA6**)<br /><br /> **MD_PROPTYPE_DATE** (**0xB1**)<br /><br /> **MD_PROPTYPE_DATE_START** (**0xB2**)<br /><br /> **MD_PROPTYPE_DATE_ENDED** (**0xB3**)<br /><br /> **MD_PROPTYPE_DATE_CANCELED** (**0xB4**)<br /><br /> **MD_PROPTYPE_DATE_MODIFIED** (**0xB5**)<br /><br /> **MD_PROPTYPE_DATE_DURATION** (**0xB6**)<br /><br /> **MD_PROPTYPE_VERSION** (**0xC1**)|  
|**SQL_COLUMN_NAME**|**DBTYPE_WSTR**||O nome da propriedade usada em consultas SQL da dimensão de cubo ou dimensão de banco de dados.|  
|**LANGUAGE**|**DBTYPE_UI2**||A conversão expressa como uma **LCID**. Só é válido para conversões de propriedade.|  
|**PROPERTY_ORIGIN**|**DBTYPE_UI2**||Identifica o tipo de hierarquia à qual a propriedade se aplica:<br /><br /> **MD_USER_DEFINED** (**1**) indica que a propriedade está em uma hierarquia definida pelo usuário<br /><br /> **MD_SYSTEM_ENABLED** (**2**) indica que a propriedade está em uma hierarquia de atributo<br /><br /> **MD_SYSTEM_DISABLED** (**4**) indica que a propriedade está em uma hierarquia de atributo que não está habilitada.|  
|**PROPERTY_ATTRIBUTE_HIERARCHY_NAME**|**DBTYPE_WSTR**||O nome da hierarquia de atributo que deu origem a essa propriedade.|  
|**PROPERTY_CARDINALITY**|**DBTYPE_WSTR**||A cardinalidade da propriedade. Os possíveis valores incluem as seguintes cadeias de caracteres:<br /><br /> **UM**<br /><br /> **MUITOS**|  
|**MIME_TYPE**|**DBTYPE_WSTR**||O tipo mime para BLOBs (objetos binários grandes).|  
|**PROPERTY_IS_VISIBLE**|**DBTYPE_BOOL**||Um Booliano que indica se a propriedade está visível.<br /><br /> **TRUE** se a propriedade estiver visível; caso contrário, **FALSE**.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O **MDSCHEMA_PROPERTIES** linhas pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Obrigatório|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Opcional|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Opcional|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional|  
|**MEMBER_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional|  
|**PROPERTY_TYPE**|**DBTYPE_I2**|Opcional|  
|**PROPERTY_NAME**|**DBTYPE_WSTR**|Opcional|  
|**PROPERTY_CONTENT_TYPE**|**DBTYPE_I2**|(Opcional) Uma restrição padrão está em vigor em **MDPROP_MEMBER** ou **MDPROP_CELL**.|  
|**PROPERTY_ORIGIN**|**DBTYPE_UI2**|(Opcional) Uma restrição padrão está em vigor em **MD_USER_DEFINED** ou **MD_SYSTEM_ENABLED**.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(Opcional) A restrição padrão é um valor de 1.  Um bitmap com um dos seguintes valores válidos:<br /><br /> 1 CUBO<br /><br /> 2 DIMENSÃO|  
|**PROPERTY_VISIBILITY**|**DBTYPE_UI2**|(Opcional) A restrição padrão é um valor de 1. Um bitmap com um dos seguintes valores válidos:<br /><br /> 1 Visível<br /><br /> 2 não visível|  
  
## <a name="see-also"></a>Consulte também  
 [OLE DB para OLAP Schema Rowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
