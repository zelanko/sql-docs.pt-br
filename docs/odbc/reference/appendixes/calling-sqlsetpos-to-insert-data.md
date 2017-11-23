---
title: Chamar SQLSetPos para inserir dados | Microsoft Docs
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
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], inserting data
- backward compatibility [ODBC], SqlSetPos
ms.assetid: 03e5c4d0-2bb3-4649-9781-89cab73f78eb
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4d7693d4072ec27264112b6cca0d79f413aa3b21
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="calling-sqlsetpos-to-insert-data"></a>Chamar SQLSetPos para inserir dados
Quando um ODBC 2. *x* aplicativo trabalhando com um ODBC 3*. x* driver chama **SQLSetPos** com um *operação* argumento de SQL_ADD, o Gerenciador de Driver não é mapeado para essa chamada para **SQLBulkOperations**. Se um ODBC 3*. x* driver deve funcionar com um aplicativo que chama **SQLSetPos** com SQL_ADD, o driver deve dar suporte a essa operação.  
  
 Uma grande diferença no comportamento quando **SQLSetPos** é chamado com SQL_ADD ocorre quando ele é chamado no estado S6. No ODBC 2. *x*, o driver retornou S1010 quando **SQLSetPos** foi chamado com SQL_ADD no estado S6 (após o cursor tiver sido posicionado com **SQLFetch**). Em ODBC 3*. x*, **SQLBulkOperations** com um *operação* de SQL_ADD pode ser chamado no estado S6. A principal diferença no comportamento a segunda é que **SQLBulkOperations** com um *operação* de SQL_ADD pode ser chamado no estado S5, enquanto **SQLSetPos** com um  **Operação** de SQL_ADD não é possível. Para as transições de instrução que podem ocorrer com a mesma chamada em ODBC 3*. x*, consulte [tabelas de transição de estado do apêndice b: ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
