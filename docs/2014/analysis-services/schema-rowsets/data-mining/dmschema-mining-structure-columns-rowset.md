---
title: Conjunto de linhas DMSCHEMA_MINING_STRUCTURE_COLUMNS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DMSCHEMA_MINING_STRUCTURE_COLUMNS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_STRUCTURE_COLUMNS rowset
ms.assetid: 81f25502-ac90-42f1-8ddf-7b0f9752ebfd
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 98c8ec286e12cfe6198c36900067a26eefd5e1ad
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010307"
---
# <a name="dmschemaminingstructurecolumns-rowset"></a>Conjunto de linhas DMSCHEMA_MINING_STRUCTURE_COLUMNS
  Descreve as colunas individuais de todas as estruturas de mineração implantadas em um servidor que esteja executando [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DMSCHEMA_MINING_STRUCTURE_COLUMNS` linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`STRUCTURE_CATALOG`|`DBTYPE_WSTR`||O nome do catálogo.|  
|`STRUCTURE_SCHEMA`|`DBTYPE_WSTR`||O nome do esquema não qualificado. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] não oferece suporte a esquemas e, portanto, essa coluna sempre é `NULL`.|  
|`STRUCTURE_NAME`|`DBTYPE_WSTR`||O nome da estrutura. Esta coluna não pode conter um `NULL`.|  
|`COLUMN_NAME`|`DBTYPE_WSTR`||O nome da coluna. A exclusividade só é garantida entre colunas que compartilham o mesmo padrão. Por exemplo, duas colunas aninhadas poderão ter o mesmo nome se pertencerem a duas tabelas aninhadas diferentes dentro da mesma estrutura.|  
|`COLUMN_GUID`|`DBTYPE_GUID`||O GUID da coluna. Os provedores que não usam GUIDs para identificar colunas devem retornar `NULL` nesta coluna.|  
|`COLUMN_PROPID`|`DBTYPE_UI4`||A ID de propriedade da coluna. Os provedores que não associam IDs de propriedade a colunas devem retornar `NULL` nesta coluna. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Retorna `NULL` para esta coluna.|  
|`ORDINAL_POSITION`|`DBTYPE_UI4`||O ordinal da coluna. As colunas são numeradas a partir de 1. `NULL` se não houver nenhum valor ordinal estável para a coluna.|  
|`COLUMN_HASDEFAULT`|`DBTYPE_BOOL`||Um booliano que indica se esta coluna tem um valor padrão.<br /><br /> Será `TRUE` se a coluna tiver um valor padrão.<br /><br /> Será `FALSE` se a coluna não tiver um valor padrão ou se não for possível determinar se a coluna tem um valor padrão.|  
|`COLUMN_DEFAULT`|`DBTYPE_WSTR`||O valor padrão da coluna. Um provedor pode expor `DBCOLUMN_DEFAULTVALUE` mas não `DBCOLUMN_HASDEFAULT` (para tabelas ISO) no conjunto de linhas retornado por `IColumnsRowset::GetColumnsRowset`.<br /><br /> Se o valor padrão for `NULL`, `COLUMN_HASDEFAULT` será `TRUE` e a coluna `COLUMN_DEFAULT` será um valor `NULL`.|  
|`COLUMN_FLAGS`|`DBTYPE_UI4`||-Um bitmask que descreve as características da coluna. O tipo enumerado `DBCOLUMNFLAGS` especifica os bits da máscara de bits. Esta coluna não pode conter um valor `NULL`. Os valores válidos incluem:<br />-   **DBCOLUMNFLAGS_ISNULLABLE** (`0x20`)<br />-   **DBCOLUMNFLAGS_MAYBENULL** (`0x40`)<br />-   **DBCOLUMNFLAGS_ISLONG** (`0x80`)|  
|`IS_NULLABLE`|`DBTYPE_BOOL`||Um booliano que indica se esta coluna tem um valor padrão.<br /><br /> Será `TRUE` se a coluna puder conter `NULL`; caso contrário, será `FALSE`.|  
|`DATA_TYPE`|`DBTYPE_UI2`||O indicador do tipo de dados da coluna. Por exemplo:<br /><br /> -   "`TABLE`" = `DBTYPE_HCHAPTER`<br />-   "`TEXT`" = `DBTYPE_WCHAR`<br />-   "`LONG`" = `DBTYPE_I8`<br />-   "`DOUBLE`" = `DBTYPE_R8`<br />-   "`DATE`" = `DBTYPE_DATE`|  
|`TYPE_GUID`|`DBTYPE_GUID`||O GUID do tipo de dados da coluna. Os provedores que não usam os GUIDs para identificar tipos de dados deverão retornar `NULL` nesta coluna.|  
|`CHARACTER_MAXIMUM_LENGTH`|`DBTYPE_UI4`||O comprimento máximo possível de um valor na coluna. Para colunas de caracteres, de binários ou de bits, será uma das opções a seguir:<br /><br /> -O comprimento máximo da coluna em caracteres, em bytes ou em bits, respectivamente, se o comprimento é definido. Por exemplo, uma coluna `CHAR(5)` de uma tabela SQL terá o comprimento máximo de 5.<br />-O comprimento máximo dos dados de tipo em caracteres, em bytes ou bits, respectivamente, se a coluna não tiver um comprimento definido.<br />-Zero (0) se a coluna ou o tipo de dados tem um comprimento máximo definido.<br />-   `NULL` todos os outros tipos de colunas.|  
|`CHARACTER_OCTET_LENGTH`|`DBTYPE_UI4`||O comprimento máximo em octetos (bytes) da coluna, se o tipo da coluna for caractere ou binário. Um valor zero (0) significa que a coluna não tem um comprimento máximo. Será `NULL` para todos os outros tipos de colunas.|  
|`NUMERIC_PRECISION`|`DBTYPE_UI2`||A precisão máxima da coluna se o seu tipo de dados for um tipo numérico diferente de `VARNUMERIC`; será `NULL` se o tipo de dados da coluna não for numérico ou se for `VARNUMERIC`.<br /><br /> A precisão de colunas com o tipo de dados `DBTYPE_DECIMAL` ou `DBTYPE_NUM`ERIC dependerá da definição da coluna.|  
|`NUMERIC_SCALE`|`DBTYPE_I2`||O número de dígitos à direita da vírgula decimal se o indicador do tipo da coluna for `DBTYPE_DECIMAL`, `DBTYPE_NUMERIC` ou `DBTYPE_VARNUMERIC`. Caso contrário, será `NULL`.|  
|`DATETIME_PRECISION`|`DBTYPE_UI4`||A precisão de DateTime (o número de dígitos na parte fracionária de segundos) da coluna se ela for do tipo datetime ou intervalo. Se o tipo de dados da coluna não for datetime, será `NULL`.|  
|`CHARACTER_SET_CATALOG`|`DBTYPE_WSTR`||O nome de catálogo no qual o conjunto de caracteres é definido. `NULL` se o provedor não oferecer suporte a catálogos ou conjuntos de caracteres diferentes.|  
|`CHARACTER_SET_SCHEMA`|`DBTYPE_WSTR`||O nome de esquema não qualificado no qual o conjunto de caracteres é definido. `NULL` se o provedor não oferecer suporte a esquemas ou conjuntos de caracteres diferentes.|  
|`CHARACTER_SET_NAME`|`DBTYPE_WSTR`||Nome do conjunto de caracteres. `NULL` se o provedor não oferecer suporte a conjuntos de caracteres diferentes.|  
|`COLLATION_CATALOG`|`DBTYPE_WSTR`||O nome de catálogo no qual o agrupamento é definido. `NULL` se o provedor não oferecer suporte a catálogos ou agrupamentos diferentes.|  
|`COLLATION_SCHEMA`|`DBTYPE_WSTR`||O nome do esquema não qualificado no qual o agrupamento é definido. `NULL` se o provedor não oferecer suporte a esquemas ou agrupamentos diferentes.|  
|`COLLATION_NAME`|`DBTYPE_WSTR`||O nome do agrupamento. `NULL` se o provedor não oferecer suporte a agrupamentos diferentes.|  
|`DOMAIN_CATALOG`|`DBTYPE_WSTR`||O nome de catálogo no qual o domínio é definido. `NULL` se o provedor não oferecer suporte a catálogos ou domínios.|  
|`DOMAIN_SCHEMA`|`DBTYPE_WSTR`||O nome do esquema não qualificado no qual o domínio é definido. `NULL` se o provedor não oferecer suporte a esquemas ou domínios.|  
|`DOMAIN_NAME`|`DBTYPE_WSTR`||O nome de domínio. `NULL` se o provedor não oferecer suporte a domínios.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Uma descrição legível da coluna. `NULL` se não houver descrição associada à coluna.|  
|`DISTRIBUTION_FLAG`|`DBTYPE_WSTR`||A distribuição da coluna de estrutura de mineração:<br /><br /> -   "`NORMAL`"<br />-"`LOG_NORM`AL"<br />-   "`UNIFORM`"|  
|`CONTENT_TYPE`|`DBTYPE_WSTR`||O tipo de conteúdo da coluna de estrutura de mineração:<br /><br /> -   "`KEY`"<br />-   "`DISCRETE`"<br />-   "`CONTINUOUS`"<br />-"`DISCRETIZED(`[args]`)`"<br />-   "`ORDERED`"<br />-   "`SEQUENCE_TIME`"<br />-   "`CYCLICAL`"<br />-   "`PROBABILITY`"<br />-   "`VARIANCE`"<br />-   "`STDEV`"<br />-   "`SUPPORT`"<br />-   "`PROBABILITY_VARIANCE`"<br />-   "`PROBABILITY_STDEV`"|  
|`MODELING_FLAG`|`DBTYPE_WSTR`||Uma lista delimitada por vírgulas de sinalizadores de modelagem. O único sinalizador suportado para uma coluna de estrutura é "`NOT NULL`".|  
|`IS_RELATED_TO_KEY`|`DBTYPE_BOOL`||Um booliano que indica se esta coluna está relacionada à chave.<br /><br /> Será `VARIANT_TRUE` se esta coluna for relacionada à chave; caso contrário, será `VARIANT_FALSE`. Se a chave for uma única coluna, o `RELATED_ATTRIBUTE` campo opcionalmente pode conter seu nome de coluna.|  
|`RELATED_ATTRIBUTE`|`DBTYPE_WSTR`||O nome da coluna de destino à qual a coluna atual está relacionada ou de quem é uma propriedade especial.|  
|`CONTAINING_COLUMN`|`DBTYPE_WSTR`||O nome do `TABLE` coluna que contém esta coluna. `NULL` se nenhuma tabela contiver a coluna.|  
|`IS_POPULATED`|`DBTYPE_BOOL`||Um booliano que indica se esta coluna aprendeu um conjunto de valores possíveis.<br /><br /> Será `TRUE` se a coluna aprendeu um conjunto de valores possíveis; caso contrário, será `FALSE`.|  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `DMSCHEMA_MINING_STRUCTURE_COLUMNS` pode ser restringido nas colunas da tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`STRUCTURE_CATALOG`|`DBTYPE_WSTR`|Opcional.|  
|`STRUCTURE_SCHEMA`|`DBTYPE_WSTR`|Opcional.|  
|`STRUCTURE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`COLUMN_NAME`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema de mineração de dados](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  