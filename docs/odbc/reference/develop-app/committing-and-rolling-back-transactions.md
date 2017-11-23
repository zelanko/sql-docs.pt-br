---
title: "Confirmação e reversão de transações | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- transactions [ODBC], committing
ms.assetid: 800f2c1a-6f79-4ed1-830b-aa1a62ff5165
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5ddf51903e3c6f8f58be1ccf0fcf5f037e4adb8c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="committing-and-rolling-back-transactions"></a>Confirmação e reversão de transações
Para confirmar ou reverter uma transação em modo de confirmação manual, um aplicativo chama **SQLEndTran**. Drivers para os que oferecem suporte a transações normalmente implementam essa função executando um **confirmar** ou **REVERSÃO** instrução. O Gerenciador de Driver não chama **SQLEndTran** quando a conexão estiver no modo de confirmação automática; ele simplesmente retorna SQL_SUCCESS, mesmo se o aplicativo tentar reverter a transação. Como os drivers para os que não oferecem suporte a transações sempre estão no modo de confirmação automática, eles podem ou implementar **SQLEndTran** retorna SQL_SUCCESS sem fazer nada ou não implementá-la.  
  
> [!NOTE]  
>  Aplicativos não devem confirmar ou reverter transações executando **confirmação** ou **REVERSÃO** instruções com **SQLExecute** ou **SQLExecDirect**. Os efeitos de fazer isso são indefinidos. Problemas possíveis incluem essas instruções falhando em relação a fontes de dados que não oferecem suporte a transações e o driver não saber quando uma transação está ativa. Esses aplicativos devem chamar **SQLEndTran** em vez disso.  
  
 Se um aplicativo passa o identificador de ambiente para **SQLEndTran** mas não passe um identificador de conexão, o Gerenciador de Driver conceitualmente chama **SQLEndTran** com o identificador de ambiente para cada driver que tem uma ou mais conexões ativas no ambiente. O driver, em seguida, confirma as transações em cada conexão no ambiente. No entanto, é importante observar que o driver e o Gerenciador de Driver realiza uma confirmação de duas fases nas conexões no ambiente; Isso é apenas uma conveniência programação simultaneamente chamar **SQLEndTran** para todas as conexões no ambiente.  
  
 (Um *2PC* geralmente é usado para confirmar transações que são distribuídas entre várias fontes de dados. Em sua primeira fase, as fontes de dados são sondadas quanto se elas podem ser confirmadas sua parte da transação. Na segunda fase, a transação é realmente confirmada em todas as fontes de dados. Se as fontes de dados de resposta na primeira etapa que eles não é possível confirmar a transação, a segunda fase não ocorrerá.)
