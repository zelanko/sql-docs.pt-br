---
title: Fechar o Cursor | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ODBC], closing
- closing cursors [ODBC]
ms.assetid: 4f19bf5e-6d8c-40ae-a975-cfd62a0790ec
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 05cf8dde95111a9f5b530b37fd9a60356f4b77bf
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="closing-the-cursor"></a>Fechar o Cursor
Quando um aplicativo terminar de usar um cursor, ele chama **SQLCloseCursor** para fechar o cursor. Por exemplo:  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 Até que o aplicativo fecha o cursor, a instrução na qual o cursor é aberto não pode ser usada para a maioria das outras operações, como executar outra instrução SQL. Para obter uma lista completa de funções que podem ser chamados enquanto o cursor estiver aberto, consulte [tabelas de transição de estado do apêndice b: ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
> [!NOTE]  
>  Para fechar um cursor, um aplicativo deve chamar **SQLCloseCursor**, não **SQLCancel**.  
  
 Os cursores permanecem abertos até que eles forem explicitamente fechados, exceto quando uma transação é confirmada ou revertida, caso em que algumas fontes de dados fechar o cursor. Em particular, se atingir o final do resultado definido, quando **SQLFetch** retorna SQL_NO_DATA, não fechar um cursor. Cursores mesmo em conjuntos de resultados vazios (conjuntos de resultados criados quando uma instrução executada com êxito, mas que não retornou nenhuma linha) devem ser explicitamente fechados.
