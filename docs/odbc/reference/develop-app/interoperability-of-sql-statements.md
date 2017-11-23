---
title: "Interoperabilidade de instruções SQL | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC]
- interoperability of SQL statements [ODBC], about interoperability
ms.assetid: 3b24c499-829c-4e65-90cf-a3a0f6d0a186
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 991208c26beba1167d083785a19c1e64ecaeaba6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="interoperability-of-sql-statements"></a>Interoperabilidade de instruções SQL
Como o restante de um aplicativo, instruções SQL podem ser interoperáveis ou DBMS específico. E como o restante do aplicativo, a escolha de instruções de SQL como interoperáveis precisam ser depende do tipo de aplicativo. Aplicativos personalizados são menos prováveis de usar instruções de SQL interoperáveis porque eles geralmente são projetados para explorar os recursos de um ou dois possivelmente DBMSs. Aplicativos genéricos usam instruções de SQL interoperáveis porque eles são projetados para trabalhar com uma variedade de DBMSs. E aplicativos verticais geralmente se encaixam em algum lugar no meio, exigindo um determinado nível de funcionalidade, mas caso contrário usando interoperáveis instruções de SQL.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Escolhendo uma gramática SQL](../../../odbc/reference/develop-app/choosing-an-sql-grammar.md)  
  
-   [Construindo instruções SQL interoperáveis](../../../odbc/reference/develop-app/constructing-interoperable-sql-statements.md)
