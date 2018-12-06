---
title: Usar a sessão de system_health | Microsoft Docs
ms.custom: ''
ms.date: 11/27/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], system health session
- extended events [SQL Server], system_health session
- system_health session [SQL Server extended events]
- system health session [SQL Server extended events]
ms.assetid: 1e1fad43-d747-4775-ac0d-c50648e56d78
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ac399872aedca094e6681e2702134ee18d51a6dc
ms.sourcegitcommit: 60739bcb48ccce17bca4e11a85df443e93ca23e3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52439618"
---
# <a name="use-the-systemhealth-session"></a>Usar a sessão de system_health
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

A sessão system_health é uma sessão de Eventos Estendidos, incluída por padrão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa sessão é iniciada automaticamente quando o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] é iniciado e executa sem qualquer efeito notável de desempenho. A sessão coleta dados do sistema que você pode usar para ajudar a solucionar problemas de desempenho no [!INCLUDE[ssDE](../../includes/ssde-md.md)]. 

> [!IMPORTANT]
> Recomendamos que você não interrompa, altere nem exclua a sessão de integridade do sistema.  
  
As informações coletadas pela sessão, incluem:  
  
-   O *sql_text* e a *session_id* de qualquer sessão que encontre um erro tenha uma gravidade >= 20.  
  
-   O *sql_text* e a *session_id* de qualquer sessão que encontre um erro relacionado à memória. Os erros incluem 17803, 701, 802, 8645, 8651, 8657 e 8902.  
  
-   Um registro de qualquer problema de agendador que não esteja respondendo. Esses registros aparecem no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como o erro 17883.  
  
-   Qualquer deadlock detectado, incluindo o gráfico de deadlock.  
  
-   O *callstack*, o *sql_text* e a *session_id* de qualquer sessão que tenha esperado em travas (ou outros recursos interessantes) por >15 segundos.  
  
-   O *callstack*, o *sql_text* e a *session_id* de qualquer sessão que tenha esperado em bloqueios por >30 segundos.  
  
-   A *callstack*, o *sql_text* e a *session_id* de qualquer sessão que tenha esperado por um longo tempo por esperas preemptivas. A duração varia de acordo com o tipo de espera. Uma espera preventiva ocorre quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está esperando por chamadas de API externas.  
  
-   A *callstack* e a *session_id* para alocação de CLR e falhas de alocação virtual.  
  
-   Os eventos de buffer de anel para o agente de memória, monitor de agendador, OOM de nó de memória, segurança e conectividade.  
  
-   Resultados de componente do sistema de `sp_server_diagnostics`.  
  
-   A integridade da instância coletada por *scheduler_monitor_system_health_ring_buffer_recorded*.  
  
-   Falhas de alocação de CLR.  
  
-   Erros de conectividade usando *connectivity_ring_buffer_recorded*.  
  
-   Erros de segurança usando *security_error_ring_buffer_recorded*.  

> [!NOTE]
> Para obter mais informações sobre deadlocks, confira [deadlock no Guia de controle de versão de linha e bloqueio de transação](../../relational-databases/sql-server-transaction-locking-and-row-versioning-guide.md#deadlocks).   
> Para obter mais informações sobre mensagens de erro SQL, confira [Erros do Mecanismo de Banco de Dados](../../relational-databases/errors-events/database-engine-events-and-errors.md).

## <a name="viewing-the-session-data"></a>Exibindo os dados da sessão  
A sessão usa o destino do buffer de anel e o destino de arquivo de evento para armazenar os dados. O destino de arquivo de evento é configurado com um tamanho máximo de 5 MB e uma política de retenção de arquivo de quatro arquivos. 

Para exibir os dados da sessão do destino de buffer de anel com a interface do usuário Eventos Estendidos disponível em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], confira [Exibição avançada de dados de destino de Eventos Estendidos no SQL Server – observar dados dinâmicos](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md#b3-watch-live-data).

Para exibir os dados da sessão do destino de buffer de anel com [!INCLUDE[tsql](../../includes/tsql-md.md)], use a seguinte consulta:  
  
```sql  
SELECT CAST(xet.target_data as xml) 
FROM sys.dm_xe_session_targets xet  
JOIN sys.dm_xe_sessions xe ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'system_health'  
```  
  
Para exibir os dados de sessão do arquivo de evento, use a interface do usuário de eventos estendidos disponível no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, consulte [Exibição avançada de dados de destino dos Eventos Estendidos no SQL Server](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md).
  
## <a name="restoring-the-systemhealth-session"></a>Restaurando a sessão de system_health  
Se você excluir a sessão de system_health, poderá restaurá-la por meio da execução do arquivo **u_tables.sql** no Editor de Consultas. Esse arquivo está localizado na seguinte pasta, em que **C:** representa a unidade em que você instalou os arquivos de programa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e **MSSQL1x** é a versão principal de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
 `C:\Program Files\Microsoft SQL Server\MSSQL1x.\<*instanceid*>\MSSQL\Install`  
  
Saiba que, depois de restaurar a sessão, você deve iniciar a sessão usando a instrução `ALTER EVENT SESSION` ou o nó **Eventos Estendidos** no Pesquisador de Objetos. Caso contrário, a sessão será iniciada automaticamente na próxima vez que você reiniciar o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)    
 [Ferramentas de Eventos Estendidos](../../relational-databases/extended-events/extended-events-tools.md)    
 [Erros do Mecanismo de Banco de Dados](../../relational-databases/errors-events/database-engine-events-and-errors.md)    
 [Exibições de Catálogo de Mensagens (para erros) – sys.messages](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md) 
