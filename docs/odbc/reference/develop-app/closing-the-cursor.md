---
title: Fechando o Cursor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], closing
- closing cursors [ODBC]
ms.assetid: 4f19bf5e-6d8c-40ae-a975-cfd62a0790ec
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 632a922abb544a379892dfa168f55efd605304c8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63125432"
---
# <a name="closing-the-cursor"></a>Fechar o cursor
Quando um aplicativo tiver terminado de usar um cursor, ele chama **SQLCloseCursor** para fechar o cursor. Por exemplo:   
  
```  
SQLCloseCursor(hstmt);  
```  
  
 Até que o aplicativo fecha o cursor, a instrução na qual o cursor é aberto não pode ser usada para a maioria das outras operações, como executar outra instrução SQL. Para obter uma lista completa de funções que podem ser chamados enquanto o cursor estiver aberto, consulte [apêndice b: Tabelas de transição de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
> [!NOTE]  
>  Para fechar um cursor, um aplicativo deve chamar **SQLCloseCursor**, e não **SQLCancel**.  
  
 Cursores permanecem abertos até que eles forem explicitamente fechados, exceto quando uma transação é confirmada ou revertida, caso em que algumas fontes de dados fechar o cursor. Em particular, chegando ao fim do resultado definido, quando **SQLFetch** retorna SQL_NO_DATA, não fechar um cursor. Cursores até mesmo em conjuntos de resultados vazios (conjuntos de resultados criados quando uma instrução executada com êxito, mas que não retornou nenhuma linha) devem ser explicitamente fechados.
