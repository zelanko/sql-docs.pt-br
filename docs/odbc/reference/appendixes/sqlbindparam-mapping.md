---
title: Mapeamento de SQLBindParam | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindparam function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLBindParam
ms.assetid: 375f8f24-36de-4946-916e-c75abc6f070d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c1df595722297c91dc75398470912188e109e278
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305436"
---
# <a name="sqlbindparam-mapping"></a>Mapeamento SQLBindParam
**SQLBindParam** não pode realmente ser chamado de preterido porque nunca estava lá no ODBC; no entanto, ele ainda representa a funcionalidade duplicada – o Gerenciador de driver precisa exportá-lo porque os aplicativos em conformidade com o ISO e o grupo aberto o usarão. Como **SQLBindParameter** contém toda a funcionalidade de **SQLBindParam**, **SQLBindParam** será mapeado na parte superior de **SQLBindParameter** (quando o driver subjacente for um driver ODBC *3. x* ). Um driver ODBC *3. x* não precisa implementar **SQLBindParam**.  
  
## <a name="remarks"></a>Comentários  
 Quando a seguinte chamada para **SQLBindParam** é feita:  
  
```  
SQLBindParam(   StatementHandle,    ParameterNumber,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    StrLen_or_IndPtr)  
```  
  
 o Gerenciador de driver chama **SQLBindParameter** no driver da seguinte maneira:  
  
```  
SQLBindParameter(   StatementHandle,    ParameterNumber,    SQL_PARAM_INPUT,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    BufferLength,    StrLen_or_IndPtr)  
```  
  
 Consulte [informações de ODBC 64-bit](../../../odbc/reference/odbc-64-bit-information.md), se seu aplicativo for executado em um sistema operacional de 64 bits.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções preteridas de mapeamento](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)
