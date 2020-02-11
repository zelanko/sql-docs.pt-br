---
title: Comportamento de confirmação e reversão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 2ac8f012-e46d-41ca-81bb-e4a3246e3241
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 643d7d4174df66abfcee274c1f987e8f405d19b9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083339"
---
# <a name="commit-and-rollback-behavior"></a>Confirmação e comportamento de reversão
Um comportamento comum entre DBMSs de servidor é fechar cursores e descartar instruções preparadas quando uma instrução for confirmada ou revertida. Os bancos de dados de desktop têm mais probabilidade de manter os cursores abertos e manter as instruções preparadas. Para obter mais informações, consulte as opções SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR na descrição da função [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) e o [efeito das transações em cursores e instruções](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)preparadas.
