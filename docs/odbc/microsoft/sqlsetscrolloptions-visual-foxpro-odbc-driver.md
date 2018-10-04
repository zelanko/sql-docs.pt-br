---
title: SQLSetScrollOptions (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 693e6e28-a845-41b1-9622-5058b0d87229
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c2d78e26309d5ea7dc5e6eed5a04e84a1651b33
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622624"
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas de Driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: parcial  
  
 Conformidade com a API ODBC: 2 de nível  
  
 Define opções que controlam o comportamento de cursores associado com um identificador de instrução *hstmt*.  
  
 O Driver de ODBC do Visual FoxPro dá suporte a apenas SQL_CONCUR_READ_ONLY; ele não oferece suporte a *fConcurrency* SQL_CONCUR_ROWVER de valor. O driver converterá SQL_KEYSET_SIZE, SQL_CURSOR_DYNAMIC e SQL_CURSOR_KEYSET_DRIVEN em SQL_SCROLL_STATIC com aviso ODBC_01S02.  
  
 Para obter mais informações, consulte [SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md) na *referência do programador de ODBC*.
