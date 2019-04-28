---
title: Excluir um rastreamento (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], deleting
- removing traces
- deleting traces
ms.assetid: a5502814-b281-42dd-b885-5c9368025ae6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 57d80824ab0dde301a0b96239636cf0f79ca032c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62714734"
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
  
  
