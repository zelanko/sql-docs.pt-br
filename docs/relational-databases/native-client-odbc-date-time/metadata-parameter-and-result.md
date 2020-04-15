---
title: Parâmetro e Metadados de Resultados | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- metadata [ODBC]
ms.assetid: 1518e6e5-a6a8-4489-b779-064c5624df53
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8ba66c950f25663dabc3c0c46f83a7589df300ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304077"
---
# <a name="metadata---parameter-and-result"></a>Metadados – Parâmetro e resultado
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Este tópico descreve o que é retornado nos campos IPD (descritor de parâmetro de implementação) e IRD (descritor de linha de implementação) dos tipos de dados de data e hora.  
  
## <a name="information-returned-in-ipd-fields"></a>Informações retornadas nos campos IPD  
 As seguintes informações são retornadas nos campos IPD:  
  
|Tipo de parâmetro|date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|--------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQL_CODE_DATE|0|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|10|8,10..16|16|23|19, 21..27|26, 28..34|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|10|8,10..16|16|23|19, 21..27|26, 28..34|  
|SQL_DESC_OCTET_LENGTH|6|12|4|8|16|20|  
|SQL_DESC_PRECISION|0|0..7|0|3|0..7|0..7|  
|SQL_DESC_SCALE|0|0..7|0|3|0..7|0..7|  
|SQL_DESC_TYPE|SQL_TYPE_DATE|SQL_SS_TYPE_TIME2|SQL_DATETIME|SQL_DATETIME|SQL_DATETIME|SQL_SS_TIMESTAMPOFFSET|  
|SQL_DESC_TYPE_NAME|**date**|**time**|**tempo de data em** IRD, **datetime2** em IPD|**datetime** em IRD, **datetime2** no IPD|**datetime2**|datetimeoffset|  
|SQL_CA_SS_VARIANT_TYPE|SQL_C_TYPE_DATE|SQL_C_TYPE_BINARY|SQL_C_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_C_TYPE_BINARY|  
|SQL_CA_SS_VARIANT_SQL_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|SQL_CA_SS_SERVER_TYPE|N/D|N/D|SQL_SS_TYPE_SMALLDATETIME|SQL_SS_TYPE_DATETIME|SQL_SS_TYPE_DEFAULT|N/D|  
  
 Às vezes, há descontinuações em intervalos de valores. Por exemplo, 9 está ausente em 8,10.. 16. Isso se deve à adição de um ponto decimal quando a precisão fracionária é maior que zero.  
  
 **datetime2** é retornado como o nome de **digitação** para data e data **de data** menor porque o driver usa isso como um tipo comum para transmitir todos os **valores SQL_TYPE_TIMESTAMP** para o servidor.  
  
 SQL_CA_SS_VARIANT_SQL_TYPE é um novo campo descritor. Este campo foi adicionado ao IRD e IPD para permitir que os aplicativos especifiquem o tipo de valor associado às colunas e parâmetros **sqlvariant** (SQL_SSVARIANT)  
  
 SQL_CA_SS_SERVER_TYPE é um novo campo somente IPD que permite aos aplicativos controlar como os valores de parâmetros associados como SQL_TYPE_TYPETIMESTAMP (ou como SQL_SS_VARIANT com um tipo C de SQL_C_TYPE_TIMESTAMP) são enviados para o servidor. Se SQL_DESC_CONCISE_TYPE estiver SQL_TYPE_TIMESTAMP (ou estiver SQL_SS_VARIANT e o tipo C for SQL_C_TYPE_TIMESTAMP) quando o SQLExecute ou o SQLExecDirect for chamado, o valor do SQL_CA_SS_SERVER_TYPE determina o tipo de fluxo de dados tabular (TDS) do valor do parâmetro, da seguinte forma:  
  
