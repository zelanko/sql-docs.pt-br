---
title: Conjunto de linhas DMSCHEMA_MINING_STRUCTURE_COLUMNS | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DMSCHEMA_MINING_STRUCTURE_COLUMNS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_STRUCTURE_COLUMNS rowset
ms.assetid: 81f25502-ac90-42f1-8ddf-7b0f9752ebfd
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ff811a339635f5ff914224a060e14a52e3f94d6c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="dmschemaminingstructurecolumns-rowset"></a>Conjunto de linhas DMSCHEMA_MINING_STRUCTURE_COLUMNS
  Descreve as colunas individuais de todas as estruturas de mineração implantadas em um servidor que esteja executando [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O **DMSCHEMA_MINING_STRUCTURE_COLUMNS** linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**STRUCTURE_CATALOG**|**DBTYPE_WSTR**||O nome do catálogo.|  
|**STRUCTURE_SCHEMA**|**DBTYPE_WSTR**||O nome do esquema não qualificado. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]não oferece suporte a esquemas, portanto, esta coluna é sempre **nulo**.|  
|**STRUCTURE_NAME**|**DBTYPE_WSTR**||O nome da estrutura. Esta coluna não pode conter um **nulo**.|  
|**NOME DA COLUNA**|**DBTYPE_WSTR**||O nome da coluna. A exclusividade só é garantida entre colunas que compartilham o mesmo padrão. Por exemplo, duas colunas aninhadas poderão ter o mesmo nome se pertencerem a duas tabelas aninhadas diferentes dentro da mesma estrutura.|  
|**COLUMN_GUID**|**DBTYPE_GUID**||O GUID da coluna. Os provedores que não usam GUIDs para identificar colunas devem retornar **nulo** nesta coluna.|  
|**COLUMN_PROPID**|**DBTYPE_UI4**||A ID de propriedade da coluna. Os provedores que não associam IDs de propriedade a colunas devem retornar **nulo** nesta coluna. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] retorna **nulo** para esta coluna.|  
|**ORDINAL_POSITION**|**DBTYPE_UI4**||O ordinal da coluna. As colunas são numeradas a partir de 1. **NULO** se não houver nenhum valor ordinal estável para a coluna.|  
|**COLUMN_HASDEFAULT**|**DBTYPE_BOOL**||Um booliano que indica se esta coluna tem um valor padrão.<br /><br /> **TRUE** se a coluna tiver um valor padrão.<br /><br /> **FALSE** se a coluna não tem um valor padrão ou se não for possível determinar se a coluna tem um valor padrão.|  
|**COLUMN_DEFAULT**|**DBTYPE_WSTR**||O valor padrão da coluna. Um provedor pode expor **DBCOLUMN_DEFAULTVALUE** mas não **DBCOLUMN_HASDEFAULT** (para tabelas ISO) no conjunto de linhas retornado por **Getcolumnsrowset**.<br /><br /> Se o valor padrão é **nulo**, **COLUMN_HASDEFAULT** é **TRUE** e **COLUMN_DEFAULT** coluna é um **NULL** valor.|  
|**COLUMN_FLAGS**|**DBTYPE_UI4**||Uma máscara de bits que descreve características da coluna. O **DBCOLUMNFLAGS** tipo enumerado Especifica os bits da máscara de bits. Esta coluna não pode conter um **nulo** valor. Os valores válidos incluem:<br /><br /> **DBCOLUMNFLAGS_ISNULLABLE** (**0x20**)<br /><br /> **DBCOLUMNFLAGS_MAYBENULL** (**0x40**)<br /><br /> **DBCOLUMNFLAGS_ISLONG** (**0x80**)|  
|**IS_NULLABLE**|**DBTYPE_BOOL**||Um booliano que indica se esta coluna tem um valor padrão.<br /><br /> **TRUE** se a coluna pode conter **nulo**; **FALSE**, caso contrário.|  
|**DATA_TYPE**|**DBTYPE_UI2**||O indicador do tipo de dados da coluna. Por exemplo:<br /><br /> "**TABELA**" = **DBTYPE_HCHAPTER**<br /><br /> "**TEXTO**" = **DBTYPE_WCHAR**<br /><br /> "**LONGO**" = **DBTYPE_I8**<br /><br /> "**DUPLO**" = **DBTYPE_R8**<br /><br /> "**DATA**" = **DBTYPE_DATE**|  
|**TYPE_GUID**|**DBTYPE_GUID**||O GUID do tipo de dados da coluna. Os provedores que não usam GUIDs para identificar os tipos de dados devem retornar **nulo** nesta coluna.|  
|**CHARACTER_MAXIMUM_LENGTH**|**DBTYPE_UI4**||O comprimento máximo possível de um valor na coluna. Para colunas de caracteres, de binários ou de bits, será uma das opções a seguir:<br /><br /> O comprimento máximo da coluna em caracteres, em bytes ou em bits, respectivamente, se o comprimento for definido. Por exemplo, uma coluna `CHAR(5)` de uma tabela SQL terá o comprimento máximo de 5.<br /><br /> O comprimento máximo do tipo de dados em caracteres, em bytes ou em bits, respectivamente, se a coluna não tiver um comprimento definido.<br /><br /> Zero (0), se a coluna ou o tipo de dados tiver um comprimento máximo definido.<br /><br /> **NULO** para todos os outros tipos de colunas.|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**||O comprimento máximo em octetos (bytes) da coluna, se o tipo da coluna for caractere ou binário. Um valor zero (0) significa que a coluna não tem um comprimento máximo. **NULO** para todos os outros tipos de colunas.|  
|**NUMERIC_PRECISION**|**DBTYPE_UI2**||A precisão máxima da coluna se o tipo de dados da coluna for um tipo de dados numérico diferente de **VARNUMERIC**; **Nulo** se o tipo de dados da coluna não for numérico ou é **VARNUMERIC**.<br /><br /> A precisão de colunas com um tipo de dados de **DBTYPE_DECIMAL** ou **DBTYPE_NUM**ERIC dependerá da definição da coluna.|  
|**NUMERIC_SCALE**|**DBTYPE_I2**||O número de dígitos à direita da vírgula decimal se o indicador de tipo da coluna é **DBTYPE_DECIMAL**, **DBTYPE_NUMERIC**, ou **DBTYPE_VARNUMERIC**. Caso contrário, isso será **nulo**.|  
|**DATETIME_PRECISION**|**DBTYPE_UI4**||A precisão de DateTime (o número de dígitos na parte fracionária de segundos) da coluna se ela for do tipo datetime ou intervalo. Se o tipo de dados da coluna não for datetime, isso será **nulo**.|  
|**CHARACTER_SET_CATALOG**|**DBTYPE_WSTR**||O nome de catálogo no qual o conjunto de caracteres é definido. **NULO** se o provedor não oferece suporte a catálogos ou conjuntos de caracteres diferentes.|  
|**CHARACTER_SET_SCHEMA**|**DBTYPE_WSTR**||O nome de esquema não qualificado no qual o conjunto de caracteres é definido. **NULO** se o provedor não oferece suporte a esquemas ou conjuntos de caracteres diferentes.|  
|**CHARACTER_SET_NAME**|**DBTYPE_WSTR**||Nome do conjunto de caracteres. **NULO** se o provedor não oferece suporte a diferentes conjuntos de caracteres.|  
|**COLLATION_CATALOG**|**DBTYPE_WSTR**||O nome de catálogo no qual o agrupamento é definido. **NULO** se o provedor não oferece suporte a catálogos ou agrupamentos diferentes.|  
|**COLLATION_SCHEMA**|**DBTYPE_WSTR**||O nome do esquema não qualificado no qual o agrupamento é definido. **NULO** se o provedor não oferece suporte a esquemas ou agrupamentos diferentes.|  
|**COLLATION_NAME**|**DBTYPE_WSTR**||O nome do agrupamento. **NULO** se o provedor não oferece suporte a agrupamentos diferentes.|  
|**DOMAIN_CATALOG**|**DBTYPE_WSTR**||O nome de catálogo no qual o domínio é definido. **NULO** se o provedor não oferece suporte a catálogos ou domínios.|  
|**DOMAIN_SCHEMA**|**DBTYPE_WSTR**||O nome do esquema não qualificado no qual o domínio é definido. **NULO** se o provedor não oferece suporte a esquemas ou domínios.|  
|**NOME_DO_DOMÍNIO**|**DBTYPE_WSTR**||O nome de domínio. **NULO** se o provedor não oferece suporte a domínios.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Uma descrição legível da coluna. **NULO** se não há nenhuma descrição associada à coluna.|  
|**DISTRIBUTION_FLAG**|**DBTYPE_WSTR**||A distribuição da coluna de estrutura de mineração:<br /><br /> "**NORMAL**"<br /><br /> "**LOG_NORM**AL"<br /><br /> "**UNIFORM**"|  
|**TIPO_DE_CONTEÚDO**|**DBTYPE_WSTR**||O tipo de conteúdo da coluna de estrutura de mineração:<br /><br /> "**CHAVE**"<br /><br /> "**DISCRETO**"<br /><br /> "**CONTÍNUO**"<br /><br /> "**DISCRETIZED (**[args]**)**"<br /><br /> "**ORDERED**"<br /><br /> "**SEQUENCE_TIME**"<br /><br /> "**CÍCLICO**"<br /><br /> "**PROBABILIDADE**"<br /><br /> "**VARIAÇÃO**"<br /><br /> "**STDEV**"<br /><br /> "**SUPORTE**"<br /><br /> "**PROBABILITY_VARIANCE**"<br /><br /> "**PROBABILITY_STDEV**"|  
|**MODELING_FLAG**|**DBTYPE_WSTR**||Uma lista delimitada por vírgulas de sinalizadores de modelagem. O único sinalizador suportado para uma coluna de estrutura é "**não NULL**".|  
|**IS_RELATED_TO_KEY**|**DBTYPE_BOOL**||Um booliano que indica se esta coluna está relacionada à chave.<br /><br /> **VARIANT_TRUE** se esta coluna está relacionada à chave; **VARIANT_FALSE** caso contrário. Se a chave for uma única coluna, o **RELATED_ATTRIBUTE** campo opcionalmente pode conter seu nome de coluna.|  
|**RELATED_ATTRIBUTE**|**DBTYPE_WSTR**||O nome da coluna de destino à qual a coluna atual está relacionada ou de quem é uma propriedade especial.|  
|**CONTAINING_COLUMN**|**DBTYPE_WSTR**||O nome do **tabela** coluna que contém esta coluna. **NULO** se nenhuma tabela contiver a coluna.|  
|**IS_POPULATED**|**DBTYPE_BOOL**||Um booliano que indica se esta coluna aprendeu um conjunto de valores possíveis.<br /><br /> **TRUE** se a coluna aprendeu um conjunto de valores possíveis; **FALSE**, caso contrário.|  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O **DMSCHEMA_MINING_STRUCTURE_COLUMNS** linhas pode ser restringido nas colunas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**STRUCTURE_CATALOG**|**DBTYPE_WSTR**|Opcional.|  
|**STRUCTURE_SCHEMA**|**DBTYPE_WSTR**|Opcional.|  
|**STRUCTURE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**NOME DA COLUNA**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [Linhas do esquema de mineração de dados](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  

