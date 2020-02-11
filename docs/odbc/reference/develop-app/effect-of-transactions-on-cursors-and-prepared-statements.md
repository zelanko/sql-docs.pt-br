---
title: Efeito de transações em cursores e instruções preparadas | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 83b693922d08f7298d0c5282fe2c7d1c20149d5b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046885"
---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>Efeito de transações em cursores e instruções preparadas
A confirmação ou reversão de uma transação tem o seguinte efeito em cursores e planos de acesso:  
  
-   Todos os cursores são fechados e os planos de acesso para instruções preparadas nessa conexão são excluídos.  
  
-   Todos os cursores são fechados e os planos de acesso para instruções preparadas nessa conexão permanecem intactos.  
  
-   Todos os cursores permanecem abertos e os planos de acesso para instruções preparadas na conexão permanecem intactos.  
  
 Por exemplo, suponha que uma fonte de dados exiba o primeiro comportamento nessa lista, o mais restritivo desses comportamentos. Agora suponha que um aplicativo faça o seguinte:  
  
1.  Define o modo de confirmação como confirmação manual.  
  
2.  Cria um conjunto de resultados de pedidos de vendas na instrução 1.  
  
3.  Cria um conjunto de resultados das linhas em uma ordem de venda na instrução 2, quando o usuário realça esse pedido.  
  
4.  Chama **SQLExecute** para executar uma instrução UPDATE posicionada que foi preparada na instrução 3, quando o usuário atualiza uma linha.  
  
5.  Chama **SQLEndTran** para confirmar a instrução UPDATE posicionada.  
  
 Devido ao comportamento da fonte de dados, a chamada para **SQLEndTran** na etapa 5 faz com que ele feche os cursores nas instruções 1 e 2 e exclua o plano de acesso em todas as instruções. O aplicativo deve executar novamente as instruções 1 e 2 para recriar os conjuntos de resultados e repreparar a instrução na instrução 3.  
  
 No modo de confirmação automática, funções diferentes de **SQLEndTran** transações de confirmação:  
  
-   **SQLExecute** ou **SQLExecDirect** no exemplo anterior, a chamada para **SQLExecute** na etapa 4 confirma uma transação. Isso faz com que a fonte de dados feche os cursores nas instruções 1 e 2 e exclua o plano de acesso em todas as instruções nessa conexão.  
  
-   **SQLBulkOperations** ou **SQLSetPos** no exemplo anterior, suponhamos que, na etapa 4, o aplicativo chame **SQLSetPos** com a opção SQL_UPDATE na instrução 2, em vez de executar uma instrução UPDATE posicionada na instrução 3. Isso confirma uma transação e faz com que a fonte de dados feche os cursores nas instruções 1 e 2 e descarta todos os planos de acesso nessa conexão.  
  
-   **SQLCloseCursor** No exemplo anterior, suponha que, quando o usuário realça uma ordem de venda diferente, o aplicativo chama **SQLCloseCursor** na instrução 2 antes de criar um resultado das linhas para a nova ordem de venda. A chamada para **SQLCloseCursor** confirma a instrução **Select** que criou o conjunto de resultados de linhas e faz com que a fonte de dados feche o cursor na instrução 1 e, em seguida, descarta todos os planos de acesso nessa conexão.  
  
 Aplicativos, especialmente aplicativos baseados em tela, nos quais o usuário rola em volta do conjunto de resultados e atualiza ou exclui linhas, devem ter cuidado ao codificar esse comportamento.  
  
 Para determinar como uma fonte de dados se comporta quando uma transação é confirmada ou revertida, um aplicativo chama **SQLGetInfo** com as opções SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR.
