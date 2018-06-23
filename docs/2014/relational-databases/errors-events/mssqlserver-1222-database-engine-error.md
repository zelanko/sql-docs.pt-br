---
title: MSSQLSERVER_1222 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 1222 (Database Engine error)
ms.assetid: c5b1c2f4-f591-4cc1-aa17-204636a27f29
caps.latest.revision: 19
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 850d4bc168be2cbbf602b3fc6ebb4e317245de7c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019179"
---
# <a name="mssqlserver1222"></a>MSSQLSERVER_1222
    
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
  
  