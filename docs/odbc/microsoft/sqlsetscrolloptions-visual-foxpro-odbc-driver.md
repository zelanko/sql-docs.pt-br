---
title: Opções de SQLSetScroll (driver Visual FoxPro ODBC) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19051fc83466bc40d72c029089cfe6ec45c20a08
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299416"
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver Visual FoxPro ODBC. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: Parcial  
  
 Conformidade da API ODBC: Nível 2  
  
 Define opções que controlam o comportamento dos cursores associados a uma alça de declaração, *hstmt*.  
  
 O driver Visual FoxPro ODBC suporta apenas SQL_CONCUR_READ_ONLY; não suporta o valor *fConcurrency* SQL_CONCUR_ROWVER. O motorista converte SQL_KEYSET_SIZE, SQL_CURSOR_DYNAMIC e SQL_CURSOR_KEYSET_DRIVEN para SQL_SCROLL_STATIC com ODBC_01S02 de advertência.  
  
 Para obter mais informações, consulte [SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md) na *referência do programador ODBC*.
