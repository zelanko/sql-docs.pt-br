---
title: Integração CLR e transações | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- common language runtime [SQL Server], ADO.NET
- managed code [SQL Server], transactions
- common language runtime [SQL Server], transactions
- System.Transactions namespace
- transactions [CLR integration]
ms.assetid: 381d206e-06e2-48d0-8206-295fcf06ac98
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c6d1b302d6ed0f35ce6fcb60e0afb90415c21d1e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874815"
---
# <a name="clr-integration-and-transactions"></a>Integração CLR e transações
  O `System.Transactions` fornece uma estrutura de transação que é totalmente integrada com o ADO.NET e a integração CLR (Common Language Runtime) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. `System.Transactions` e o ADO.NET operam juntos para estender e simplificar o uso de transações locais e distribuídas nos aplicativos gerenciados.  
  
> [!NOTE]  
>  Um UDP (user-defined procedure) CLR não pode estabelecer uma conexão com o mesmo servidor no qual está sendo executado (uma conexão de loopback) e se inscrever na mesma transação. Caso uma dessas ações seja tentada, a tentativa de conexão será bloqueada e o controle não será devolvido ao UDP. Isso resultará em um erro de tempo limite (Msg 1206) no UDP.  
  
 Para obter mais informações sobre transações e o .NET Framework, consulte "Performing Transactions" e "Leveraging Transactions" no SDK do .NET Framework.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Promoção de transações](transaction-promotion.md)  
 Descreve a capacidade de promover transações e como usar este recurso.  
  
 [Acessando a transação atual](accessing-the-current-transaction.md)  
 Descreve como acessar uma transação que está atualmente sendo executada em processo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Usando System.Transactions](../native-client-ole-db-transactions/transactions.md)  
 Descreve como usar a API (application programming interface) `System.Transactions` em seu aplicativo gerenciado.  
  
 [Tempos de vida de transação](transaction-lifetimes.md)  
 Descreve a diferença no tempo de vida entre transações iniciadas nos procedimentos armazenados [!INCLUDE[tsql](../../includes/tsql-md.md)] e transações iniciadas nos aplicativos de CLR.  
  
## <a name="see-also"></a>Consulte também  
 [Acesso aos dados dos objetos de banco de dados CLR](../clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
