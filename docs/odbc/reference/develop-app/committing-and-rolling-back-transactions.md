---
title: Confirmando e revertendo transações | Microsoft Docs
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
- transactions [ODBC], committing
ms.assetid: 800f2c1a-6f79-4ed1-830b-aa1a62ff5165
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1c272d60242d31622452c4dcb0f6a16c4838768f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299106"
---
# <a name="committing-and-rolling-back-transactions"></a>Confirmar e reverter transações
Para confirmar ou reverter uma transação no modo de confirmação manual, um aplicativo chama **SQLEndTran**. Os drivers para DBMSs que dão suporte a transações normalmente implementam essa função executando uma instrução **Commit** ou **Rollback** . O Gerenciador de driver não chama **SQLEndTran** quando a conexão está no modo de confirmação automática; Ele simplesmente retorna SQL_SUCCESS, mesmo se o aplicativo tentar reverter a transação. Como os drivers para DBMSs que não dão suporte a transações estão sempre no modo de confirmação automática, eles podem implementar **SQLEndTran** para retornar SQL_SUCCESS sem fazer nada ou não implementá-lo.  
  
> [!NOTE]  
>  Os aplicativos não devem confirmar ou reverter transações executando instruções **Commit** ou **Rollback** com **SQLExecute** ou **SQLExecDirect**. Os efeitos dessa ação são indefinidos. Possíveis problemas incluem o driver que não está mais sabendo quando uma transação está ativa e essas instruções falham em fontes de dados que não dão suporte a transações. Esses aplicativos devem chamar **SQLEndTran** em vez disso.  
  
 Se um aplicativo passar o identificador de ambiente para **SQLEndTran** , mas não passar um identificador de conexão, o Gerenciador de driver chamará conceitualmente **SQLEndTran** com o identificador de ambiente para cada driver que tenha uma ou mais conexões ativas no ambiente. O driver então confirma as transações em cada conexão no ambiente. No entanto, é importante perceber que nem o driver nem o Gerenciador de driver executa uma confirmação de duas fases nas conexões no ambiente; Essa é meramente uma conveniência de programação para chamar simultaneamente **SQLEndTran** para todas as conexões no ambiente.  
  
 (Uma *confirmação de duas fases* geralmente é usada para confirmar as transações que são distribuídas por várias fontes de dados. Em sua primeira fase, as fontes de dados são sondadas quanto à possibilidade de confirmarem sua parte da transação. Na segunda fase, a transação é realmente confirmada em todas as fontes de dados. Se qualquer fonte de dados responder na primeira fase que não puder confirmar a transação, a segunda fase não ocorrerá.)
