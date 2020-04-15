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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 723e40e6d83eed84ed93ee1eeab3535622ad5f04
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299136"
---
# <a name="closing-the-cursor"></a>Fechar o cursor
Quando um aplicativo termina usando um cursor, ele chama **sqlCloseCursor** para fechar o cursor. Por exemplo:  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 Até que o aplicativo feche o cursor, a declaração na qual o cursor é aberto não pode ser usada para a maioria das outras operações, como a execução de outra declaração SQL. Para obter uma lista completa de funções que podem ser chamadas enquanto um cursor está aberto, consulte [apêndice B: Tabelas de transição do estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
> [!NOTE]  
>  Para fechar um cursor, um aplicativo deve chamar **SQLCloseCursor**, não **SQLCancel**.  
  
 Os cursors permanecem abertos até que sejam explicitamente fechados, exceto quando uma transação é cometida ou revertida, nesse caso algumas fontes de dados fecham o cursor. Em particular, chegar ao final do conjunto de resultados, quando **o SQLFetch** retorna SQL_NO_DATA, não fecha um cursor. Mesmo os cursores em conjuntos de resultados vazios (conjuntos de resultados criados quando uma instrução executada com sucesso, mas que não retornou linhas) devem ser explicitamente fechados.
