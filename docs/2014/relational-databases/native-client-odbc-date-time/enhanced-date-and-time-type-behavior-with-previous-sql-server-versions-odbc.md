---
title: Comportamento de tipo de data e hora aprimorado com versões anteriores do SQL Server (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- date/time [ODBC], enhanced behavior with earlier SQL Server versions
ms.assetid: cd4e137f-dc5e-4df7-bc95-51fe18c587e0
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d400faa496740182a1407f89e095ebaccf884b3a
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705471"
---
# <a name="enhanced-date-and-time-type-behavior-with-previous-sql-server-versions-odbc"></a>Comportamento de tipos de data e hora aprimorados com versões anteriores do SQL Server (ODBC)
  Este tópico descreve o comportamento esperado quando um aplicativo cliente que usa recursos aprimorados de data e hora se comunica com uma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anterior ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e quando um aplicativo cliente que usa o Microsoft Data Access Components, o Windows Data Access Components ou uma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client anterior ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] envia comandos para um servidor que oferece suporte a recursos aprimorados de data e hora.  
  
## <a name="down-level-client-behavior"></a>Comportamento do cliente de versão anterior  
 Os aplicativos cliente que foram compilados usando uma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client anterior ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] vêm os novos tipos de data/hora como colunas nvarchar. O conteúdo da coluna são as representações literais, conforme descrito na seção "formatos de dados: cadeias de caracteres e literais" do [suporte de tipo de dados para melhorias de data e hora ODBC](data-type-support-for-odbc-date-and-time-improvements.md). O tamanho da coluna é o comprimento de literal máximo para a precisão de segundos fracionários especificada da coluna.  
  
 As APIs de catálogo retornarão metadados consistentes com o código de tipo de dados de versão anterior retornado ao cliente (por exemplo, nvarchar) e a representação de versão anterior associada (por exemplo, o formato de literal apropriado). Entretanto, o nome do tipo de dados retornado será o nome de tipo [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] real.  
  
 Os metadados de instrução retornados por SQLDescribeCol, SQLDescribeParam, SQGetDescField e SQLColAttribute retornarão metadados que são consistentes com o tipo de nível inferior em todos os aspectos, incluindo o nome do tipo. Um exemplo desse tipo de versão anterior é `nvarchar`.  
  
 Quando um aplicativo cliente de nível inferior é executado em um [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] servidor (ou posterior) no qual são feitas alterações de esquema nos tipos de data/hora, o comportamento esperado é o seguinte:  
  
|Tipo SQL Server 2005|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]Tipo  (ou posterior)|Tipo de cliente ODBC|Conversão do resultado (de SQL para C)|Conversão do parâmetro (de C para SQL)|  
|--------------------------|----------------------------------------------|----------------------|------------------------------------|---------------------------------------|  
|Datetime|Data|SQL_C_TYPE_DATE|OK|OK (1)|  
|||SQL_C_TYPE_TIMESTAMP|Campos de hora definidos como zero.|OK (2)<br /><br /> Falha se o campo de hora for diferente de zero. Funciona com o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||Time(0)|SQL_C_TYPE_TIME|OK|OK (1)|  
|||SQL_C_TYPE_TIMESTAMP|Campos de data definidos como a data atual.|OK (2)<br /><br /> Data ignorada. Falhará se os segundos fracionários forem diferentes de zero. Funciona com o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||Time(7)|SQL_C_TIME|Falha-literal de tempo inválido.|OK (1)|  
|||SQL_C_TYPE_TIMESTAMP|Falha-literal de tempo inválido.|OK (1)|  
||Datetime2 (3)|SQL_C_TYPE_TIMESTAMP|OK|OK (1)|  
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
  
|Tipo de coluna|date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|-----------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_WVARCHAR|SQL_WVARCHAR|  
|TYPE_NAME|date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|COLUMN_SIZE|10|8, 10.. 16|16|23|19, 21..27|26, 28..34|  
|BUFFER_LENGTH|20|16, 20.. 32|16|16|38, 42.54|52, 56.68|  
|DECIMAL_DIGITS|NULO|NULO|0|3|NULO|NULO|  
|SQL_DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_DATETIME|SQL_DATETIME|SQL_WVARCHAR|SQL_WVARCHAR|  
|SQL_DATETIME_SUB|NULO|NULO|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|NULO|NULO|  
|CHAR_OCTET_LENGTH|NULO|NULO|NULO|NULO|NULO|NULO|  
|SS_DATA_TYPE|0|0|111|111|0|0|  
  
 SQLSpecialColumns não retorna SQL_DATA_TYPE, SQL_DATETIME_SUB, CHAR_OCTET_LENGTH ou SS_DATA_TYPE.  
  
### <a name="data-type-metadata-returned-by-sqlgettypeinfo"></a>Metadados de tipo de dados retornados por SQLGetTypeInfo  
 Os valores de coluna a seguir são retornados para tipos de data/hora:  
  
|Tipo de coluna|date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|-----------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_WVARCHAR|SQL_WVARCHAR|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|'|'|'|'|'|'|  
|LITERAL_SUFFIX|'|'|'|'|'|'|  
|CREATE_PARAMS|NULO|NULO|NULO|NULO|NULO|NULO|  
|NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|  
|CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULO|NULO|NULO|NULO|NULO|NULO|  
|FXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|AUTO_UNIQUE_VALUE|NULO|NULO|NULO|NULO|NULO|NULO|  
|LOCAL_TYPE_NAME|date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULO|NULO|0|3|NULO|NULO|  
|MAXIMUM_SCALE|NULO|NULO|0|3|NULO|NULO|  
|SQL_DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_DATETIME|SQL_DATETIME|SQL_WVARCHAR|SQL_WVARCHAR|  
|SQL_DATETIME_SUB|NULO|NULO|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|NULO|NULO|  
|NUM_PREC_RADIX|NULO|NULO|NULO|NULO|NULO|NULO|  
|INTERVAL_PRECISION|NULO|NULO|NULO|NULO|NULO|NULO|  
|USERTYPE|0|0|12|22|0|0|  
  
## <a name="down-level-server-behavior"></a>Comportamento de servidor de versão anterior  
 Quando você está conectado a uma instância de servidor de uma versão anterior do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], qualquer tentativa de usar os novos tipos de servidor ou os códigos de metadados e campos de descritor associados resultará no retorno de SQL_ERROR. Um registro de diagnóstico será gerado com SQLSTATE HY004 e a mensagem "Tipo de dados SQL inválido para a versão do servidor na conexão" ou com 07006 e "Violação do atributo de tipo de dados restrito".  
  
## <a name="see-also"></a>Consulte Também  
 [Melhorias de data e hora &#40;&#41;ODBC](date-and-time-improvements-odbc.md)  
  
  
