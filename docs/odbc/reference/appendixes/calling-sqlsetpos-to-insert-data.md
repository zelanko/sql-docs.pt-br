---
title: Chamando SQLSetPos para inserir dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], inserting data
- backward compatibility [ODBC], SqlSetPos
ms.assetid: 03e5c4d0-2bb3-4649-9781-89cab73f78eb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cb374b2506d55b400207c8f60bdf42bb6bb4065e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306597"
---
# <a name="calling-sqlsetpos-to-insert-data"></a>Chamar SQLSetPos para inserir dados
Quando um aplicativo ODBC *2.x* que trabalha com um driver ODBC *3.x* chama **SQLSetPos** com um argumento de *operação* de SQL_ADD, o Driver Manager não mapeia essa chamada para **SQLBulkOperations**. Se um driver ODBC *3.x* trabalhar com um aplicativo que chama **SQLSetPos** com SQL_ADD, o driver deve suportar essa operação.  
  
 Uma grande diferença de comportamento quando **SQLSetPos** é chamado de SQL_ADD ocorre quando é chamado no estado S6. No ODBC *2.x,* o driver retornou s1010 quando **SQLSetPos** foi chamado com SQL_ADD no estado S6 (após o cursor ter sido posicionado com **SQLFetch**). No ODBC *3.x,* **a SQLBulkOperations** com uma *Operação* de SQL_ADD pode ser chamada no estado S6. Uma segunda grande diferença de comportamento é que **as Operações SQLBulk** com uma *Operação* de SQL_ADD podem ser chamadas no estado S5, enquanto **sQLSetPos** com uma **Operação** de SQL_ADD não podem. Para as transições de declaração que podem ocorrer para a mesma chamada em ODBC *3.x*, consulte [Apêndice B: Tabelas de Transição do Estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
