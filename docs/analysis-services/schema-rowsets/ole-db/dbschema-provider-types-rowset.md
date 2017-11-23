---
title: Conjunto de linhas DBSCHEMA_PROVIDER_TYPES | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DBSCHEMA_PROVIDER_TYPES
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DBSCHEMA_PROVIDER_TYPES rowset
ms.assetid: 255e01ba-53a9-478d-9b86-45faba76710e
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3de186cec4b3299bbdc43cf2fe63c806c228cb66
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="dbschemaprovidertypes-rowset"></a>Conjunto de linhas DBSCHEMA_PROVIDER_TYPES
  Identifica os tipos de dados (base) suportados pelo provedor de dados.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DBSCHEMA_PROVIDER_TYPES** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Description|  
|-----------------|--------------------|-----------------|  
|**TYPE_NAME**|**DBTYPE_WSTR**|O nome de tipo de dados específico do provedor.|  
|**DATA_TYPE**|**DBTYPE_UI2**|O indicador do tipo de dados.|  
|**COLUMN_SIZE**|**DBTYPE_UI4**|O comprimento de uma coluna não numérica ou parâmetro que se refere ao máximo ou ao comprimento definido para esse tipo pelo provedor. Para dados de caracteres, esse é o máximo ou o comprimento definido em caracteres. Para tipos de dados DateTime, esse é o comprimento da representação de cadeia de caracteres (supondo que o máximo permitiu a precisão do componente em frações de segundo).<br /><br /> Se o tipo de dados for numérico, esse será o limite superior na precisão máxima do tipo de dados.|  
|**LITERAL_PREFIX**|**DBTYPE_WSTR**|O caractere ou caracteres usados para prefixar um literal deste tipo em um comando de texto.|  
|**LITERAL_SUFFIX**|**DBTYPE_WSTR**|O caractere ou caracteres usados para sufixar um literal deste tipo em um comando de texto.|  
|**CREATE_PARAMS**|**DBTYPE_WSTR**|Os parâmetros de criação especificados pelo consumidor ao criar uma coluna deste tipo de dados. Por exemplo, o tipo de dados de SQL, **DECIMAL,** requer uma precisão e uma escala. Nesse caso, os parâmetros de criação devem ser a cadeia de caracteres "precisão, escala". Em um comando de texto, para criar uma coluna **DECIMAL** com uma precisão de 10 e uma escala de 2, o valor da coluna **TYPE_NAME** seria **DECIMAL()** e a especificação de tipo completa seria **DECIMAL(10,2)**.<br /><br /> Os parâmetros de criação aparecem como uma lista de valores separados por vírgulas, na ordem em que eles serão fornecidos e sem parênteses. Se um parâmetro de criação for comprimento, comprimento máximo, precisão, escala, semente ou incremento, use "comprimento", "comprimento máximo", "precisão", "escala", "semente" e "incremento", respectivamente. Se o parâmetro de criação for algum outro valor, o provedor determinará que texto será usado para descrever o parâmetro de criação.<br /><br /> Quando o tipo de dados requer parâmetros de criação, "()" costuma aparecer no nome de tipo. Isso indica a posição na qual os parâmetros de criação devem ser inseridos. Quando o nome de tipo não inclui "()", os parâmetros de criação estar entre parênteses e anexados ao nome de tipo de dados.|  
|**IS_NULLABLE**|**DBTYPE_BOOL**|Um Booliano que indica se o tipo de dados permite valores nulos.<br /><br /> **VARIANT_TRUE** indica que o tipo de dados permite valores nulos.<br /><br /> **VARIANT_FALSE** indica que o tipo de dados não permite valores nulos.<br /><br /> **NULL**indica que é desconhecido se o tipo de dados permite valores nulos.|  
|**CASE_SENSITIVE**|**DBTYPE_BOOL**|Um Booliano que indica se o tipo de dados é um tipo de caracteres e se diferencia maiúsculas de minúsculas.<br /><br /> **VARIANT_TRUE** indica que o tipo de dados é um tipo de caracteres e que diferencia maiúsculas de minúsculas.<br /><br /> **VARIANT_FALSE** indica que o tipo de dados não é um tipo de caracteres ou que não diferencia maiúsculas de minúsculas.|  
|**PESQUISÁVEL**|**DBTYPE_UI4**|Um inteiro que indica como o tipo de dados poderá ser usado em pesquisas se o provedor der suporte ao **ICommandText**; caso contrário, **NULL**. Esta coluna pode ter os seguintes valores:<br /><br /> **DB_UNSEARCHABLE** indica que o tipo de dados não pode ser usado em uma cláusula **WHERE** .<br /><br /> **DB_LIKE_ONLY** indica que o tipo de dados só pode ser usado em uma cláusula **WHERE** com o predicado **LIKE** .<br /><br /> **DB_ALL_EXCEPT_LIKE** indica que o tipo de dados pode ser usado em uma cláusula **WHERE** com todos os operadores de comparação, com exceção de **LIKE**.<br /><br /> **DB_SEARCHABLE** indica que o tipo de dados pode ser usado em uma cláusula **WHERE** com qualquer operador de comparação.|  
|**UNSIGNED_ATTRIBUTE**|**DBTYPE_BOOL**|Um Booliano que indica se o tipo de dados é não assinado.<br /><br /> **VARIANT_TRUE** indica que o tipo de dados é não assinado.<br /><br /> **VARIANT_FALSE** indica que o tipo de dados é assinado.<br /><br /> **NULL** indica que isso não é aplicável ao tipo de dados.|  
|**FIXED_PREC_SCALE**|**DBTYPE_BOOL**|Um Booliano que indica se o tipo de dados tem uma precisão e uma escala fixas.<br /><br /> **VARIANT_TRUE** indica que o tipo de dados tem uma precisão e uma escala fixas.<br /><br /> **VARIANT_FALSE** indica que o tipo de dados não tem uma precisão e uma escala fixas.|  
|**AUTO_UNIQUE_VALUE**|**DBTYPE_BOOL**|Um Booliano que indica se o tipo de dados é incrementado automaticamente.<br /><br /> **VARIANT_TRUE** indica que valores deste tipo podem ser incrementados automaticamente.<br /><br /> **VARIANT_FALSE** indica que valores deste tipo não podem ser incrementados automaticamente.<br /><br /> Se esse valor for **VARIANT_TRUE**, para determinar se uma coluna desse tipo sempre será incrementada automaticamente, verifique a propriedade da coluna **DBPROP_COL_AUTOINCREMENT** do provedor. Se a propriedade de **DBPROP_COL_AUTOINCREMENT** for de leitura/gravação, para determinar se uma coluna desse tipo será incrementada automaticamente, verifique a configuração da propriedade de **DBPROP_COL_AUTOINCREMENT** . Se **DBPROP_COL_AUTOINCREMENT** for uma propriedade somente leitura, todas as colunas ou nenhuma coluna desse tipo será incrementada automaticamente.|  
|**LOCAL_TYPE_NAME**|**DBTYPE_WSTR**|A versão localizada do **TYPE_NAME**. **NULL** será retornado se o provedor de dados não oferecer suporte a um nome localizado.|  
|**MINIMUM_SCALE**|**DBTYPE_I2**|Se o indicador de tipo for **DBTYPE_VARNUMERIC**, **DBTYPE_DECIMAL**ou **DBTYPE_NUMERIC**, o número mínimo de dígitos permitidos à direita do separador decimal. Caso contrário, **NULL**.|  
|**MAXIMUM_SCALE**|**DBTYPE_I2**|O número máximo de dígitos permitidos à direita do separador decimal quando o indicador de tipo é **DBTYPE_VARNUMERIC**, **DBTYPE_DECIMAL**ou **DBTYPE_NUMERIC**; caso contrário, N**U**LL.|  
|**GUID**|**DBTYPE_GUID**|(Para uso futuro) O **GUID** do tipo, se o tipo for descrito em uma biblioteca de tipos. Caso contrário, **NULL**.|  
|**TYPELIB**|**DBTYPE_WSTR**|(Para uso futuro) A biblioteca de tipos que contém a descrição do tipo, se o tipo for descrito em uma biblioteca de tipos. Caso contrário, NULL.|  
|**VERSION**|**DBTYPE_WSTR**|(Para uso futuro) A versão da definição de tipo. Talvez os provedores queiram obter definições de tipo de versão. Provedores diferentes podem usar esquemas de controle de versão diferentes, tais como um carimbo de data/hora ou número (inteiro ou float). **NULL** se não tiver suporte.|  
|**IS_LONG**|**DBTYPE_BOOL**|Um Booliano que indica se o tipo de dados é um objeto binário grande (BLOB) e se tem dados muito longos.<br /><br /> **VARIANT_TRUE** indica que o tipo de dados é um **BLOB** que contém dados muito longos; a definição de dados muito longos é específica do provedor.<br /><br /> **VARIANT_FALSE** indica que o tipo de dados é um **BLOB** que não contém dados muito longos ou não é um **BLOB**.<br /><br /> Este valor determina a configuração do sinalizador **DBCOLUMNFLAGS_ISLONG** retornada por **GetColumnInfo** em **IColumnsInfo** e **GetParameterInfo** em **ICommandWithParameters**.|  
|**BEST_MATCH**|**DBTYPE_BOOL**|Um Booliano que indica se o tipo de dados é a melhor correspondência.<br /><br /> **VARIANT_TRUE** indica que o tipo de dados é a melhor correspondência entre todos os tipos de dados do repositório de dados e o tipo de dados OLE DB indicado pelo valor na coluna **DATA_TYPE** .<br /><br /> **VARIANT_FALSE** indica que o tipo de dados não é a melhor correspondência.<br /><br /> Para cada conjunto de linhas no qual o valor da coluna **DATA_TYPE** for idêntico, a coluna **BEST_MATCH** será definida como **VARIANT_TRUE** em apenas uma linha.|  
|**IS_FIXEDLENGTH**|**DBTYPE_BOOL**|Um Booliano que indica se a coluna tem um comprimento fixo.<br /><br /> **VARIANT_TRUE** indica que colunas deste tipo criadas pela linguagem de definição de dados (DDL) terão um comprimento fixo.<br /><br /> **VARIANT_FALSE** indica que colunas deste tipo, criadas pela DDL, terão comprimento variável.<br /><br /> Se o campo for **NULL**, será desconhecido se o provedor mapeará esse campo com uma coluna de comprimento fixo ou variável.|  
  
 O conjunto de linhas é classificado em **DATA_TYPE**.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas **DBSCHEMA_PROVIDER_TYPES** pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|  
|-----------------|--------------------|  
|**DATA_TYPE**|**DBTYPE_UI2**|  
|**BEST_MATCH**|**DBTYPE_BOOL**|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas do esquema OLE DB](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  
