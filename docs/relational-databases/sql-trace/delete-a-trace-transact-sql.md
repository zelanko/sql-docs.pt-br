---
title: Excluir um rastreamento (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], deleting
- removing traces
- deleting traces
ms.assetid: a5502814-b281-42dd-b885-5c9368025ae6
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5d9eb3c4aeafab2fb6337da5d0bb24c3f4d3b8f7
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="delete-a-trace-transact-sql"></a>Excluir um rastreamento (Transact-SQL)
  Este tópico descreve como usar procedimentos armazenados para excluir um rastreamento.  
  
 Para obter um exemplo de como usar procedimentos armazenados de rastreamento, veja [Criar um rastreamento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md).  
  
### <a name="to-delete-a-trace"></a>Para excluir um rastreamento  
  
1.  Execute **sp_trace_setstatus** especificando **@status = 0** para interromper o rastreamento.  
  
2.  Execute **sp_trace_setstatus** especificando **@status = 2** para encerrar o rastreamento e excluir suas informações do servidor.  
  
> [!NOTE]  
>  Um rastreamento deve ser interrompido primeiro antes de ser encerrado.  
  
## <a name="see-also"></a>Consulte também  
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do SQL Server Profiler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  
