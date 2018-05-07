---
title: sys.dm_os_wait_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/23/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_wait_stats_TSQL
- dm_os_wait_stats
- sys.dm_os_wait_stats
- sys.dm_os_wait_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_wait_stats dynamic management view
ms.assetid: 568d89ed-2c96-4795-8a0c-2f3e375081da
caps.latest.revision: 111
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 85961f9956c93c3bbd2e37393c6f3d0ad3e57e95
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmoswaitstats-transact-sql"></a>sys.dm_os_wait_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna informações sobre todas as esperas encontradas por threads executados. É possível usar essa exibição agregada para diagnosticar problemas de desempenho com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e também com consultas e lotes específicos. [sys.DM exec_session_wait_stats &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md) fornece informações semelhantes por sessão.  
  
> [!NOTE] 
> Para chamar essa de **[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]**, use o nome **sys.dm_pdw_nodes_os_wait_stats**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|wait_type|**nvarchar(60)**|Nome do tipo de espera. Para obter mais informações, consulte [tipos de espera](#WaitTypes), mais adiante neste tópico.|  
|waiting_tasks_count|**bigint**|Número de esperas nesse tipo de espera. O contador é incrementado no início de cada espera.|  
|wait_time_ms|**bigint**|Tempo de espera total para esse tipo de espera em milissegundos. Essa hora é inclusiva de signal_wait_time_ms.|  
|max_wait_time_ms|**bigint**|Tempo de espera máximo neste tipo de espera.|  
|signal_wait_time_ms|**bigint**|Diferença entre a hora em que o thread de espera foi sinalizado e quando ele começou a ser executado.|  
|pdw_node_id|**Int**|O identificador para o nó que essa distribuição é no. <br/> **Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] |  
  
