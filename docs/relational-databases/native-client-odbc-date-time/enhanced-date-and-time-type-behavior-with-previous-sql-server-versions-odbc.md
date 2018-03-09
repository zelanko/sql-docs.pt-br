---
title: "Comportamento com versões anteriores do SQL Server (ODBC) de tipo de aprimorados de data e hora | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-date-time
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: date/time [ODBC], enhanced behavior with earlier SQL Server versions
ms.assetid: cd4e137f-dc5e-4df7-bc95-51fe18c587e0
caps.latest.revision: "21"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f2acc8c52d6e16cf17c05cc421faf5ea52b20e71
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="enhanced-date-and-time-type-behavior-with-previous-sql-server-versions-odbc"></a>Comportamento de tipos de data e hora aprimorados com versões anteriores do SQL Server (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Este tópico descreve o comportamento esperado quando um aplicativo cliente que usa recursos aprimorados de data e hora se comunica com uma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anterior ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e quando um aplicativo cliente que usa o Microsoft Data Access Components, o Windows Data Access Components ou uma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client anterior ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] envia comandos para um servidor que oferece suporte a recursos aprimorados de data e hora.  
  
## <a name="down-level-client-behavior"></a>Comportamento do cliente de versão anterior  
 Os aplicativos cliente que foram compilados usando uma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client anterior ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] vêm os novos tipos de data/hora como colunas nvarchar. O conteúdo da coluna é representações literais, conforme descrito na seção "Formatos de dados: cadeias e literais" de [suporte de tipo de dados para aprimoramentos de hora e data de ODBC](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md). O tamanho da coluna é o comprimento de literal máximo para a precisão de segundos fracionários especificada da coluna.  
  
 As APIs de catálogo retornarão metadados consistentes com o código de tipo de dados de versão anterior retornado ao cliente (por exemplo, nvarchar) e a representação de versão anterior associada (por exemplo, o formato de literal apropriado). Entretanto, o nome do tipo de dados retornado será o nome de tipo [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] real.  
  
 Metadados de instrução retornados por SQLDescribeCol, SQLDescribeParam, SQGetDescField e SQLColAttribute retornarão metadados consistentes com o tipo de nível inferior em todos os aspectos, incluindo o nome do tipo. Um exemplo desse tipo de nível inferior é **nvarchar**.  
  
 Quando um aplicativo cliente de nível inferior é executada em relação a um [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (ou posterior) no qual as alterações de esquema de data/hora foram feitas tipos de servidor, o comportamento esperado é o seguinte:  
  
|Tipo SQL Server 2005|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)](ou posterior) Tipo de|Tipo de cliente ODBC|Conversão do resultado (de SQL para C)|Conversão do parâmetro (de C para SQL)|  
|--------------------------|----------------------------------------------|----------------------|------------------------------------|---------------------------------------|  
|Datetime|Data|SQL_C_TYPE_DATE|OK|OK (1)|  
|||SQL_C_TYPE_TIMESTAMP|Campos de hora definidos como zero.|OK (2)<br /><br /> Falha se o campo de hora for diferente de zero. Funciona com o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||Time(0)|SQL_C_TYPE_TIME|OK|OK (1)|  
|||SQL_C_TYPE_TIMESTAMP|Campos de data definidos como a data atual.|OK (2)<br /><br /> Data ignorada. Falhará se os segundos fracionários forem diferentes de zero. Funciona com o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||Time(7)|SQL_C_TIME|Falha – literal de hora inválido.|OK (1)|  
|||SQL_C_TYPE_TIMESTAMP|Falha – literal de hora inválido.|OK (1)|  
||Datetime2(3)|SQL_C_TYPE_TIMESTAMP|OK|OK (1)|  
||Datetime2 (7)|SQL_C_TYPE_TIMESTAMP|OK|Valor será arredondado para 1/300º segundo por conversão de cliente.|  
|Smalldatetime|Data|SQL_C_TYPE_DATE|OK|OK|  
|||SQL_C_TYPE_TIMESTAMP|Campos de hora definidos como zero.|OK (2)<br /><br /> Falha se o campo de hora for diferente de zero. Funciona com o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||Time(0)|SQL_C_TYPE_TIME|OK|OK|  
|||SQL_C_TYPE_TIMESTAMP|Campos de data definidos como a data atual.|OK (2)<br /><br /> Data ignorada. Falha se os segundos fracionários forem diferentes de zero.<br /><br /> Funciona com o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||Datetime2(0)|SQL_C_TYPE_TIMESTAMP|OK|OK|  
  
