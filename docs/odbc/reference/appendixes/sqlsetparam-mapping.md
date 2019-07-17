---
title: Mapeamento SQLSetParam | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetParam
- SQLSetParam function [ODBC], mapping
ms.assetid: 022dfbc0-8d18-4c35-8a28-d9eb16063188
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6c8d2d567f899c30dfe91cd35445956cd6214da9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125548"
---
# <a name="sqlsetparam-mapping"></a>Mapeamento SQLSetParam
**SQLSetParam** continua a ser mapeada na parte superior da **SQLBindParameter** como no ODBC 2. *x*. Mesmo que ele é conceitualmente semelhante a **SQLBindParam**, o Gerenciador de Driver não mapeia **SQLSetParam** para **SQLBindParam**. Isso ocorre porque determinado existente ODBC 2. *x* drivers usam o valor especial *BufferLength* (SQL_SETPARAM_VALUE_MAX) que o Gerenciador de Driver gera quando ele mapeia **SQLSetParam** na parte superior da  **SQLBindParameter** para determinar quando ele é chamado por 1. *x* aplicativo ODBC.  
  
 Uma chamada para  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 resultará no seguinte:  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
