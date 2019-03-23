---
title: Várias transações | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Integration Services], multiple
- multiple transactions
ms.assetid: c3664a94-be89-40c0-a3a0-84b74a7fedbe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b6c66d64d7dc7117c5903f1eb3ac2e2ad97178af
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58378614"
---
# <a name="multiple-transactions"></a>Transações múltiplas
  É possível que um pacote inclua transações não relacionadas em um pacote [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . A qualquer hora que um contêiner no meio de uma hierarquia de contêineres aninhada não oferecer suporte a transações, os contêineres acima ou abaixo da mesma na hierarquia começa a separar as transações, se elas estiverem configuradas para oferecem suporte às transações. As transações confirmam ou revertem na ordem da tarefa interna na hierarquia de contêineres aninhados para o pacote. Entretanto, depois que a transação interna é confirmada, ela não será revertida se uma transação externa for anulada.  
  
## <a name="illustration-of-multiple-transactions"></a>Ilustração de várias transações  
 Por exemplo, um pacote tem um contêiner de Sequência que mantém dois contêineres Loop Foreach, e cada contêiner inclui duas tarefas Executar SQL. O contêiner Sequência oferece suporte a transações, os contêineres Loop Foreach não oferecem e as tarefas Executar SQL oferecem. Nesse exemplo, cada tarefa Executar SQL começaria sua própria transação e não reverteria se a transação da tarefa de Sequência fosse cancelada.  
  
 As propriedades TransactionOption do contêiner Sequência, do contêiner Loop Foreach e das tarefas Executar SQL são definidas da seguinte maneira:  
  
-   As propriedades TransactionOption do contêiner de Sequência está definida como **Obrigatória**.  
  
-   As propriedades TransactionOption dos contêineres Loop Foreach são definidas como **NotSupported**.  
  
-   As propriedades TransactionOption das tarefas Executar SQL são definidas como **Obrigatória**.  
  
 O diagrama a seguir mostra as cinco transações não relacionadas no pacote. Uma transação é iniciada pelo contêiner de Sequência e quatro transações são iniciadas pelas tarefas Executar SQL.  
  
 ![Implementação de transações múltiplas](media/mw-dts-trans2.gif "Implementation of multiple transactions")  
  
## <a name="related-tasks"></a>Related Tasks  
 [Configurar um pacote para usar transações](../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
