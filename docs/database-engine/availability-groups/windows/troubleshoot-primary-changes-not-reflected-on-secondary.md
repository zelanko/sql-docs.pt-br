---
title: As alterações não são visíveis na réplica do grupo de disponibilidade secundário
ms.description: Troubleshoot to determine why changes occurring on a primary replica are not reflected on the secondary replica for an Always On availability group.
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: c602fd39-db93-4717-8f3a-5a98b940f9cc
author: rothja
ms.author: jroth
ms.openlocfilehash: 55dc6787960fbb4979bbe0d21f27f0fa43437662
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75243008"
---
# <a name="determine-why-changes-from-primary-replica-are-not-reflected-on-secondary-replica-for-an-always-on-availability-group"></a>Determine por que as alterações da réplica primária não são refletidas na réplica secundária de um Grupo de Disponibilidade AlwaysOn
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O aplicativo cliente conclui uma atualização na réplica primária com êxito, mas uma consulta à réplica secundária mostra que a alteração não foi refletida. Esse caso presume que sua disponibilidade está com um estado de sincronização íntegro. Na maioria dos casos, esse comportamento se resolve após alguns minutos.  
  
 Se as alterações ainda não estiverem refletidas na réplica secundária depois de alguns minutos, poderá haver um gargalo no fluxo de trabalho de sincronização. O local do gargalo depende de se a réplica secundária está definida como confirmação síncrona ou confirmação assíncrona.  
  
 **Confirmação síncrona**  
  
 Cada atualização bem-sucedida na réplica primária já foi sincronizada com a réplica secundária, ou os registros de log já foram liberados para proteção na réplica secundária. Portanto, o gargalo deve estar no processo da fase refazer, que acontece depois que o log é liberado na réplica secundária.  
  
 No entanto, assim que a fase refazer é compensada, todas as cargas de trabalho de leitura da réplica secundária são consultas de isolamento de instantâneo:  
  
  -   Transações de longa execução na réplica primária  
  
  -   Fase refazer na réplica secundária  


**Confirmação assíncrona**  
 
 A confirmação assíncrona reconhece uma transação assim que ela é liberada para o disco local, por isso, o gargalo pode estar em qualquer lugar após esse ponto:  
 
  -   Transações de longa execução na réplica primária  
  
  -   Latência ou taxa de transferência de rede  
  
  -   Proteção de log na réplica secundária  
  
  -   Fase refazer na réplica secundária  


As seções a seguir descrevem as causas comuns porque as alterações na réplica primária não são refletidas na réplica secundária em consultas somente leitura.  


##  <a name="BKMK_OLDTRANS"></a> Transações ativas de longa execução  
 Uma transação de longa execução na réplica primária impede que as atualizações sejam lidas na réplica secundária.  
  
### <a name="explanation"></a>Explicação  
 Todas as cargas de trabalho de leitura na réplica secundária são consultas de isolamento de instantâneo. No isolamento de instantâneo, os clientes somente leitura veem o banco de dados de disponibilidade na réplica secundária no ponto de início da transação ativa mais antiga no log da operação de refazer. Se uma transação não for confirmada em algumas horas, a transação aberta impedirá todas as consultas somente leitura de ver as novas atualizações.  
  
### <a name="diagnosis-and-resolution"></a>Diagnóstico e resolução  
 Na réplica primária, use [DBCC OPENTRAN &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-opentran-transact-sql.md) para exibir as transações ativas mais antigas e ver se elas podem ser revertidas. Depois que as transações ativas mais antigas são revertidas e sincronizadas com a réplica secundária, as cargas de trabalho de leitura na réplica secundária podem ver as atualizações no banco de dados de disponibilidade até o início da transação ativa mais antiga até então.  
  
##  <a name="BKMK_LATENCY"></a> Alta latência da rede ou baixa taxa de transferência de rede causa o acúmulo de log na réplica primária  
 A alta latência ou baixa taxa de transferência da rede pode impedir que os logs sejam enviados à réplica secundária com a rapidez necessária.  
  
### <a name="explanation"></a>Explicação  
 A réplica primária ativa o controle de fluxo no envio de log quando ele excede o número máximo permitido de mensagens não confirmadas enviadas para a réplica secundária. Até que algumas dessas mensagens sejam confirmadas, não será possível enviar mais logs para a réplica secundária. Essa situação poderá ter um impacto mais sério na potencial perda de dados, possivelmente prejudicando seu RPO Objetivo de ponto de recuperação).  
  
### <a name="diagnosis-and-resolution"></a>Diagnóstico e resolução  
 Um valor alto de DMV, [log_send_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md), pode indicar logs sendo retidos na réplica primária. A divisão desse valor por [log_send_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) poderá fornecer uma estimativa aproximada de quanto tempo levará para os dados serem compensados na réplica secundária.  
  
 Além disso, ele é útil para verificar se os dois objetos de desempenho [SQL Server:Availability Replica > Tempo de controle de fluxo (ms/s)](~/relational-databases/performance-monitor/sql-server-availability-replica.md) e [SQL Server:Availability Replica > Controle de fluxo/s](~/relational-databases/performance-monitor/sql-server-availability-replica.md). A multiplicação desses dois valores mostra quanto tempo, no último segundo, foi gasto aguardando a limpeza do controle de fluxo. Quanto maior o tempo de espera do controle de fluxo, menor será a taxa de envio.  
  
 Abaixo está uma lista de métricas úteis no diagnóstico de taxa de transferência e latência de rede. Você pode usar outras ferramentas do Windows, como **ping.exe** para avaliar a utilização de rede.  
  
