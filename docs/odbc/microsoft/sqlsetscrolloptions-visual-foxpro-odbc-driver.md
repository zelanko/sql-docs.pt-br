---
description: SQLSetScrollOptions (Driver ODBC do Visual FoxPro)
title: SQLSetScrollOptions (driver ODBC do Visual FoxPro) | Microsoft Docs
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
ms.openlocfilehash: c0e7cecfb0ce7640575cb69f1e84e805a884b57b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421630"
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: parcial  
  
 Conformidade da API ODBC: nível 2  
  
 Define opções que controlam o comportamento dos cursores associados a um identificador de instrução, *HSTMT*.  
  
 O driver ODBC do Visual FoxPro dá suporte apenas a SQL_CONCUR_READ_ONLY; Ele não dá suporte ao valor de *fConcurrency* SQL_CONCUR_ROWVER. O driver converte SQL_KEYSET_SIZE, SQL_CURSOR_DYNAMIC e SQL_CURSOR_KEYSET_DRIVEN para SQL_SCROLL_STATIC com ODBC_01S02 de aviso.  
  
 Para obter mais informações, consulte [SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md) na *referência do programador de ODBC*.
