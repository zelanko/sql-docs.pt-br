---
description: Interoperabilidade de instruções SQL
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 64127e97adf08c3de9f391810a259a3b7045bdc1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476618"
---
# <a name="interoperability-of-sql-statements"></a>Interoperabilidade de instruções SQL
Como o restante de um aplicativo, as instruções SQL podem ser interoperáveis ou específicas do DBMS. E, assim como o restante do aplicativo, a escolha de como as instruções SQL interoperáveis precisam depender do tipo de aplicativo. Os aplicativos personalizados têm menos probabilidade de usar instruções SQL interoperáveis, pois normalmente são projetados para explorar os recursos de um ou possivelmente dois DBMSs. Aplicativos genéricos usam instruções SQL interoperáveis porque são projetados para trabalhar com uma variedade de DBMSs. E os aplicativos verticais geralmente ficam em algum lugar entre eles, exigindo um certo nível de funcionalidade, mas, caso contrário, usam instruções SQL interoperáveis.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Escolher uma gramática SQL](../../../odbc/reference/develop-app/choosing-an-sql-grammar.md)  
  
-   [Construir instruções SQL interoperáveis](../../../odbc/reference/develop-app/constructing-interoperable-sql-statements.md)