|Valor de SQL_CA_SS_SERVER_TYPE|Valores válidos para SQL_DESC_PRECISION|Valores válidos para SQL_DESC_LENGTH|Tipo de TDS|  
|----------------------------------------|-------------------------------------------|----------------------------------------|--------------|  
|SQL_SS_TYPE_DEFAULT|0..7|19, 21..27|**datetime2**|  
|SQL_SS_TYPE_SMALLDATETIME|0|19|**smalldatetime**|  
|SQL_SS_TYPE_DATETIME|3|23|**datetime**|  
  
 A configuração padrão de SQL_CA_SS_SERVER_TYPE é SQL_SS_TYPE_DEFAULT. As configurações de SQL_DESC_PRECISION e SQL_DESC_LENGTH são validadas com a configuração de SQL_CA_SS_SERVER_TYPE, conforme descrição na tabela acima. Caso essa validação falhe, SQL_ERROR é retornado, e um registro de diagnóstico é feito com SQLState 07006 e a mensagem "Violação do atributo de tipo de dados restrito". Esse erro também é retornado caso SQL_CA_SS_SERVER_TYPE seja definido como um valor diferente de SQL_SS_TYPE DEFAULT e DESC_CONCISE_TYPE não seja SQL_TYPE_TIMESTAMP. Essas validações são executadas quando ocorre a validação de consistência do descritor. Por exemplo:  
  
-   Quando SQL_DESC_DATA_PTR é alterado.  
  
-   No momento da preparação ou da execução (quando SQLExecute, SQLExecDirect, SQLSetPos ou SQLBulkOperations é chamado).  
  
-   Quando um aplicativo força uma preparação não diferida ligando para o SQLPrepare com preparação diferida desativada, ou ligando para SQLNumResultCols, SQLDescribeCol ou SQLDescribeParam para uma declaração preparada, mas não executada.  
  
 Quando SQL_CA_SS_SERVER_TYPE é definido por uma chamada para SQLSetDescField, seu valor deve ser SQL_SS_TYPE_DEFAULT, SQL_SS_TYPE_SMALLDATETIME ou SQL_SS_TYPE_DATETIME. Caso não seja esse o caso, SQL_ERROR é retornado, e um registro de diagnóstico é feito com SQLState HY092 e a mensagem "Identificador de atributo/opção inválido".  
  
 O SQL_CA_SS_SERVER_TYPE atributo pode ser usado por aplicativos que dependem da funcionalidade suportada por **data e** **data pequena,** mas não **data2**. Por exemplo, **datetime2** requer o uso das funções **dateadd** e **dateiif,** enquanto **a data e** a data **reduzida** também permitem operadores aritméticos. A maioria dos aplicativos não precisará usar esse atributo, e seu uso deve ser evitado.  
  
## <a name="information-returned-in-ird-fields"></a>Informações retornadas nos campos IRD  
 As seguintes informações são retornadas nos campos IRD:  
  
|Tipo de coluna|date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|-----------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQL_CODE_DATE|0|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|10|8,10..16|16|23|19, 21..27|26, 28..34|  
|SQL_DESC_DISPLAY_SIZE|10|8,10..16|16|23|19, 21..27|26, 28..34|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|10|8,10..16|16|2|19, 21..27|26, 28..34|  
|SQL_DESC_LITERAL_PREFIX|'|'|'|'|'|'|  
|SQL_DESC_LITERAL_SUFFIX|'|'|'|'|'|'|  
|SQL_DESC_LOCAL_TYPE_NAME|**date**|**time**|**smalldatetime**|**datetime**|**datetime2**|datetimeoffset|  
|SQL_DESC_OCTET_LENGTH|6|12|4|8|16|20|  
|SQL_DESC_PRECISION|0|0..7|0|3|0..7|0..7|  
|SQL_DESC_SCALE|0|0..7|0|3|0..7|0..7|  
|SQL_DESC_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|  
|SQL_DESC_TYPE|SQL_DATETIME|SQL_SS_TIME2|SQL_DATETIME|SQL_DATETIME|SQL_DATETIME|SQL_SS_TIMESTAMPOFFSET|  
|SQL_DESC_TYPE_NAME|**date**|**time**|**smalldatetime**|**datetime**|**datetime2**|datetimeoffset|  
|SQL_DESC_UNSIGNED|SQL_TRUE|SQL_TRUE|SQL_TRUE|SQL_TRUE|SQL_TRUE|SQL_TRUE|  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;de Metadados &#40;ODBC](https://msdn.microsoft.com/library/99133efc-b1f2-46e9-8203-d90c324a8e4c)  
  
  
