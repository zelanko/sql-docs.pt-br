---
title: Integração e transações do CLR | Microsoft Docs
description: Para integração e transações do CLR, System. Transactions e ADO.NET trabalham juntos para estender e simplificar o uso de transações locais e distribuídas em aplicativos gerenciados.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: bd65fce2f2a2bdf2ce25f4811063f7f9d56d2e15
ms.sourcegitcommit: 36fe62a3ccf34979bfde3e192cfa778505add465
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/11/2020
ms.locfileid: "94521109"
---
# <a name="clr-integration-and-transactions"></a>Integração CLR e transações
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  O **System.Transactions** fornece uma estrutura de transação que é totalmente integrada com o ADO.NET e a integração CLR (Common Language Runtime) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . **System. Transactions** e ADO.net trabalham juntos para estender e simplificar o uso de transações locais e distribuídas em aplicativos gerenciados.  
  
> [!NOTE]  
>  Um UDP (user-defined procedure) CLR não pode estabelecer uma conexão com o mesmo servidor no qual está sendo executado (uma conexão de loopback) e se inscrever na mesma transação. Caso uma dessas ações seja tentada, a tentativa de conexão será bloqueada e o controle não será devolvido ao UDP. Isso resultará em um erro de tempo limite (Msg 1206) no UDP.  
  
 Para obter mais informações sobre transações e o .NET Framework, consulte "Performing Transactions" e "Leveraging Transactions" no SDK do .NET Framework.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Promoção de transações](../../relational-databases/clr-integration-data-access-transactions/transaction-promotion.md)  
 Descreve a capacidade de promover transações e como usar este recurso.  
  
 [Acessando a transação atual](../../relational-databases/clr-integration-data-access-transactions/accessing-the-current-transaction.md)  
 Descreve como acessar uma transação que está atualmente sendo executada em processo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Usando System.Transactions](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md)  
 Descreve como usar a API (interface de programação de aplicativo) do **System. Transactions** em seu aplicativo gerenciado.  
  
 [Vidas úteis de transação](../../relational-databases/clr-integration-data-access-transactions/transaction-lifetimes.md)  
 Descreve a diferença no tempo de vida entre transações iniciadas nos procedimentos armazenados [!INCLUDE[tsql](../../includes/tsql-md.md)] e transações iniciadas nos aplicativos de CLR.  
  
## <a name="see-also"></a>Consulte Também  
 [Acesso aos dados dos objetos de banco de dados CLR](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