-   DMV [log_send_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)  
  
-   DMV [log_send_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)  
  
-   Contador de desempenho `SQL Server:Database > Log Bytes Flushed/sec`  
  
-   Contador de desempenho `SQL Server:Database Mirroring > Send/Receive Ack Time`  
  
-   Contador de desempenho `SQL Server:Availability Replica > Bytes Sent to Replica/sec`  
  
-   Contador de desempenho `SQL Server:Availability Replica > Bytes Sent to Transport/sec`  
  
-   Contador de desempenho `SQL Server:Availability Replica > Flow Control Time (ms/sec)`  
  
-   Contador de desempenho `SQL Server:Availability Replica > Flow Control/sec`  
  
-   Contador de desempenho `SQL Server:Availability Replica > Resent Messages/sec`  
  
 Para corrigir esse problema, tente atualizar a largura de banda da sua rede ou remover ou reduzir o tráfego de rede desnecessário.  
  
##  <a name="BKMK_REDOBLOCK"></a> Outra carga de trabalho de relatório impede a execução do thread refazer  
 O thread refazer na réplica secundária é impedido de fazer alterações de DDL (linguagem de definição de dados) por uma consulta somente leitura de longa execução. O thread refazer deve ser desbloqueado antes de poder fazer novas atualizações disponíveis para cargas de trabalho de leitura.  
  
### <a name="explanation"></a>Explicação  
 Na réplica secundária, as consultas somente leitura adquirem bloqueios de estabilidade de esquema (`Sch-S`). Esses bloqueios `Sch-S` podem impedir o thread refazer de adquirir bloqueios de modificação de esquema (`Sch-M`) para fazer alterações de DDL. Um thread refazer bloqueado não pode aplicar registros de log até que seja desbloqueado.  
  
### <a name="diagnosis-and-resolution"></a>Diagnóstico e resolução  
 Quando o thread refazer é bloqueado, um evento estendido chamado `sqlserver.lock_redo_blocked` é gerado. Além disso, você pode consultar o sys.dm_exec_request do DMV na réplica secundária para descobrir qual sessão está bloqueando o thread REDO e, em seguida, tomar uma ação corretiva. A consulta a seguir retorna a ID de sessão da carga de trabalho de relatório que está bloqueando o thread refazer.  
  
```sql  
select session_id, command, blocking_session_id, wait_time, wait_type, wait_resource   
from sys.dm_exec_requests where command = 'DB STARTUP'  
```  
  
 Você pode permitir que a carga de trabalho de relatório seja concluída, momento em que o thread refazer é desbloqueado, ou pode desbloquear imediatamente o thread refazer executando o comando [KILL &#40;Transact-SQL&#41;](~/t-sql/language-elements/kill-transact-sql.md) na ID de sessão que está bloqueando.  
  
##  <a name="BKMK_REDOBEHIND"></a> Thread refazer atrasa devido à contenção de recursos  
 Uma grande carga de trabalho de relatório na réplica secundária reduziu o desempenho da réplica secundária, e o thread refazer atrasou.  
  
### <a name="explanation"></a>Explicação  
 Ao aplicar registros de log na réplica secundária, o thread refazer lê os registros de log no disco de log e, em seguida, para cada registro de log, ele acessa as páginas de dados para aplicar o registro de log. O acesso à página poderá ser associado a E/S (acessando o disco físico) se a página ainda não estiver no pool de buffers. Se houver carga de trabalho de relatório associada a E/S, a carga de trabalho de relatório concorrerá, em termos de recursos de E/S, com o thread refazer e poderá causar lentidão nesse thread. Essa situação não apenas afeta outras cargas de trabalho de relatório ao ver dados atualizados, mas também afeta o RTO.  
  
### <a name="diagnosis-and-resolution"></a>Diagnóstico e resolução  
 Você pode usar a seguinte consulta DMV para ver quanto o thread refazer atrasou, medindo a diferença entre a lacuna entre `last_redone_lsn` e `last_received_lsn`.  
  
```sql  
select recovery_lsn, truncation_lsn, last_hardened_lsn, last_received_lsn,   
   last_redone_lsn, last_redone_time  
from sys.dm_hadr_database_replica_states  
  
```  
  
 Se o thread refazer estiver realmente atrasado, será necessário investigar a causa raiz da degradação do desempenho na réplica secundária. Se houver uma contenção de E/S com a carga de trabalho de relatório, você poderá usar o [Resource Governor](~/relational-databases/resource-governor/resource-governor.md) para controlar os ciclos de CPU que são usados pela carga de trabalho de relatório para controlar indiretamente os ciclos de E/S executados, até certo ponto. Por exemplo, se sua carga de trabalho de relatório estiver consumindo 10% da CPU, mas a carga de trabalho estiver associada a E/S, você poderá usar o Resource Governor para limitar o uso de recursos de CPU a 5% a fim de limitar a carga de trabalho de leitura, minimizando o impacto na E/S.  
  
## <a name="next-steps"></a>Próximas etapas  
 [Solução de problemas de desempenho no SQL Server 2008](https://msdn.microsoft.com/library/dd672789(v=sql.100).aspx) 
  
  
