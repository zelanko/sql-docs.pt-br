---
title: Recursos a serem observados | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 10fa5df8a47837e92d4215f558d52711a0df3440
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305677"
---
# <a name="features-to-watch-for"></a>Recursos a serem inspecionados
Esta seção descreve uma série de recursos que os desenvolvedores de aplicativos geralmente levam para serem concedidos. Na verdade, esses recursos variam amplamente em suporte e modo de suporte entre DBMSs; a falha no código para eles provavelmente causará problemas em aplicativos interoperáveis.  
  
 Esta seção não lista todos os recursos que os desenvolvedores de aplicativos precisam considerar. Para obter essas informações, consulte as descrições da função [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md), [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)e [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) , [Apêndice C: gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)e as seções deste manual que discutem cada recurso.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Número de versão](../../../odbc/reference/develop-app/version-number.md)  
  
-   [Várias instruções e conexões ativas](../../../odbc/reference/develop-app/multiple-active-statements-and-connections.md)  
  
-   [Suporte à transação em DBMSs](../../../odbc/reference/develop-app/transaction-support-in-dbmss.md)  
  
-   [Confirmação e comportamento de reversão](../../../odbc/reference/develop-app/commit-and-rollback-behavior.md)  
  
-   [NOT NULL em instruções CREATE TABLE](../../../odbc/reference/develop-app/not-null-in-create-table-statements.md)  
  
-   [Tipos de dados com suporte](../../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)  
  
-   [Gramática SQL ODBC](../../../odbc/reference/develop-app/odbc-sql-grammar.md)  
  
-   [Processamento em lotes](../../../odbc/reference/develop-app/batch-processing.md)
