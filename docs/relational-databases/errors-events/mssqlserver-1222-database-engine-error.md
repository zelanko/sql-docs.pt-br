---
title: MSSQLSERVER_1222 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 1222 (Database Engine error)
ms.assetid: c5b1c2f4-f591-4cc1-aa17-204636a27f29
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b1731b81065ab3ab1e4420ff5a9b55719502f1a1
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34318317"
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
  
