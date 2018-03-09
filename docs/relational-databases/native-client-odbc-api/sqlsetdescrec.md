---
title: SQLSetDescRec | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: SQLSetDescRec function
ms.assetid: 203d02a2-aa09-462b-a489-a2cdd6f6023b
caps.latest.revision: "23"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 26821deb5f1d2404d1ea41ede439cfde403c265b
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2018
---
# <a name="sqlsetdescrec"></a>SQLSetDescRec
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Este tópico discute SQLSetDescRec funcionalidade específica para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="sqlsetdescrec-and-table-valued-parameters"></a>SQLSetDescRec e parâmetros com valor de tabela  
 SQLSetDescRec pode ser usado para definir campos de descritor para parâmetros com valor de tabela e colunas de parâmetro com valor de tabela. As colunas do parâmetro com valor de tabela ficam disponíveis somente quando o campo do cabeçalho do descritor SQL_SOPT_SS_PARAM_FOCUS é definido como o ordinal de um registro que tenha SQL_DESC_TYPE definido como SQL_SS_TABLE. Para obter mais informações sobre SQL_SOPT_SS_PARAM_FOCUS, consulte [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 A seguinte tabela descreve o mapeamento entre parâmetros e campos de descritor.  
  
|Parâmetro|Atributo relacionado a tipos de parâmetros sem-valor de tabela, inclusive colunas de parâmetros com valor de tabela|Atributo relacionado para parâmetros com valor de tabela|  
|---------------|--------------------------------------------------------------------------------------------------------|----------------------------------------------------|  
|*Tipo*|SQL_DESC_TYPE|SQL_SS_TABLE|  
|*SubType*|Ignored|Para registros de tipo SQL_DATETIME ou SQL_INTERVAL, defina como SQL_DESC_DATETIME_INTERVAL_CODE.|  
|*Comprimento*|SQL_DESC_OCTET_LENGTH|O comprimento do nome do tipo de parâmetro com valor de tabela. Isso poderá ser SQL_NTS se o nome do tipo terminar com caractere nulo ou zero se o nome do tipo de parâmetro com valor de tabela não for necessário.|  
|*Precisão*|SQL_DESC_PRECISION|SQL_DESC_ARRAY_SIZE|  
|*Escala*|SQL_DESC_SCALE|Não utilizado. O parâmetro deve ser zero.|  
|*DataPtr*|SQL_DESC_DATA_PTR em APD|SQL_CA_SS_TYPE_NAME<br /><br /> O parâmetro é opcional para chamadas de procedimento armazenado e NULL poderá ser especificado se ele não for necessário. Esse parâmetro deve ser especificado para instruções SQL que não sejam chamadas de procedimento.<br /><br /> *DataPtr* também serve como um valor exclusivo que o aplicativo pode usar para identificar esse parâmetro com valor de tabela quando a associação de linha variável é usada.|  
|*StringLengthPtr*|SQL_DESC_OCTET_LENGTH_PTR|SQL_DESC_OCTET_LENGTH_PTR<br /><br /> Para um parâmetro com valor de tabela, trata-se do número de linhas de transferência ou SQL_DATA_AT_EXEC. Este é um ponteiro para um valor que contém o número de linhas a serem transferidas com SQLExecDirect.|  
|*IndicatorPtr*|SQL_DESC_INDICATOR_PTR|SQL_DESC_INDICATOR_PTR|  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlsetdescrec-support-for-enhanced-date-and-time-features"></a>Suporte de SQLSetDescRec a recursos aprimorados de data e hora  
 Os valores permitidos para tipos de data/hora são os seguintes:  
  
||*Tipo*|*SubType*|*Comprimento*|*Precisão*|*Escala*|  
|-|------------|---------------|--------------|-----------------|-------------|  
|datetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|4|3|3|  
|smalldatetime|SQL_SQL_DATETIME|SQL_CODE_TIMESTAMP|8|0|0|  
|date|SQL_DATETIME|SQL_CODE_DATE|6|0|0|  
|time|SQL_SS_TIME2|0|10|0..7|0..7|  
|datetime2|SQL_DATETIME|SQL_CODE_TIMESTAMP|16|0..7|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|0|20|0..7|0..7|  
  
 Para obter mais informações, consulte [data e hora melhorias &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlsetdescrec-support-for-large-clr-udts"></a>Suporte de SQLSetDescRec para UDTs CLR grandes  
 **SQLSetDescRec** oferece suporte a grandes CLR definido pelo usuário (UDTs tipos). Para obter mais informações, consulte [Large CLR User-Defined tipos &#40; ODBC &#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [SQLSetDescRec](http://go.microsoft.com/fwlink/?LinkId=80704)   
 [Detalhes de implementação de API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
