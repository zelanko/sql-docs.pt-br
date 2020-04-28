---
title: Mapeamento de SQLSetParam | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d8e632412965664e5cdd9c87dc1e26787dcdab2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300526"
---
# <a name="sqlsetparam-mapping"></a>Mapeamento SQLSetParam
**SQLSetParam** continua a ser mapeado sobre o **SQLBINDPARAMETER** como no ODBC 2. *x*. Embora seja conceitualmente semelhante a **SQLBindParam**, o Gerenciador de driver não mapeia **SQLSetParam** para **SQLBindParam**. Isso ocorre porque certos ODBC 2 existentes. os drivers *x* usam o valor especial de *BufferLength* (SQL_SETPARAM_VALUE_MAX) que o Gerenciador de driver gera quando mapeia **SQLSetParam** sobre **SQLBindParameter** para determinar quando ele é chamado por um 1. *x* aplicativo ODBC.  
  
 Uma chamada para  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 resultará no seguinte:  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
