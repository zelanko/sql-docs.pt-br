---
title: Confirmando e Revertendo transações | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c7c028ca7e89378e959b11f59cad4119cef5086a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083315"
---
# <a name="committing-and-rolling-back-transactions"></a>Confirmar e reverter transações
Para confirmar ou reverter uma transação em modo de confirmação manual, um aplicativo chama **SQLEndTran**. Drivers para DBMSs que dão suporte a transações normalmente implementam essa função, executando uma **COMMIT** ou **REVERSÃO** instrução. O Gerenciador de Driver não chama **SQLEndTran** quando a conexão está no modo de confirmação automática; ele simplesmente retorna SQL_SUCCESS, mesmo se o aplicativo tentará reverter a transação. Como os drivers para os que não dão suporte a transações sempre estão no modo de confirmação automática, podem implementar **SQLEndTran** para retornar SQL_SUCCESS sem fazer nada ou não implementá-lo.  
  
> [!NOTE]  
>  Aplicativos não devem confirmar ou reverter transações executando **confirmação** ou **REVERSÃO** instruções com **SQLExecute** ou **SQLExecDirect**. Os efeitos de fazer isso são indefinidos. Problemas possíveis incluem o driver não precisa mais saber quando uma transação está ativa e essas instruções falhando em relação a fontes de dados que não dão suporte a transações. Esses aplicativos devem chamar **SQLEndTran** em vez disso.  
  
 Se o identificador de ambiente para um aplicativo é aprovado **SQLEndTran** mas não passe um identificador de conexão, o Gerenciador de Driver conceitualmente chama **SQLEndTran** com o identificador de ambiente para cada driver que tem uma ou mais conexões ativas no ambiente. O driver, em seguida, confirma as transações em cada conexão no ambiente. No entanto, é importante perceber que o driver e o Gerenciador de Driver executa uma confirmação de duas fases nas conexões no ambiente; Isso é apenas uma conveniência de programação para chamar simultaneamente **SQLEndTran** para todas as conexões no ambiente.  
  
 (Um *2PC* geralmente é usado para confirmar as transações que são distribuídas entre várias fontes de dados. Em sua primeira fase, as fontes de dados de sondagem como se eles podem confirmar sua parte da transação. Na segunda fase, a transação é realmente confirmada em todas as fontes de dados. Se nenhuma fonte de dados de resposta na primeira fase que eles não é possível confirmar a transação, a segunda fase não ocorrerá.)
