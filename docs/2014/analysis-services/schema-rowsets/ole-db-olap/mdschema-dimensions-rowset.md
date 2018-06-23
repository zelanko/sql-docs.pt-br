---
title: Conjunto de linhas MDSCHEMA_DIMENSIONS | Microsoft Docs
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
- MDSCHEMA_DIMENSIONS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_DIMENSIONS rowset
ms.assetid: a0fd94bb-359a-4df6-93a6-d60d50223944
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b00b617adf90e1dba8eac94a9872ce07c0773e7c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008294"
---
# <a name="mdschemadimensions-rowset"></a>Conjunto de linhas MDSCHEMA_DIMENSIONS
  Descreve as dimensões compartilhadas e privadas dentro de um banco de dados.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas `MDSCHEMA_DIMENSIONS` contém as seguintes colunas:  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||O nome do banco de dados.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||Sem suporte.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||O nome do cubo.|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`||O nome da dimensão. Se uma dimensão fizer parte de mais de um cubo ou grupo de medidas, haverá uma linha para cada combinação exclusiva de dimensão, grupo de medidas e cubo.|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`||O nome exclusivo da dimensão.|  
|`DIMENSION_GUID`|`DBTYPE_GUID`||Sem suporte.|  
|`DIMENSION_CAPTION`|`DBTYPE_WSTR`||A legenda da dimensão. Isso deve ser usado durante a exibição do nome da dimensão para o usuário, como na interface do usuário ou em relatórios.|  
|`DIMENSION_ORDINAL`|`DBTYPE_UI4`||A posição da dimensão dentro do cubo.|  
|`DIMENSION_TYPE`|`DBTYPE_I2`||O tipo da dimensão. Os valores válidos incluem:<br /><br /> -   `MD_DIMTYPE_UNKNOWN` (`0`)<br />-   `MD_DIMTYPE_TIME` (`1`)<br />-   `MD_DIMTYPE_MEASURE` (`2`)<br />-   `MD_DIMTYPE_OTHER` (`3`)<br />-   `MD_DIMTYPE_QUANTITATIVE` (`5`)<br />-   `MD_DIMTYPE_ACCOUNTS` (`6`)<br />-   `MD_DIMTYPE_CUSTOMERS` (`7`)<br />-   `MD_DIMTYPE_PRODUCTS` (`8`)<br />-   `MD_DIMTYPE_SCENARIO` (`9`)<br />-   `MD_DIMTYPE_UTILIY` (`10`)<br />-   `MD_DIMTYPE_CURRENCY` (`11`)<br />-   `MD_DIMTYPE_RATES` (`12`)<br />-   `MD_DIMTYPE_CHANNEL` (`13`)<br />-   `MD_DIMTYPE_PROMOTION` (`14`)<br />-   `MD_DIMTYPE_ORGANIZATION` (`15`)<br />-   `MD_DIMTYPE_BILL_OF_MATERIALS` (`16`)<br />-   `MD_DIMTYPE_GEOGRAPHY` (`17`)|  
|`DIMENSION_CARDINALITY`|`DBTYPE_UI4`||O número de membros no atributo de chave.|  
|`DEFAULT_HIERARCHY`|`DBTYPE_WSTR`||Uma hierarquia da dimensão. Preservada para compatibilidade com versões anteriores.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Uma descrição amigável da dimensão.|  
|`IS_VIRTUAL`|`DBTYPE_BOOL`||Sempre `FALSE`.|  
|`IS_READWRITE`|`DBTYPE_BOOL`||Um Booliano que indica se a dimensão está habilitada para gravação.<br /><br /> `TRUE` se a dimensão está habilitada para gravação.|  
|`DIMENSION_UNIQUE_SETTINGS`|`DBTYPE_I4`||Um bitmap que especifica quais colunas contêm valores exclusivos se a dimensão contém apenas os membros com nomes exclusivos. As seguintes constantes de valor de bit são definidas no Msmd.h para este bitmap:<br /><br /> -   `MDDIMENSIONS_MEMBER_KEY_UNIQUE`|  
|`DIMENSION_MASTER_UNIQUE_NAME`|`DBTYPE_WSTR`||Sempre `NULL`.|  
|`DIMENSION_IS_VISIBLE`|`DBTYPE_BOOL`||Sempre `TRUE`. **Observação:** uma dimensão não estiver visível, a menos que uma ou mais hierarquias da dimensão estão visíveis.|  
  
 O conjunto de linhas é classificado em `CATALOG_NAME`, `SCHEMA_NAME`, `CUBE_NAME`, `DIMENSION_NAME`.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `MDSCHEMA_DIMENSIONS` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(Opcional) Um bitmap com um dos seguintes valores válidos:<br /><br /> -CUBO DE 1<br />-DIMENSÃO DE 2<br /><br /> A restrição padrão tem valor 1.|  
|`DIMENSION_VISIBILITY`|`DBTYPE_UI2`|(Opcional) Um bitmap com um dos seguintes valores válidos:<br /><br /> -1 visível<br />-2 não visível<br /><br /> A restrição padrão tem valor 1.|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema OLE DB para OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  