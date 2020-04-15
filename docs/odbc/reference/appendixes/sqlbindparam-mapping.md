---
title: Mapeamento SQLBindParam | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305436"
---
# <a name="sqlbindparam-mapping"></a>Mapeamento SQLBindParam
**SQLBindParam** não pode ser verdadeiramente chamado de preterido porque nunca esteve lá na ODBC; no entanto, ele ainda representa a funcionalidade duplicada - o Driver Manager precisa exportá-la porque os aplicativos compatíveis com ISO e Open Group estarão usando-o. Como **o SQLBindParameter** contém todas as funcionalidades do **SQLBindParam,** **o SQLBindParam** será mapeado em cima do **SQLBindParameter** (quando o driver subjacente for um driver ODBC *3.x).* Um driver ODBC *3.x* não precisa implementar **o SQLBindParam**.  
  
## <a name="remarks"></a>Comentários  
 Quando a seguinte chamada para **SQLBindParam** for feita:  
  
```  
SQLBindParam(   StatementHandle,    ParameterNumber,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    StrLen_or_IndPtr)  
```  
  
 o Driver Manager chama **sQLBindParameter** no driver da seguinte forma:  
  
```  
SQLBindParameter(   StatementHandle,    ParameterNumber,    SQL_PARAM_INPUT,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    BufferLength,    StrLen_or_IndPtr)  
```  
  
 Consulte [As informações de 64 bits do ODBC,](../../../odbc/reference/odbc-64-bit-information.md)se o aplicativo for executado em um sistema operacional de 64 bits.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções preteridas de mapeamento](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)
