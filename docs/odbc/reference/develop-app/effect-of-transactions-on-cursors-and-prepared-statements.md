---
title: Efeito de transações em cursores e instruções preparadas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- cursors [ODBC], transaction commits or roll backs
- prepared statements [ODBC]
- transactions [ODBC], cursors
ms.assetid: 523e22a2-7b53-4c25-97c1-ef0284aec76e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ceb7aaae6967376c454d32633cda6043bc281825
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>Efeito de transações em cursores e instruções preparadas
Confirmar ou reverter uma transação tem o seguinte efeito em cursores e planos de acesso:  
  
-   Todos os cursores são fechados e planos de acesso para instruções preparadas nessa conexão são excluídos.  
  
-   Todos os cursores são fechados e planos de acesso para instruções preparadas nessa conexão permanecem intactos.  
  
-   Todos os cursores permanecem abertos e planos de acesso para instruções preparadas nessa conexão permanecem intactos.  
  
 Por exemplo, suponha que uma fonte de dados exibe o comportamento primeiro na lista, o mais restritivo desses comportamentos. Agora suponha que um aplicativo faz o seguinte:  
  
1.  Define o modo de confirmação para confirmação manual.  
  
2.  Cria um conjunto de resultados de ordens de venda na instrução 1.  
  
3.  Cria um conjunto de resultados das linhas em uma ordem de venda na instrução 2, quando o usuário realça a ordem.  
  
4.  Chamadas **SQLExecute** para executar uma instrução de atualização posicionada que foi preparada na instrução 3, quando o usuário atualiza uma linha.  
  
5.  Chamadas **SQLEndTran** para confirmar a instrução update posicionadas.  
  
 Por causa de comportamento da fonte de dados, a chamada para **SQLEndTran** na etapa 5 faz com que ele para fechar cursores em instruções 1 e 2 e para excluir o plano de acesso em todas as instruções. O aplicativo deve executar novamente os conjuntos de instruções 1 e 2 para recriar o resultado e reprepare a instrução na instrução 3.  
  
 No modo de confirmação automática, diferente de funções **SQLEndTran** confirmar transações:  
  
-   **SQLExecute** ou **SQLExecDirect** no exemplo anterior, a chamada para **SQLExecute** na etapa 4 confirma uma transação. Isso faz com que a fonte de dados fechar os cursores em instruções 1 e 2 e excluir o plano de acesso em todas as instruções nessa conexão.  
  
-   **SQLBulkOperations** ou **SQLSetPos** no exemplo anterior, suponha que, na etapa 4 o aplicativo chama **SQLSetPos** com a opção de SQL_UPDATE na instrução 2, em vez de executar um instrução de atualização posicionada na instrução 3. Isso confirma uma transação e faz com que a fonte de dados fechar cursores em instruções 1 e 2 e descarta todos os planos de acesso dessa conexão.  
  
-   **SQLCloseCursor** no exemplo anterior, suponha que quando o usuário realça um pedido de vendas diferente, o aplicativo chama **SQLCloseCursor** na instrução 2 antes de criar um resultado das linhas para as vendas de novo ordem. A chamada para **SQLCloseCursor** confirma o **selecione** instrução que criou o conjunto de resultados de linhas e faz com que a fonte de dados fechar o cursor na instrução 1 e, em seguida, descarta todos os planos de acesso em que conexão.  
  
 Aplicativos, especialmente em tela em que o usuário rola em todo o conjunto de resultados e as atualizações ou exclui as linhas, devem ter cuidadosos ao código alternativa para esse comportamento.  
  
 Para determinar como uma fonte de dados se comporta quando uma transação é confirmada ou revertida, um aplicativo chama **SQLGetInfo** com as opções SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR.
