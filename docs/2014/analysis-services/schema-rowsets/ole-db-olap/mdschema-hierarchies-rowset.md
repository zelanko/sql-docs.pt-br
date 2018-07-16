---
title: Conjunto de linhas MDSCHEMA_HIERARCHIES | Microsoft Docs
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
- MDSCHEMA_HIERARCHIES
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_HIERARCHIES rowset
ms.assetid: 2e5b2a81-366e-4d5b-af1e-1d372bf596d9
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a38dd03023fc266c5b8505979766d90979d16f05
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37321216"
---
# <a name="mdschemahierarchies-rowset"></a>Conjunto de linhas MDSCHEMA_HIERARCHIES
  Descreve cada hierarquia dentro de determinada dimensão.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `MDSCHEMA_HIERARCHIES` linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||O nome do catálogo ao qual essa hierarquia pertence. `NULL` se o provedor não oferecer suporte a catálogos.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||Sem suporte|  
|`CUBE_NAME`|`DBTYPE_WSTR`||(Necessário) O nome exclusivo do cubo ao qual pertence essa hierarquia.|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`||O nome exclusivo da dimensão à qual pertence essa hierarquia. Para provedores que geram nomes exclusivos por qualificação, cada componente desse nome é delimitado.|  
|`HIERARCHY_NAME`|`DBTYPE_WSTR`||O nome da hierarquia. Em branco quando há uma única hierarquia na dimensão. Este item sempre terá um valor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`||O nome exclusivo da hierarquia.|  
|`HIERARCHY_GUID`|`DBTYPE_GUID`||Sem suporte|  
|`HIERARCHY_CAPTION`|`DBTYPE_WSTR`||Um rótulo ou legenda associada à hierarquia. Usado principalmente para fins de exibição. Se não houver uma legenda, `HIERARCHY_NAME` será retornado. Se a dimensão não contiver uma hierarquia ou tiver apenas uma hierarquia, essa coluna conterá o nome da dimensão.|  
|`DIMENSION_TYPE`|`DBTYPE_I2`||O tipo da dimensão. Os valores válidos incluem:<br /><br /> -   `MD_DIMTYPE_UNKNOWN` (`0`)<br />-   `MD_DIMTYPE_TIME` (`1`)<br />-   `MD_DIMTYPE_MEASURE` (`2`)<br />-   `MD_DIMTYPE_OTHER` (`3`)<br />-   `MD_DIMTYPE_QUANTITATIVE` (`5`)<br />-   `MD_DIMTYPE_ACCOUNTS` (`6`)<br />-   `MD_DIMTYPE_CUSTOMERS` (`7`)<br />-   `MD_DIMTYPE_PRODUCTS` (`8`)<br />-   `MD_DIMTYPE_SCENARIO` (`9`)<br />-   `MD_DIMTYPE_UTILIY` (`10`)<br />-   `MD_DIMTYPE_CURRENCY` (`11`)<br />-   `MD_DIMTYPE_RATES` (`12`)<br />-   `MD_DIMTYPE_CHANNEL` (`13`)<br />-   `MD_DIMTYPE_PROMOTION` (`14`)<br />-   `MD_DIMTYPE_ORGANIZATION` (`15`)<br />-   `MD_DIMTYPE_BILL_OF_MATERIALS` (`16`)<br />-   `MD_DIMTYPE_GEOGRAPHY` (`17`)|  
|`HIERARCHY_CARDINALITY`|`DBTYPE_UI4`||O número de membros na hierarquia.|  
|`DEFAULT_MEMBER`|`DBTYPE_WSTR`||O membro padrão dessa hierarquia. Este é um nome exclusivo. Cada hierarquia deve ter um membro padrão.|  
|`ALL_MEMBER`|`DBTYPE_WSTR`||O membro no nível mais alto do rollup.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Uma descrição humanamente legível da hierarquia. `NULL` quando não existe descrição.|  
|`STRUCTURE`|`DBTYPE_I2`||A estrutura da hierarquia. Os valores válidos incluem:<br /><br /> -   `MD_STRUCTURE_FULLYBALANCED` (`0`)<br />-   `MD_STRUCTURE_RAGGEDBALANCED` (`1`)<br />-   `MD_STRUCTURE_UNBALANCED` (`2`)<br />-   `MD_STRUCTURE_NETWORK` (`3`)|  
|`IS_VIRTUAL`|`DBTYPE_BOOL`||Sempre retorna `False`.|  
|`IS_READWRITE`|`DBTYPE_BOOL`||Um booliano que indica se a coluna Write Back to dimension está habilitada.<br /><br /> Retornará `TRUE` se a coluna `Write Back to dimension` que representa essa hierarquia estiver habilitada.|  
|`DIMENSION_UNIQUE_SETTINGS`|`DBTYPE_I4`||Sempre retorna `MDDIMENSIONS_MEMBER_KEY_UNIQUE` (`1`).|  
|`DIMENSION_MASTER_UNIQUE_NAME`|`DBTYPE_WSTR`||Sempre retorna `NULL`.|  
|`DIMENSION_IS_VISIBLE`|`DBTYPE_BOOL`||Sempre retorna `true`. Se a dimensão não estiver visível, ela não aparecerá no conjunto de linhas de esquema.|  
|`HIERARCHY_ORDINAL`|`DBTYPE_UI4`||O número ordinal da hierarquia em todas as hierarquias do cubo.|  
|`DIMENSION_IS_SHARED`|`DBTYPE_BOOL`||Sempre retorna `TRUE`.|  
|`HIERARCHY_IS_VISIBLE`|`DBTYPE_BOOL`||Um Booliano que indica se a hierarquia está visível.<br /><br /> Retornará `TRUE` se a hierarquia estiver visível; caso contrário, `FALSE`.|  
|`HIERARCHY_ORIGIN`|`DBTYPE_UI2`||Uma máscara de bits que determina a origem da hierarquia:<br /><br /> -   `MD_USER_DEFINED` identifica hierarquias definidas pelo usuário, e tem um valor de `0x0000001`.<br />-   `MD_SYSTEM_ENABLED` identifica hierarquias de atributo e tem um valor de `0x0000002`.<br />-   `MD_SYSTEM_INTERNAL` identifica atributos sem hierarquias de atributo e tem um valor de **0x0000004**.<br /><br /> Uma hierarquia de atributo de pai/filho é `MD_USER_DEFINED` e `MD_SYSTEM_ENABLED`.|  
|`HIERARCHY_DISPLAY_FOLDER`|`DBTYPE_WSTR`||O caminho a ser usado ao exibir a hierarquia na interface do usuário. Os nomes de pastas serão separados por ponto-e-vírgula (;). Pastas aninhadas são indicadas por uma barra invertida (\\).|  
|`INSTANCE_SELECTION`|`DBTYPE_UI2`||Uma dica para o aplicativo cliente sobre como mostrar a hierarquia. Os valores válidos incluem:<br /><br /> -   `MD_INSTANCE_SELECTION_NONE`<br />-   `MD_INSTANCE_SELECTION_DROPDOWN`<br />-   `MD_INSTANCE_SELECTION_LIST`<br />-   `MD_INSTANCE_SELECTION_FILTEREDLIST`<br />-   `MD_INSTANCE_SELECTION_MANDATORYFILTER`|  
|`GROUPING_BEHAVIOR`|`DBTYPE_I2`||Uma enumeração que especifica o comportamento de agrupamento esperado de clientes para esta hierarquia. Os valores possíveis são os seguintes:<br /><br /> -   **EncourageGrouping** (1)<br />-   **DiscourageGrouping** (2)|  
|`STRUCTURE_TYPE`|`DBTYPE_WSTR`||Indica o tipo de hierarquia. Os valores válidos incluem:<br /><br /> -   `Natural`<br />-   `Unnatural`<br />-   `Unknown`|  
  
 O conjunto de linhas é classificado em `CATALOG_NAME`, `SCHEMA_NAME`, `CUBE_NAME`, `DIMENSION_UNIQUE_NAME`, `HIERARCHY_NAME`.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `MDSCHEMA_HIERARCHIES` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`HIERARCHY_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`HIERARCHY_ORIGIN`|`DBTYPE_UI2`|(Opcional) Uma restrição padrão está em vigor em MD_USER_DEFINED e MD_SYSTEM_ENABLED.|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(Opcional) Um bitmap com um dos seguintes valores válidos:<br /><br /> -CUBO DE 1<br />-DIMENSÃO DE 2<br /><br /> A restrição padrão tem valor 1.|  
|`HIERARCHY_VISIBILITY`|`DBTYPE_UI2`|(Opcional) Um bitmap com um dos seguintes valores válidos:<br /><br /> -Visible 1<br />-2 não visível<br /><br /> A restrição padrão tem valor 1.|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema OLE DB para OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  
