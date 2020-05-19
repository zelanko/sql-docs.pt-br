---
title: SQLSetDescField | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLSetDescField function
ms.assetid: de4bed15-15be-4825-994c-1046255e725a
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2ac1f46529dc16c67de7237f191f81decf9a2c0c
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702165"
---
# <a name="sqlsetdescfield"></a>SQLSetDescField
  SQLSetDescField pode ser usado para definir campos de descritor para parâmetros com valor de tabela e colunas de parâmetro com valor de tabela. Para obter informações sobre os campos disponíveis, consulte [campos de descritor de parâmetro com valor de tabela](../native-client-odbc-table-valued-parameters/table-valued-parameter-descriptor-fields.md) e [campos de descritor para colunas constituintes de parâmetro com valor de tabela](../native-client-odbc-table-valued-parameters/descriptor-fields-for-table-valued-parameter-constituent-columns.md).  
  
## <a name="remarks"></a>Comentários  
 As colunas do parâmetro com valor de tabela ficam disponíveis somente quando o campo do cabeçalho do descritor SQL_SOPT_SS_PARAM_FOCUS é definido como o ordinal de um registro que tenha SQL_DESC_TYPE definido como SQL_SS_TABLE. Para obter mais informações sobre SQL_SPOT_SS_PARAM_FOCUS, consulte [SQLSetStmtAttr](sqlsetstmtattr.md).  
  
 Se for feita uma tentativa de definir SQL_SOPT_SS_PARAM_FOCUS para o ordinal de um parâmetro que não seja um parâmetro com valor de tabela, SQLSetStmtAttr retornará SQL_ERROR e um registro de diagnóstico será criado com SQLSTATE = HY024 e a mensagem "valor de atributo inválido". SQL_SOPT_SS_PARAM_FOCUS não é alterado quando SQL_ERROR é retornado.  
  
 A definição de SQL_SOPT_SS_PARAM_FOCUS como 0 restaura o acesso a registros de descritor para parâmetros.  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;&#41;ODBC ](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-enhanced-date-and-time-features"></a>Suporte do SQLSetDescField a recursos aprimorados de data e hora  
 Os recursos de data/hora foram aprimorados no ODBC. Para obter informações sobre o campo de descritor fornecido para os novos tipos de data/hora, consulte [Parameter and Result Metadata](../native-client-odbc-date-time/metadata-parameter-and-result.md).  
  
 Para obter mais informações, consulte [melhorias de data e hora &#40;&#41;ODBC ](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-large-clr-udts"></a>Suporte de SQLSetDescField a UDTs grandes do CLR  
 O SQLSetDescField dá suporte a UDTs (tipos definidos pelo usuário) CLR grandes. Para obter mais informações, consulte [tipos CLR grandes definidos pelo usuário &#40;&#41;ODBC ](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="sqlsetdescfield-support-for-sparse-columns"></a>Suporte de SQLSetDescField a colunas esparsas  
 SQLSetDecField pode ser usado para definir SQL_SOPT_SS_NAME_SCOPE no descritor de parâmetro do aplicativo (APD) para os valores SQL_SS_NAME_SCOPE_EXTENDED e SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET.  
  
 Para obter mais informações, consulte [suporte a colunas esparsas &#40;&#41;ODBC ](../native-client/odbc/sparse-columns-support-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [SQLSetDescField](https://go.microsoft.com/fwlink/?LinkId=80705)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
