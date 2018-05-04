---
title: Mapeamento de SQLBindParam | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLBindparam function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLBindParam
ms.assetid: 375f8f24-36de-4946-916e-c75abc6f070d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45bd2ccaf64f13e419e7a8da1e772a7d6ad93758
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlbindparam-mapping"></a>Mapeamento de SQLBindParam
**SQLBindParam** não podem realmente ser chamado preterido porque ele nunca houve no ODBC; no entanto, ele ainda representa funções duplicadas — deve exportá-lo porque ISO e abrir grupo compatível com aplicativos usará o Gerenciador de Driver. Porque **SQLBindParameter** contém toda a funcionalidade de **SQLBindParam**, **SQLBindParam** serão mapeados na parte superior do **SQLBindParameter** (quando o driver subjacente é um ODBC 3 *. x* driver). Um ODBC 3 *. x* driver não precisa implementar **SQLBindParam**.  
  
## <a name="remarks"></a>Remarks  
 Quando a seguinte chamada para **SQLBindParam** é feita:  
  
```  
SQLBindParam(   StatementHandle,    ParameterNumber,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    StrLen_or_IndPtr)  
```  
  
 as chamadas de Gerenciador de Driver **SQLBindParameter** no driver da seguinte maneira:  
  
```  
SQLBindParameter(   StatementHandle,    ParameterNumber,    SQL_PARAM_INPUT,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    BufferLength,    StrLen_or_IndPtr)  
```  
  
 Consulte [informações de ODBC de 64 bits](../../../odbc/reference/odbc-64-bit-information.md), se o aplicativo será executado em um sistema operacional de 64 bits.  
  
## <a name="see-also"></a>Consulte também  
 [Funções preteridas de mapeamento](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)
