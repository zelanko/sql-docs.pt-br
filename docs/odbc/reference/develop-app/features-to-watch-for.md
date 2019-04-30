---
title: Recursos a serem inspecionados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], writing interoperable applications
ms.assetid: 0fb1693b-11c3-43b1-bb16-c3323b7b2d45
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fe5bce7a8a13c7296ce08f84ea4b0c60c2eb5261
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061604"
---
# <a name="features-to-watch-for"></a>Recursos a serem inspecionados
Esta seção descreve uma série de recursos que os desenvolvedores de aplicativos muitas vezes, considera natural. Na verdade, esses recursos variam muito em forma de suporte entre DBMSs; e suporte Falha ao código para que eles provavelmente causar problemas em aplicativos interoperáveis.  
  
 Esta seção não lista todos os recursos que os desenvolvedores de aplicativos precisam considerar. Para obter essas informações, consulte o [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md), [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md), e [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) função descrições, [apêndice c: Gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)e as seções que abordam cada recurso deste manual.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Número de versão](../../../odbc/reference/develop-app/version-number.md)  
  
-   [Várias instruções e conexões ativas](../../../odbc/reference/develop-app/multiple-active-statements-and-connections.md)  
  
-   [Suporte à transação em DBMSs](../../../odbc/reference/develop-app/transaction-support-in-dbmss.md)  
  
-   [Confirmação e comportamento de reversão](../../../odbc/reference/develop-app/commit-and-rollback-behavior.md)  
  
-   [NOT NULL em instruções CREATE TABLE](../../../odbc/reference/develop-app/not-null-in-create-table-statements.md)  
  
-   [Tipos de dados com suporte](../../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)  
  
-   [Gramática SQL ODBC](../../../odbc/reference/develop-app/odbc-sql-grammar.md)  
  
-   [Processamento em lotes](../../../odbc/reference/develop-app/batch-processing.md)
