---
title: Metadados de parâmetro e resultado | Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1f8f04d699c46c654290d1badc26de246a2d9125
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73783696"
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
|SQL_DESC_DATETIME_INTERVAL_PRECISION|10|8, 10.. 16|16|23|19, 21..27|26, 28..34|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|10|8, 10.. 16|16|23|19, 21..27|26, 28..34|  
|SQL_DESC_OCTET_LENGTH|6|12|4|8|16|20|  
|SQL_DESC_PRECISION|0|0..7|0|3|0..7|0..7|  
|SQL_DESC_SCALE|0|0..7|0|3|0..7|0..7|  
|SQL_DESC_TYPE|SQL_TYPE_DATE|SQL_SS_TYPE_TIME2|SQL_DATETIME|SQL_DATETIME|SQL_DATETIME|SQL_SS_TIMESTAMPOFFSET|  
|SQL_DESC_TYPE_NAME|**date**|**time**|**smalldatetime** em IRD, **datetime2** em IPD|**DateTime** em IRD, **datetime2** em IPD|**datetime2**|datetimeoffset|  
|SQL_CA_SS_VARIANT_TYPE|SQL_C_TYPE_DATE|SQL_C_TYPE_BINARY|SQL_C_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_C_TYPE_BINARY|  
|SQL_CA_SS_VARIANT_SQL_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|SQL_CA_SS_SERVER_TYPE|N/D|N/D|SQL_SS_TYPE_SMALLDATETIME|SQL_SS_TYPE_DATETIME|SQL_SS_TYPE_DEFAULT|N/D|  
  
 Às vezes, há descontinuações em intervalos de valores. Por exemplo, 9 está ausente em 8,10.. 16. Isso se deve à adição de um ponto decimal quando a precisão fracionária é maior que zero.  
  
 **datetime2** é retornado como TypeName para **smalldatetime** e **DateTime** porque o driver usa isso como um tipo comum para transmitir todos os valores de **SQL_TYPE_TIMESTAMP** para o servidor.  
  
 SQL_CA_SS_VARIANT_SQL_TYPE é um novo campo descritor. Este campo foi adicionado ao IRD e ao IPD para permitir que os aplicativos especifiquem o tipo de valor associado a colunas e parâmetros **sqlvariant** (SQL_SSVARIANT)  
  
 SQL_CA_SS_SERVER_TYPE é um novo campo somente IPD que permite aos aplicativos controlar como os valores de parâmetros associados como SQL_TYPE_TYPETIMESTAMP (ou como SQL_SS_VARIANT com um tipo C de SQL_C_TYPE_TIMESTAMP) são enviados para o servidor. Se SQL_DESC_CONCISE_TYPE for SQL_TYPE_TIMESTAMP (ou for SQL_SS_VARIANT e o tipo C for SQL_C_TYPE_TIMESTAMP) quando SQLExecute ou SQLExecDirect for chamado, o valor de SQL_CA_SS_SERVER_TYPE determinará o tipo TDS do valor do parâmetro , da seguinte maneira:  
  
|Valor de SQL_CA_SS_SERVER_TYPE|Valores válidos para SQL_DESC_PRECISION|Valores válidos para SQL_DESC_LENGTH|Tipo de TDS|  
|----------------------------------------|-------------------------------------------|----------------------------------------|--------------|  
|SQL_SS_TYPE_DEFAULT|0..7|19, 21..27|**datetime2**|  
|SQL_SS_TYPE_SMALLDATETIME|0|19|**smalldatetime**|  
|SQL_SS_TYPE_DATETIME|3|23|**datetime**|  
  
 A configuração padrão de SQL_CA_SS_SERVER_TYPE é SQL_SS_TYPE_DEFAULT. As configurações de SQL_DESC_PRECISION e SQL_DESC_LENGTH são validadas com a configuração de SQL_CA_SS_SERVER_TYPE, conforme descrição na tabela acima. Caso essa validação falhe, SQL_ERROR é retornado, e um registro de diagnóstico é feito com SQLState 07006 e a mensagem "Violação do atributo de tipo de dados restrito". Esse erro também é retornado caso SQL_CA_SS_SERVER_TYPE seja definido como um valor diferente de SQL_SS_TYPE DEFAULT e DESC_CONCISE_TYPE não seja SQL_TYPE_TIMESTAMP. Essas validações são executadas quando ocorre a validação de consistência do descritor. Por exemplo:  
  
-   Quando SQL_DESC_DATA_PTR é alterado.  
  
-   No momento da preparação ou da execução (quando SQLExecute, SQLExecDirect, SQLSetPos ou SQLBulkOperations é chamado).  
  
-   Quando um aplicativo força uma preparação não adiada chamando SQLPrepare com a preparação adiada desabilitada ou chamando SQLNumResultCols, SQLDescribeCol ou SQLDescribeParam para uma instrução preparada, mas não executada.  
  
 Quando SQL_CA_SS_SERVER_TYPE é definido por uma chamada para SQLSetDescField, seu valor deve ser SQL_SS_TYPE_DEFAULT, SQL_SS_TYPE_SMALLDATETIME ou SQL_SS_TYPE_DATETIME. Caso não seja esse o caso, SQL_ERROR é retornado, e um registro de diagnóstico é feito com SQLState HY092 e a mensagem "Identificador de atributo/opção inválido".  
  
 O atributo SQL_CA_SS_SERVER_TYPE pode ser usado por aplicativos que dependem da funcionalidade com suporte de **DateTime** e **smalldatetime**, mas não **datetime2**. Por exemplo, **datetime2** requer o uso das funções **DateAdd** e **datediif** , enquanto **DateTime** e **smalldatetime** também permitem operadores aritméticos. A maioria dos aplicativos não precisará usar esse atributo, e seu uso deve ser evitado.  
  
## <a name="information-returned-in-ird-fields"></a>Informações retornadas nos campos IRD  
 As seguintes informações são retornadas nos campos IRD:  
  
|Tipo de coluna|date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|-----------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQL_CODE_DATE|0|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|10|8, 10.. 16|16|23|19, 21..27|26, 28..34|  
|SQL_DESC_DISPLAY_SIZE|10|8, 10.. 16|16|23|19, 21..27|26, 28..34|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|10|8, 10.. 16|16|2|19, 21..27|26, 28..34|  
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
 [Metadados &#40;&#41;ODBC](https://msdn.microsoft.com/library/99133efc-b1f2-46e9-8203-d90c324a8e4c)  
  
  
