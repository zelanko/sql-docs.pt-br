---
title: MSSQLSERVER_17300 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17300 (Database Engine error)
ms.assetid: c1d6bfb6-28af-4df6-8087-25807602d282
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1d6b4f7cdabc8688fda5ad21cc40e6c5f11fa39e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68131656"
---
# <a name="mssqlserver_17300"></a>MSSQLSERVER_17300
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|17300|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PROC_OUT_OF_SYSTASK_SESSIONS|  
|Texto da mensagem|O SQL Server não pôde executar uma nova tarefa do sistema, porque não há memória suficiente ou o número de sessões configuradas excede o máximo permitido no servidor. Verifique se o servidor tem memória suficiente. Use sp_configure com a opção 'conexões de usuário' para verificar o número de máximo de conexões de usuário permitidas. Use sys.dm_exec_sessions para verificar o número atual de sessões, inclusive processos de usuário.|  
  
## <a name="explanation"></a>Explicação  
Uma tentativa de executar uma nova tarefa do sistema falhou devido à memória insuficiente ou porque o número de sessões configuradas no servidor foi excedido.  
  
## <a name="user-action"></a>Ação do usuário  
Verifique se o servidor tem memória suficiente. Verifique o número atual de tarefas do sistema usando sys.dm_exec_sessions e verifique o valor configurado de máximo de conexões do usuário usando sp_configure.  
  
Execute as seguintes tarefas, conforme apropriado:  
  
-   Adicione mais memória ao servidor.  
  
-   Termine uma ou mais sessões.  
  
-   Aumente o número de máximo de conexões do usuário permitido no servidor.  
  
## <a name="see-also"></a>Consulte Também  
[sp_configure &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
[Opções de configuração do servidor &#40;SQL Server&#41;](~/database-engine/configure-windows/server-configuration-options-sql-server.md)  
[sys.dm_exec_sessions &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
[Configurar a opção user connections de configuração do servidor](~/database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md)  
[KILL &#40;Transact-SQL&#41;](~/t-sql/language-elements/kill-transact-sql.md)  
  
