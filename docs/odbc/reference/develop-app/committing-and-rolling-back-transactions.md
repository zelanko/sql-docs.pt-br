---
title: Cometendo e revertendo transações | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299106"
---
# <a name="committing-and-rolling-back-transactions"></a>Confirmar e reverter transações
Para cometer ou reverter uma transação no modo de confirmação manual, um aplicativo chama **SQLEndTran**. Drivers para DBMSs que suportam transações normalmente implementam essa função executando uma declaração **COMMIT** ou **ROLLBACK.** O Driver Manager não chama **SQLEndTran** quando a conexão está no modo de confirmação automática; ele simplesmente retorna SQL_SUCCESS, mesmo que o aplicativo tente reverter a transação. Como os drivers para DBMSs que não suportam transações estão sempre no modo de confirmação automática, eles podem implementar **o SQLEndTran** para retornar SQL_SUCCESS sem fazer nada ou não implementá-lo.  
  
> [!NOTE]  
>  Os aplicativos não devem cometer ou reverter transações executando demonstrações **COMMIT** ou **ROLLBACK** com **SQLExecute** ou **SQLExecDirect**. Os efeitos de fazer isso são indefinidos. Os possíveis problemas incluem o driver não saber mais quando uma transação está ativa e essas declarações falharem contra fontes de dados que não suportam transações. Esses aplicativos devem chamar **sqlendtran** em vez disso.  
  
 Se um aplicativo passar a alça do ambiente para **o SQLEndTran,** mas não passar uma alça de conexão, o Driver Manager chama conceitualmente **o SQLEndTran** com a alça do ambiente para cada driver que tenha uma ou mais conexões ativas no ambiente. Em seguida, o motorista comete as transações em cada conexão no ambiente. No entanto, é importante perceber que nem o motorista nem o Driver Manager realizam um compromisso bifásico sobre as conexões no ambiente; esta é apenas uma conveniência de programação para chamar simultaneamente **SQLEndTran** para todas as conexões no ambiente.  
  
 (Um *compromisso em duas fases* é geralmente usado para cometer transações que são espalhadas por várias fontes de dados. Em sua primeira fase, as fontes de dados são pesquisadas sobre se podem cometer sua parte na transação. Na segunda fase, a transação é realmente comprometida em todas as fontes de dados. Se alguma fonte de dados responder na primeira fase que não pode cometer a transação, a segunda fase não ocorrerá.)
