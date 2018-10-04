---
title: Linhas de DMSCHEMA_MINING_COLUMNS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DMSCHEMA_MINING_COLUMNS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_COLUMNS rowset
ms.assetid: ae35ccde-4438-46f4-8611-40b2b1a42fce
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2f7d19a29ceb67f83742e19615d9086315b600b6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200696"
---
# <a name="dmschemaminingcolumns-rowset"></a>Conjunto de linhas de DMSCHEMA_MINING_COLUMNS
  Descreve as colunas individuais de todos os modelos de mineração de dados no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Este conjunto de linhas é restrito ao catálogo atual.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DMSCHEMA_MINING_COLUMNS` linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`||O nome do catálogo. Preenchido com o nome do banco de dados do qual o modelo é membro.|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`||O nome do esquema não qualificado. Esta coluna não é suportada pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá `NULL`.|  
|`MODEL_NAME`|`DBTYPE_WSTR`||O nome do modelo de mineração. Esta coluna contém o nome do modelo de mineração ao qual uma coluna é associada, e nunca estará vazia.|  
|`COLUMN_NAME`|`DBTYPE_WSTR`||O nome da coluna.|  
|`COLUMN_GUID`|`DBTYPE_GUID`||O GUID da coluna. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá `NULL`.|  
|`COLUMN_PROPID`|`DBTYPE_UI4`||A ID de propriedade da coluna. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá `NULL`.|  
|`ORDINAL_POSITION`|`DBTYPE_UI4`||A posição ordinal da coluna. As colunas são numeradas a partir de 1. Esta coluna conterá `NULL` se não houver nenhum valor ordinal estável para ela.|  
|`COLUMN_HAS_DEFAULT`|`DBTYPE_BOOL`||Um Booliano que indica se a coluna tem um valor padrão.<br /><br /> Será `TRUE` se a coluna tiver um valor padrão, caso contrário, será `FALSE`.|  
|`COLUMN_DEFAULT`|`DBTYPE_WSTR`||O valor padrão da coluna.<br /><br /> Se o valor padrão for `NULL`, `COLUMN_HASDEFAULT` conterá `TRUE` e esta coluna conterá `NULL`.|  
|`COLUMN_FLAGS`|`DBTYPE_UI4`||Uma máscara de bits que descreve as características da coluna. O tipo enumerado `DBCOLUMNFLAGS` especifica os bits da máscara de bits. Esta coluna nunca está vazia.|  
|`IS_NULLABLE`|`DBTYPE_BOOL`||Um Booliano que indica se a coluna pode conter valores nulos.<br /><br /> Será `FALSE` se a coluna não puder conter valores nulos; caso contrário, será `TRUE`.|  
|`DATA_TYPE`|`DBTYPE_UI2`||O indicador do tipo de dados da coluna. A lista a seguir mostra exemplos dos tipos de indicadores retornados:<br /><br /> "`TABLE`" retornaria `DBTYPE_HCHAPTER`.<br /><br /> "`TEXT`" retornaria `DBTYPE_WCHAR`.<br /><br /> "`LONG`" retornaria `DBTYPE_I8`.<br /><br /> "`DOUBLE`" retornaria `DBTYPE_R8`.<br /><br /> "`DATE`" retornaria `DBTYPE_DATE`.|  
|`TYPE_GUID`|`DBTYPE_GUID`||O GUID do tipo de dados da coluna. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá `VT_NULL`.|  
|`CHARACTER_MAXIMUM_LENGTH`|`DBTYPE_UI4`||O comprimento máximo possível de um valor na coluna. Para colunas de caracteres, de binários ou de bits, será uma das opções a seguir:<br /><br /> -O comprimento máximo da coluna em bits, respectivo ao tipo de coluna, se um comprimento for definido, em bytes ou caracteres. Por exemplo, uma coluna `CHAR(5)` de uma tabela SQL terá o comprimento máximo de 5.<br />-O comprimento máximo do tipo de dados em bits, respectivo ao tipo de coluna, se a coluna não tiver um comprimento definido, em bytes ou caracteres.<br />-Zero (0) se a coluna ou o tipo de dados tem um comprimento máximo definido.<br />-   `NULL` para todos os outros tipos de colunas|  
|`CHARACTER_OCTET_LENGTH`|`DBTYPE_UI4`||O comprimento máximo em octetos (bytes) da coluna, se o tipo da coluna for caractere ou binário. Um valor zero (0) significa que a coluna não tem um comprimento máximo. Esta coluna contém `NULL` para todos os outros tipos de colunas.|  
|`NUMERIC_PRECISION`|`DBTYPE_UI2`||A precisão máxima da coluna se o tipo de dados da coluna for um tipo numérico diferente de `VARNUMERIC`.<br /><br /> Será `NULL` se o tipo de dados da coluna não for numérico ou se for `VARNUMERIC`.<br /><br /> A precisão de colunas com o tipo de dados `DBTYPE_DECIMAL` ou `DBTYPE_NUMERIC` dependerá da definição da coluna.|  
|`NUMERIC_SCALE`|`DBTYPE_I2`||O número de dígitos à direita da vírgula decimal se o indicador do tipo da coluna for `DBTYPE_DECIMAL`, `DBTYPE_NUMERIC` ou `DBTYPE_VARNUMERIC`. Caso contrário, esta coluna conterá `VT_NULL`.|  
|`DATETIME_PRECISION`|`DBTYPE_UI4`||A precisão de data/hora (o número de dígitos na parte fracionária de segundos) da coluna se seu tipo de dados por DateTime ou do tipo intervalo; caso contrário, será `NULL`.|  
|`CHARACTER_SET_CATALOG`|`DBTYPE_WSTR`||O nome de catálogo no qual o conjunto de caracteres é definido. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá `NULL`.|  
|`CHARACTER_SET_SCHEMA`|`DBTYPE_WSTR`||Um nome de esquema não qualificado no qual o conjunto de caracteres é definido. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá `NULL`.|  
|`CHARACTER_SET_NAME`|`DBTYPE_WSTR`||Nome do conjunto de caracteres. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá `NULL`.|  
|`COLLATION_CATALOG`|`DBTYPE_WSTR`||O nome de catálogo no qual o agrupamento é definido. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá `NULL`.|  
|`COLLATION_SCHEMA`|`DBTYPE_WSTR`||Um nome do esquema não qualificado no qual o agrupamento é definido. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá `NULL`.|  
|`COLLATION_NAME`|`DBTYPE_WSTR`||O nome do agrupamento. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá `NULL`.|  
|`DOMAIN_CATALOG`|`DBTYPE_WSTR`||O nome de catálogo no qual o domínio é definido. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá `NULL`.|  
|`DOMAIN_SCHEMA`|`DBTYPE_WSTR`||O nome do esquema não qualificado no qual o domínio é definido. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá `NULL`.|  
|`DOMAIN_NAME`|`DBTYPE_WSTR`||O nome de domínio. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá `NULL`.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Uma descrição amigável da coluna. Essa coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá `NULL`.|  
|`DISTRIBUTION_FLAG`|`DBTYPE_WSTR`||Uma descrição da distribuição estatística da coluna. Esta coluna contém uma das opções a seguir:<br /><br /> -   "`NORMAL`"<br />-   "`LOG_NORMAL`"<br />-   "`UNIFORM`"|  
|`CONTENT_TYPE`|`DBTYPE_WSTR`||Uma descrição do conteúdo da coluna. Esta coluna contém uma das opções a seguir:<br /><br /> -   "`KEY`"<br />-   "`DISCRETE`"<br />-   "`CONTINUOUS`"<br />-"`DISCRETIZED(`[argumentos]`)`"<br />-   "`ORDERED`"<br />-   "`KEY TIME`"<br />-   "`CYCLICAL`"<br />-   "`PROBABILITY`"<br />-   "`VARIANCE`"<br />-   "`STDEV`"<br />-   "`SUPPORT`"<br />-   "`PROBABILITY_VARIANCE`"<br />-   "`PROBABILITY_STDEV`"<br />-   `"KEY SEQUENCE`"|  
|`MODELING_FLAG`|`DBTYPE_WSTR`||Uma lista de sinalizadores delimitada por vírgulas. Os sinalizadores definidos são:<br /><br /> -   "`MODEL_EXISTENCE_ONLY`"<br />-   "`REGRESSOR`"<br /><br /> Os sinalizadores de modelagem específicos do algoritmo também pode ser armazenados nesta coluna.|  
|`IS_RELATED_TO_KEY`|`DBTYPE_BOOL`||Um Booliano que indica se a coluna está relacionada à chave.<br /><br /> Será `TRUE` se esta coluna estiver relacionada à chave. Se a chave for uma única coluna, o campo `RELATED_ATTRIBUTE` opcionalmente poderá conter seu nome de coluna.|  
|`RELATED_ATTRIBUTE`|`DBTYPE_WSTR`||O nome da coluna de destino ao qual a coluna atual está relacionada ou é uma propriedade especial.|  
|`IS_INPUT`|`DBTYPE_BOOL`||Um Booliano que indica se a coluna é uma coluna de entrada.<br /><br /> Será `VARIANT_TRUE` se esta for uma coluna de entrada.|  
|`IS_PREDICTABLE`|`DBTYPE_BOOL`||Um Booliano que indica se a coluna é previsível.<br /><br /> Será `TRUE` se a coluna for previsível.|  
|`CONTAINING_COLUMN`|`DBTYPE_WSTR`||O nome da coluna de `TABLE` que contém esta coluna. Essa coluna conterá `NULL` se a coluna não estiver contida em outra.|  
|`PREDICTION_SCALAR_FUNCTIONS`|`DBTYPE_WSTR`||Uma lista delimitada por vírgulas de funções escalares que podem ser executadas na coluna.|  
|`PREDICTION_TABLE_FUNCTIONS`|`DBTYPE_WSTR`||Uma lista delimitada por vírgulas de funções que podem ser se aplicadas à coluna. As funções devem retornar uma tabela. A lista tem o seguinte formato:<br /><br /> `<function name>(<column1> [, <column2>], ...)`<br /><br /> O formato permite que o aplicativo cliente determine a assinatura (lista de parâmetros) para a função respectiva.|  
|`IS_POPULATED`|`DBTYPE_BOOL`||Um Booliano que indica se a coluna foi treinada com um conjunto de valores possíveis.<br /><br /> Será `TRUE` se a coluna foi treinada com um conjunto de valores possíveis.<br /><br /> Conterá `FALSE` se a coluna não estiver preenchida.|  
|`PREDICTION_SCORE`|`DBTYPE_R8`||A pontuação do modelo em relação à previsão da coluna. A pontuação é usada para medir a exatidão de um modelo.|  
|`SOURCE_COLUMN`|`DBTYPE_WSTR`||O nome da coluna de estrutura de mineração de origem para a coluna de mineração atual.|  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `DMSCHEMA_MINING_COLUMNS` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`|Opcional.|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`|Opcional.|  
|`MODEL_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`COLUMN_NAME`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema de mineração de dados](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
