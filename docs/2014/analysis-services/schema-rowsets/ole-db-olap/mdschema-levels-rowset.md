---
title: Conjunto de linhas MDSCHEMA_LEVELS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MDSCHEMA_LEVELS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_LEVELS rowset
ms.assetid: 4313e268-33f4-4e99-96d7-2ec26775c580
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9491143a33dbd68ab0f0ea9cb3745f1e784879b8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48191796"
---
# <a name="mdschemalevels-rowset"></a>Conjunto de linhas MDSCHEMA_LEVELS
  Descreve cada nível dentro de uma hierarquia específica.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `MDSCHEMA_LEVELS` linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||O nome do catálogo ao qual esse nível pertence. `NULL` se o provedor não oferecer suporte a catálogos.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||O nome do esquema ao qual esse nível pertence. `NULL` se o provedor não oferecer suporte a esquemas.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||O nome do cubo ao qual pertence esse nível.|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`||O nome exclusivo da dimensão à qual pertence esse nível. Para provedores que geram nomes exclusivos por qualificação, cada componente desse nome é delimitado.|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`||O nome exclusivo da hierarquia. Se o nível pertencer a mais de uma hierarquia, haverá uma fila para cada hierarquia à qual ele pertence. Para provedores que geram nomes exclusivos por qualificação, cada componente desse nome é delimitado.|  
