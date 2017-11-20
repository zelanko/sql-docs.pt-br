---
title: Mapeamento de SQLSetParam | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetParam
- SQLSetParam function [ODBC], mapping
ms.assetid: 022dfbc0-8d18-4c35-8a28-d9eb16063188
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bd23345c0e403e6f4f16419e539c2b5ae277c9d4
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetparam-mapping"></a>Mapeamento de SQLSetParam
**SQLSetParam** continua a ser mapeada na parte superior do **SQLBindParameter** como ODBC 2. *x*. Mesmo que ele é conceitualmente semelhante a **SQLBindParam**, o Gerenciador de Driver não mapear **SQLSetParam** para **SQLBindParam**. Isso ocorre porque determinado existente ODBC 2. *x* drivers usam o valor especial de *BufferLength* (SQL_SETPARAM_VALUE_MAX) que o Gerenciador de Driver gera quando ele mapeia **SQLSetParam** na parte superior do  **SQLBindParameter** para determinar quando ele é chamado por 1. *x* aplicativo ODBC.  
  
 Uma chamada para  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 resultará no seguinte:  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```

