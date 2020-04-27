---
title: MSSQLSERVER_1222 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1222 (Database Engine error)
ms.assetid: c5b1c2f4-f591-4cc1-aa17-204636a27f29
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 01325e8d83a5a7d7b65398f4e0cb981b1fca7540
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62915888"
---
# <a name="mssqlserver_1222"></a>MSSQLSERVER_1222
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|1222|  
|Origem do Evento|MSSQLSERVER|  
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
  
  
