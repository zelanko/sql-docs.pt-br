---
title: SQLSetDescField | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLSetDescField function
ms.assetid: de4bed15-15be-4825-994c-1046255e725a
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b883a4f7fa079462c18b45d41915968763eb9ca5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlsetdescfield"></a>SQLSetDescField
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  SQLSetDescField pode ser usado para definir campos de descritor para parâmetros com valor de tabela e colunas de parâmetro com valor de tabela. Para obter informações sobre os campos disponíveis, consulte [campos de descritor de parâmetro com valor de tabela](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-descriptor-fields.md) e [campos de descritor para colunas de constituinte de parâmetro com valor de tabela](../../relational-databases/native-client-odbc-table-valued-parameters/descriptor-fields-for-table-valued-parameter-constituent-columns.md).  
  
## <a name="remarks"></a>Remarks  
 As colunas do parâmetro com valor de tabela ficam disponíveis somente quando o campo do cabeçalho do descritor SQL_SOPT_SS_PARAM_FOCUS é definido como o ordinal de um registro que tenha SQL_DESC_TYPE definido como SQL_SS_TABLE. Para obter mais informações sobre SQL_SOPT_SS_PARAM_FOCUS, consulte [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Se for feita uma tentativa de definir SQL_SOPT_SS_PARAM_FOCUS como o ordinal de um parâmetro que não é um parâmetro com valor de tabela, SQLSetStmtAttr retornará SQL_ERROR e é criado um registro de diagnóstico com SQLSTATE = HY024 e a mensagem "valor de atributo inválido". SQL_SOPT_SS_PARAM_FOCUS não é alterado quando SQL_ERROR é retornado.  
  
 A definição de SQL_SOPT_SS_PARAM_FOCUS como 0 restaura o acesso a registros de descritor para parâmetros.  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela & #40; ODBC & #41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-enhanced-date-and-time-features"></a>Suporte do SQLSetDescField a recursos aprimorados de data e hora  
 Os recursos de data/hora foram aprimorados no ODBC. Para obter informações sobre o campo de descritor fornecido para os tipos de data/hora novo, consulte [parâmetro e metadados de resultado](../../relational-databases/native-client-odbc-date-time/metadata-parameter-and-result.md).  
  
 Para obter mais informações, consulte [data e hora melhorias & #40; ODBC & #41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-large-clr-udts"></a>Suporte de SQLSetDescField a UDTs grandes do CLR  
 SQLSetDescField oferece suporte a grandes CLR definido pelo usuário (UDTs tipos). Para obter mais informações, consulte [Large CLR User-Defined tipos & #40; ODBC & #41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-sparse-columns"></a>Suporte de SQLSetDescField a colunas esparsas  
 SQLSetDecField pode ser usado para definir SQL_SOPT_SS_NAME_SCOPE no descritor de parâmetro de aplicativo (APD) com os valores SQL_SS_NAME_SCOPE_EXTENDED e SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET.  
  
 Para obter mais informações, consulte [suporte a colunas esparsas &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [SQLSetDescField](http://go.microsoft.com/fwlink/?LinkId=80705)   
 [Detalhes de implementação de API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
