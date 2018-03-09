---
title: "Integração CLR e transações | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- common language runtime [SQL Server], ADO.NET
- managed code [SQL Server], transactions
- common language runtime [SQL Server], transactions
- System.Transactions namespace
- transactions [CLR integration]
ms.assetid: 381d206e-06e2-48d0-8206-295fcf06ac98
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b6975d640f1c65c945337432d18fa2bfbc03e971
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="clr-integration-and-transactions"></a>Integração CLR e transações
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
O **System.Transactions** fornece uma estrutura de transação que é totalmente integrada com o ADO.NET e a integração CLR (Common Language Runtime) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . **System. Transactions** e o ADO.NET operam juntos para estender e simplificar o uso de transações locais e distribuídas nos aplicativos gerenciados.  
  
> [!NOTE]  
>  Um UDP (user-defined procedure) CLR não pode estabelecer uma conexão com o mesmo servidor no qual está sendo executado (uma conexão de loopback) e se inscrever na mesma transação. Caso uma dessas ações seja tentada, a tentativa de conexão será bloqueada e o controle não será devolvido ao UDP. Isso resultará em um erro de tempo limite (Msg 1206) no UDP.  
  
 Para obter mais informações sobre transações e o .NET Framework, consulte "Performing Transactions" e "Leveraging Transactions" no SDK do .NET Framework.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Promoção de transações](../../relational-databases/clr-integration-data-access-transactions/transaction-promotion.md)  
 Descreve a capacidade de promover transações e como usar este recurso.  
  
 [Acessando a transação atual](../../relational-databases/clr-integration-data-access-transactions/accessing-the-current-transaction.md)  
 Descreve como acessar uma transação que está atualmente sendo executada em processo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Usando System.Transactions](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md)  
 Descreve como usar o **System. Transactions** interface de programação de aplicativo (API) em seu aplicativo gerenciado.  
  
 [Tempos de vida de transação](../../relational-databases/clr-integration-data-access-transactions/transaction-lifetimes.md)  
 Descreve a diferença no tempo de vida entre transações iniciadas nos procedimentos armazenados [!INCLUDE[tsql](../../includes/tsql-md.md)] e transações iniciadas nos aplicativos de CLR.  
  
## <a name="see-also"></a>Consulte também  
 [Acesso aos dados dos objetos de banco de dados CLR](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
