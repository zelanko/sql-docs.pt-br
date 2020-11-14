---
description: Efeito de transações em cursores e instruções preparadas
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 495bb8455c3e13b88d2d3ae6b400c5c0f2167604
ms.sourcegitcommit: 0f484f32709a414f05562bbaafeca9a9fc57c9ed
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2020
ms.locfileid: "94631672"
---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>Efeito de transações em cursores e instruções preparadas
A confirmação ou reversão de uma transação tem um dos seguintes efeitos em cursores e planos de acesso:  
  
-   Todos os cursores são fechados e os planos de acesso para instruções preparadas nessa conexão são excluídos ou  
  
-   Todos os cursores são fechados e os planos de acesso para instruções preparadas na conexão permanecem intactos ou 
  
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