|`LEVEL_NAME`|`DBTYPE_WSTR`||O nome do nível.|  
|`LEVEL_UNIQUE_NAME`|`DBTYPE_WSTR`||O nome exclusivo do nível com caracteres de escape corretos.|  
|`LEVEL_GUID`|`DBTYPE_GUID`||Sem suporte.|  
|`LEVEL_CAPTION`|`DBTYPE_WSTR`||Um rótulo ou legenda associada à hierarquia. Usado principalmente para fins de exibição. Se não houver uma legenda, `LEVEL_NAME` será retornado.|  
|`LEVEL_NUMBER`|`DBTYPE_UI4`||A distância do nível a partir da raiz da hierarquia. O nível da raiz é zero (`0)`.|  
|`LEVEL_CARDINALITY`|`DBTYPE_UI4`||O número de membros no nível.|  
|`LEVEL_TYPE`|`DBTYPE_I4`||O tipo do nível:<br /><br /> -   `MDLEVEL_TYPE_GEO_CONTINENT` (`0x2001`)<br />-   `MDLEVEL_TYPE_GEO_REGION` (`0x2002`)<br />-   `MDLEVEL_TYPE_GEO_COUNTRY` (`0x2003`)<br />-   `MDLEVEL_TYPE_GEO_STATE_OR_PROVINCE` (`0x2004`)<br />-   `MDLEVEL_TYPE_GEO_COUNTY` (`0x2005`)<br />-   `MDLEVEL_TYPE_GEO_CITY` (`0x2006`)<br />-   `MDLEVEL_TYPE_GEO_POSTALCODE` (`0x2007`)<br />-   `MDLEVEL_TYPE_GEO_POINT` (`0x2008`)<br />-   `MDLEVEL_TYPE_ORG_UNIT` (`0x1011`)<br />-   `MDLEVEL_TYPE_BOM_RESOURCE` (`0x1012`)<br />-   **MDLEVEL_TYPE_QUANTITATIVE** (`0x1013`)<br />-   `MDLEVEL_TYPE_ACCOUNT` (`0x1014`)<br />-   `MDLEVEL_TYPE_CUSTOMER` (`0x1021`)<br />-   `MDLEVEL_TYPE_CUSTOMER_GROUP` (`0x1022`)<br />-   `MDLEVEL_TYPE_CUSTOMER_HOUSEHOLD` (`0x1023`)<br />-   `MDLEVEL_TYPE_PRODUCT` (`0x1031`)<br />-   `MDLEVEL_TYPE_PRODUCT_GROUP` (`0x1032`)<br />-   `MDLEVEL_TYPE_SCENARIO` (`0x1015`)<br />-   `MDLEVEL_TYPE_UTILITY` (`0x1016`)<br />-   `MDLEVEL_TYPE_PERSON` (`0x1041`)<br />-   `MDLEVEL_TYPE_COMPANY` (`0x1042`)<br />-   `MDLEVEL_TYPE_CURRENCY_SOURCE` (`0x1051`)<br />-   `MDLEVEL_TYPE_CURRENCY_DESTINATION` (`0x1052`)<br />-   `MDLEVEL_TYPE_CHANNEL` (`0x1061`)<br />-   `MDLEVEL_TYPE_REPRESENTATIVE` (`0x1062`)<br />-   `MDLEVEL_TYPE_PROMOTION` (`0x1071`)|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Uma descrição legível do nível. NULL quando não existe descrição.|  
|`CUSTOM_ROLLUP_SETTINGS`|`DBTYPE_I4`||Um bitmap que especifica as opções de rollup personalizado:<br /><br /> -   `MDLEVELS_CUSTOM_ROLLUP_EXPRESSION` (`0x01`) indica que existe uma expressão para esse nível. (Preterido)<br />-   `MDLEVELS_CUSTOM_ROLLUP_COLUMN` (`0x02`) indica que há uma coluna de rollup personalizado para esse nível.<br />-   `MDLEVELS_SKIPPED_LEVELS` (`0x04`) indica que há um nível ignorado associado a membros desse nível.<br />-   `MDLEVELS_CUSTOM_MEMBER_PROPERTIES` (`0x08`) indica que os membros do nível têm propriedades de membro personalizado.<br />-   `MDLEVELS_UNARY_OPERATOR` (`0x10`) indica que os membros do nível têm operadores unários.|  
|`LEVEL_UNIQUE_SETTINGS`|`DBTYPE_I4`||Um bitmap que especifica quais colunas contêm valores exclusivos, se o nível só contém os membros com nomes ou chaves exclusivas. O arquivo Msmd.h define as seguintes constantes do valor de bit para esse bitmap:<br /><br /> -   `MDDIMENSIONS_MEMBER_KEY_UNIQUE` (`1`)<br />-   `MDDIMENSIONS_MEMBER_NAME_UNIQUE` (`2`)<br /><br /> A chave é sempre exclusiva no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. O nome será exclusivo se a configuração no atributo for `UniqueInDimension` ou `UniqueInAttribute`|  
|`LEVEL_IS_VISIBLE`|`DBTYPE_BOOL`||Um Booliano que indica se o nível é visível.<br /><br /> Sempre retorna True. Se o nível não for visível, ele não será incluído no conjunto de linhas de esquema.|  
|`LEVEL_ORDERING_PROPERTY`|`DBTYPE_WSTR`||A ID do atributo no qual o nível é classificado.|  
|`LEVEL_DBTYPE`|`DBTYPE_I4`||A enumeração `DBTYPE` da coluna de chave do membro que é usada para o atributo de nível.<br /><br /> Nulo quando chaves concatenadas são usadas como a coluna de chave do membro.|  
|`LEVEL_MASTER_UNIQUE_NAME`|`DBTYPE_WSTR`||Sempre retorna NULL.|  
|`LEVEL_NAME_SQL_COLUMN_NAME`|`DBTYPE_WSTR`||A representação de SQL dos nomes de membro de nível.|  
|`LEVEL_KEY_SQL_COLUMN_NAME`|`DBTYPE_WSTR`||A representação de SQL dos valores de chaves do membro de nível.|  
|`LEVEL_UNIQUE_NAME_SQL_COLUMN_NAME`|`DBTYPE_WSTR`||A representação de SQL dos nomes exclusivos de membro.|  
|`LEVEL_ATTRIBUTE_HIERARCHY_NAME`|`DBTYPE_WSTR`||O nome da hierarquia de atributos que fornece a origem do nível.|  
|`LEVEL_KEY_CARDINALITY`|`DBTYPE_UI2`||O número de colunas na chave de nível.|  
|`LEVEL_ORIGIN`|`DBTYPE_UI2`||Um bitmap que define a origem do nível:<br /><br /> -   `MD_ORIGIN_USER_DEFINED` identifica níveis em uma hierarquia definida pelo usuário.<br />-   `MD_ORIGIN_ATTRIBUTE` identifica níveis em uma hierarquia de atributo.<br />-   `MD_ORIGIN_KEY_ATTRIBUTE` identifica níveis em uma hierarquia de atributo de chave.<br />-   `MD_ORIGIN_INTERNAL` identifica níveis em hierarquias de atributo que não estão habilitados.|  
  
 O conjunto de linhas é classificado em `CATALOG_NAME`, `SCHEMA_NAME`, `CUBE_NAME`, `DIMENSION_UNIQUE_NAME`, `HIERARCHY_UNIQUE_NAME`, `LEVEL_NUMBER`.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `MDSCHEMA_LEVELS` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`LEVEL_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`LEVEL_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`LEVEL_ORIGIN`|`DBTYPE_UI2`|(Opcional) Uma restrição padrão está em vigor em `MD_USER_DEFINED` e `MD_SYSTEM_ENABLED`|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(Opcional) Um bitmap com um dos seguintes valores válidos:<br /><br /> -CUBO DE 1<br />-DIMENSÃO DE 2<br /><br /> A restrição padrão tem valor 1.|  
|`LEVEL_VISIBILITY`|`DBTYPE_UI2`|(Opcional) Um bitmap com um dos seguintes valores:<br /><br /> -Visible 1<br />-2 não visível<br /><br /> A restrição padrão tem valor 1.|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema OLE DB para OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  
