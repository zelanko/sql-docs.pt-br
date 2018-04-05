---
title: SQLSetScrollOptions (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 693e6e28-a845-41b1-9622-5058b0d87229
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 43f92a786bf2c4d77ad18c7ed6391abd4eff933d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do Driver ODBC do Visual FoxPro. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: parcial  
  
 Conformidade de API de ODBC: Nível 2  
  
 Define opções que controlam o comportamento de cursores associado com um identificador de instrução, *hstmt*.  
  
 O Driver de ODBC do Visual FoxPro oferece suporte a apenas SQL_CONCUR_READ_ONLY; ele não oferece suporte a *fConcurrency* SQL_CONCUR_ROWVER de valor. O driver converterá SQL_KEYSET_SIZE, SQL_CURSOR_DYNAMIC e SQL_CURSOR_KEYSET_DRIVEN para SQL_SCROLL_STATIC ODBC_01S02 de aviso.  
  
 Para obter mais informações, consulte [SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md) no *referência do programador de ODBC*.
