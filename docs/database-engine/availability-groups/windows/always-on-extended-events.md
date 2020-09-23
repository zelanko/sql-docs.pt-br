---
title: Configurar eventos estendidos para grupos de disponibilidade
description: O SQL Server define eventos estendidos que são específicos aos Grupos de Disponibilidade AlwaysOn. Você pode monitorar esses eventos estendidos em uma sessão para ajudar no diagnóstico da causa raiz ao solucionar problemas de um grupo de disponibilidade.
ms.custom: ag-guide, seodec18
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
ms.assetid: 5950f98a-3950-473d-95fd-cde3557b8fc2
author: rothja
ms.author: jroth
ms.openlocfilehash: 3a5b2f339f5aec4d97daaee9ac273dd73833d564
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91115847"
---
# <a name="configure-extended-events-for-always-on-availability-groups"></a>Configurar eventos estendidos para Grupos de Disponibilidade AlwaysOn
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  O SQL Server define eventos estendidos que são específicos aos Grupos de Disponibilidade AlwaysOn. Você pode monitorar esses eventos estendidos em uma sessão para ajudar no diagnóstico da causa raiz ao solucionar problemas de um grupo de disponibilidade. Você pode exibir os eventos estendidos do grupo de disponibilidade usando a seguinte consulta:  
  
```sql  
SELECT * FROM sys.dm_xe_objects WHERE name LIKE '%hadr%'  
```  
   
##  <a name="alwayson_health-session"></a><a name="BKMK_alwayson_health"></a> Sessão Alwayson_health  
 A sessão de eventos estendidos alwayson_health é criada automaticamente quando você cria o grupo de disponibilidade e captura um subconjunto dos eventos relacionados do grupo de disponibilidade. Esta sessão é pré-configurada como uma ferramenta útil e conveniente para ajudá-lo a começar rapidamente ao solucionar problemas de um grupo de disponibilidade. O assistente Criar grupo de disponibilidade inicia automaticamente a sessão em cada réplica de disponibilidade participante configurada no assistente.  
  
> [!IMPORTANT]  
>  Se você não criou o grupo de disponibilidade usando o **assistente Novo Grupo de Disponibilidade**, a sessão alwayson_health poderá não ser iniciada automaticamente. Se a sessão não for iniciada, não será possível capturar dados de evento quando ocorrer um problema inesperado. Você deverá iniciar a sessão manualmente e configurá-la para iniciar automaticamente por meio das propriedades da sessão.  
  
 Para exibir a definição da sessão alwayson_health:  
  
1.  No **Pesquisador de Objetos**, expanda **Gerenciamento**, **Eventos Estendidos** e, em seguida, **Sessões**.  
  
2.  Clique com o botão direito do mouse em **Alwayson_health**, aponte para **sessão de Script como**, aponte para **Criar Para** e, em seguida, clique em **Janela do Editor de Nova Consulta**.  