## <a name="permissions"></a>Permissões

Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` no banco de dados.   

##  <a name="WaitTypes"></a> Tipos de esperas  
 **Esperas de recurso** esperas de recurso ocorrem quando um trabalhador solicita acesso a um recurso que não está disponível porque o recurso está sendo usado por outro trabalhador ou ainda não está disponível. Exemplos de esperas de recurso são bloqueios, travas, rede e esperas de E/S de disco. Bloqueio e trava são esperas em objetos de sincronização  
  
**Esperas de fila**  
 As esperas de fila acontecem quando um trabalhador está inativo, aguardando atribuição de trabalho. As esperas de fila são geralmente vistas com tarefas em segundo plano de sistema, como monitor de deadlocks e tarefas de limpeza de registro excluídas. Essas tarefas aguardarão as solicitações de trabalho serem colocadas em uma fila de trabalho. Esperas de fila também poderão ficar periodicamente ativas mesmo se nenhum pacote novo tiver sido colocado na fila.  
  
 **Esperas externas**  
 As esperas externas ocorrem quando um trabalhador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está aguardando um evento externo, como uma chamada de procedimento armazenado estendido ou consulta de servidor vinculada, terminar Quando você diagnostica os problemas de bloqueio, lembre-se de que as esperas externas nem sempre indicam que o trabalhador está ocioso, porque ele pode estar ativamente executando algum código externo.  
  
 `sys.dm_os_wait_stats` mostra a hora das esperas concluídas. Essa exibição de gerenciamento dinâmico não mostra esperas atuais.  
  
 Não será considerado que um thread de trabalho [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esteja sendo esperado se qualquer um dos seguintes for verdadeiro:  
  
-   Um recurso fica disponível.  
  
-   Uma fila não está vazia.  
  
-   Um processo externo termina.  
  
 Embora o thread já não esteja mais aguardando, ele não precisa iniciar a execução imediatamente. Isso ocorre porque esse thread é colocado primeiro na fila de trabalhadores executáveis e deve aguardar a execução de um quantum no agendador.  
  
 Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os contadores de tempo de espera são **bigint** valores e, portanto, não são tão suscetíveis à substituição de contador quanto os contadores equivalentes em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Tipos específicos de horas de espera durante execução de consulta podem indicar gargalos ou pontos de pausa dentro da consulta. Da mesma forma, os tempos de espera altos ou as contagens de espera em todo o servidor podem indicar gargalos nas interações de consulta de interação na instância do servidor. Por exemplo, as esperas de bloqueio indicam a contenção de dados por consultas; as esperas de trava de ES de página indicam tempos de resposta de ES lentos; as esperas de atualização de trava de página indicam layout de arquivo incorreto.  
  
 Os conteúdos desta exibição de gerenciamento dinâmico podem ser reajustados executando o seguinte comando:  
  
```sql  
DBCC SQLPERF ('sys.dm_os_wait_stats', CLEAR);  
GO  
```  
  
Esse comando redefine todos os contadores como 0.  
  
> [!NOTE]
> Essas estatísticas não são persistidas em reinicializações [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e todos os dados são cumulativos desde a última vez em que as estatísticas foram redefinidas ou o servidor foi iniciado.  
  
 A tabela a seguir lista os tipos de espera encontrados por tarefas.  

|Tipo |Description| 
|-------------------------- |--------------------------| 
|ABR |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| | 
|AM_INDBUILD_ALLOCATION |TBD <br />**Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|AM_SCHEMAMGR_UNSHARED_CACHE |TBD <br />**Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ASSEMBLY_FILTER_HASHTABLE |TBD <br />**Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ASSEMBLY_LOAD |Ocorre durante o acesso exclusivo ao carregamento do assembly.| 
|ASYNC_DISKPOOL_LOCK |Ocorre quando há uma tentativa de sincronizar threads paralelos que estão executando tarefas, como criação ou inicialização de um arquivo.| 
|ASYNC_IO_COMPLETION |Ocorre quando uma tarefa estiver esperando a conclusão de E/Ss.| 
|ASYNC_NETWORK_IO |Ocorre em gravações de rede quando a tarefa é bloqueada por trás da rede. Verifique se o cliente está processando dados do servidor.| 
|ASYNC_OP_COMPLETION |TBD <br />**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ASYNC_OP_CONTEXT_READ |TBD <br />**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ASYNC_OP_CONTEXT_WRITE |TBD <br />**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ASYNC_SOCKETDUP_IO |TBD <br />**Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|AUDIT_GROUPCACHE_LOCK |Ocorre quando há uma espera em um bloqueio que controla o acesso a um cache especial. O cache contém informações sobre as auditorias que estão sendo usadas para auditar cada grupo de ações de auditoria.| 
|AUDIT_LOGINCACHE_LOCK |Ocorre quando há uma espera em um bloqueio que controla o acesso a um cache especial. O cache contém informações sobre as auditorias que estão sendo usadas para auditar grupos de ações de auditoria de logon.| 
|AUDIT_ON_DEMAND_TARGET_LOCK |Ocorre quando há uma espera em um bloqueio que é usado para garantir a inicialização única dos destinos do Evento Estendido relacionados à auditoria.| 
|AUDIT_XE_SESSION_MGR |Ocorre quando há uma espera em um bloqueio que é usado para sincronizar o início e a interrupção de sessões de Eventos Estendidos relacionadas à auditoria.| 
|BACKUP |Ocorre quando uma tarefa é bloqueada como parte do processamento do backup.| 
|BACKUP_OPERATOR |Ocorre quando uma tarefa está aguardando uma montagem de fita. Para exibir o status da fita, consulte sys.DM io_backup_tapes. Se uma operação de montagem não estiver pendente, esse tipo de espera poderá indicar um problema de hardware na unidade de fita.| 
|BACKUPBUFFER |Ocorre quando uma tarefa de backup estiver aguardando dados ou um buffer para armazenar dados nele. Esse tipo não é comum, exceto quando uma tarefa estiver aguardando uma montagem de fita.| 
|BACKUPIO |Ocorre quando uma tarefa de backup estiver aguardando dados ou um buffer para armazenar dados nele. Esse tipo não é comum, exceto quando uma tarefa estiver aguardando uma montagem de fita.| 
|BACKUPTHREAD |Ocorre quando uma tarefa estiver esperando a conclusão da tarefa de backup. Os tempos de espera podem ser longos, de alguns minutos até várias horas. Se a tarefa sendo aguardada estiver em um processo de E/S, esse tipo não indicará um problema.| 
|BAD_PAGE_PROCESS |Ocorre quando o registrador de página suspeita em segundo plano estiver tentando evitar a execução mais que cada cinco segundos. Páginas suspeitas em excesso causam a execução frequente do registrador.| 
|BLOB_METADATA |TBD <br />**Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BMPALLOCATION |TBD <br />**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BMPBUILD |TBD <br />**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BMPREPARTITION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BMPREPLICATION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BPSORT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_CONNECTION_RECEIVE_TASK |Ocorre ao aguardar o acesso para receber uma mensagem em um ponto de extremidade de conexão. O acesso de recepção para o ponto de extremidade é serializado.| 
|BROKER_DISPATCHER |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_ENDPOINT_STATE_MUTEX |Ocorre quando houver contenção para acessar o estado de um ponto de extremidade de conexão do Service Broker. O acesso ao estado das alterações é serializado.| 
|BROKER_EVENTHANDLER |Ocorre quando uma tarefa estiver aguardando o manipulador de eventos principal do Service Broker. Isso deve ocorrer muito brevemente.| 
|BROKER_FORWARDER |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_INIT |Ocorre ao inicializar o Service Broker em cada banco de dados ativo. Isso deve ocorrer raramente.| 
|BROKER_MASTERSTART |Ocorre quando uma tarefa está aguardando o manipulador de eventos principal do Service Broker para iniciar. Isso deve ocorrer muito brevemente.| 
|BROKER_RECEIVE_WAITFOR |Ocorre quando RECEIVE WAITFOR estiver aguardando. Isso pode significar que nenhuma mensagem estiver pronta para ser recebida da fila ou uma contenção de bloqueio está impedindo que ele receba mensagens da fila.| 
|BROKER_REGISTERALLENDPOINTS |Ocorre durante a inicialização de um ponto de extremidade de conexão do Service Broker. Isso deve ocorrer muito brevemente.| 
|BROKER_SERVICE |Ocorre quando a lista de destino do Service Broker que está associada um serviço de destino é atualizada ou priorizada novamente.| 
|BROKER_SHUTDOWN |Ocorre quando há um desligamento planejado do Service Broker. Isso deve ocorrer muito brevemente, se ocorrer.| 
|BROKER_START |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TASK_SHUTDOWN |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TASK_STOP |Ocorre quando o manipulador de tarefa de fila do Service Broker tenta desligar a tarefa. A verificação do estado é serializada e deve estar em um estado de execução antecipadamente.| 
|BROKER_TASK_SUBMIT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TO_FLUSH |Ocorre quando objetos de transmissão flusher lenta liberações na memória do Service Broker para uma tabela de trabalho.| 
|BROKER_TRANSMISSION_OBJECT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TRANSMISSION_TABLE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TRANSMISSION_WORK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TRANSMITTER |Ocorre quando o transmissor do Service Broker está aguardando o trabalho.| 
|BUILTIN_HASHKEY_MUTEX |Pode ocorrer depois de inicialização de instância, enquanto as estruturas de dados internos estiverem sendo inicializadas. Não ocorrerá antes que as estruturas de dados tiverem inicializado.| 
|CHANGE_TRACKING_WAITFORCHANGES |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CHECK_PRINT_RECORD |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|CHECK_SCANNER_MUTEX |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CHECK_TABLES_INITIALIZATION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CHECK_TABLES_SINGLE_SCAN |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CHECK_TABLES_THREAD_BARRIER |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CHECKPOINT_QUEUE |Ocorre enquanto a tarefa de ponto de verificação aguarda a próxima solicitação de ponto de verificação.| 
|CHKPT |Ocorre na inicialização de servidor para informar ao thread de ponto de verificação que ele pode iniciar.| 
|CLEAR_DB |Ocorre durante operações que alteram o estado de um banco de dados, como abrir ou fechar um banco de dados.| 
|CLR_AUTO_EVENT |Ocorre quando uma tarefa executa o CLR (Common Language Runtime) e aguarda o início de um determinado evento automático. Esperas longas são comuns e não indicam um problema.| 
|CLR_CRST |Ocorre quando uma tarefa está executando o CLR e aguarda a apresentação de uma seção crítica da tarefa que está, atualmente, sendo usada por outra tarefa.| 
|CLR_JOIN |Ocorre quando uma tarefa executa o CLR e aguarda o término de outra tarefa. Esse estado de espera quando há uma junção entre tarefas.| 
|CLR_MANUAL_EVENT |Ocorre quando uma tarefa está executando o CLR atualmente e está aguardando um evento manual específico a ser iniciado.| 
|CLR_MEMORY_SPY |Ocorre durante uma espera na aquisição de bloqueio para uma estrutura de dados que é usada para registrar todas as alocações de memória virtual provenientes do CLR. A estrutura de dados será bloqueada para manter sua integridade se houver acesso paralelo.| 
|CLR_MONITOR |Ocorre quando uma tarefa está executando o CLR atualmente e aguardando para obter um bloqueio no monitor.| 
|CLR_RWLOCK_READER |Ocorre quando uma tarefa executa o CLR e aguarda um bloqueio de leitor.| 
|CLR_RWLOCK_WRITER |Ocorre quando uma tarefa executa o CLR e aguarda um bloqueio de gravador.| 
|CLR_SEMAPHORE |Ocorre quando uma tarefa executa o CLR e aguarda um semáforo.| 
|CLR_TASK_START |Ocorre enquanto aguarda a inicialização de uma tarefa de CLR ser concluída.| 
|CLRHOST_STATE_ACCESS |Ocorre quando há uma espera para adquirir acesso exclusivo às estruturas de dados de hospedagem de CLR. Esse tipo de espera ocorre ao configurar ou subdividir o tempo de execução do CLR.| 
|CMEMPARTITIONED |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CMEMTHREAD |Ocorre quando uma tarefa está aguardando um objeto de memória protegido por thread. O tempo de espera pode aumentar quando há contenção provocada por várias tarefas tentando alocar memória do mesmo objeto de memória.| 
|COLUMNSTORE_BUILD_THROTTLE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|COLUMNSTORE_COLUMNDATASET_SESSION_LIST |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|COMMIT_TABLE |TBD| 
|CONNECTION_ENDPOINT_LOCK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|COUNTRECOVERYMGR |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CREATE_DATINISERVICE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CXCONSUMER |Ocorre com planos de consulta paralelos quando um thread de consumidor aguarda um thread de produtor enviar linhas. Isso é uma parte normal da execução de consulta paralela. <br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2, [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3), [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|
|CXPACKET |Ocorre com planos de consulta paralelos ao sincronizar o iterador de troca do processador de consulta e ao produzir e consumir linhas. Se a espera for excessiva e não puder ser reduzida ajustando a consulta (como adicionando índices), ajuste o limite de custo para paralelismo ou reduza o grau de paralelismo.<br /> **Observação:** começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2, [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3, e [!INCLUDE[ssSDS](../../includes/sssds-md.md)], CXPACKET refere-se apenas para sincronizar o iterador de troca do processador de consulta e produzindo linhas para threads de consumidor. Threads de consumidor são rastreadas separadamente no tipo de espera CXCONSUMER.| 
|CXROWSET_SYNC |Ocorre durante um exame de intervalo paralelo.| 
|DAC_INIT |Ocorre enquanto a conexão de administrador dedicada estiver inicializando.| 
|DBCC_SCALE_OUT_EXPR_CACHE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DBMIRROR_DBM_EVENT |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|DBMIRROR_DBM_MUTEX |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|DBMIRROR_EVENTS_QUEUE |Ocorre quando o espelhamento de banco de dados aguarda o processamento de eventos.| 
|DBMIRROR_SEND |Ocorre quando uma tarefa aguarda que os registros acumulados de comunicações na camada de rede a serem apagados possam enviar mensagens. Indica que a camada de comunicações está começando a ser sobrecarregada e a afetar a taxa de transferência de dados de espelhamento de banco de dados.| 
|DBMIRROR_WORKER_QUEUE |Indica que a tarefa de trabalhador de espelhamento de banco de dados está aguardando mais trabalho.| 
|DBMIRRORING_CMD |Ocorre quando uma tarefa aguarda a liberação dos registros para o disco. Estima-se que esse estado de espera seja mantido por longos períodos de tempo.| 
|DBSEEDING_FLOWCONTROL |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DBSEEDING_OPERATION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DEADLOCK_ENUM_MUTEX |Ocorre quando o monitor de deadlock e sys.DM os_waiting_tasks tentam Certifique-se de que o SQL Server não está executando várias pesquisas de deadlock ao mesmo tempo.| 
|DEADLOCK_TASK_SEARCH |Um grande tempo de espera nesse recurso indica que o servidor está realizando consultas na parte superior de sys.dm_os_waiting_tasks e que essas consultas estão impedindo o monitor de deadlock de pesquisar deadlocks. Esse tipo de espera só é usado através de monitor de deadlock. Consultas na parte superior de sys.dm_os_waiting_tasks usam DEADLOCK_ENUM_MUTEX.| 
|DEBUG |Ocorre durante o Transact-SQL e a depuração CLR para sincronização interna.| 
|DIRECTLOGCONSUMER_LIST |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DIRTY_PAGE_POLL |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DIRTY_PAGE_SYNC |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DIRTY_PAGE_TABLE_LOCK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DISABLE_VERSIONING |Ocorre quando o SQL Server sonda o Gerenciador de transações de versão para ver se o carimbo de hora da transação ativa mais antiga é posterior ao carimbo de hora de quando o estado começou a mudar. Se esse for o caso, todas as transações de instantâneo iniciadas antes de a instrução ALTER DATABASE ter sido executada serão finalizadas. Esse estado de espera é usado quando o SQL Server desabilita o controle de versão usando a instrução ALTER DATABASE.| 
|DISKIO_SUSPEND |Ocorre quando uma tarefa estiver esperando para acessar um arquivo quando um backup externo está ativo. Isso é informado a cada processo de usuário de espera. Uma contagem maior que cinco por processo de usuário pode indicar que o backup externo está levando muito tempo para ser concluído.| 
|DISPATCHER_PRIORITY_QUEUE_SEMAPHORE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DISPATCHER_QUEUE_SEMAPHORE |Ocorre quando um thread do pool de dispatcher está aguardando mais trabalho para processamento. Estima-se que o tempo para esse tipo de espera aumente quando o dispatcher estiver ocioso.| 
|DLL_LOADING_MUTEX |Ocorre uma vez ao aguardar a DLL do analisador XML ser carregada.| 
|DPT_ENTRY_LOCK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DROP_DATABASE_TIMER_TASK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DROPTEMP |Ocorre entre tentativas para descartar um objeto temporário caso a tentativa anterior tenha falhado. A duração da espera cresce bastante em cada tentativa de descarte com falha.| 
|DTC |Ocorre quando uma tarefa estiver esperando um evento usado para gerenciar a transição de estado. Controles esse estado quando a recuperação de transações do coordenador de transações distribuídas da Microsoft (MS DTC) ocorre depois que o SQL Server recebe notificação que o serviço MS DTC se tornou indisponível.| 
|DTC_ABORT_REQUEST |Ocorre em uma sessão de trabalhador de MS DTC quando a sessão estiver aguardando para obter a propriedade de uma transação de MS DTC. Depois que o MS DTC for proprietário da transação, a sessão poderá reverter a transação. Geralmente, a sessão esperará por outra sessão que está usando a transação.| 
|DTC_RESOLVE |Ocorre quando uma tarefa de recuperação está aguardando o banco de dados mestre em uma transação de banco de dados cruzado de forma que a tarefa possa consultar o resultado da transação.| 
|DTC_STATE |Ocorre quando uma tarefa está esperando um evento que protege as alterações no objeto de estado global de MS DTC. Esse estado deve ser mantido para intervalos de tempo muito curtos.| 
|DTC_TMDOWN_REQUEST |Ocorre em uma sessão de trabalhador de MS DTC quando o SQL Server recebe notificação que o serviço MS DTC não está disponível. Primeiro, o trabalhador aguardará o processo de recuperação de MS DTC iniciar. Em seguida, o trabalhador espera para obter o resultado da transação distribuída em que o trabalhador está trabalhando. Isso pode continuar até a conexão com o serviço de MS DTC ser restabelecida.| 
|DTC_WAITFOR_OUTCOME |Ocorre quando as tarefas de recuperação aguardam o MS DTC ficar ativo para ativar a resolução de transações preparadas.| 
|DTCNEW_ENLIST |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DTCNEW_PREPARE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DTCNEW_RECOVERY |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DTCNEW_TM |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DTCNEW_TRANSACTION_ENLISTMENT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DTCPNTSYNC |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DUMP_LOG_COORDINATOR |Ocorre quando uma tarefa principal está esperando uma subtarefa gerar dados. Em geral, esse estado não ocorre. Uma espera longa indica um bloqueio inesperado. A subtarefa deve ser investigada.| 
|DUMP_LOG_COORDINATOR_QUEUE |TBD| 
|DUMPTRIGGER |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|EC |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|EE_PMOLOCK |Ocorre durante a sincronização de certos tipos de alocações de memória durante execução de instrução.| 
|EE_SPECPROC_MAP_INIT |Ocorre durante sincronização da criação de tabela de hash de procedimento interno. Essa espera só pode ocorrer durante o acesso inicial da tabela de hash depois que a instância do SQL Server é iniciado.| 
|ENABLE_EMPTY_VERSIONING |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ENABLE_VERSIONING |Ocorre quando o SQL Server aguardará para todas as transações de atualização neste banco de dados para concluir antes de declarar o banco de dados pronto para fazer a transição para estado permitido de isolamento de instantâneo. Esse estado é usado quando o SQL Server permite o isolamento de instantâneo usando a instrução ALTER DATABASE.| 
|ERROR_REPORTING_MANAGER |Ocorre durante a sincronização de várias inicializações de log de erros simultâneas.| 
|EXCHANGE |Ocorre durante a sincronização no iterador de troca de processador de consulta durante consultas paralelas.| 
|EXECSYNC |Ocorre durante consultas paralelas durante a sincronização em processador de consulta em áreas não relacionadas ao iterador de troca. Exemplos dessas áreas são bitmaps, LOBs (objetos binários grandes) e o iterador de spool. Os LOBs podem usar esse estado de espera frequentemente.| 
|EXECUTION_PIPE_EVENT_INTERNAL |Ocorre durante a sincronização entre o produtor e partes do consumidor de execução em lotes que são enviados por meio do contexto da conexão.| 
|EXTERNAL_RG_UPDATE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|EXTERNAL_SCRIPT_NETWORK_IO |TBD <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] até a versão atual.| 
|EXTERNAL_SCRIPT_PREPARE_SERVICE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|EXTERNAL_SCRIPT_SHUTDOWN |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|EXTERNAL_WAIT_ON_LAUNCHER, |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_HADR_TRANSPORT_CONNECTION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_REPLICA_CONTROLLER_LIST |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_REPLICA_CONTROLLER_STATE_AND_CONFIG |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_REPLICA_PUBLISHER_EVENT_PUBLISH |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_REPLICA_PUBLISHER_SUBSCRIBER_LIST |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_WAIT_FOR_BUILD_REPLICA_EVENT_PROCESSING |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FAILPOINT |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|FCB_REPLICA_READ |Ocorre quando as leituras de um arquivo esparso de instantâneo (ou um instantâneo temporário criado por DBCC) são sincronizadas.| 
|FCB_REPLICA_WRITE |Ocorre quando o envio ou a remoção de uma página de um arquivo esparso de instantâneo (ou de um instantâneo temporário criado por DBCC) é sincronizado.| 
|FEATURE_SWITCHES_UPDATE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_DB_KILL_FLAG |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_DB_LIST |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FCB |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FCB_FIND |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FCB_PARENT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FCB_RELEASE_CACHED_ENTRIES |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FCB_STATE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FILEOBJECT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_TABLE_LIST |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NTFS_STORE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_RECOVERY |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_RSFX_COMM |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_RSFX_WAIT_FOR_MEMORY |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_STARTUP_SHUTDOWN |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_STORE_DB |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_STORE_ROWSET_LIST |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_STORE_TABLE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILE_VALIDATION_THREADS |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_CACHE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_CHUNKER |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_CHUNKER_INIT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_FCB |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_FILE_OBJECT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_WORKITEM_QUEUE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILETABLE_SHUTDOWN |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FOREIGN_REDO |TBD <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] até a versão atual.| 
|FORWARDER_TRANSITION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FS_FC_RWLOCK |Ocorre quando há uma espera pelo coletor de lixo do FILESTREAM para proceder de uma das seguintes maneiras:| 
|FS_GARBAGE_COLLECTOR_SHUTDOWN |Ocorre quando o coletor de lixo do FILESTREAM está aguardando que tarefas de limpeza sejam concluídas.| 
|FS_HEADER_RWLOCK |Ocorre quando há uma espera para adquirir acesso ao cabeçalho do FILESTREAM de um contêiner de dados do FILESTREAM para ler ou atualizar o conteúdo no arquivo de cabeçalho do FILESTREAM (Filestream.hdr).| 
|FS_LOGTRUNC_RWLOCK |Ocorre quando há uma espera para adquirir acesso ao truncamento de log do FILESTREAM para proceder de uma das seguintes maneiras:| 
|FSA_FORCE_OWN_XACT |Ocorre quando uma operação de E/S de arquivo do FILESTREAM precisa associar-se à transação associada, mas a transação pertence a outra sessão no momento.| 
|FSAGENT |Ocorre quando uma operação de E/S de arquivo FILESTREAM está aguardando um recurso do agente do FILESTREAM que está sendo usado por outra operação de E/S de arquivo.| 
|FSTR_CONFIG_MUTEX |Ocorre quando há uma espera para que outra reconfiguração de recurso do FILESTREAM seja concluída.| 
|FSTR_CONFIG_RWLOCK |Ocorre quando há uma espera para serializar o acesso aos parâmetros de configuração do FILESTREAM.| 
|FT_COMPROWSET_RWLOCK |O texto completo está pendente na operação de metadados de fragmento. Documentado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|FT_IFTS_RWLOCK |O texto completo está pendente na sincronização interna. Documentado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|FT_IFTS_SCHEDULER_IDLE_WAIT |Tipo de espera de suspensão do agendador de texto completo. O agendador está ocioso.| 
|FT_IFTSHC_MUTEX |O texto completo está pendente em uma operação de controle fdhost. Documentado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|FT_IFTSISM_MUTEX |O texto completo está pendente na operação de comunicação. Documentado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|FT_MASTER_MERGE |O texto completo está pendente na operação de mesclagem mestre. Documentado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|FT_MASTER_MERGE_COORDINATOR |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FT_METADATA_MUTEX |Documentado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|FT_PROPERTYLIST_CACHE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FT_RESTART_CRAWL |Ocorre quando um rastreamento de texto completo precisa ser reiniciado a partir do último ponto conhecido bom para recuperação de uma falha momentânea. A espera deixa as tarefas do trabalhador em execução na população para concluir a etapa atual ou sair dela.| 
|FULLTEXT GATHERER |Ocorre durante a sincronização de operações de texto completo.| 
|GDMA_GET_RESOURCE_OWNER |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GHOSTCLEANUP_UPDATE_STATS |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GHOSTCLEANUPSYNCMGR |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_QUERY_CANCEL |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_QUERY_CLOSE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_QUERY_CONSUMER |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_QUERY_PRODUCER |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_TRAN_CREATE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_TRAN_UCS_SESSION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GUARDIAN |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|HADR_AG_MUTEX |Ocorre quando uma instrução DDL AlwaysOn ou o comando do Windows Server Failover Clustering está aguardando acesso de leitura/gravação exclusivo para a configuração de um grupo de disponibilidade., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_AR_CRITICAL_SECTION_ENTRY |Ocorre quando uma instrução DDL AlwaysOn ou o comando de cluster de Failover do Windows Server está aguardando acesso de leitura/gravação para o estado de tempo de execução da réplica local do grupo de disponibilidade associado., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_AR_MANAGER_MUTEX |Ocorre quando um desligamento da réplica de disponibilidade está aguardando a inicialização ser concluída ou uma inicialização de réplica de disponibilidade está aguardando o desligamento ser concluído. Somente para uso interno., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_AR_UNLOAD_COMPLETED |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_ARCONTROLLER_NOTIFICATIONS_SUBSCRIBER_LIST |O publicador para um evento de réplica de disponibilidade (como uma alteração de estado ou alteração de configuração) está aguardando acesso de leitura/gravação exclusivo à lista de assinantes do evento. Somente para uso interno., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_BACKUP_BULK_LOCK |Sempre no banco de dados primário recebeu uma solicitação de backup do banco de dados secundário e está aguardando que o plano de fundo thread para concluir o processamento da solicitação sobre adquirir ou liberar o bloqueio BulkOp., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_BACKUP_QUEUE |O thread em segundo plano backup sempre no banco de dados primário está aguardando uma nova solicitação de trabalho do banco de dados secundário. (normalmente, isso ocorre quando o banco de dados primário está mantendo o log BulkOp e está aguardando o banco de dados secundário indicar que o banco de dados primário pode liberar o bloqueio)., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_CLUSAPI_CALL |Um thread do SQL Server está aguardando para alternar do modo não preemptivo (agendado pelo SQL Server) para o modo preemptivo (agendado pelo sistema operacional) para invocar as APIs de Clustering de Failover do Windows Server., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_COMPRESSED_CACHE_SYNC |Aguardando acesso ao cache de blocos de log compactado que é usado para evitar compactação redundante dos blocos de log enviados para vários bancos de dados secundários., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_CONNECTIVITY_INFO |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DATABASE_FLOW_CONTROL |Aguardando as mensagens serem enviadas ao parceiro quando o número máximo de mensagens enfileiradas tiver sido alcançado. Indica que os exames de log estão sendo executadas mais rapidamente que os envios da rede. Esse é um problema apenas se os envios da rede são mais lentos do que o esperado., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DATABASE_VERSIONING_STATE |Ocorre a alteração de estado de controle de versão de um sempre no banco de dados secundário. Essa espera é para estruturas de dados internas e geralmente é muito curta sem efeito direto no acesso a dados., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DATABASE_WAIT_FOR_RECOVERY |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DATABASE_WAIT_FOR_RESTART |Aguardando o banco de dados reiniciar no controle de grupos de disponibilidade AlwaysOn. Em condições normais, isso não é um problema do cliente porque esperas são previstas aqui., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DATABASE_WAIT_FOR_TRANSITION_TO_VERSIONING |Uma consulta em objetos em um banco de dados secundário legível de um sempre no grupo de disponibilidade está bloqueado no controle de versão de linha enquanto aguarda a confirmação ou reversão de todas as transações que estão em curso quando a réplica secundária foi habilitada para cargas de trabalho de leitura. Esse tipo de espera garante que as versões de linha estão disponíveis antes da execução de uma consulta em isolamento de instantâneo., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DB_COMMAND |Aguardando respostas a mensagens de conversas (que exigem uma resposta explícita do outro lado, usando a infraestrutura de mensagem de conversação sempre ativada). Um número de diferentes tipos de mensagens usam esse tipo de espera., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DB_OP_COMPLETION_SYNC |Aguardando respostas a mensagens de conversas (que exigem uma resposta explícita do outro lado, usando a infraestrutura de mensagem de conversação sempre ativada). Um número de diferentes tipos de mensagens usam esse tipo de espera., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DB_OP_START_SYNC |Uma instrução DDL AlwaysOn ou um comando do Windows Server Failover Clustering está aguardando acesso serializado para um banco de dados de disponibilidade e seu estado de tempo de execução., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DBR_SUBSCRIBER |O publicador para um evento de réplica de disponibilidade (como uma alteração de estado ou alteração de configuração) está aguardando acesso de leitura/gravação para o estado de tempo de execução de um assinante de evento que corresponda a um banco de dados de disponibilidade. Somente para uso interno., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DBR_SUBSCRIBER_FILTER_LIST |O publicador para um evento de réplica de disponibilidade (como uma alteração de estado ou alteração de configuração) está aguardando acesso de leitura/gravação para a lista de assinantes do evento que correspondam aos bancos de dados de disponibilidade. Somente para uso interno., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DBSEEDING |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DBSEEDING_LIST |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DBSTATECHANGE_SYNC |Espera de controle de simultaneidade para atualizar o estado interno da réplica de banco de dados., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FABRIC_CALLBACK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_BLOCK_FLUSH |O Gerenciador de transporte FILESTREAM AlwaysOn está aguardando a conclusão do processamento de um bloco de log., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_FILE_CLOSE |O Gerenciador de transporte FILESTREAM AlwaysOn está aguardando até que o próximo arquivo FILESTREAM é processado e seu identificador seja fechado., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_FILE_REQUEST |Um sempre na réplica secundária está aguardando a réplica primária enviar FILESTREAM solicitado todos os arquivos durante o UNDO., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_IOMGR |O Gerenciador de transporte FILESTREAM AlwaysOn está aguardando o bloqueio de R/W que protege o Gerenciador de FILESTREAM sempre em e/s durante a inicialização ou desligamento., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_IOMGR_IOCOMPLETION |O Gerenciador de FILESTREAM sempre em e/s está aguardando a conclusão de e/s., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_MANAGER |O Gerenciador de transporte FILESTREAM AlwaysOn está aguardando o bloqueio de R/W que protege o Gerenciador de transporte FILESTREAM AlwaysOn durante a inicialização ou desligamento., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_PREPROC |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_GROUP_COMMIT |O processamento da confirmação de transação está aguardando uma confirmação de grupo de modo que vários registros de log de confirmação possam ser colocados em um único bloco de log. Essa espera é uma condição prevista que otimiza o e/s de log, captura e operações de envio., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_LOGCAPTURE_SYNC |Controle de simultaneidade ao redor da captura de log ou objeto de aplicação ao criar ou destruir exames. Isso é uma espera prevista quando os parceiros alteram o status de estado ou de conexão., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_LOGCAPTURE_WAIT |Aguardando os registros de log ficarem disponíveis. Pode ocorrer ao esperar novos registros de log serem gerados por conexões ou para a conclusão de E/S ao ler log não no cache. Isso é uma espera prevista se a verificação de log é detectada para o final do log ou estiver lendo do disco., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_LOGPROGRESS_SYNC |Espera de controle de simultaneidade ao atualizar o status do andamento do log de réplicas de banco de dados., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_NOTIFICATION_DEQUEUE |Uma tarefa em segundo plano que processa as notificações do Windows Server Failover Clustering está aguardando a próxima notificação. Somente para uso interno., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_NOTIFICATION_WORKER_EXCLUSIVE_ACCESS |O Gerenciador de réplica de disponibilidade AlwaysOn está aguardando acesso serializado para o estado de tempo de execução de uma tarefa em segundo plano que processa as notificações de cluster de Failover do Windows Server. Somente para uso interno., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_NOTIFICATION_WORKER_STARTUP_SYNC |Uma tarefa em segundo plano está aguardando a conclusão da inicialização de uma tarefa em segundo plano que processa as notificações do Windows Server Failover Clustering. Somente para uso interno., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_NOTIFICATION_WORKER_TERMINATION_SYNC |Uma tarefa em segundo plano está aguardando a conclusão de uma tarefa em segundo plano que processa as notificações do Windows Server Failover Clustering. Somente para uso interno., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_PARTNER_SYNC |Espera de controle de simultaneidade na lista de parceiro., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_READ_ALL_NETWORKS |Aguardando para obter acesso de leitura ou gravação para a lista de redes do WSFC. Somente para uso interno. Observação: O mecanismo mantém uma lista de redes do WSFC que é usada em exibições de gerenciamento dinâmico (como sys.DM hadr_cluster_networks) ou para validar sempre em Transact-SQL instruções que referenciam WSFC as informações de rede. Esta lista é atualizada após a inicialização do mecanismo, relacionados ao WSFC notificações e interno sempre na reinicialização (por exemplo, perda e recuperando quorum do WSFC). As tarefas serão geralmente bloqueadas quando uma atualização nessa lista estiver em andamento. , <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_RECOVERY_WAIT_FOR_CONNECTION |Aguardando o banco de dados secundário conectar-se ao banco de dados primário antes de executar a recuperação. Isso é uma espera prevista, que pode ser prolongada se a conexão para o primário for lento para estabelecer., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_RECOVERY_WAIT_FOR_UNDO |A recuperação de banco de dados está aguardando o banco de dados secundário concluir a fase de reversão e inicialização para devolvê-lo ao ponto de log comum com o banco de dados primário. Essa é uma espera prevista após failovers. Desfazer progresso pode ser acompanhado por meio do Monitor do sistema do Windows (perfmon.exe) e exibições de gerenciamento dinâmico., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_REPLICAINFO_SYNC |Aguardando o controle de simultaneidade para atualizar o estado atual da réplica., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_CANCELLATION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_FILE_LIST |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_LIMIT_BACKUPS |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_SYNC_COMPLETION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_TIMEOUT_TASK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_WAIT_FOR_COMPLETION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SYNC_COMMIT |Aguardando o processamento da confirmação de transação para os bancos de dados secundários sincronizados proteger o log. Esta espera também é refletida pelo contador de desempenho de Atraso na Transação. Esse tipo de espera é esperado para sincronizados grupos de disponibilidade e indica o tempo para enviar, gravar e reconhecer o log para os bancos de dados secundários., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SYNCHRONIZING_THROTTLE |Aguardando o processamento de confirmação de transação permitir que um banco de dados secundário de sincronização atualize o final primário do log para fazer a transição para o estado sincronizado. Isso é uma espera prevista quando um banco de dados secundário é atualizado., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TDS_LISTENER_SYNC |O sistema interno AlwaysOn ou o cluster WSFC solicita que os ouvintes são iniciados ou interrompidos. O processamento desta solicitação é sempre assíncrono e há um mecanismo para remover solicitações redundantes. Também há momentos em que este processo é suspenso devido a alterações de configuração. Todas as esperas relacionadas com este mecanismo de sincronização de ouvinte usam este tipo de espera. Somente para uso interno., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TDS_LISTENER_SYNC_PROCESSING |Usado no final de uma instrução sempre em Transact-SQL que requer o início e/ou interromper o ouvinte do grupo anavailability. Desde que a operação de iniciar/parar é feita de forma assíncrona, o thread do usuário bloqueará usando esse tipo de espera até que a situação do ouvinte é conhecida., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_THROTTLE_LOG_RATE_GOVERNOR |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_THROTTLE_LOG_RATE_LOG_SIZE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_THROTTLE_LOG_RATE_SEEDING |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_THROTTLE_LOG_RATE_SEND_RECV_QUEUE_SIZE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TIMER_TASK |Aguardando para obter o bloqueio no objeto de tarefa de temporizador e também é usado para as esperas reais entre os momentos em que o trabalho está sendo realizado. Por exemplo, para uma tarefa que executa a cada 10 segundos, depois de uma execução, grupos de disponibilidade AlwaysOn aguardam aproximadamente 10 segundos para replanejar a tarefa e o tempo de espera é incluído aqui., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TRANSPORT_DBRLIST |Aguardando acesso à lista de réplica de banco de dados da camada de transporte. Usado para o spinlock que concede acesso a ele., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TRANSPORT_FLOW_CONTROL |Aguardando quando o número de não confirmados AlwaysOn mensagens pendentes está fora o limite de controle de fluxo. Em uma base para a réplica de disponibilidade (não em uma base de banco de dados no banco de dados)., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TRANSPORT_SESSION |Grupos de disponibilidade AlwaysOn está aguardando enquanto alteram ou acessam o estado de transporte subjacente., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_WORK_POOL |Espera de controle de simultaneidade no objeto de tarefa de trabalho de grupos de disponibilidade AlwaysOn em segundo plano., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_WORK_QUEUE |Grupos de disponibilidade AlwaysOn aguardando o novo trabalho a ser atribuído de thread de trabalho do plano de fundo. Isso é uma espera prevista quando há trabalhadores prontos aguardando o novo trabalho, que é o estado normal., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_XRF_STACK_ACCESS |Acessando (Pesquisar, adicionar e excluir) a pilha de bifurcação de recuperação estendida para um banco de dados de disponibilidade AlwaysOn., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HCCO_CACHE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HK_RESTORE_FILEMAP |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HKCS_PARALLEL_MIGRATION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HKCS_PARALLEL_RECOVERY |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTBUILD |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTDELETE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTMEMO |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTREINIT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTREPARTITION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTTP_ENUMERATION |Ocorre na inicialização para enumerar os pontos de extremidade de HTTP para iniciar o HTTP.| 
|HTTP_START |Ocorre quando uma conexão está esperando que o HTTP conclua a inicialização.| 
|HTTP_STORAGE_CONNECTION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|IMPPROV_IOWAIT |Ocorre quando o SQL Server espera um e/s a conclusão do carregamento em massa.| 
|INSTANCE_LOG_RATE_GOVERNOR |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|INTERNAL_TESTING |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|IO_AUDIT_MUTEX |Ocorre durante a sincronização de buffers de evento de rastreamento.| 
|IO_COMPLETION |Ocorre enquanto se espera as operações de E/S serem concluídas. Esse tipo de espera geralmente representa E/Ss de página sem-dados. Esperas de conclusão de e/s de página de dados aparecem como PAGEIOLATCH\_ \* espera.| 
|IO_QUEUE_LIMIT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|IO_RETRY |Ocorre quando uma operação de E/S, como uma leitura ou uma gravação no disco, falha devido a recursos insuficientes, e é tentada novamente.| 
|IOAFF_RANGE_QUEUE |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|KSOURCE_WAKEUP |Usado pela tarefa de controle de serviço ao aguardar solicitações do Gerenciador de Controle de Serviços. Esperas longas estão previstas e não indicam um problema.| 
|KTM_ENLISTMENT |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|KTM_RECOVERY_MANAGER |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|KTM_RECOVERY_RESOLUTION |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|LATCH_DT |Ocorre ao esperar uma trava de DT (destruir). Isso não inclui travas de buffer ou de marcação de transação. Uma listagem da trava\_ \* esperas está disponível em sys.DM os_latch_stats. Observe que sys.dm_os_latch_stats agrupa LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX e LATCH_DT.| 
|LATCH_EX |Ocorre ao esperar uma trava de EX (exclusivo). Isso não inclui travas de buffer ou de marcação de transação. Uma listagem da trava\_ \* esperas está disponível em sys.DM os_latch_stats. Observe que sys.dm_os_latch_stats agrupa LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX e LATCH_DT.| 
|LATCH_KP |Ocorre ao esperar uma trava de KP (manutenção). Isso não inclui travas de buffer ou de marcação de transação. Uma listagem da trava\_ \* esperas está disponível em sys.DM os_latch_stats. Observe que sys.dm_os_latch_stats agrupa LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX e LATCH_DT.| 
|LATCH_NL |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|LATCH_SH |Ocorre ao esperar uma trava de SH (compartilhamento). Isso não inclui travas de buffer ou de marcação de transação. Uma listagem da trava\_ \* esperas está disponível em sys.DM os_latch_stats. Observe que sys.dm_os_latch_stats agrupa LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX e LATCH_DT.| 
|LATCH_UP |Ocorre ao esperar uma trava de UP (atualização). Isso não inclui travas de buffer ou de marcação de transação. Uma listagem da trava\_ \* esperas está disponível em sys.DM os_latch_stats. Observe que sys.dm_os_latch_stats agrupa LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX e LATCH_DT.| 
|LAZYWRITER_SLEEP |Ocorre quando as tarefas lazywriter são suspensas. É uma medição do tempo gasto por tarefas em segundo plano em espera. Não considere esse estado quando você estiver procurando pausas de usuário.| 
|LCK_M_BU |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização em Massa (BU).| 
|LCK_M_BU_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio BU (Atualização em Massa) com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_BU_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio BU (Atualização em Massa) com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Tentativa Compartilhada (IS).| 
|LCK_M_IS_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio IS (Tentativa Compartilhada) com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IS_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio IS (Tentativa Compartilhada) com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IU |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização da Tentativa (IU).| 
|LCK_M_IU_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio IU (Tentativa de Atualização) com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IU_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio IU (Tentativa de Atualização) com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IX |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Exclusivo da Tentativa (IX).| 
|LCK_M_IX_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio IX (Exclusivo da Tentativa) com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IX_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio IX (Exclusivo da Tentativa) com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_NL |Ocorre quando uma tarefa está esperando adquirir um bloqueio NULL no valor de chave atual e um bloqueio Inserção de Intervalo entre a chave atual e a anterior. Um bloqueio NULL na chave é um bloqueio de liberação instantâneo.| 
|LCK_M_RIn_NL_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio NULL com Bloqueadores de Anulação no valor da chave atual e um bloqueio Inserção de Intervalo com Bloqueadores de Anulação entre a chave atual e a anterior. Um bloqueio NULL na chave é um bloqueio de liberação instantâneo. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_NL_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio NULL com Baixa Prioridade no valor da chave atual e um bloqueio Inserção de Intervalo com Baixa Prioridade entre a chave atual e a anterior. Um bloqueio NULL na chave é um bloqueio de liberação instantâneo. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_S |Ocorre quando uma tarefa está esperando adquirir um bloqueio compartilhado no valor de chave atual e um bloqueio Inserção de Intervalo entre a chave atual e a anterior.| 
|LCK_M_RIn_S_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio compartilhado com Bloqueadores de Anulação no valor da chave atual e um bloqueio Inserção de Intervalo com Bloqueadores de Anulação entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_S_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio compartilhado com Baixa Prioridade no valor da chave atual e um bloqueio Inserção de Intervalo com Baixa Prioridade entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_U |Uma tarefa que está esperando para adquirir um bloqueio Atualização no valor de chave atual e um bloqueio Inserção de Intervalo entre a chave atual e a anterior.| 
|LCK_M_RIn_U_ABORT_BLOCKERS |A tarefa está esperando para adquirir um bloqueio Atualização com Bloqueadores de Anulação no valor da chave atual e um bloqueio Inserção de Intervalo com Bloqueadores de Anulação entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_U_LOW_PRIORITY |A tarefa está esperando para adquirir um bloqueio Atualização com Baixa Prioridade no valor da chave atual e um bloqueio Inserção de Intervalo com Baixa Prioridade entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_X |Ocorre quando uma tarefa está esperando adquirir um bloqueio Exclusivo no valor de chave atual e um bloqueio Inserção de Intervalo entre a chave atual e a anterior.| 
|LCK_M_RIn_X_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Exclusivo com Bloqueadores de Anulação no valor da chave atual e um bloqueio Inserção de Intervalo com Bloqueadores de Anulação entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_X_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Exclusivo com Baixa Prioridade no valor da chave atual e um bloqueio Inserção de Intervalo com Baixa Prioridade entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RS_S |Ocorre quando uma tarefa está esperando adquirir um bloqueio Compartilhado no valor de chave atual e um bloqueio Intervalo Compartilhado entre a chave atual e a anterior.| 
|LCK_M_RS_S_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Bloqueadores de Anulação no valor da chave atual e um bloqueio Intervalo Compartilhado com Bloqueadores de Anulação entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RS_S_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Baixa Prioridade no valor da chave atual e um bloqueio Intervalo Compartilhado com Baixa Prioridade entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RS_U |Ocorre quando uma tarefa está esperando adquirir um bloqueio Atualização no valor de chave atual e um bloqueio Atualização de Intervalo entre a chave atual e a anterior.| 
|LCK_M_RS_U_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização com Bloqueadores de Anulação no valor da chave atual e um bloqueio Intervalo de Atualização com Bloqueadores de Anulação entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RS_U_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização com Baixa Prioridade no valor da chave atual e um bloqueio Intervalo de Atualização com Baixa Prioridade entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_S |Ocorre quando uma tarefa está esperando adquirir um bloqueio Compartilhado no valor de chave atual e um bloqueio Intervalo Exclusivo entre a chave atual e a anterior.| 
|LCK_M_RX_S_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Bloqueadores de Anulação no valor da chave atual e um bloqueio Intervalo Exclusivo com Bloqueadores de Anulação entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_S_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Baixa Prioridade no valor da chave atual e um bloqueio Intervalo Exclusivo com Baixa Prioridade entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_U |Ocorre quando uma tarefa está esperando adquirir um bloqueio Atualização no valor de chave atual e um bloqueio Intervalo Exclusivo entre a chave atual e a anterior.| 
|LCK_M_RX_U_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização com Bloqueadores de Anulação no valor da chave atual e um bloqueio Intervalo Exclusivo com Bloqueadores de Anulação entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_U_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização com Baixa Prioridade no valor da chave atual e um bloqueio Intervalo Exclusivo com Baixa Prioridade entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_X |Ocorre quando uma tarefa está esperando adquirir um bloqueio Exclusivo no valor de chave atual e um bloqueio Intervalo Exclusivo entre a chave atual e a anterior.| 
|LCK_M_RX_X_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Exclusivo com Bloqueadores de Anulação no valor da chave atual e um bloqueio Intervalo Exclusivo com Bloqueadores de Anulação entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_X_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Exclusivo com Baixa Prioridade no valor da chave atual e um bloqueio Intervalo Exclusivo com Baixa Prioridade entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_S |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado.| 
|LCK_M_S_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_S_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SCH_M |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Modificação de Esquema.| 
|LCK_M_SCH_M_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Modificação de Esquema com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SCH_M_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Modificação de Esquema com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SCH_S |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhamento de Esquema.| 
|LCK_M_SCH_S_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhamento de Esquema com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SCH_S_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhamento de Esquema com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SIU |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Atualização da Tentativa.| 
|LCK_M_SIU_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Tentativa de Atualização com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SIU_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Tentativa de Atualização com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SIX |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Exclusivo da Tentativa.| 
|LCK_M_SIX_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Exclusivo da Tentativa com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SIX_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Exclusivo da Tentativa com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_U |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização.| 
|LCK_M_U_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_U_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_UIX |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização com Exclusivo da Tentativa.| 
|LCK_M_UIX_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização com Exclusivo da Tentativa com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_UIX_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização com Exclusivo da Tentativa com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_X |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Exclusivo.| 
|LCK_M_X_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Exclusivo com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_X_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Exclusivo com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.), <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOG_POOL_SCAN |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOG_RATE_GOVERNOR |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGBUFFER |Ocorre quando uma tarefa está esperando espaço no buffer de log para armazenar um registro de log. Consistentemente, valores altos podem indicar que os dispositivos de log não podem acompanhar a quantidade de log que está sendo gerada pelo servidor.| 
|LOGCAPTURE_LOGPOOLTRUNCPOINT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGGENERATION |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|LOGMGR |Ocorre quando uma tarefa está aguardando que qualquer E/S de log pendente seja concluída antes de desativar o log durante o fechamento do banco de dados.| 
|LOGMGR_FLUSH |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|LOGMGR_PMM_LOG |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGMGR_QUEUE |Ocorre enquanto a tarefa de gravador de log aguarda solicitações de trabalho.| 
|LOGMGR_RESERVE_APPEND |Ocorre quando uma tarefa está esperando para verificar se o truncamento de log libera espaço para logs, para que a tarefa possa gravar um novo registro de log. Considere aumentar o tamanho do(s) arquivo(s) de log para o banco de dados afetado para reduzir essa espera.| 
|LOGPOOL_CACHESIZE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOL_CONSUMER |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOL_CONSUMERSET |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOL_FREEPOOLS |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOL_MGRSET |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOL_REPLACEMENTSET |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOLREFCOUNTEDOBJECT_REFDONE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOWFAIL_MEMMGR_QUEUE |Ocorre ao aguardar que a memória esteja disponível para uso.| 
|MD_AGENT_YIELD |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|MD_LAZYCACHE_RWLOCK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|MEMORY_ALLOCATION_EXT |Ocorre durante a alocação de memória do pool de memória interno do SQL Server ou o sistema operacional., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|MEMORY_GRANT_UPDATE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|METADATA_LAZYCACHE_RWLOCK |TBD <br /> **Aplica-se a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] apenas. |  
|MIGRATIONBUFFER |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|MISCELLANEOUS |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|MISCELLANEOUS |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|MSQL_DQ |Ocorre quando uma tarefa está aguardando que uma operação de consulta distribuída seja concluída. Isso é usado para detectar deadlocks de aplicativo MARS (Vários Conjuntos de Resultados Ativos) potenciais. A espera termina quando a chamada de consulta distribuída é concluída.| 
|MSQL_XACT_MGR_MUTEX |Ocorre quando uma tarefa está aguardando para obter a propriedade do gerenciador de transações de sessão para executar uma operação de transação em nível de sessão.| 
|MSQL_XACT_MUTEX |Ocorre durante sincronização de uso de transação. Uma solicitação deve adquirir o mutex antes de usar a transação.| 
|MSQL_XP |Ocorre quando uma tarefa está esperando a finalização de um procedimento armazenado estendido. SQL Server usa esse estado de espera para detectar deadlocks de aplicativo MARS potencial. A espera para quando a chamada do procedimento armazenado estendido termina.| 
|MSSEARCH |Ocorre durante chamadas de pesquisa de texto completo. Essa espera termina quando a operação de texto completo é concluída. Ela não indica contenção, mas a duração de operações de texto completo.| 
|NET_WAITFOR_PACKET |Ocorre quando uma conexão está esperando um pacote de rede durante uma leitura de rede.| 
|NETWORKSXMLMGRLOAD |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|NODE_CACHE_MUTEX |TBD| 
|OLEDB |Ocorre quando o SQL Server chama o provedor SQL Server Native Client OLE DB. Esse tipo de espera não é usado para sincronização. Em vez disso, ele indica a duração de chamadas ao provedor OLE DB.| 
|ONDEMAND_TASK_QUEUE |Ocorre enquanto uma tarefa em segundo plano aguarda solicitações de tarefa de sistema de alta prioridade. Os tempos de espera longos indicam que não houve nenhuma solicitação de alta prioridade a ser processada e que isso não deve causar nenhuma preocupação.| 
|PAGEIOLATCH_DT |Ocorre quando uma tarefa está esperando em uma trava por um buffer que está em uma solicitação de E/S. A solicitação de trava está no modo Destruição. Esperas longas podem indicar problemas no subsistema de disco.| 
|PAGEIOLATCH_EX |Ocorre quando uma tarefa está esperando em uma trava por um buffer que está em uma solicitação de E/S. A solicitação de trava está em modo Exclusivo. Esperas longas podem indicar problemas no subsistema de disco.| 
|PAGEIOLATCH_KP |Ocorre quando uma tarefa está esperando em uma trava por um buffer que está em uma solicitação de E/S. A solicitação de trava está no modo Manutenção. Esperas longas podem indicar problemas no subsistema de disco.| 
|PAGEIOLATCH_NL |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|PAGEIOLATCH_SH |Ocorre quando uma tarefa está esperando em uma trava por um buffer que está em uma solicitação de E/S. A solicitação de trava está no modo Compartilhado. Esperas longas podem indicar problemas no subsistema de disco.| 
|PAGEIOLATCH_UP |Ocorre quando uma tarefa está esperando em uma trava por um buffer que está em uma solicitação de E/S. A solicitação de trava está no modo Atualização. Esperas longas podem indicar problemas no subsistema de disco.| 
|PAGELATCH_DT |Ocorre quando uma tarefa está esperando em uma trava por um buffer que não está em uma solicitação de E/S. A solicitação de trava está no modo Destruição.| 
|PAGELATCH_EX |Ocorre quando uma tarefa está esperando em uma trava por um buffer que não está em uma solicitação de E/S. A solicitação de trava está em modo Exclusivo.| 
|PAGELATCH_KP |Ocorre quando uma tarefa está esperando em uma trava por um buffer que não está em uma solicitação de E/S. A solicitação de trava está no modo Manutenção.| 
|PAGELATCH_NL |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|PAGELATCH_SH |Ocorre quando uma tarefa está esperando em uma trava por um buffer que não está em uma solicitação de E/S. A solicitação de trava está no modo Compartilhado.| 
|PAGELATCH_UP |Ocorre quando uma tarefa está esperando em uma trava por um buffer que não está em uma solicitação de E/S. A solicitação de trava está no modo Atualização.| 
|PARALLEL_BACKUP_QUEUE |Ocorre ao serializar a saída produzida por RESTORE HEADERONLY, RESTORE FILELISTONLY ou RESTORE LABELONLY.| 
|PARALLEL_REDO_DRAIN_WORKER |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_FLOW_CONTROL |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_LOG_CACHE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_TRAN_LIST |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_TRAN_TURN |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_WORKER_SYNC |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_WORKER_WAIT_WORK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PERFORMANCE_COUNTERS_RWLOCK |TBD| 
|PHYSICAL_SEEDING_DMV |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|POOL_LOG_RATE_GOVERNOR |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_ABR |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|PREEMPTIVE_AUDIT_ACCESS_EVENTLOG |Ocorre quando o agendador de Sistema operacional (SQLOS) [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] alterna para o modo preemptivo para gravar um evento de auditoria para o log de eventos do Windows. <br /> **Aplica-se a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] apenas. |  
|PREEMPTIVE_AUDIT_ACCESS_SECLOG |Ocorre quando o agendador de Sistema operacional (SQLOS) alterna para o modo preemptivo para gravar um evento de auditoria para o log de segurança do Windows. <br /> **Aplica-se a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] apenas. |  
|PREEMPTIVE_CLOSEBACKUPMEDIA |Ocorre quando o agendador de SQLOS alterna para o modo preventivo para fechar a mídia de backup.| 
|PREEMPTIVE_CLOSEBACKUPTAPE |Ocorre quando o agendador de SQLOS alterna para o modo preemptivo para fechar um dispositivo de backup em fita.| 
|PREEMPTIVE_CLOSEBACKUPVDIDEVICE |Ocorre quando o agendador de SQLOS alterna para o modo preemptivo para fechar um dispositivo de backup virtual.| 
|PREEMPTIVE_CLUSAPI_CLUSTERRESOURCECONTROL |Ocorre quando o agendador de Sistema operacional (SQLOS) alterna para o modo preemptivo para executar operações de cluster de failover do Windows.| 
|PREEMPTIVE_COM_COCREATEINSTANCE |Ocorre quando o agendador de SQLOS alterna para o modo preemptivo para criar um objeto COM.| 
|PREEMPTIVE_COM_COGETCLASSOBJECT |TBD| 
|PREEMPTIVE_COM_CREATEACCESSOR |TBD| 
|PREEMPTIVE_COM_DELETEROWS |TBD| 
|PREEMPTIVE_COM_GETCOMMANDTEXT |TBD| 
|PREEMPTIVE_COM_GETDATA |TBD| 
|PREEMPTIVE_COM_GETNEXTROWS |TBD| 
|PREEMPTIVE_COM_GETRESULT |TBD| 
|PREEMPTIVE_COM_GETROWSBYBOOKMARK |TBD| 
|PREEMPTIVE_COM_LBFLUSH |TBD| 
|PREEMPTIVE_COM_LBLOCKREGION |TBD| 
|PREEMPTIVE_COM_LBREADAT |TBD| 
|PREEMPTIVE_COM_LBSETSIZE |TBD| 
|PREEMPTIVE_COM_LBSTAT |TBD| 
|PREEMPTIVE_COM_LBUNLOCKREGION |TBD| 
|PREEMPTIVE_COM_LBWRITEAT |TBD| 
|PREEMPTIVE_COM_QUERYINTERFACE |TBD| 
|PREEMPTIVE_COM_RELEASE |TBD| 
|PREEMPTIVE_COM_RELEASEACCESSOR |TBD| 
|PREEMPTIVE_COM_RELEASEROWS |TBD| 
|PREEMPTIVE_COM_RELEASESESSION |TBD| 
|PREEMPTIVE_COM_RESTARTPOSITION |TBD| 
|PREEMPTIVE_COM_SEQSTRMREAD |TBD| 
|PREEMPTIVE_COM_SEQSTRMREADANDWRITE |TBD| 
|PREEMPTIVE_COM_SETDATAFAILURE |TBD| 
|PREEMPTIVE_COM_SETPARAMETERINFO |TBD| 
|PREEMPTIVE_COM_SETPARAMETERPROPERTIES |TBD| 
|PREEMPTIVE_COM_STRMLOCKREGION |TBD| 
|PREEMPTIVE_COM_STRMSEEKANDREAD |TBD| 
|PREEMPTIVE_COM_STRMSEEKANDWRITE |TBD| 
|PREEMPTIVE_COM_STRMSETSIZE |TBD| 
|PREEMPTIVE_COM_STRMSTAT |TBD| 
|PREEMPTIVE_COM_STRMUNLOCKREGION |TBD| 
|PREEMPTIVE_CONSOLEWRITE |TBD| 
|PREEMPTIVE_CREATEPARAM |TBD| 
|PREEMPTIVE_DEBUG |TBD| 
|PREEMPTIVE_DFSADDLINK |TBD| 
|PREEMPTIVE_DFSLINKEXISTCHECK |TBD| 
|PREEMPTIVE_DFSLINKHEALTHCHECK |TBD| 
|PREEMPTIVE_DFSREMOVELINK |TBD| 
|PREEMPTIVE_DFSREMOVEROOT |TBD| 
|PREEMPTIVE_DFSROOTFOLDERCHECK |TBD| 
|PREEMPTIVE_DFSROOTINIT |TBD| 
|PREEMPTIVE_DFSROOTSHARECHECK |TBD| 
|PREEMPTIVE_DTC_ABORT |TBD| 
|PREEMPTIVE_DTC_ABORTREQUESTDONE |TBD| 
|PREEMPTIVE_DTC_BEGINTRANSACTION |TBD| 
|PREEMPTIVE_DTC_COMMITREQUESTDONE |TBD| 
|PREEMPTIVE_DTC_ENLIST |TBD| 
|PREEMPTIVE_DTC_PREPAREREQUESTDONE |TBD| 
|PREEMPTIVE_FILESIZEGET |TBD| 
|PREEMPTIVE_FSAOLEDB_ABORTTRANSACTION |TBD| 
|PREEMPTIVE_FSAOLEDB_COMMITTRANSACTION |TBD| 
|PREEMPTIVE_FSAOLEDB_STARTTRANSACTION |TBD| 
|PREEMPTIVE_FSRECOVER_UNCONDITIONALUNDO |TBD| 
|PREEMPTIVE_GETRMINFO |TBD| 
|PREEMPTIVE_HADR_LEASE_MECHANISM |Gerenciador de concessão de grupos de disponibilidade AlwaysOn para diagnóstico de CSS de agendamento., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_HTTP_EVENT_WAIT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_HTTP_REQUEST |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_LOCKMONITOR |TBD| 
|PREEMPTIVE_MSS_RELEASE |TBD| 
|PREEMPTIVE_ODBCOPS |TBD| 
|PREEMPTIVE_OLE_UNINIT |TBD| 
|PREEMPTIVE_OLEDB_ABORTORCOMMITTRAN |TBD| 
|PREEMPTIVE_OLEDB_ABORTTRAN |TBD| 
|PREEMPTIVE_OLEDB_GETDATASOURCE |TBD| 
|PREEMPTIVE_OLEDB_GETLITERALINFO |TBD| 
|PREEMPTIVE_OLEDB_GETPROPERTIES |TBD| 
|PREEMPTIVE_OLEDB_GETPROPERTYINFO |TBD| 
|PREEMPTIVE_OLEDB_GETSCHEMALOCK |TBD| 
|PREEMPTIVE_OLEDB_JOINTRANSACTION |TBD| 
|PREEMPTIVE_OLEDB_RELEASE |TBD| 
|PREEMPTIVE_OLEDB_SETPROPERTIES |TBD| 
|PREEMPTIVE_OLEDBOPS |TBD| 
|PREEMPTIVE_OS_ACCEPTSECURITYCONTEXT |TBD| 
|PREEMPTIVE_OS_ACQUIRECREDENTIALSHANDLE |TBD| 
|PREEMPTIVE_OS_AUTHENTICATIONOPS |TBD| 
|PREEMPTIVE_OS_AUTHORIZATIONOPS |TBD| 
|PREEMPTIVE_OS_AUTHZGETINFORMATIONFROMCONTEXT |TBD| 
|PREEMPTIVE_OS_AUTHZINITIALIZECONTEXTFROMSID |TBD| 
|PREEMPTIVE_OS_AUTHZINITIALIZERESOURCEMANAGER |TBD| 
|PREEMPTIVE_OS_BACKUPREAD |TBD| 
|PREEMPTIVE_OS_CLOSEHANDLE |TBD| 
|PREEMPTIVE_OS_CLUSTEROPS |TBD| 
|PREEMPTIVE_OS_COMOPS |TBD| 
|PREEMPTIVE_OS_COMPLETEAUTHTOKEN |TBD| 
|PREEMPTIVE_OS_COPYFILE |TBD| 
|PREEMPTIVE_OS_CREATEDIRECTORY |TBD| 
|PREEMPTIVE_OS_CREATEFILE |TBD| 
|PREEMPTIVE_OS_CRYPTACQUIRECONTEXT |TBD| 
|PREEMPTIVE_OS_CRYPTIMPORTKEY |TBD| 
|PREEMPTIVE_OS_CRYPTOPS |TBD| 
|PREEMPTIVE_OS_DECRYPTMESSAGE |TBD| 
|PREEMPTIVE_OS_DELETEFILE |TBD| 
|PREEMPTIVE_OS_DELETESECURITYCONTEXT |TBD| 
|PREEMPTIVE_OS_DEVICEIOCONTROL |TBD| 
|PREEMPTIVE_OS_DEVICEOPS |TBD| 
|PREEMPTIVE_OS_DIRSVC_NETWORKOPS |TBD| 
|PREEMPTIVE_OS_DISCONNECTNAMEDPIPE |TBD| 
|PREEMPTIVE_OS_DOMAINSERVICESOPS |TBD| 
|PREEMPTIVE_OS_DSGETDCNAME |TBD| 
|PREEMPTIVE_OS_DTCOPS |TBD| 
|PREEMPTIVE_OS_ENCRYPTMESSAGE |TBD| 
|PREEMPTIVE_OS_FILEOPS |TBD| 
|PREEMPTIVE_OS_FINDFILE |TBD| 
|PREEMPTIVE_OS_FLUSHFILEBUFFERS |TBD| 
|PREEMPTIVE_OS_FORMATMESSAGE |TBD| 
|PREEMPTIVE_OS_FREECREDENTIALSHANDLE |TBD| 
|PREEMPTIVE_OS_FREELIBRARY |TBD| 
|PREEMPTIVE_OS_GENERICOPS |TBD| 
|PREEMPTIVE_OS_GETADDRINFO |TBD| 
|PREEMPTIVE_OS_GETCOMPRESSEDFILESIZE |TBD| 
|PREEMPTIVE_OS_GETDISKFREESPACE |TBD| 
|PREEMPTIVE_OS_GETFILEATTRIBUTES |TBD| 
|PREEMPTIVE_OS_GETFILESIZE |TBD| 
|PREEMPTIVE_OS_GETFINALFILEPATHBYHANDLE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_OS_GETLONGPATHNAME |TBD| 
|PREEMPTIVE_OS_GETPROCADDRESS |TBD| 
|PREEMPTIVE_OS_GETVOLUMENAMEFORVOLUMEMOUNTPOINT |TBD| 
|PREEMPTIVE_OS_GETVOLUMEPATHNAME |TBD| 
|PREEMPTIVE_OS_INITIALIZESECURITYCONTEXT |TBD| 
|PREEMPTIVE_OS_LIBRARYOPS |TBD| 
|PREEMPTIVE_OS_LOADLIBRARY |TBD| 
|PREEMPTIVE_OS_LOGONUSER |TBD| 
|PREEMPTIVE_OS_LOOKUPACCOUNTSID |TBD| 
|PREEMPTIVE_OS_MESSAGEQUEUEOPS |TBD| 
|PREEMPTIVE_OS_MOVEFILE |TBD| 
|PREEMPTIVE_OS_NETGROUPGETUSERS |TBD| 
|PREEMPTIVE_OS_NETLOCALGROUPGETMEMBERS |TBD| 
|PREEMPTIVE_OS_NETUSERGETGROUPS |TBD| 
|PREEMPTIVE_OS_NETUSERGETLOCALGROUPS |TBD| 
|PREEMPTIVE_OS_NETUSERMODALSGET |TBD| 
|PREEMPTIVE_OS_NETVALIDATEPASSWORDPOLICY |TBD| 
|PREEMPTIVE_OS_NETVALIDATEPASSWORDPOLICYFREE |TBD| 
|PREEMPTIVE_OS_OPENDIRECTORY |TBD| 
|PREEMPTIVE_OS_PDH_WMI_INIT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_OS_PIPEOPS |TBD| 
|PREEMPTIVE_OS_PROCESSOPS |TBD| 
|PREEMPTIVE_OS_QUERYCONTEXTATTRIBUTES |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_OS_QUERYREGISTRY |TBD| 
|PREEMPTIVE_OS_QUERYSECURITYCONTEXTTOKEN |TBD| 
|PREEMPTIVE_OS_REMOVEDIRECTORY |TBD| 
|PREEMPTIVE_OS_REPORTEVENT |TBD| 
|PREEMPTIVE_OS_REVERTTOSELF |TBD| 
|PREEMPTIVE_OS_RSFXDEVICEOPS |TBD| 
|PREEMPTIVE_OS_SECURITYOPS |TBD| 
|PREEMPTIVE_OS_SERVICEOPS |TBD| 
|PREEMPTIVE_OS_SETENDOFFILE |TBD| 
|PREEMPTIVE_OS_SETFILEPOINTER |TBD| 
|PREEMPTIVE_OS_SETFILEVALIDDATA |TBD| 
|PREEMPTIVE_OS_SETNAMEDSECURITYINFO |TBD| 
|PREEMPTIVE_OS_SQLCLROPS |TBD| 
|PREEMPTIVE_OS_SQMLAUNCH |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] ao [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]. |  
|PREEMPTIVE_OS_VERIFYSIGNATURE |TBD| 
|PREEMPTIVE_OS_VERIFYTRUST |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_OS_VSSOPS |TBD| 
|PREEMPTIVE_OS_WAITFORSINGLEOBJECT |TBD| 
|PREEMPTIVE_OS_WINSOCKOPS |TBD| 
|PREEMPTIVE_OS_WRITEFILE |TBD| 
|PREEMPTIVE_OS_WRITEFILEGATHER |TBD| 
|PREEMPTIVE_OS_WSASETLASTERROR |TBD| 
|PREEMPTIVE_REENLIST |TBD| 
|PREEMPTIVE_RESIZELOG |TBD| 
|PREEMPTIVE_ROLLFORWARDREDO |TBD| 
|PREEMPTIVE_ROLLFORWARDUNDO |TBD| 
|PREEMPTIVE_SB_STOPENDPOINT |TBD| 
|PREEMPTIVE_SERVER_STARTUP |TBD| 
|PREEMPTIVE_SETRMINFO |TBD| 
|PREEMPTIVE_SHAREDMEM_GETDATA |TBD| 
|PREEMPTIVE_SNIOPEN |TBD| 
|PREEMPTIVE_SOSHOST |TBD| 
|PREEMPTIVE_SOSTESTING |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|PREEMPTIVE_SP_SERVER_DIAGNOSTICS |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_STARTRM |TBD| 
|PREEMPTIVE_STREAMFCB_CHECKPOINT |TBD| 
|PREEMPTIVE_STREAMFCB_RECOVER |TBD| 
|PREEMPTIVE_STRESSDRIVER |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|PREEMPTIVE_TESTING |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|PREEMPTIVE_TRANSIMPORT |TBD| 
|PREEMPTIVE_UNMARSHALPROPAGATIONTOKEN |TBD| 
|PREEMPTIVE_VSS_CREATESNAPSHOT |TBD| 
|PREEMPTIVE_VSS_CREATEVOLUMESNAPSHOT |TBD| 
|PREEMPTIVE_XE_CALLBACKEXECUTE |TBD| 
|PREEMPTIVE_XE_CX_FILE_OPEN |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_XE_CX_HTTP_CALL |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_XE_DISPATCHER |TBD| 
|PREEMPTIVE_XE_ENGINEINIT |TBD| 
|PREEMPTIVE_XE_GETTARGETSTATE |TBD| 
|PREEMPTIVE_XE_SESSIONCOMMIT |TBD| 
|PREEMPTIVE_XE_TARGETFINALIZE |TBD| 
|PREEMPTIVE_XE_TARGETINIT |TBD| 
|PREEMPTIVE_XE_TIMERRUN |TBD| 
|PREEMPTIVE_XETESTING |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|PRINT_ROLLBACK_PROGRESS |Usado para aguardar enquanto os processos do usuário são finalizados em um banco de dados que passou por transição usando a cláusula de término ALTER DATABASE. Para obter mais informações, consulte ALTER DATABASE (Transact-SQL).| 
|PRU_ROLLBACK_DEFERRED |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_ALL_COMPONENTS_INITIALIZED |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_COOP_SCAN |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_DIRECTLOGCONSUMER_GETNEXT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_EVENT_SESSION_INIT_MUTEX |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_FABRIC_REPLICA_CONTROLLER_DATA_LOSS |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_ACTION_COMPLETED |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_CHANGE_NOTIFIER_TERMINATION_SYNC |Ocorre quando uma tarefa em segundo plano está aguardando a conclusão de uma tarefa em segundo plano que recebe (via sondagem) as notificações de cluster de Failover do Windows Server., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_CLUSTER_INTEGRATION |Um acréscimo, substituir e/ou Remover operação está aguardando para obter um bloqueio de gravação em um AlwaysOn lista interna (como uma lista de redes, endereços de rede ou ouvintes de grupo de disponibilidade). Somente para uso interno <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_FAILOVER_COMPLETED |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_JOIN |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_OFFLINE_COMPLETED |Uma AlwaysOn drop operação grupo de disponibilidade está aguardando o grupo de disponibilidade de destino ficar offline antes de destruir os objetos de cluster de Failover do Windows Server., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_ONLINE_COMPLETED |Um sempre em criar ou operação de failover do grupo de disponibilidade está aguardando o grupo de disponibilidade de destino ficar online., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_POST_ONLINE_COMPLETED |Uma AlwaysOn drop operação grupo de disponibilidade está aguardando o término de uma tarefa em segundo plano que foi agendada como parte de um comando anterior. Por exemplo, pode haver uma tarefa em segundo plano que está fazendo a transição de bancos de dados de disponibilidade para a função primária. DROP AVAILABILITY GROUP DDL deve aguardar esta tarefa em segundo plano ser finalizada para evitar condições de corrida., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_SERVER_READY_CONNECTIONS |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_WORKITEM_COMPLETED |Espera interna por um thread que espera uma tarefa de trabalho assíncrona ser concluída. Esta é uma espera prevista e é para usar o CSS., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADRSIM |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_LOG_CONSOLIDATION_IO |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_LOG_CONSOLIDATION_POLL |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_MD_LOGIN_STATS |Ocorre durante sincronização interna nos metadados nas estatísticas de logon., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_MD_RELATION_CACHE |Ocorre durante sincronização interna nos metadados na tabela ou índice., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_MD_SERVER_CACHE |Ocorre durante sincronização interna nos metadados em servidores vinculados., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_MD_UPGRADE_CONFIG |Ocorre durante sincronização interna ao atualizar as configurações do servidor amplas., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_PREEMPTIVE_APP_USAGE_TIMER |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_PREEMPTIVE_AUDIT_ACCESS_WINDOWSLOG |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_QRY_BPMEMORY |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_REPLICA_ONLINE_INIT_MUTEX |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_RESOURCE_SEMAPHORE_FT_PARALLEL_QUERY_SYNC |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_SBS_FILE_OPERATION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_XTP_FSSTORAGE_MAINTENANCE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_XTP_HOST_STORAGE_WAIT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_ASYNC_CHECK_CONSISTENCY_TASK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_ASYNC_PERSIST_TASK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_ASYNC_PERSIST_TASK_START |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_ASYNC_QUEUE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_BCKG_TASK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_BLOOM_FILTER |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_CLEANUP_STALE_QUERIES_TASK_MAIN_LOOP_SLEEP |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_CTXS |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_DB_DISK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_DYN_VECTOR |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_EXCLUSIVE_ACCESS |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_HOST_INIT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_LOADDB |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_PERSIST_TASK_MAIN_LOOP_SLEEP |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_QDS_CAPTURE_INIT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_SHUTDOWN_QUEUE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_STMT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_STMT_DISK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_TASK_SHUTDOWN |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_TASK_START |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QE_WARN_LIST_SYNC |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QPJOB_KILL |Indica que uma atualização de estatística automática e assíncrona foi cancelada por uma chamada para KILL enquanto a atualização estava começando a ser executada. O thread de término está suspenso, esperando que ele inicie a escuta dos comandos KILL. Um valor bom é menos de um segundo.| 
|QPJOB_WAITFOR_ABORT |Indica que uma atualização assíncrona de estatísticas automática foi cancelada por uma chamada a KILL quando estava sendo executada. A atualização agora está concluída, mas está suspensa até que a coordenação de mensagens de thread de término seja concluída. Esse é um estado comum, mas raro, e deve ser bem curto. Um valor bom é menos de um segundo.| 
|QRY_MEM_GRANT_INFO_MUTEX |Ocorre quando o gerenciamento de memória de execução de consulta tenta controlar o acesso à lista de informações de concessão estáticas. Esse estado lista informações sobre as solicitações de memória em espera e concedidas atuais. É um estado de controle de acesso simples. Nunca deverá haver uma espera longa nesse estado. Se o mutex não for liberado, todas as novas consultas que usam memória deixarão de responder.| 
|QRY_PARALLEL_THREAD_MUTEX |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QRY_PROFILE_LIST_MUTEX |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QUERY_ERRHDL_SERVICE_DONE |Identificado apenas para fins informativos. Sem suporte. <br /> **Aplica-se a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] apenas. |  
|QUERY_WAIT_ERRHDL_SERVICE |Identificado apenas para fins informativos.  Sem suporte. <br /> **Aplica-se a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] apenas.  |  
|QUERY_EXECUTION_INDEX_SORT_EVENT_OPEN |Ocorre em determinados casos quando a criação de índice offline é executada em paralelo, e os diferentes threads de trabalho que estão classificando sincronizam o acesso aos arquivos de classificação.| 
|QUERY_NOTIFICATION_MGR_MUTEX |Ocorre durante a sincronização da fila de coleta de lixo do gerenciador de notificação de consulta.| 
|QUERY_NOTIFICATION_SUBSCRIPTION_MUTEX |Ocorre durante a sincronização de estado para transações em notificações de consulta.| 
|QUERY_NOTIFICATION_TABLE_MGR_MUTEX |Ocorre durante sincronização interna no gerenciador de notificação de consulta.| 
|QUERY_NOTIFICATION_UNITTEST_MUTEX |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|QUERY_OPTIMIZER_PRINT_MUTEX |Ocorre durante sincronização de produção de saída de diagnóstico do otimizador de consulta. Esse tipo de espera só ocorrerá se as configurações de diagnóstico estiverem habilitadas sob a direção do suporte técnico da Microsoft.| 
|QUERY_TASK_ENQUEUE_MUTEX |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QUERY_TRACEOUT |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|RBIO_WAIT_VLF |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RECOVER_CHANGEDB |Ocorre durante a sincronização do status do banco de dados em espera passiva.| 
|RECOVERY_MGR_LOCK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REDO_THREAD_PENDING_WORK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REDO_THREAD_SYNC |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REMOTE_BLOCK_IO |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REMOTE_DATA_ARCHIVE_MIGRATION_DMV |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REMOTE_DATA_ARCHIVE_SCHEMA_DMV |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REMOTE_DATA_ARCHIVE_SCHEMA_TASK_QUEUE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REPL_CACHE_ACCESS |Ocorre durante a sincronização em um cache de artigo de replicação. Durante essas esperas, o leitor de log de replicação entra em pausa e as instruções DDL (linguagem de definição de dados) em uma tabela publicada, são bloqueadas.| 
|REPL_HISTORYCACHE_ACCESS |TBD| 
|REPL_SCHEMA_ACCESS |Ocorre durante sincronização das informações de versão do esquema de replicação. Esse estado ocorre quando as instruções DDL são executadas no objeto replicado e quando o leitor de log gera ou consome esquema com controle de versão com base em uma ocorrência DDL. Contenção pode ser vista nesse tipo de espera se você tiver vários bancos de dados publicados em um único publicador com a replicação transacional e bancos de dados publicados são muito ativos.| 
|REPL_TRANFSINFO_ACCESS |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REPL_TRANHASHTABLE_ACCESS |TBD| 
|REPL_TRANTEXTINFO_ACCESS |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REPLICA_WRITES |Ocorre enquanto uma tarefa espera a conclusão de gravações de página em instantâneos de banco de dados ou réplicas de DBCC.| 
|REQUEST_DISPENSER_PAUSE |Ocorre quando uma tarefa está esperando a conclusão de todas as E/Ss pendentes, de forma que a E/S para um arquivo possa ser congelada para backup de instantâneo.| 
|REQUEST_FOR_DEADLOCK_SEARCH |Ocorre enquanto o monitor de deadlock espera iniciar a próxima pesquisa de deadlock. Essa espera é prevista entre as detecções de deadlock e, o tempo total maior nesse recurso, não significa que existe um problema.| 
|RESERVED_MEMORY_ALLOCATION_EXT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RESMGR_THROTTLED |Ocorre quando uma nova solicitação chega e é suprimida com base na configuração de GROUP_MAX_REQUESTS.| 
|RESOURCE_GOVERNOR_IDLE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RESOURCE_QUEUE |Ocorre durante a sincronização de várias filas de recurso internos.| 
|RESOURCE_SEMAPHORE |Ocorre quando uma solicitação de memória de consulta não pode ser concedida imediatamente devido a outras consultas simultâneas. Esperas e tempos de espera longos podem indicar número excessivo de consultas simultâneas ou valores de solicitação de memória excessivos.| 
|RESOURCE_SEMAPHORE_MUTEX |Ocorre enquanto uma consulta aguarda a sua solicitação de uma reserva de thread ser atendida. Também ocorre durante a sincronização de solicitações de compilação de consulta e concessão de memória.| 
|RESOURCE_SEMAPHORE_QUERY_COMPILE |Ocorre quando o número de compilações de consulta simultâneas atinge um limite de estrangulamento. Esperas e tempos de espera longos podem indicar compilações excessivas, recompilações ou planos que não sejam para cache.| 
|RESOURCE_SEMAPHORE_SMALL_QUERY |Ocorre quando uma solicitação de memória por meio de uma pequena consulta não pode ser concedida imediatamente devido a outras consultas simultâneas. O tempo de espera não deve exceder mais do que alguns segundos porque o servidor transfere a solicitação ao pool de memória de consulta principal se ele falhar ao conceder a memória solicitada dentro de alguns segundos. Esperas longas podem indicar número excessivo de pequenas consultas simultâneas enquanto o pool de memória principal está sendo bloqueado por consultas em espera. <br /> **Aplica-se a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] apenas. |  
|RESTORE_FILEHANDLECACHE_ENTRYLOCK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RESTORE_FILEHANDLECACHE_LOCK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RG_RECONFIG |TBD| 
|ROWGROUP_OP_STATS |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ROWGROUP_VERSION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RTDATA_LIST |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SATELLITE_CARGO |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SATELLITE_SERVICE_SETUP |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SATELLITE_TASK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SBS_DISPATCH |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SBS_RECEIVE_TRANSPORT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SBS_TRANSPORT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SCAN_CHAR_HASH_ARRAY_INITIALIZATION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SEC_DROP_TEMP_KEY |Ocorre depois de uma falha ao tentar descartar uma chave de segurança temporária antes de uma nova tentativa.| 
|SECURITY_CNG_PROVIDER_MUTEX |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SECURITY_CRYPTO_CONTEXT_MUTEX |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SECURITY_DBE_STATE_MUTEX |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SECURITY_KEYRING_RWLOCK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SECURITY_MUTEX |Ocorre quando há uma espera por mutexes que controlam o acesso à lista global de provedores criptográficos de EKM (Gerenciamento Extensível de Chaves) e à lista de escopo de sessões de EKM.| 
|SECURITY_RULETABLE_MUTEX |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SEMPLAT_DSI_BUILD |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SEQUENCE_GENERATION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SEQUENTIAL_GUID |Ocorre enquanto um novo GUID sequencial está sendo obtido.| 
|SERVER_IDLE_CHECK |Ocorre durante a sincronização do status ocioso da instância do SQL Server quando um monitor de recursos está tentando declarar uma instância do SQL Server como ociosa ou tentando ativar.| 
|SERVER_RECONFIGURE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SESSION_WAIT_STATS_CHILDREN |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SHARED_DELTASTORE_CREATION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SHUTDOWN |Ocorre enquanto uma instrução de desligamento aguarda o encerramento de conexões ativas.| 
|SLEEP_BPOOL_FLUSH |Ocorre quando um ponto de verificação está estrangulando a emissão de E/Ss novas para evitar o enchimento do subsistema de disco.| 
|SLEEP_BUFFERPOOL_HELPLW |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_DBSTARTUP |Ocorre durante a inicialização do banco de dados enquanto aguarda a recuperação de todos os bancos de dados.| 
|SLEEP_DCOMSTARTUP |Ocorre uma vez no máximo durante inicialização de instância do SQL Server enquanto aguarda a conclusão da inicialização do DCOM.| 
|SLEEP_MASTERDBREADY |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_MASTERMDREADY |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_MASTERUPGRADED |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_MEMORYPOOL_ALLOCATEPAGES |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_MSDBSTARTUP |Ocorre quando o SQL Trace aguarda o banco de dados msdb concluir a inicialização.| 
|SLEEP_RETRY_VIRTUALALLOC |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_SYSTEMTASK |Ocorre durante o início de uma tarefa em segundo plano enquanto aguarda tempdb concluir a inicialização.| 
|SLEEP_TASK |Ocorre quando uma tarefa suspensa espera a ocorrência de um evento genérico.| 
|SLEEP_TEMPDBSTARTUP |Ocorre enquanto uma tarefa espera tempdb completar a inicialização.| 
|SLEEP_WORKSPACE_ALLOCATEPAGE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLO_UPDATE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SMSYNC |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SNI_CONN_DUP |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SNI_CRITICAL_SECTION |Ocorre durante sincronização interna nos componentes de rede do SQL Server.| 
|SNI_HTTP_WAITFOR_0_DISCON |Ocorre durante o desligamento do SQL Server, ao aguardar o encerramento de conexões HTTP pendentes.| 
|SNI_LISTENER_ACCESS |Ocorre ao aguardar que os nós NUMA (acesso não uniforme à memória) atualizem a alteração do estado. O acesso à alteração de estado é serializado.| 
|SNI_TASK_COMPLETION |Ocorre quando há uma espera para que todas as tarefas sejam concluídas durante uma alteração de estado de nó NUMA.| 
|SNI_WRITE_ASYNC |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SOAP_READ |Ocorre ao aguardar pela conclusão de uma leitura de rede HTTP.| 
|SOAP_WRITE |Ocorre enquanto aguarda a conclusão de uma gravação de rede HTTP.| 
|SOCKETDUPLICATEQUEUE_CLEANUP |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SOS_CALLBACK_REMOVAL |Ocorre enquanto executa a sincronização em uma lista de retorno de chamada para remover um retorno de chamada. Não se espera que esse contador seja alterado depois que a inicialização do servidor é concluída.| 
|SOS_DISPATCHER_MUTEX |Ocorre durante a sincronização interna do pool de dispatchers. Isto inclui o período de ajuste do pool.| 
|SOS_LOCALALLOCATORLIST |Ocorre durante a sincronização interna no gerenciador de memória do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. <br /> **Aplica-se a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] apenas. |  
|SOS_MEMORY_TOPLEVELBLOCKALLOCATOR |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SOS_MEMORY_USAGE_ADJUSTMENT |Ocorre quando o uso de memória está sendo ajustado entre pools.| 
|SOS_OBJECT_STORE_DESTROY_MUTEX |Ocorre durante sincronização interna em pools de memória na destruição de objetos do pool.| 
|SOS_PHYS_PAGE_CACHE |Contabiliza o tempo que um thread aguarda para obter o mutex necessário antes de alocar páginas físicas ou antes de retornar essas páginas para o sistema operacional. Esperas nesse tipo aparecem somente se a instância do SQL Server usar memória AWE., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SOS_PROCESS_AFFINITY_MUTEX |Ocorre durante a sincronização de acesso para processar configurações de afinidade.| 
|SOS_RESERVEDMEMBLOCKLIST |Ocorre durante sincronização interna no Gerenciador de memória do SQL Server. <br /> **Aplica-se a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] apenas. |  
|SOS_SCHEDULER_YIELD |Ocorre quando uma tarefa cede o agendador para a execução de outras tarefas. Durante essa espera, a tarefa espera que seu quantum seja renovado.| 
|SOS_SMALL_PAGE_ALLOC |Ocorre durante a alocação e a liberação de memória que é gerenciada por alguns objetos de memória.| 
|SOS_STACKSTORE_INIT_MUTEX |Ocorre durante a sincronização da inicialização do repositório interno.| 
|SOS_SYNC_TASK_ENQUEUE_EVENT |Ocorre quando uma tarefa é iniciada em uma maneira síncrona. A maioria das tarefas no SQL Server são iniciadas de maneira assíncrona, em que o controle retorna ao iniciador imediatamente após a solicitação de tarefa ter sido colocada na fila de trabalhos.| 
|SOS_VIRTUALMEMORY_LOW |Ocorre quando uma alocação de memória espera um gerenciador de recursos liberar memória virtual.| 
|SOSHOST_EVENT |Ocorre quando um componente hospedado, como CLR, espera um objeto de sincronização de evento do SQL Server.| 
|SOSHOST_INTERNAL |Ocorre durante a sincronização de retornos de chamada de gerenciador de memória usada por componentes hospedados, como CLR.| 
|SOSHOST_MUTEX |Ocorre quando um componente hospedado, como CLR, espera um objeto de sincronização de mutex do SQL Server.| 
|SOSHOST_RWLOCK |Ocorre quando um componente hospedado, como CLR, espera um objeto de sincronização de leitor-gravador do SQL Server.| 
|SOSHOST_SEMAPHORE |Ocorre quando um componente hospedado, como CLR, espera um objeto de sincronização de semáforo do SQL Server.| 
|SOSHOST_SLEEP |Ocorre quando uma tarefa hospedada entra em suspensão enquanto espera a ocorrência de um evento genérico. As tarefas hospedadas são usadas por componentes hospedados, como CLR.| 
|SOSHOST_TRACELOCK |Ocorre durante a sincronização de acesso para rastreamento de fluxos.| 
|SOSHOST_WAITFORDONE |Ocorre quando um componente hospedado, como CLR, aguarda a conclusão de uma tarefa.| 
|SP_PREEMPTIVE_SERVER_DIAGNOSTICS_SLEEP |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SP_SERVER_DIAGNOSTICS_BUFFER_ACCESS |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SP_SERVER_DIAGNOSTICS_INIT_MUTEX |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SP_SERVER_DIAGNOSTICS_SLEEP |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLCLR_APPDOMAIN |Ocorre enquanto CLR espera que um domínio de aplicativo conclua a inicialização.| 
|SQLCLR_ASSEMBLY |Ocorre enquanto aguarda o acesso à lista de assemblies carregados em appdomain.| 
|SQLCLR_DEADLOCK_DETECTION |Ocorre enquanto CLR aguarda a conclusão da detecção de deadlock.| 
|SQLCLR_QUANTUM_PUNISHMENT |Ocorre quando uma tarefa CLR é estrangulada porque excedeu seu quantum de execução. Esse estrangulamento é feito para reduzir o efeito dessa tarefa com muitos recursos em outras tarefas.| 
|SQLSORT_NORMMUTEX |Ocorre durante sincronização interna na inicialização das estruturas de classificação internas.| 
|SQLSORT_SORTMUTEX |Ocorre durante sincronização interna na inicialização das estruturas de classificação internas.| 
|SQLTRACE_BUFFER_FLUSH |Ocorre quando uma tarefa espera que, uma tarefa em segundo plano, libere buffers de rastreamento para o disco a cada quatro segundos. <br /> **Aplica-se a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] apenas. |  
|SQLTRACE_FILE_BUFFER |Ocorre durante a sincronização em buffers de rastreamento durante um rastreamento de arquivo., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLTRACE_FILE_READ_IO_COMPLETION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLTRACE_FILE_WRITE_IO_COMPLETION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLTRACE_INCREMENTAL_FLUSH_SLEEP |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLTRACE_LOCK |TBD <br /> **Aplica-se a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] apenas. |  
|SQLTRACE_PENDING_BUFFER_WRITERS |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLTRACE_SHUTDOWN |Ocorre enquanto o desligamento de rastreamento aguarda a conclusão dos eventos de rastreamento pendentes.| 
|SQLTRACE_WAIT_ENTRIES |Ocorre enquanto uma fila de eventos do Rastreamento do SQL aguarda a chegada de pacotes na fila.| 
|SRVPROC_SHUTDOWN |Ocorre enquanto o processo de desligamento aguarda a liberação dos recursos internos para desligamento completo.| 
|STARTUP_DEPENDENCY_MANAGER |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|TDS_BANDWIDTH_STATE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|TDS_INIT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|TDS_PROXY_CONTAINER |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|TEMPOBJ |Ocorre quando os descartes de objetos temporários são sincronizados. Essa espera é rara e só acontecerá se uma tarefa solicitar acesso exclusivo para descartes de tabelas temporárias.| 
|TEMPORAL_BACKGROUND_PROCEED_CLEANUP |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|TERMINATE_LISTENER |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|THREADPOOL |Ocorre quando uma tarefa estiver esperando que um trabalhador seja processado no sistema. Isso pode indicar que a configuração máxima do trabalhador está muito baixa ou que as execuções em lotes estão demorando normalmente mais tempo, reduzindo o número de trabalhadores disponíveis para atender outros lotes.| 
|TIMEPRIV_TIMEPERIOD |Ocorre durante a sincronização interna do timer de Eventos Estendidos.| 
|TRACE_EVTNOTIF |TBD| 
|TRACEWRITE |Ocorre quando o provedor de rastreamento do conjunto de linhas de Rastreamento do SQL aguarda que um buffer livre ou um buffer com eventos seja processado.| 
|TRAN_MARKLATCH_DT |Ocorre ao esperar uma trava de modo de destruição em uma destruição de marcação de transação. Essas travas são usadas para sincronização de confirmações com transações marcadas.| 
|TRAN_MARKLATCH_EX |Ocorre ao esperar uma trava de modo exclusiva em uma transação marcada. Essas travas são usadas para sincronização de confirmações com transações marcadas.| 
|TRAN_MARKLATCH_KP |Ocorre ao esperar uma trava de modo de manutenção em uma transação marcada. Essas travas são usadas para sincronização de confirmações com transações marcadas.| 
|TRAN_MARKLATCH_NL |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|TRAN_MARKLATCH_SH |Ocorre ao esperar uma trava de modo compartilhado em uma transação marcada. Essas travas são usadas para sincronização de confirmações com transações marcadas.| 
|TRAN_MARKLATCH_UP |Ocorre ao esperar uma trava de modo de atualização em uma transação marcada. Essas travas são usadas para sincronização de confirmações com transações marcadas.| 
|TRANSACTION_MUTEX |Ocorre durante a sincronização de acesso a uma transação por meio de vários lotes.| 
|UCS_ENDPOINT_CHANGE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UCS_MANAGER |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UCS_MEMORY_NOTIFICATION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UCS_SESSION_REGISTRATION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UCS_TRANSPORT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UCS_TRANSPORT_STREAM_CHANGE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UTIL_PAGE_ALLOC |Ocorre quando exames de log de transação aguardam que memória esteja disponível durante pressão da memória.| 
|VDI_CLIENT_COMPLETECOMMAND |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|VDI_CLIENT_GETCOMMAND |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|VDI_CLIENT_OPERATION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|VDI_CLIENT_OTHER |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|VERSIONING_COMMITTING |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|VIA_ACCEPT |Ocorre quando uma conexão do provedor Virtual Interface Adapter (VIA) é concluída durante a inicialização.| 
|VIEW_DEFINITION_MUTEX |Ocorre durante a sincronização no acesso às definições de exibição em cache.| 
|WAIT_FOR_RESULTS |Ocorre ao esperar a ativação de uma notificação de consulta.| 
|WAIT_SCRIPTDEPLOYMENT_REQUEST |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_SCRIPTDEPLOYMENT_WORKER |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XLOGREAD_SIGNAL |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_ASYNC_TX_COMPLETION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_CKPT_AGENT_WAKEUP |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_CKPT_CLOSE |Ocorre ao esperar um ponto de verificação concluir., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_CKPT_ENABLED |Ocorre quando o ponto de verificação é o ponto de verificação desabilitado e está aguardando para ser habilitado., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_CKPT_STATE_LOCK |Ocorre quando a sincronização da verificação do estado do ponto de verificação., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_COMPILE_WAIT |TBD <br /> **APLICA-SE A**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_GUEST |Ocorre quando o alocador de memória do banco de dados precisa parar de receber notificações de memória insuficiente., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_HOST_WAIT |Ocorre quando as esperas são disparadas pelo mecanismo de banco de dados e implementadas pelo host., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_OFFLINE_CKPT_BEFORE_REDO |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_OFFLINE_CKPT_LOG_IO |Ocorre quando o ponto de verificação offline está esperando um log de leitura e/s para concluir., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_OFFLINE_CKPT_NEW_LOG |Ocorre quando o ponto de verificação offline está esperando para novos registros de log verificar., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_PROCEDURE_ENTRY |Ocorre quando um procedimento de descarte aguarda que todas as execuções atuais desse procedimento sejam concluídas., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_RECOVERY |Ocorre quando a recuperação de banco de dados está aguardando a recuperação de objetos com otimização de memória para concluir., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_SERIAL_RECOVERY |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_SWITCH_TO_INACTIVE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_TASK_SHUTDOWN |Ocorre ao esperar um thread de OLTP na memória concluir., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_TRAN_DEPENDENCY |Ocorre ao aguardar dependências de transação., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAITFOR |Ocorre como resultado de uma instrução WAITFOR Transact-SQL. A duração da espera é determinada pelos parâmetros da instrução. Essa é uma espera iniciada pelo usuário.| 
|WAITFOR_PER_QUEUE |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAITFOR_TASKSHUTDOWN |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|WAITSTAT_MUTEX |Ocorre durante a sincronização de acesso à coleção de estatísticas usadas para popular sys.dm_os_wait_stats.| 
|WCC |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|WINDOW_AGGREGATES_MULTIPASS |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WINFAB_API_CALL |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WINFAB_REPLICA_BUILD_OPERATION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WINFAB_REPORT_FAULT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WORKTBL_DROP |Ocorre ao pausar antes de tentar novamente, após uma falha no descarte de uma tabela de trabalho.| 
|WRITE_COMPLETION |Ocorre quando uma operação de gravação está em andamento.| 
|WRITELOG |Ocorre ao aguardar que uma liberação de log seja concluída. As operações comuns que causam liberações de log são pontos de verificação e confirmações de transação.| 
|XACT_OWN_TRANSACTION |Ocorre enquanto se espera a aquisição da propriedade de uma transação.| 
|XACT_RECLAIM_SESSION |Ocorre enquanto se espera que o proprietário atual de uma sessão libere a propriedade da sessão.| 
|XACTLOCKINFO |Ocorre durante a sincronização de acesso à lista de bloqueios para uma transação. Além da própria transação, a lista de bloqueios é acessada por operações como detecção de deadlock e migração de bloqueio durante divisões de páginas.| 
|XACTWORKSPACE_MUTEX |Ocorre durante a sincronização de remoções de uma transação, bem como do número de bloqueios de banco de dados entre os membros registrados de uma transação.| 
|XDB_CONN_DUP_HASH |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XDES_HISTORY |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XDES_OUT_OF_ORDER_LIST |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XDES_SNAPSHOT |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XDESTSVERMGR |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XE_BUFFERMGR_ALLPROCESSED_EVENT |Ocorre quando buffers de sessão de Eventos Estendidos são liberados para destinos. Essa espera ocorre em um thread em segundo plano.| 
|XE_BUFFERMGR_FREEBUF_EVENT |Ocorre quando uma destas condições é verdadeira:| 
|XE_CALLBACK_LIST |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XE_CX_FILE_READ |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XE_DISPATCHER_CONFIG_SESSION_LIST |Ocorre quando uma sessão de Eventos Estendidos que está usando destinos assíncronos é iniciada ou interrompida. Essa espera indica qualquer um dos seguintes:| 
|XE_DISPATCHER_JOIN |Ocorre quando um thread em segundo plano que é usado para sessões de Eventos Estendidos está sendo encerrado.| 
|XE_DISPATCHER_WAIT |Ocorre quando um thread em segundo plano que é usado para sessões de Eventos Estendidos está esperando o processamento de buffers de evento.| 
|XE_FILE_TARGET_TVF |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XE_LIVE_TARGET_TVF |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XE_MODULEMGR_SYNC |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|XE_OLS_LOCK |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|XE_PACKAGE_LOCK_BACKOFF |Identificado apenas para fins informativos. Sem suporte. <br /> **Aplica-se a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] apenas. |  
|XE_SERVICES_EVENTMANUAL |TBD| 
|XE_SERVICES_MUTEX |TBD| 
|XE_SERVICES_RWLOCK |TBD| 
|XE_SESSION_CREATE_SYNC |TBD| 
|XE_SESSION_FLUSH |TBD| 
|XE_SESSION_SYNC |TBD| 
|XE_STM_CREATE |TBD| 
|XE_TIMER_EVENT |TBD| 
|XE_TIMER_MUTEX |TBD| 
|XE_TIMER_TASK_DONE |TBD| 
|XIO_CREDENTIAL_MGR_RWLOCK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_CREDENTIAL_RWLOCK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_EDS_MGR_RWLOCK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_EDS_RWLOCK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_IOSTATS_BLOBLIST_RWLOCK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_IOSTATS_FCBLIST_RWLOCK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_LEASE_RENEW_MGR_RWLOCK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTP_HOST_DB_COLLECTION |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTP_HOST_LOG_ACTIVITY |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTP_HOST_PARALLEL_RECOVERY |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTP_PREEMPTIVE_TASK |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTP_TRUNCATION_LSN |TBD <br /> **Aplica-se a**: do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTPPROC_CACHE_ACCESS |Ocorre quando acessa todos os objetos de cache de procedimento armazenado compilado nativamente., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTPPROC_PARTITIONED_STACK_CREATE |Ocorre quando alocar por nó NUMA nativamente compilada estruturas de cache de procedimento armazenado (deve ser feito em thread único) para um determinado procedimento., <br /> **Aplica-se a**: do [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|

  
 Os XEvents a seguir estão relacionados a partição **SWITCH** e recompilação de índice online. Para obter informações sobre a sintaxe, consulte [ALTER TABLE &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-table-transact-sql.md) e [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
-   lock_request_priority_state  
  
-   process_killed_by_abort_blockers  
  
-   ddl_with_wait_at_low_priority  
  
 Para uma matriz de compatibilidade de bloqueio, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).  
  
## <a name="see-also"></a>Consulte também  
    
 [Sistema operacional SQL Server relacionadas exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_exec_session_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md)   
 [sys.DM db_wait_stats &#40;banco de dados do SQL Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-wait-stats-azure-sql-database.md)  
  
  


