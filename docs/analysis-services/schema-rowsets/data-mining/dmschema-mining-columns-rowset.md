---
title: Linhas de DMSCHEMA_MINING_COLUMNS | Microsoft Docs
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
- DMSCHEMA_MINING_COLUMNS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_COLUMNS rowset
ms.assetid: ae35ccde-4438-46f4-8611-40b2b1a42fce
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aa9ee7c66193eb84f883ba0500a8617421f2228e
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="dmschemaminingcolumns-rowset"></a>Conjunto de linhas de DMSCHEMA_MINING_COLUMNS
  Descreve as colunas individuais de todos os modelos de mineração de dados no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Este conjunto de linhas é restrito ao catálogo atual.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O **DMSCHEMA_MINING_COLUMNS** linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Description|  
|-----------------|--------------------|-----------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|O nome do catálogo. Preenchido com o nome do banco de dados do qual o modelo é membro.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|O nome do esquema não qualificado. Esta coluna não é suportada pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá **nulo**.|  
|**NOME_DO_MODELO**|**DBTYPE_WSTR**|O nome do modelo de mineração. Esta coluna contém o nome do modelo de mineração ao qual uma coluna é associada, e nunca estará vazia.|  
|**NOME DA COLUNA**|**DBTYPE_WSTR**|O nome da coluna.|  
|**COLUMN_GUID**|**DBTYPE_GUID**|O GUID da coluna. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá **nulo**.|  
|**COLUMN_PROPID**|**DBTYPE_UI4**|A ID de propriedade da coluna. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá **nulo**.|  
|**ORDINAL_POSITION**|**DBTYPE_UI4**|A posição ordinal da coluna. As colunas são numeradas a partir de 1. Esta coluna contém **nulo** se não houver nenhum valor ordinal estável para a coluna.|  
|**COLUMN_HAS_DEFAULT**|**DBTYPE_BOOL**|Um Booliano que indica se a coluna tem um valor padrão.<br /><br /> **TRUE** se a coluna tiver um valor padrão, caso contrário, **FALSE**.|  
|**COLUMN_DEFAULT**|**DBTYPE_WSTR**|O valor padrão da coluna.<br /><br /> Se o valor padrão é o **nulo** valor, **COLUMN_HASDEFAULT** contém **TRUE**, e essa coluna contém **nulo**.|  
|**COLUMN_FLAGS**|**DBTYPE_UI4**|Uma máscara de bits que descreve as características da coluna. O **DBCOLUMNFLAGS** tipo enumerado Especifica os bits da máscara de bits. Esta coluna nunca está vazia.|  
|**IS_NULLABLE**|**DBTYPE_BOOL**|Um Booliano que indica se a coluna pode conter valores nulos.<br /><br /> **FALSE** se a coluna é conhecida por não ser anulável; caso contrário, **TRUE**.|  
|**DATA_TYPE**|**DBTYPE_UI2**|O indicador do tipo de dados da coluna. A lista a seguir mostra exemplos dos tipos de indicadores retornados:<br /><br /> "**Tabela**" retornaria **DBTYPE_HCHAPTER**.<br /><br /> "**Texto**" retornaria **DBTYPE_WCHAR**.<br /><br /> "**Longo**" retornaria **DBTYPE_I8**.<br /><br /> "**Duplo**" retornaria **DBTYPE_R8**.<br /><br /> "**Data**" retornaria **DBTYPE_DATE**.|  
|**TYPE_GUID**|**DBTYPE_GUID**|O GUID do tipo de dados da coluna. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá **VT_NULL**.|  
|**CHARACTER_MAXIMUM_LENGTH**|**DBTYPE_UI4**|O comprimento máximo possível de um valor na coluna. Para colunas de caracteres, de binários ou de bits, será uma das opções a seguir:<br /><br /> O comprimento máximo da coluna em caracteres, em bytes ou em bits, respectivo ao tipo de coluna, se um comprimento for definido. Por exemplo, um **char (5)** coluna em uma tabela SQL tem um comprimento máximo de 5.<br /><br /> O comprimento máximo do tipo de dados em caracteres, em bytes ou em bits, respectivo ao tipo de coluna, se a coluna não tiver um comprimento definido.<br /><br /> Zero (0), se a coluna ou o tipo de dados tiver um comprimento máximo definido.<br /><br /> **NULO** para todos os outros tipos de colunas|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**|O comprimento máximo em octetos (bytes) da coluna, se o tipo da coluna for caractere ou binário. Um valor zero (0) significa que a coluna não tem um comprimento máximo. Esta coluna contém **nulo** para todos os outros tipos de colunas.|  
|**NUMERIC_PRECISION**|**DBTYPE_UI2**|A precisão máxima da coluna se o tipo de dados da coluna for um tipo de dados numérico diferente de **VARNUMERIC**.<br /><br /> **NULO** se o tipo de dados da coluna não for numérico ou é **VARNUMERIC**.<br /><br /> A precisão de colunas com um tipo de dados de **DBTYPE_DECIMAL** ou **DBTYPE_NUMERIC** dependerá da definição de coluna.|  
|**NUMERIC_SCALE**|**DBTYPE_I2**|O número de dígitos à direita da vírgula decimal se o indicador de tipo da coluna é **DBTYPE_DECIMAL**, **DBTYPE_NUMERIC**, ou **DBTYPE_VARNUMERIC**. Caso contrário, esta coluna contém **VT_NULL**.|  
|**DATETIME_PRECISION**|**DBTYPE_UI4**|A precisão de data/hora (número de dígitos na parte fracionária de segundos) da coluna se o tipo de dados da coluna for um tipo DateTime ou intervalo; Caso contrário, **nulo**.|  
|**CHARACTER_SET_CATALOG**|**DBTYPE_WSTR**|O nome de catálogo no qual o conjunto de caracteres é definido. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá **nulo**.|  
|**CHARACTER_SET_SCHEMA**|**DBTYPE_WSTR**|Um nome de esquema não qualificado no qual o conjunto de caracteres é definido. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá **nulo**.|  
|**CHARACTER_SET_NAME**|**DBTYPE_WSTR**|Nome do conjunto de caracteres. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá **nulo**.|  
|**COLLATION_CATALOG**|**DBTYPE_WSTR**|O nome de catálogo no qual o agrupamento é definido. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá **nulo**.|  
|**COLLATION_SCHEMA**|**DBTYPE_WSTR**|Um nome do esquema não qualificado no qual o agrupamento é definido. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá **nulo**.|  
|**COLLATION_NAME**|**DBTYPE_WSTR**|O nome do agrupamento. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá **nulo**.|  
|**DOMAIN_CATALOG**|**DBTYPE_WSTR**|O nome de catálogo no qual o domínio é definido. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá **nulo**.|  
|**DOMAIN_SCHEMA**|**DBTYPE_WSTR**|O nome do esquema não qualificado no qual o domínio é definido. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá **nulo**.|  
|**NOME_DO_DOMÍNIO**|**DBTYPE_WSTR**|O nome de domínio. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá **nulo**.|  
|**DESCRIPTION**|**DBTYPE_WSTR**|Uma descrição amigável da coluna esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá **nulo**.|  
|**DISTRIBUTION_FLAG**|**DBTYPE_WSTR**|Uma descrição da distribuição estatística da coluna. Esta coluna contém uma das opções a seguir:<br /><br /> "**NORMAL**"<br /><br /> "**LOG_NORMAL**"<br /><br /> "**UNIFORM**"|  
|**TIPO_DE_CONTEÚDO**|**DBTYPE_WSTR**|Uma descrição do conteúdo da coluna. Esta coluna contém uma das opções a seguir:<br /><br /> "**CHAVE**"<br /><br /> "**DISCRETO**"<br /><br /> "**CONTÍNUO**"<br /><br /> "**DISCRETIZED (**[argumentos]**)**"<br /><br /> "**ORDERED**"<br /><br /> "**KEY TIME**"<br /><br /> "**CÍCLICO**"<br /><br /> "**PROBABILIDADE**"<br /><br /> "**VARIAÇÃO**"<br /><br /> "**STDEV**"<br /><br /> "**SUPORTE**"<br /><br /> "**PROBABILITY_VARIANCE**"<br /><br /> "**PROBABILITY_STDEV**"<br /><br /> **"SEQUÊNCIA DE TECLAS**"|  
|**MODELING_FLAG**|**DBTYPE_WSTR**|Uma lista de sinalizadores delimitada por vírgulas. Os sinalizadores definidos são:<br /><br /> "**MODEL_EXISTENCE_ONLY**"<br /><br /> "**REGRESSOR**"<br /><br /> Os sinalizadores de modelagem específicos do algoritmo também pode ser armazenados nesta coluna.|  
|**IS_RELATED_TO_KEY**|**DBTYPE_BOOL**|Um Booliano que indica se a coluna está relacionada à chave.<br /><br /> **TRUE** se esta coluna está relacionada à chave. Se a chave for uma única coluna, o **RELATED_ATTRIBUTE** campo pode conter, opcionalmente, o nome da coluna.|  
|**RELATED_ATTRIBUTE**|**DBTYPE_WSTR**|O nome da coluna de destino para o qual a coluna atual está relacionado tanto é uma propriedade especial.|  
|**IS_INPUT**|**DBTYPE_BOOL**|Um Booliano que indica se a coluna é uma coluna de entrada.<br /><br /> **VARIANT_TRUE** quando se trata de uma coluna de entrada.|  
|**IS_PREDICTABLE**|**DBTYPE_BOOL**|Um Booliano que indica se a coluna é previsível.<br /><br /> **TRUE** se a coluna é previsível.|  
|**CONTAINING_COLUMN**|**DBTYPE_WSTR**|O nome do **tabela** coluna que contém essa coluna. Esta coluna contém **nulo** se a coluna não estiver contida em outra coluna.|  
|**PREDICTION_SCALAR_FUNCTIONS**|**DBTYPE_WSTR**|Uma lista delimitada por vírgulas de funções escalares que podem ser executadas na coluna.|  
|**PREDICTION_TABLE_FUNCTIONS**|**DBTYPE_WSTR**|Uma lista delimitada por vírgulas de funções que podem ser se aplicadas à coluna. As funções devem retornar uma tabela. A lista tem o seguinte formato:<br /><br /> `<function name>(<column1> [, <column2>], ...)`<br /><br /> O formato permite que o aplicativo cliente determine a assinatura (lista de parâmetros) para a função respectiva.|  
|**IS_POPULATED**|**DBTYPE_BOOL**|Um Booliano que indica se a coluna foi treinada com um conjunto de valores possíveis.<br /><br /> **TRUE** se a coluna foi treinada com um conjunto de valores possíveis.<br /><br /> Contém **FALSE** se a coluna não é preenchida.|  
|**PREDICTION_SCORE**|**DBTYPE_R8**|A pontuação do modelo em relação à previsão da coluna. A pontuação é usada para medir a exatidão de um modelo.|  
|**SOURCE_COLUMN**|**DBTYPE_WSTR**|O nome da coluna de estrutura de mineração de origem para a coluna de mineração atual.|  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O **DMSCHEMA_MINING_COLUMNS** linhas pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|Opcional.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|Opcional.|  
|**NOME_DO_MODELO**|**DBTYPE_WSTR**|Opcional.|  
|**NOME DA COLUNA**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [Linhas do esquema de mineração de dados](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  

