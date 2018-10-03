---
title: Reproduzir um Script Transact-SQL (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- scripts [SQL Server], traces
- replaying traces
ms.assetid: 9c0eb222-e6e3-4bc1-a25f-a41e962d361b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b7fe14bf583c04165566ad99f278b82a34ca8e2f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48162406"
---
# <a name="replay-a-transact-sql-script-sql-server-profiler"></a>Repetir um script Transact-SQL (SQL Server Profiler)
  Ao testar possíveis soluções para um problema de desempenho, use o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para repetir scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] e compare o desempenho antes e depois das alterações.  
  
### <a name="to-replay-a-transact-sql-script"></a>Para repetir um script Transact-SQL  
  
1.  No menu **Arquivo** , aponte para **Abrir**e clique em **Arquivo de Script**.  
  
2.  Selecione o arquivo de script [!INCLUDE[tsql](../../includes/tsql-md.md)] que deseja abrir. Certifique-se de que o script [!INCLUDE[tsql](../../includes/tsql-md.md)] contenha os eventos necessários para a repetição. Para obter mais informações, consulte [Replay Requirements](replay-requirements.md).  
  
3.  No menu **Repetir** , clique em **Iniciar**e conecte-se ao servidor em que deseja repetir o script.  
  
4.  Na caixa de diálogo **Configuração de Repetição** , verifique as definições e clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Repetir rastreamentos](replay-traces.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
