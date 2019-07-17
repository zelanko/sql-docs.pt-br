---
title: Interoperabilidade de instruções SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC]
- interoperability of SQL statements [ODBC], about interoperability
ms.assetid: 3b24c499-829c-4e65-90cf-a3a0f6d0a186
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ed366acde11778342387d3bcb152a6619a6a3778
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138874"
---
# <a name="interoperability-of-sql-statements"></a>Interoperabilidade de instruções SQL
Como o restante de um aplicativo, as instruções SQL podem ser interoperável ou específicos de DBMS. E como o restante do aplicativo, a escolha de instruções de SQL como interoperáveis precisam ser depende do tipo de aplicativo. Aplicativos personalizados são menos prováveis usar instruções de SQL interoperáveis porque eles geralmente são projetados para explorar os recursos de um ou dois possivelmente DBMSs. Aplicativos genéricos usam instruções de SQL interoperáveis porque eles são projetados para trabalhar com uma variedade de DBMSs. E aplicativos verticais geralmente se encaixam em algum lugar entre os dois, exigindo um certo nível de funcionalidade, mas caso contrário, usando as instruções de SQL interoperáveis.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Escolhendo uma gramática SQL](../../../odbc/reference/develop-app/choosing-an-sql-grammar.md)  
  
-   [Construindo instruções SQL interoperáveis](../../../odbc/reference/develop-app/constructing-interoperable-sql-statements.md)
