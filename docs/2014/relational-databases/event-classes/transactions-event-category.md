---
title: Categoria de evento de transações | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
topic_type:
- apiref
helpviewer_keywords:
- SQL Server event classes, Transactions event category
- event classes [SQL Server], Transactions event category
- Transactions event category [SQL Server]
ms.assetid: bfc75c5b-7115-49d8-9148-a0c84ee66a9a
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8c58f6393cc722eed061e83299bff1e825d47a93
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019812"
---
# <a name="transactions-event-category"></a>Categoria de eventos Transactions
  As classes de evento **Transactions** podem ser usadas para monitorar o status das transações. Os nomes da classe de evento que são predeterminados com **TM:** são usados para rastrear as operações relacionadas à transação que são enviadas pela interface de gerenciamento de transações.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Classe de evento DTCTransaction](dtctransaction-event-class.md)|Rastreia as transações coordenadas pelo MS DTC (Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../includes/msconame-md.md)] ). Essas são transações distribuídas entre dois ou mais bancos de dados ou instâncias do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
|[Classe de evento SQLTransaction](sqltransaction-event-class.md)|Rastreia as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] BEGIN TRAN, COMMIT TRAN, SAVE TRAN e ROLLBACK TRAN.|  
|[Classe de evento TM: Begin Tran Completed](tm-begin-tran-completed-event-class.md)|Indica que uma solicitação BEGIN TRANSACTION foi concluída.|  
|[Classe de evento TM: Begin Tran Starting](tm-begin-tran-starting-event-class.md)|Indica que uma solicitação BEGIN TRANSACTION está iniciando.|  
|[Classe de evento TM: Commit Tran Completed](tm-commit-tran-completed-event-class.md)|Indica que uma solicitação COMMIT TRANSACTION foi concluída.|  
|[Classe de evento TM: Commit Tran Starting](tm-commit-tran-starting-event-class.md)|Indica que uma solicitação COMMIT TRANSACTION está iniciando.|  
|[Classe de evento TM: Promote Tran Completed](tm-promote-tran-completed-event-class.md)|Indica que uma solicitação PROMOTE TRANSACTION foi concluída.|  
|[Classe de evento TM: Promote Tran Starting](tm-promote-tran-starting-event-class.md)|Indica que uma solicitação PROMOTE TRANSACTION está iniciando.|  
|[Classe de evento TM: Rollback Tran Completed](tm-rollback-tran-completed-event-class.md)|Indica que uma solicitação ROLLBACK TRANSACTION foi concluída.|  
|[Classe de evento TM: Rollback Tran Starting](tm-rollback-tran-starting-event-class.md)|Indica que uma solicitação ROLLBACK TRANSACTION está iniciando.|  
|[Classe de evento TM: Save Tran Completed](tm-save-tran-completed-event-class.md)|Indica que uma solicitação SAVE TRANSACTION foi concluída.|  
|[Classe de evento TM: Save Tran Starting](tm-save-tran-starting-event-class.md)|Indica que uma solicitação SAVE TRANSACTION está iniciando.|  
|[Classe de evento TransactionLog](transactionlog-event-class.md)|Rastreia quando as transações são gravadas em um log de transações do banco de dados.|  
  
  