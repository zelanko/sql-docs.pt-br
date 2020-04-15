---
title: Efeito das Transações em Cursors e Declarações Preparadas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- cursors [ODBC], transaction commits or roll backs
- prepared statements [ODBC]
- transactions [ODBC], cursors
ms.assetid: 523e22a2-7b53-4c25-97c1-ef0284aec76e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ef3cb4095410b8ccb03b0a138f65b8df2cfb1a4b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300466"
---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>Efeito de transações em cursores e instruções preparadas
Cometer ou reverter uma transação tem o seguinte efeito sobre cursores e planos de acesso:  
  
-   Todos os cursores estão fechados e os planos de acesso para declarações preparadas sobre essa conexão são excluídos.  
  
-   Todos os cursores estão fechados, e os planos de acesso para declarações preparadas sobre essa conexão permanecem intactos.  
  
-   Todos os cursores permanecem abertos, e os planos de acesso para declarações preparadas sobre essa conexão permanecem intactos.  
  
 Por exemplo, suponha que uma fonte de dados exiba o primeiro comportamento desta lista, o mais restritivo desses comportamentos. Agora suponha que um aplicativo faça o seguinte:  
  
1.  Define o modo de confirmação como compromisso manual.  
  
2.  Cria um conjunto de resultados de ordens de venda no comunicado 1.  
  
3.  Cria um conjunto de resultados das linhas em uma ordem de venda na declaração 2, quando o usuário destaca essa ordem.  
  
4.  Chama **sqlExecute** para executar uma declaração de atualização posicionada que foi preparada na declaração 3, quando o usuário atualiza uma linha.  
  
5.  Chama **o SQLEndTran** para comprometer a declaração de atualização posicionada.  
  
 Devido ao comportamento da fonte de dados, a chamada para **o SQLEndTran** na etapa 5 faz com que ele feche os cursores nas declarações 1 e 2 e exclua o plano de acesso em todas as declarações. O aplicativo deve reexecutar as instruções 1 e 2 para recriar os conjuntos de resultados e repreparar a instrução na declaração 3.  
  
 No modo de confirmação automática, funções diferentes **do SQLEndTran** confirmam transações:  
  
-   **SQLExecute** ou **SQLExecDirect** No exemplo anterior, a chamada para **SQLExecute** na etapa 4 compromete uma transação. Isso faz com que a fonte de dados feche os cursores nas declarações 1 e 2 e exclua o plano de acesso em todas as declarações sobre essa conexão.  
  
-   **SQLBulkOperations** ou **SQLSetPos** No exemplo anterior, suponha que na etapa 4 o aplicativo chame **SQLSetPos** com a opção SQL_UPDATE na declaração 2, em vez de executar uma declaração de atualização posicionada na declaração 3. Isso compromete uma transação e faz com que a fonte de dados feche os cursores nas declarações 1 e 2, e descarta todos os planos de acesso nessa conexão.  
  
-   **SQLCloseCursor** No exemplo anterior, suponha que quando o usuário destaca uma ordem de venda diferente, o aplicativo chama **sqlCloseCursor** na declaração 2 antes de criar um resultado das linhas para a nova ordem de venda. A chamada para **sqlCloseCursor** compromete a declaração **SELECT** que criou o conjunto de linhas de resultado e faz com que a fonte de dados feche o cursor na declaração 1 e, em seguida, descarte todos os planos de acesso nessa conexão.  
  
 Os aplicativos, especialmente os aplicativos baseados em tela, nos quais o usuário rola ao redor do conjunto de resultados e atualiza ou exclui linhas, devem ter cuidado para codificar esse comportamento.  
  
 Para determinar como uma fonte de dados se comporta quando uma transação é cometida ou revertida, um aplicativo chama **o SQLGetInfo** com as opções de SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR.
