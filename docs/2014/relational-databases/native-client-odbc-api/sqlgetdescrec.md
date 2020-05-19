---
title: SQLGetDescRec | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLGetDescRec function
ms.assetid: f3389ff2-f3be-4035-9fb5-c9ebc2f15025
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f3a2bbebc947d0c245e00c39fca2d4e69fbb5666
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706031"
---
# <a name="sqlgetdescrec"></a>SQLGetDescRec
  Este tópico discute a funcionalidade do SQLGetDescRec que é específica para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="sqlgetdescrec-and-table-valued-parameters"></a>SQLGetDescRec e parâmetros com valor de tabela  
 SQLGetDescRec pode ser usado para obter valores para atributos de parâmetros com valor de tabela e colunas de parâmetro com valor de tabela. O parâmetro *RecNumber* de SQLGetDescRec corresponde ao parâmetro *ParameterNumber* de SQLBindParameter.  
  
 As colunas do parâmetro com valor de tabela ficam disponíveis somente quando o campo do cabeçalho do descritor SQL_SOPT_SS_PARAM_FOCUS é definido como o ordinal de um registro que tenha SQL_DESC_TYPE definido como SQL_SS_TABLE. Para obter mais informações sobre SQL_SOPT_SS_PARAM_FOCUS, consulte [SQLSetStmtAttr](sqlsetstmtattr.md).  
  
 SQLGetDescRec retorna os seguintes dados:  
  
|Parâmetro|Parâmetro com valor de tabela|Colunas de parâmetro com valor de tabela e outros parâmetros|  
|---------------|-----------------------------|----------------------------------------------------------|  
|*Nome*|O nome de parâmetro formal para uma chamada de procedimento armazenado; caso contrário, uma cadeia de caracteres de comprimento 0.|O nome da coluna do parâmetro com valor de tabela.|  
|*TypePtr*|SQL_DESC_TYPE. Para parâmetros com valor de tabela, este é SQL_SS_TABLE.|SQL_DESC_TYPE|  
|*SubTypePtr*|Indefinido|SQL_DESC_DATETIME_INTERVAL_CODE (Para registros do tipo SQL_DATETIME ou SQL_INTERVAL.)|  
|*LengthPtr*|0|SQL_DESC_OCTET_LENGTH|  
|*PrecisionPtr*|0|SQL_DESC_PRECISION|  
|*ScalePtr*|0|SQL_DESC_SCALE|  
|*NullablePtr*|1|SQL_DESC_NULLABLE|  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;&#41;ODBC ](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlgetdescrec-support-for-enhanced-date-and-time-features"></a>Suporte de SQLGetDescRec a recursos aprimorados de data e hora  
 Os valores retornados para tipos de data/hora são os seguintes:  
  
||*TypePtr*|*SubTypePtr*|*LengthPtr*|*PrecisionPtr*|*ScalePtr*|  
|-|---------------|------------------|-----------------|--------------------|----------------|  
|DATETIME|SQL_DATETIME|SQL_CODE_TIMESTAMP|4|3|3|  
|smalldatetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|8|0|0|  
|data|SQL_DATETIME|SQL_CODE_DATE|6|0|0|  
|time|SQL_SS_TIME2|0|10|0..7|0..7|  
|datetime2|SQL_DATETIME|SQL_CODE_TIMESTAMP|16|0..7|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|0|20|0..7|0..7|  
  
 Para obter mais informações, consulte [melhorias de data e hora &#40;&#41;ODBC ](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlgetdescrec-support-for-large-clr-udts"></a>Suporte de SQLGetDescRec para UDTs CLR grandes  
 `SQLGetDescRec` dá suporte a UDTs grandes do CLR. Para obter mais informações, consulte [tipos CLR grandes definidos pelo usuário &#40;&#41;ODBC ](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [SQLGetDescRec](https://go.microsoft.com/fwlink/?LinkId=80707)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
