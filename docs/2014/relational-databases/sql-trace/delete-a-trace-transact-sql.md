---
title: Excluir um rastreamento (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], deleting
- removing traces
- deleting traces
ms.assetid: a5502814-b281-42dd-b885-5c9368025ae6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1262232a7fdc42c443f624aca8334dce1e48a3f9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48055646"
---
# <a name="delete-a-trace-transact-sql"></a>Excluir um rastreamento (Transact-SQL)
  Este tópico descreve como usar procedimentos armazenados para excluir um rastreamento.  
  
 Para obter um exemplo de como usar procedimentos armazenados de rastreamento, veja [Criar um rastreamento &#40;Transact-SQL&#41;](create-a-trace-transact-sql.md).  
  
### <a name="to-delete-a-trace"></a>Para excluir um rastreamento  
  
1.  Execute **sp_trace_setstatus** especificando **@status = 0** para interromper o rastreamento.  
  
2.  Execute **sp_trace_setstatus** especificando **@status = 2** para encerrar o rastreamento e excluir suas informações do servidor.  
  
> [!NOTE]  
>  Um rastreamento deve ser interrompido primeiro antes de ser encerrado.  
  
## <a name="see-also"></a>Consulte também  
 [sp_trace_setstatus &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)   
 [Procedimentos armazenados do SQL Server Profiler &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)  
  
  
