---
title: Usar a sessão de system_health | Microsoft Docs
ms.custom: ''
ms.date: 06/25/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: xevents
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- extended events [SQL Server], system health session
- extended events [SQL Server], system_health session
- system_health session [SQL Server extended events]
- system health session [SQL Server extended events]
ms.assetid: 1e1fad43-d747-4775-ac0d-c50648e56d78
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 57bdc59b3b5db69fdf01737b0a850725e9b17f88
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="use-the-systemhealth-session"></a>Usar a sessão de system_health
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  A sessão system_health é uma sessão de Eventos Estendidos, incluída por padrão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa sessão é iniciada automaticamente quando o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] é iniciado e executa sem qualquer efeito notável de desempenho. A sessão coleta dados do sistema que você pode usar para ajudar a solucionar problemas de desempenho no [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Portanto, é recomendável não interromper ou excluir a sessão.  
  
 As informações coletadas pela sessão, incluem:  
  
-   O sql_text e o session_id de qualquer sessão que encontre um erro tenha uma severidade >= 20.  
  
-   O sql_text e o session_id de qualquer sessão que encontre um erro relacionado à memória. Os erros incluem 17803, 701, 802, 8645, 8651, 8657 e 8902.  
  
-   Um registro de qualquer problema de agendador que não esteja respondendo. (Esses registros aparecem no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como o erro 17883.)  
  
-   Qualquer deadlock que tenha sido detectado.  
  
-   O callstack, o sql_text e o session_id de qualquer sessão que teve esperas em travas (ou outros recursos interessantes) por > 15 segundos.  
  
-   O callstack, o sql_text e o session_id de qualquer sessão que teve esperas em travas por > 30 segundos.  
  
-   O callstack, o sql_text e o session_id de qualquer sessão que teve esperas em travas por muito tempo por esperas preemptivas. A duração varia de acordo com o tipo de espera. Uma espera preventiva ocorre quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está esperando por chamadas de API externas.  
  
-   A pilha de chamadas e a session_id para alocação de CLR e falhas de alocação virtual.  
  
-   Os eventos de ring_buffer para o agente de memória, monitor de agendador, OOM de nó de memória, segurança e conectividade.  
  
-   Resultados de componente de sistema de sp_server_diagnostics.  
  
-   A integridade da instância coletada por scheduler_monitor_system_health_ring_buffer_recorded.  
  
-   Falhas de alocação de CLR.  
  
-   Erros de conectividade usando connectivity_ring_buffer_recorded.  
  
-   Erros de segurança usando security_error_ring_buffer_recorded.  
  
## <a name="viewing-the-session-data"></a>Exibindo os dados da sessão  
 A sessão usa o destino do buffer de anéis para armazenar os dados. Para exibir os dados da sessão, use a consulta a seguir:  
  
```  
SELECT CAST(xet.target_data as xml) FROM sys.dm_xe_session_targets xet  
JOIN sys.dm_xe_sessions xe  
ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'system_health'  
```  
  
Para visualizar os dados de sessão do arquivo de evento, use a interface de usuário de eventos estendidos disponível no Management Studio. Para obter mais informações, consulte [Exibição avançada de dados de destino dos Eventos Estendidos no SQL Server](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md).
  
## <a name="restoring-the-systemhealth-session"></a>Restaurando a sessão de system_health  
 Se você excluir a sessão de system_health, poderá restaurá-la por meio da execução do arquivo **u_tables.sql** no Editor de Consultas. Esse arquivo está localizado na pasta seguinte, onde C: representa a unidade onde você instalou os arquivos de programa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
 C:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.\<*instanceid*>\MSSQL\Install  
  
 Lembre-se de que, depois de restaurar a sessão, você deve iniciá-la com a instrução ALTER EVENT SESSION ou usando o nó **Eventos Estendidos** no Pesquisador de Objetos. Caso contrário, a sessão será iniciada automaticamente na próxima vez que você reiniciar o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Ferramentas de eventos estendidos](../../relational-databases/extended-events/extended-events-tools.md)  
  
  
