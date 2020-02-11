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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f48a3c7568a9db8b599f6d5a1997607fb16e6020
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069879"
---
# <a name="features-to-watch-for"></a>Recursos a serem inspecionados
Esta seção descreve uma série de recursos que os desenvolvedores de aplicativos geralmente levam para serem concedidos. Na verdade, esses recursos variam amplamente em suporte e modo de suporte entre DBMSs; a falha no código para eles provavelmente causará problemas em aplicativos interoperáveis.  
  
 Esta seção não lista todos os recursos que os desenvolvedores de aplicativos precisam considerar. Para obter essas informações, consulte as descrições da função [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md), [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)e [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) , [Apêndice C: gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)e as seções deste manual que discutem cada recurso.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Número da versão](../../../odbc/reference/develop-app/version-number.md)  
  
-   [Várias instruções e conexões ativas](../../../odbc/reference/develop-app/multiple-active-statements-and-connections.md)  
  
-   [Suporte à transação em DBMSs](../../../odbc/reference/develop-app/transaction-support-in-dbmss.md)  
  
-   [Confirmação e comportamento de reversão](../../../odbc/reference/develop-app/commit-and-rollback-behavior.md)  
  
-   [NOT NULL em instruções CREATE TABLE](../../../odbc/reference/develop-app/not-null-in-create-table-statements.md)  
  
-   [Tipos de dados com suporte](../../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md)  
  
-   [Gramática SQL ODBC](../../../odbc/reference/develop-app/odbc-sql-grammar.md)  
  
-   [Processamento em lote](../../../odbc/reference/develop-app/batch-processing.md)