Para obter informações sobre alguns dos eventos cobertos pelo alwayson_health, veja a [referência de eventos estendidos](always-on-extended-events.md#BKMK_Reference).  


##  <a name="extended-events-for-debugging"></a><a name="BKMK_Debugging"></a> Eventos estendidos para depuração  
 Além dos eventos estendidos cobertos pela sessão Alwayson_health, o SQL Server define um amplo conjunto de eventos de depuração para grupos de disponibilidade. Para aproveitar esses eventos estendidos adicionais em uma sessão, siga os procedimentos abaixo:  
  
1.  No **Pesquisador de Objetos**, expanda **Gerenciamento**, **Eventos Estendidos** e, em seguida, **Sessões**.  
  
2.  Clique com o botão direito do mouse em **Sessões** e selecione **Nova Sessão**. Ou clique com o botão direito do mouse em **Alwayson_health** e selecione **Propriedades**.  
  
3.  No painel **Selecionar uma página**, clique em **Eventos**.  
  
4.  Na biblioteca de eventos, na coluna **Categoria**, selecione **alwayson** e desmarque todas as outras categorias.  
  
5.  Na coluna **Canal**, selecione **Depurar**. Todos os eventos relacionados a grupos de disponibilidade que ainda não estiverem selecionados agora aparecerão na biblioteca de eventos.  
  
6.  Realce um evento na biblioteca de eventos e, em seguida, clique no botão **>** para selecioná-lo para a sessão.  
  
7.  Ao terminar a sessão, clique em **OK** para fechá-la. Verifique se a sessão foi iniciada para capturar os eventos que você selecionou.  
  
##  <a name="always-on-availability-groups-extended-events-reference"></a><a name="BKMK_Reference"></a> Referência de eventos estendidos de Grupos de Disponibilidade Always On  
 Esta seção descreve alguns dos eventos estendidos que são usados para monitorar os grupos de disponibilidade.  
  
 [availability_replica_state_change](#BKMK_availability_replica_state_change)  
  
 [availability_group_lease_expired](#BKMK_availability_group_lease_expired)  
  
 [availability_replica_automatic_failover_validation](#BKMK_availability_replica_automatic_failover_validation)  
  
 [error_reported (vários números de erro): para problemas de conexão ou transporte](#BKMK_error_reported)  
  
 [data_movement_suspend_resume](#BKMK_data_movement_suspend_resume)  
  
 [alwayson_ddl_executed](#BKMK_alwayson_ddl_executed)  
  
 [availability_replica_manager_state](#BKMK_availability_replica_manager_state)  
  
 [error_reported (1480): Alteração da função de réplica de banco de dados](#BKMK_error_reported_1480)  
  
###  <a name="availability_replica_state_change"></a><a name="BKMK_availability_replica_state_change"></a> availability_replica_state_change  
 Ocorre quando o estado de uma réplica de disponibilidade foi alterado. A criação de um grupo de disponibilidade ou a junção de uma réplica de disponibilidade pode disparar esse evento. É útil para o diagnóstico de failover automático com falha. Ele também pode ser usado para rastrear as etapas de failover.  
  
#### <a name="event-information"></a>Informações de evento  
  
|Coluna|Descrição|  
|------------|-----------------|  
|Nome|availability_replica_state_change|  
|Categoria|always on|  
|Canal|Operacional|  
  
#### <a name="event-fields"></a>Campos de evento  
  
|Nome|Type_name|Descrição|  
|----------|----------------|-----------------|  
|availability_group_id|guid|A ID do Grupo de Disponibilidade.|  
|availability_group_name|unicode_string|O nome do Grupo de Disponibilidade.|  
|availability_replica_id|guid|A ID da Réplica de Disponibilidade.|  
|previous_state|availability_replica_state|A função da réplica antes da alteração.<br /><br /> **Os valores possíveis são:**<br /><br /> Primary_Normal<br /><br /> Secondary_Normal<br /><br /> Resolving_Pending_Failover<br /><br /> Resolving_Normal<br /><br /> Primary_Pending<br /><br /> Not_Available|  
|current_state|availability_replica_state|A função da réplica após a alteração.<br /><br /> **Os valores possíveis são:**<br /><br /> Primary_Normal<br /><br /> Secondary_Normal<br /><br /> Resolving_Pending_Failover<br /><br /> Resolving_Normal<br /><br /> Primary_Pending<br /><br /> Not_Available|  
  
#### <a name="alwayson_health-session-definition"></a>Definição de sessão alwayson_health  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
ADD EVENT availability_replica_state_change  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="availability_group_lease_expired"></a><a name="BKMK_availability_group_lease_expired"></a> availability_group_lease_expired  
 Ocorre quando o cluster e o grupo de disponibilidade têm um problema de conectividade e o tempo de concessão expirou. Esse evento indica que a conectividade entre o grupo de disponibilidade e o cluster WSFC subjacente foi interrompida. Se o problema de conectividade ocorrer na réplica primária, o evento poderá causar um failover automático ou fazer com que o grupo de disponibilidade fique offline.  
  
#### <a name="event-information"></a>Informações de evento  
  
|Coluna|Descrição|  
|------------|-----------------|  
|Nome|availability_group_lease_expired|  
|Categoria|always on|  
|Canal|Operacional|  
  
#### <a name="event-fields"></a>Campos de evento  
  
|Nome|Type_name|Descrição|  
|----------|----------------|-----------------|  
|availability_group_id|guid|A ID do grupo de disponibilidade.|  
|availability_group_name|unicode_string|O nome do grupo de disponibilidade.|  
  
#### <a name="alwayson_health-session-definition"></a>Definição de sessão alwayson_health  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
ADD EVENT availability_group_lease_expired  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="availability_replica_automatic_failover_validation"></a><a name="BKMK_availability_replica_automatic_failover_validation"></a> availability_replica_automatic_failover_validation  
 Ocorre quando o failover automático valida a preparação de uma réplica de disponibilidade como uma réplica primária e mostra se a réplica de disponibilidade de destino está pronta para ser a nova réplica primária. Por exemplo, a validação de failover retornará falso se nem todos os bancos de dados estiverem sincronizados ou não estiverem unidos. Esse evento foi projetado para fornecer um ponto de falha durante failovers. Essas informações são de interesse do administrador de banco de dados, especialmente em casos de failovers automáticos, pois um failover automático é uma operação autônoma. O administrador de banco de dados pode examinar o evento para ver por que um failover automático falhou.  
  
#### <a name="event-information"></a>Informações de evento  
  
|Nome|Descrição|  
|----------|-----------------|  
|availability_replica_automatic _failover_validation||  
|Categoria|always on|  
|Canal|Analítico|  
  
#### <a name="event-fields"></a>Campos de evento  
  
|Nome|Type_name|Descrição|  
|----------|----------------|-----------------|  
|availability_group_id|guid|A ID do grupo de disponibilidade.|  
|availability_group_name|unicode_string|O nome do grupo de disponibilidade.|  
|availability_replica_id|guid|A ID da réplica de disponibilidade.|  
|forced_quorum|validation_result_type|Se o valor for TRUE, o failover automático será invalidado nesta réplica de disponibilidade.<br /><br /> TRUE<br /><br /> FALSE|  
|joined_and_synchronized|validation_result_type|Se o valor for FALSE, o failover automático será invalidado nesta réplica de disponibilidade.<br /><br /> TRUE<br /><br /> FALSE|  
|previous_primary_or_automatic_failover_target|validation_result_type|Se o valor for FALSE, o failover automático será invalidado nesta réplica de disponibilidade.<br /><br /> TRUE<br /><br /> FALSE|  
  
#### <a name="alwayson_health-session-definition"></a>Definição de sessão alwayson_health  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
  
ADD EVENT availability_replica_automatic_failover_validation (  
WHERE (  
[forced_quorum]=(TRUE) OR [joined_and_synchronized]=(FALSE) OR [previous_primary_or_automatic_failover_target]=(TRUE)  
)  
)  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
  
```  
  
###  <a name="error_reported-multiple-error-numbers-for-transport-or-connection-issues"></a><a name="BKMK_error_reported"></a> error_reported (vários números de erro): para problemas de conexão ou transporte  
 Cada evento filtrado indica que um problema de conectividade ocorreu no transporte ou no ponto de extremidade de espelhamento de banco de dados do qual esse grupo de disponibilidade depende.  
  
|Coluna|Descrição|  
|------------|-----------------|  
|Nome|error_reported<br /><br /> números a serem filtrados: 35201, 35202, 35206, 35204, 35207, 9642, 9666, 9691, 9692, 9693, 28034, 28036, 28080, 28091, 33309|  
|Categoria|erros|  
|Canal|Admin|  
  
#### <a name="error-numbers-to-filter"></a>Números de erro a serem filtrados  
  
|Número do erro|Descrição|  
|------------------|-----------------|  
|35201|Ocorreu um tempo limite de conexão ao tentar estabelecer uma conexão com a réplica de disponibilidade '%ls'.|  
|35202|Uma conexão com o grupo de disponibilidade '%ls' da réplica de disponibilidade '%ls' com a ID [%ls] para '%ls' com a ID [%ls] foi estabelecida com êxito.  Essa mensagem é apenas informativa. Não é necessária nenhuma ação do usuário.|  
|35206|Ocorreu um tempo limite de conexão em uma conexão estabelecida anteriormente com a réplica de disponibilidade '%ls'.|  
|35204|A conexão entre as instâncias '%ls' e '%ls' foi desabilitada devido ao desligamento do ponto de extremidade.|  
|Tempo limite + conectado|  
|35207|A tentativa de conexão no grupo de disponibilidade ID '%ls' da ID de réplica '%ls' para a ID de réplica '%ls' falhou devido ao erro %d, à gravidade %d e o estado %d.  gravidade %d estado %d. (essa conexão pode não ser adequada para uso DBA. Verifique e remova mais tarde, neste caso)|  
|9642|Erro em um ponto de extremidade de conexão de transporte do Service Broker/Espelhamento de Banco de Dados. Erro: %i. Estado: %i. (Função do ponto de extremidade próximo: %S_MSG, endereço do ponto de extremidade distante: '%.*hs') Erro: %i Estado: %i. (Função do ponto de extremidade próximo: %S_MSG, endereço do ponto de extremidade distante: '%.\*hs')|  
|9666|O ponto de extremidade %S_MSG está no estado desabilitado ou parado.|  
|9691|O ponto de extremidade %S_MSG parou de escutar conexões.|  
|9692|O ponto de extremidade %S_MSG não pode escutar na porta %d porque ela está sendo usada por outro processo.|  
|9693|O ponto de extremidade %S_MSG não pode escutar conexões devido ao seguinte erro: '%.*ls'.|  
|28034|Falha no handshake de conexão. O logon '%.*ls' não dispõe de permissão CONNECT no ponto de extremidade. Estado %d.|  
|28036|Falha no handshake de conexão. O certificado usado por este ponto de extremidade não foi encontrado: %S_MSG. Use DBCC CHECKDB no banco de dados mestre para verificar a integridade dos metadados dos pontos de extremidade. Estado %d.|  
|28080|Falha no handshake de conexão. O ponto de extremidade %S_MSG não está configurado. Estado %d.|  
|28091|Não há suporte para o início do ponto de extremidade para %S_MSG sem autenticação.|  
|33309|Não é possível iniciar o ponto de extremidade do cluster porque a configuração de ponto de extremidade padrão %S_MSG ainda não foi carregada.|  
  
#### <a name="alwayson_health-session-definition"></a>Definição de sessão alwayson_health  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
ADD EVENT sqlserver.error_reported(  
    WHERE   
(  
--Connectivity Error Messages  
[error_number]=(35201)   
OR [error_number]=(35202)   
OR [error_number]=(35204)   
OR [error_number]=(35206)   
OR [error_number]=(35207)   
OR [error_number]=(9642)   
--OR [error_number]=(9666)   
OR [error_number]=(9691)   
OR [error_number]=(9692)   
OR [error_number]=(9693)   
OR [error_number]=(28034)   
OR [error_number]=(28036)   
OR [error_number]=(28080)   
OR [error_number]=(28091)   
OR [error_number]=(33309)  
)  
)  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="data_movement_suspend_resume"></a><a name="BKMK_data_movement_suspend_resume"></a> data_movement_suspend_resume  
 Ocorre quando a movimentação do banco de dados de uma réplica de banco de dados é suspensa ou retomada.  
  
#### <a name="event-information"></a>Informações de evento  
  
|Coluna|Descrição|  
|------------|-----------------|  
|Nome|data_movement_suspend_resume|  
|Categoria|Sempre ativo|  
|Canal|Operacional|  
  
#### <a name="event-fields"></a>Campos de evento  
  
|Nome|Type_name|Descrição|  
|-|-|-|  
|availability_group_id|guid|A ID do grupo de disponibilidade.|  
|availability_group_name|unicode_string|O nome do grupo de disponibilidade, se disponível.|  
|availability_replica_id|guid|A ID da réplica de disponibilidade.|  
|database_replica_id|guid|A ID do banco de dados de disponibilidade.|  
|database_replica_name|unicode_string|O nome do banco de dados de disponibilidade.|  
|database_id|uint32|A ID do banco de dados de disponibilidade.|  
|suspend_status|suspend_status_type|Os valores de status de suspensão.<br /><br /> SUSPEND_NULL<br /><br /> RESUMED<br /><br /> SUSPENDED<br /><br /> SUSPENDED_INVALID|  
|suspend_source|suspend_source_type|A origem da ação suspender ou retomar.|  
|suspend_reason|unicode_string|O motivo da suspensão capturado no gerenciador de réplica de banco de dados.|  
  
#### <a name="alwayson_health-session-definition"></a>Definição de sessão alwayson_health  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
  
ADD EVENT data_movement_suspend_resume (  
WHERE (  
[suspend_status]=(SUSPENDED)or [suspend_status]=(SUSPENDED_INVALID) or   
[suspend_status]=(SUSPEND_NULL)  
)  
)  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="alwayson_ddl_executed"></a><a name="BKMK_alwayson_ddl_executed"></a> alwayson_ddl_executed  
 Ocorre quando uma instrução DDL (linguagem de definição de dados) do grupo de disponibilidade está sendo executada, incluindo CREATE, ALTER ou DROP. O principal objetivo do evento é indicar um problema com uma ação do usuário em uma réplica de disponibilidade ou para indicar o ponto de partida de uma ação operacional, que é seguida por um problema de runtime, como um failover manual, um failover forçado, a movimentação de dados suspensa ou a movimentação de dados retomada.  
  
#### <a name="event-information"></a>Informações de evento  
  
|Coluna|Descrição|  
|------------|-----------------|  
|Nome|alwayson_ddl_execution|  
|Categoria|always on|  
|Canal|Analítico|  
  
#### <a name="event-fields"></a>Campos de evento  
  
|Nome|Type_name|Descrição|  
|----------|----------------|-----------------|  
|availability_group_id|Guid|A ID do grupo de disponibilidade.|  
|availability_group_name|unicode_string|O nome do grupo de disponibilidade.|  
|ddl_action|alwayson_ddl_action|Indica o tipo de ação DDL: CREATE, ALTER ou DROP.|  
|ddl_phase|ddl_opcode|Indica a fase da operação DDL: BEGIN, COMMIT ou ROLLBACK.|  
|de|unicode_string|O texto da instrução que foi executada.|  
  
#### <a name="alwayson_health-session-definition"></a>Definição de sessão alwayson_health  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
  
ADD EVENT alwayson_ddl_executed  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="availability_replica_manager_state"></a><a name="BKMK_availability_replica_manager_state"></a> availability_replica_manager_state  
 Ocorre quando o estado do gerenciador de réplica de disponibilidade é alterado. Esse evento indica a pulsação do gerenciador de réplica de disponibilidade. Quando o gerenciador de réplica de disponibilidade não está em estado íntegro, todas as réplicas de disponibilidade da instância do SQL Server ficarão inoperantes.  
  
#### <a name="event-information"></a>Informações de evento  
  
|Coluna|Descrição|  
|------------|-----------------|  
|Nome|availability_replica_manager_state_change|  
|Categoria|always on|  
|Canal|Operacional|  
  
#### <a name="event-fields"></a>Campos de evento  
  
|Nome|Type_name|Descrição|  
|----------|----------------|-----------------|  
|current_state|manager_state|O estado atual do gerenciador de réplica de disponibilidade.<br /><br /> Online<br /><br /> Offline<br /><br /> WaitingForClusterCommunication|  
  
#### <a name="alwayson_health-session-definition"></a>Definição de sessão Alwayson_health  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
  
ADD EVENT availability_replica_manager_state (  
WHERE ([current_state]=(OFFLINE))  
)  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="error_reported-1480-database-replica-role-change"></a><a name="BKMK_error_reported_1480"></a> error_reported (1480): Alteração da função de réplica de banco de dados  
 Esse evento error_reported filtrado ocorre de forma assíncrona depois da alteração de uma função de réplica de disponibilidade. Ele indica qual banco de dados de disponibilidade falha ao alterar sua função esperada durante o processo de failover.  
  
#### <a name="event-information"></a>Informações de evento  
  
|Coluna|Descrição|  
|------------|-----------------|  
|Nome|error_reported<br /><br /> Erro número 1480: O banco de dados REPLICATION_TYPE_MSG "DATABASE_NAME" está alterando funções de "OLD_ROLE" para "NEW_ROLE" devido a REASON_MSG|  
|Categoria|erros|  
|Canal|Admin|  
  
#### <a name="alwayson_health-session-definition"></a>Definição de sessão alwayson_health  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
ADD EVENT sqlserver.error_reported(  
    WHERE   
(  
--database replica role change message  
OR [error_number] = (1480)  
  
--database replica runtime error messages  
OR [error_number]=(823)   
OR [error_number]=(824)   
OR [error_number]=(829)  
)  
)  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
## <a name="next-steps"></a>Próximas etapas  
 [Exibir dados de sessão de evento](https://msdn.microsoft.com/library/hh710068(v=sql.110).aspx)   