## <a name="key-to-symbols"></a>Legenda dos símbolos  
  
|Símbolo|Significado|  
|------------|-------------|  
|1|Se funcionar com o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], deverá continuar a funcionar com uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|2|Um aplicativo que funcionava com o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] poderia falhar com uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
 Observe que só foram consideradas alterações de esquema comuns. A seguir estão as alterações comuns:  
  
-   Usar um novo tipo em que logicamente um aplicativo exige somente um valor de data ou hora. Entretanto, o aplicativo foi obrigado a usar datetime ou smalldatetime devido à falta de tipos de data e hora separados.  
  
-   Usar um novo tipo para obter precisão ou exatidão adicional de frações de segundos.  
  
-   Trocar para datetime2 porque esse é o tipo de dados de data e hora preferido.  
  
### <a name="column-metadata-returned-by-sqlcolumns-sqlprocedurecolumns-and-sqlspecialcolumns"></a>Metadados de coluna retornados por SQLColumns, SQLProcedureColumns e SQLSpecialColumns  
 Os valores de coluna a seguir são retornados para tipos de data/hora:  
  
|Tipo de coluna|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|-----------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_WVARCHAR|SQL_WVARCHAR|  
|TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|COLUMN_SIZE|10|8,10..16|16|23|19, 21..27|26, 28..34|  
|BUFFER_LENGTH|20|16, 20..32|16|16|38, 42..54|52, 56..68|  
|DECIMAL_DIGITS|NULL|NULL|0|3|NULL|NULL|  
|SQL_DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_DATETIME|SQL_DATETIME|SQL_WVARCHAR|SQL_WVARCHAR|  
|SQL_DATETIME_SUB|NULL|NULL|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|NULL|NULL|  
|CHAR_OCTET_LENGTH|NULL|NULL|NULL|NULL|NULL|NULL|  
|SS_DATA_TYPE|0|0|111|111|0|0|  
  
 SQLSpecialColumns não retorna SQL_DATA_TYPE, SQL_DATETIME_SUB, CHAR_OCTET_LENGTH ou SS_DATA_TYPE.  
  
### <a name="data-type-metadata-returned-by-sqlgettypeinfo"></a>Metadados de tipo de dados retornados por SQLGetTypeInfo  
 Os valores de coluna a seguir são retornados para tipos de data/hora:  
  
|Tipo de coluna|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|-----------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_WVARCHAR|SQL_WVARCHAR|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|‘|‘|‘|‘|‘|‘|  
|LITERAL_SUFFIX|‘|‘|‘|‘|‘|‘|  
|CREATE_PARAMS|NULL|NULL|NULL|NULL|NULL|NULL|  
|NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|  
|CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|AUTO_UNIQUE_VALUE|NULL|NULL|NULL|NULL|NULL|NULL|  
|LOCAL_TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|NULL|0|3|NULL|NULL|  
|MAXIMUM_SCALE|NULL|NULL|0|3|NULL|NULL|  
|SQL_DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_DATETIME|SQL_DATETIME|SQL_WVARCHAR|SQL_WVARCHAR|  
|SQL_DATETIME_SUB|NULL|NULL|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|NULL|NULL|  
|NUM_PREC_RADIX|NULL|NULL|NULL|NULL|NULL|NULL|  
|INTERVAL_PRECISION|NULL|NULL|NULL|NULL|NULL|NULL|  
|USERTYPE|0|0|12|22|0|0|  
  
## <a name="down-level-server-behavior"></a>Comportamento de servidor de versão anterior  
 Quando você está conectado a uma instância de servidor de uma versão anterior do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], qualquer tentativa de usar os novos tipos de servidor ou os códigos de metadados e campos de descritor associados resultará no retorno de SQL_ERROR. Um registro de diagnóstico será gerado com SQLSTATE HY004 e a mensagem "Tipo de dados SQL inválido para a versão do servidor na conexão" ou com 07006 e "Violação do atributo de tipo de dados restrito".  
  
## <a name="see-also"></a>Consulte também  
 [Data e hora melhorias &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
