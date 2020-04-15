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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d8e632412965664e5cdd9c87dc1e26787dcdab2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300526"
---
# <a name="sqlsetparam-mapping"></a>Mapeamento SQLSetParam
**O SQLSetParam** continua a ser mapeado em cima do **SQLBindParameter** como em ODBC 2. *x*. Embora seja conceitualmente semelhante ao **SQLBindParam,** o Driver Manager não mapeia **SQLSetParam** para **SQLBindParam**. Isso porque certos ODBC 2 existentes. *x* drivers usam o valor especial de *BufferLength* (SQL_SETPARAM_VALUE_MAX) que o Driver Manager gera quando mapeia **SQLSetParam** em cima do **SQLBindParameter** para determinar quando ele é chamado por um 1. *x* aplicação ODBC.  
  
 Uma chamada para  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 resultará no seguinte:  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
