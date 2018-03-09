---
title: MSSQLSERVER_1222 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 1222 (Database Engine error)
ms.assetid: c5b1c2f4-f591-4cc1-aa17-204636a27f29
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 743031212890f81073ac39bb617170cc0e4d218e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver1222"></a>MSSQLSERVER_1222
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|1222|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|LK_TIMEOUT|  
|Texto da mensagem|Tempo limite da solicitação de bloqueio excedido.|  
  
## <a name="explanation"></a>Explicação  
Outra transação manteve um bloqueio em um recurso necessário por mais tempo do que esta consulta podia aguardar.  
  
## <a name="user-action"></a>Ação do usuário  
Execute as seguintes tarefas para aliviar o problema:  
  
1.  Localize a transação que está mantendo o bloqueio no recurso necessário, se possível. Use as exibições de gerenciamento dinâmico **sys.dm_os_waiting_tasks** e **sys.dm_tran_locks**.  
  
2.  Se a transação ainda estiver mantendo o bloqueio, termine a transação, se necessário.  
  
3.  Execute a consulta novamente.  
  
Se esse erro ocorrer com frequência, altere o período de tempo limite de bloqueio ou modifique as transações incorretas para que mantenham o bloqueio por menos tempo.  
  
