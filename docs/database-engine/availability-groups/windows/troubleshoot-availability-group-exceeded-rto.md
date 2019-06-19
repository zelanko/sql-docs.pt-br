---
title: 'Solução de problemas: o grupo de disponibilidade excedeu o RTO (SQL Server) | Microsoft Docs'
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: e83e4ef8-92f0-406f-bd0b-dc48dc210517
author: rothja
ms.author: jroth
manager: jroth
ms.openlocfilehash: c40755122775faa3b67fb0f46f5f13b3a789bb32
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66803472"
---
# <a name="troubleshoot-availability-group-exceeded-rto"></a>Solução de problemas: o grupo de disponibilidade excedeu o RTO
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Após um failover automático ou um failover manual planejado sem perda de dados em um grupo de disponibilidade, você descobre que o tempo de failover excedeu o RTO (objetivo de tempo de recuperação). Ou, quando você calcula o tempo de failover de uma réplica secundária de confirmação síncrona (como um parceiro de failover automático) usando o método em [Monitorar o desempenho de Grupos de Disponibilidade Always On](monitor-performance-for-always-on-availability-groups.md), você descobre que ele excede o RTO.  
  
 Se o failover automático ainda não foi concluído, veja [Solução de problemas de failover automático em ambientes de Always On do SQL Server 2012](https://support.microsoft.com/kb/2833707).  
  
 As seções a seguir descrevem as causas comuns de um tempo de failover que excede o RTO.  
  
1.  [Carga de trabalho de relatório impede a execução do thread refazer](#BKMK_REDOBLOCK)  
  
2.  [Thread refazer atrasa devido à contenção de recursos](#BKMK_CONTENTION)  
  
##  <a name="BKMK_REDOBLOCK"></a> Carga de trabalho de relatório bloqueia a execução do thread refazer  
 O thread refazer na réplica secundária é impedido de fazer alterações de DDL (linguagem de definição de dados) por uma consulta somente leitura de longa execução.  
  
### <a name="explanation"></a>Explicação  
 Na réplica secundária, as consultas somente leitura adquirem bloqueios de estabilidade de esquema (`Sch-S`). Esses bloqueios `Sch-S` podem impedir o thread refazer de adquirir bloqueios de modificação de esquema (`Sch-M`) para fazer alterações de DDL. Um thread refazer bloqueado não pode aplicar registros de log até que seja desbloqueado. Quando desbloqueado, ele poderá continuar a compensar até o final do log e permitir que o processo de failover e de desfazer subsequentes prossigam.  
  
### <a name="diagnosis-and-resolution"></a>Diagnóstico e resolução  
 Quando o thread refazer é bloqueado, um evento estendido chamado `sqlserver.lock_redo_blocked` é gerado. Além disso, você pode consultar o sys.dm_exec_request do DMV na réplica secundária para descobrir qual sessão está bloqueando o thread REDO e, em seguida, tomar uma ação corretiva. A consulta a seguir retorna a ID da sessão da consulta somente leitura que está bloqueando o thread refazer.  
  
```sql  
select session_id, command, blocking_session_id, wait_time, wait_type, wait_resource   
from sys.dm_exec_requests where command = 'DB STARTUP'  
```  
  
 Você pode permitir que a carga de trabalho de relatório seja concluída, momento em que o thread refazer é desbloqueado, ou pode desbloquear imediatamente o thread refazer executando o comando [KILL &#40;Transact-SQL&#41;](~/t-sql/language-elements/kill-transact-sql.md) na ID de sessão que está bloqueando.  
  
##  <a name="BKMK_CONTENTION"></a> Thread refazer atrasa devido à contenção de recursos  
 Uma grande carga de trabalho de relatório na réplica secundária reduziu o desempenho da réplica secundária, e o thread refazer atrasou.  
  
### <a name="explanation"></a>Explicação  
 Ao aplicar registros de log na réplica secundária, o thread refazer lê os registros de log no disco de log e, em seguida, para cada registro de log, ele acessa as páginas de dados para aplicar o registro de log. O acesso à página poderá ser associado a E/S (acessando o disco físico) se a página ainda não estiver no pool de buffers. Se houver carga de trabalho de relatório associada a E/S, a carga de trabalho de relatório concorrerá, em termos de recursos de E/S, com o thread refazer e poderá causar lentidão nesse thread.  
  
### <a name="diagnosis-and-resolution"></a>Diagnóstico e resolução  
 Você pode usar a seguinte consulta DMV para ver quanto o thread refazer atrasou, medindo a diferença entre a lacuna entre `last_redone_lsn` e `last_received_lsn`.  
  
```sql  
select recovery_lsn, truncation_lsn, last_hardened_lsn, last_received_lsn,   
   last_redone_lsn, last_redone_time  
from sys.dm_hadr_database_replica_states  
  
```  
  
 Se o thread refazer estiver realmente atrasado, será necessário investigar a causa raiz da degradação do desempenho na réplica secundária. Se houver uma contenção de E/S com a carga de trabalho de relatório, você poderá usar o [Resource Governor](~/relational-databases/resource-governor/resource-governor.md) para controlar os ciclos de CPU que são usados pela carga de trabalho de relatório para controlar indiretamente os ciclos de E/S executados, até certo ponto. Por exemplo, se sua carga de trabalho de relatório estiver consumindo 10% da CPU, mas a carga de trabalho estiver associada a E/S, você poderá usar o Resource Governor para limitar o uso de recursos de CPU a 5% a fim de limitar a carga de trabalho de leitura, minimizando o impacto na E/S.  
  
## <a name="next-steps"></a>Próximas etapas  
 [Solução de problemas de desempenho no SQL Server (aplica-se ao SQL Server 2012)](https://msdn.microsoft.com/library/dd672789(v=SQL.100).aspx)  
  
  
