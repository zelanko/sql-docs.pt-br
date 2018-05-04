---
title: Confirmação e o comportamento de reversão | Microsoft Docs
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
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 2ac8f012-e46d-41ca-81bb-e4a3246e3241
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 54dc518099d55193efa502887c9b89308d40b75f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="commit-and-rollback-behavior"></a>Confirmação e o comportamento de reversão
É um comportamento comum entre o servidor DBMSs fechar cursores e descartar instruções preparadas quando uma instrução é confirmada ou revertida. Bancos de dados de área de trabalho têm mais probabilidade de mantém os cursores abertos e mantenha as instruções preparadas. Para obter mais informações, consulte as opções SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR no [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrição da função e [efeito de transações em cursores e instruções preparadas](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).
