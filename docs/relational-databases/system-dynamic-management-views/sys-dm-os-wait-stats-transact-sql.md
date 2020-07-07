---
title: sys. dm_os_wait_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ee313bdcda6b005a3f3a80725908244d3a496b67
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86011602"
---
# <a name="sysdm_os_wait_stats-transact-sql"></a>sys.dm_os_wait_stats (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Retorna informações sobre todas as esperas encontradas por threads executados. É possível usar essa exibição agregada para diagnosticar problemas de desempenho com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e também com consultas e lotes específicos. o [Sys. dm_exec_session_wait_stats &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md) fornece informações semelhantes por sessão.  
  
> [!NOTE] 
> Para chamá-lo de ** [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] **, use o nome **Sys. dm_pdw_nodes_os_wait_stats**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|wait_type|**nvarchar(60)**|Nome do tipo de espera. Para obter mais informações, consulte [Tipos de espera](#WaitTypes) mais adiante neste tópico.|  
|waiting_tasks_count|**bigint**|Número de esperas nesse tipo de espera. O contador é incrementado no início de cada espera.|  
|wait_time_ms|**bigint**|Tempo de espera total para esse tipo de espera em milissegundos. Essa hora é inclusiva de signal_wait_time_ms.|  
|max_wait_time_ms|**bigint**|Tempo de espera máximo neste tipo de espera.|  
|signal_wait_time_ms|**bigint**|Diferença entre a hora em que o thread de espera foi sinalizado e quando ele começou a ser executado.|  
|pdw_node_id|**int**|O identificador do nó em que essa distribuição está. <br/> **Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] |  
  
## <a name="permissions"></a>Permissões

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   

##  <a name="types-of-waits"></a><a name="WaitTypes"></a>Tipos de esperas  
 **Esperas de recursos** As esperas de recurso ocorrem quando um trabalho solicita acesso a um recurso que não está disponível porque o recurso está sendo usado por algum outro operador ou ainda não está disponível. Exemplos de esperas de recurso são bloqueios, travas, rede e esperas de E/S de disco. Bloqueio e trava são esperas em objetos de sincronização  
  
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
  
 Nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contadores de tempo de espera são valores **bigint** e, portanto, não são tão propensos à substituição de contador como os contadores equivalentes em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
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

|tipo |Descrição| 
|-------------------------- |--------------------------| 
|ABR |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| | 
|AM_INDBUILD_ALLOCATION |Somente para uso interno. <br />**Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|AM_SCHEMAMGR_UNSHARED_CACHE |Somente para uso interno. <br />**Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|ASSEMBLY_FILTER_HASHTABLE |Somente para uso interno. <br />**Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|ASSEMBLY_LOAD |Ocorre durante o acesso exclusivo ao carregamento do assembly.| 
|ASYNC_DISKPOOL_LOCK |Ocorre quando há uma tentativa de sincronizar threads paralelos que estão executando tarefas, como criação ou inicialização de um arquivo.| 
|ASYNC_IO_COMPLETION |Ocorre quando uma tarefa estiver esperando a conclusão de E/Ss.| 
|ASYNC_NETWORK_IO |Ocorre em gravações de rede quando a tarefa é bloqueada por trás da rede. Verifique se o cliente está processando dados do servidor.| 
|ASYNC_OP_COMPLETION |Somente para uso interno. <br />**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|ASYNC_OP_CONTEXT_READ |Somente para uso interno. <br />**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|ASYNC_OP_CONTEXT_WRITE |Somente para uso interno. <br />**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|ASYNC_SOCKETDUP_IO |Somente para uso interno. <br />**Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|AUDIT_GROUPCACHE_LOCK |Ocorre quando há uma espera em um bloqueio que controla o acesso a um cache especial. O cache contém informações sobre as auditorias que estão sendo usadas para auditar cada grupo de ações de auditoria.| 
|AUDIT_LOGINCACHE_LOCK |Ocorre quando há uma espera em um bloqueio que controla o acesso a um cache especial. O cache contém informações sobre as auditorias que estão sendo usadas para auditar grupos de ações de auditoria de logon.| 
|AUDIT_ON_DEMAND_TARGET_LOCK |Ocorre quando há uma espera em um bloqueio que é usado para garantir a inicialização única dos destinos do Evento Estendido relacionados à auditoria.| 
|AUDIT_XE_SESSION_MGR |Ocorre quando há uma espera em um bloqueio que é usado para sincronizar o início e a interrupção de sessões de Eventos Estendidos relacionadas à auditoria.| 
|BACKUP |Ocorre quando uma tarefa é bloqueada como parte do processamento do backup.| 
|BACKUP_OPERATOR |Ocorre quando uma tarefa está aguardando uma montagem de fita. Para exibir o status da fita, consulte sys.dm_io_backup_tapes. Se uma operação de montagem não estiver pendente, esse tipo de espera poderá indicar um problema de hardware na unidade de fita.| 
|BACKUPBUFFER |Ocorre quando uma tarefa de backup estiver aguardando dados ou um buffer para armazenar dados nele. Esse tipo não é comum, exceto quando uma tarefa estiver aguardando uma montagem de fita.| 
|BACKUPIO |Ocorre quando uma tarefa de backup estiver aguardando dados ou um buffer para armazenar dados nele. Esse tipo não é comum, exceto quando uma tarefa estiver aguardando uma montagem de fita.| 
|BACKUPTHREAD |Ocorre quando uma tarefa estiver esperando a conclusão da tarefa de backup. Os tempos de espera podem ser longos, de alguns minutos até várias horas. Se a tarefa sendo aguardada estiver em um processo de E/S, esse tipo não indicará um problema.| 
|BAD_PAGE_PROCESS |Ocorre quando o registrador de página suspeita em segundo plano estiver tentando evitar a execução mais que cada cinco segundos. Páginas suspeitas em excesso causam a execução frequente do registrador.| 
|BLOB_METADATA |Somente para uso interno. <br />**Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|BMPALLOCATION |Ocorre com planos paralelos de modo de lote ao sincronizar a alocação de um filtro de bitmap grande. Se a espera for excessiva e não puder ser reduzida ajustando a consulta (como adicionando índices), ajuste o limite de custo para paralelismo ou reduza o grau de paralelismo.<br />**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|BMPBUILD |Ocorre com planos paralelos de modo de lote ao sincronizar a compilação de um filtro de bitmap grande. Se a espera for excessiva e não puder ser reduzida ajustando a consulta (como adicionando índices), ajuste o limite de custo para paralelismo ou reduza o grau de paralelismo. <br />**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|BMPREPARTITION |Ocorre com planos paralelos de modo de lote ao sincronizar o reparticionamento de um filtro de bitmap grande. Se a espera for excessiva e não puder ser reduzida ajustando a consulta (como adicionando índices), ajuste o limite de custo para paralelismo ou reduza o grau de paralelismo. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|BMPREPLICATION |Ocorre com planos paralelos de modo de lote ao sincronizar a replicação de um filtro de bitmap grande entre threads de trabalho. Se a espera for excessiva e não puder ser reduzida ajustando a consulta (como adicionando índices), ajuste o limite de custo para paralelismo ou reduza o grau de paralelismo. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|BPSORT |Ocorre com planos paralelos de modo de lote ao sincronizar a classificação de um conjunto de um DataSet entre vários threads. Se a espera for excessiva e não puder ser reduzida ajustando a consulta (como adicionando índices), ajuste o limite de custo para paralelismo ou reduza o grau de paralelismo. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|BROKER_CONNECTION_RECEIVE_TASK |Ocorre ao aguardar o acesso para receber uma mensagem em um ponto de extremidade de conexão. O acesso de recepção para o ponto de extremidade é serializado.| 
|BROKER_DISPATCHER |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|BROKER_ENDPOINT_STATE_MUTEX |Ocorre quando há contenção para acessar o estado de um ponto de extremidade de conexão Service Broker. O acesso ao estado das alterações é serializado.| 
|BROKER_EVENTHANDLER |Ocorre quando uma tarefa está aguardando no manipulador de eventos primário da Service Broker. Isso deve ocorrer muito brevemente.| 
|BROKER_FORWARDER |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|BROKER_INIT |Ocorre ao inicializar Service Broker em cada banco de dados ativo. Isso deve ocorrer raramente.| 
|BROKER_MASTERSTART |Ocorre quando uma tarefa está aguardando o manipulador de eventos primário do Service Broker iniciar. Isso deve ocorrer muito brevemente.| 
|BROKER_RECEIVE_WAITFOR |Ocorre quando RECEIVE WAITFOR estiver aguardando. Isso pode significar que nenhuma mensagem está pronta para ser recebida na fila ou uma contenção de bloqueio está impedindo o recebimento de mensagens da fila.| 
|BROKER_REGISTERALLENDPOINTS |Ocorre durante a inicialização de um ponto de extremidade de conexão Service Broker. Isso deve ocorrer muito brevemente.| 
|BROKER_SERVICE |Ocorre quando a Service Broker lista de destino associada a um serviço de destino é atualizada ou priorizada novamente.| 
|BROKER_SHUTDOWN |Ocorre quando há um desligamento planejado de Service Broker. Isso deve ocorrer muito brevemente, se ocorrer.| 
|BROKER_START |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|BROKER_TASK_SHUTDOWN |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|BROKER_TASK_STOP |Ocorre quando o manipulador de tarefa de fila de Service Broker tenta desligar a tarefa. A verificação do estado é serializada e deve estar em um estado de execução antecipadamente.| 
|BROKER_TASK_SUBMIT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|BROKER_TO_FLUSH |Ocorre quando o Service Broker liberação lenta libera os objetos de transmissão na memória para uma tabela de trabalho.| 
|BROKER_TRANSMISSION_OBJECT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|BROKER_TRANSMISSION_TABLE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|BROKER_TRANSMISSION_WORK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|BROKER_TRANSMITTER |Ocorre quando o transmissor de Service Broker está aguardando trabalho. Service Broker tem um componente conhecido como transmissor que agenda mensagens de várias caixas de diálogo a serem enviadas pela conexão por um ou mais pontos de extremidade de conexão. O transmissor tem 2 threads dedicados para essa finalidade. Esse tipo de espera é cobrado quando esses threads de transmissor estão aguardando que as mensagens de caixa de diálogo sejam enviadas usando as conexões de transporte. Valores altos de waiting_tasks_count para esse tipo de espera apontam para o trabalho intermitente para esses threads de transmissor e não são indicações de nenhum problema de desempenho. Se o Service Broker não for usado, waiting_tasks_count deve ser 2 (para os dois threads de transmissor) e wait_time_ms deve ser duas vezes a duração desde a inicialização da instância. Consulte [Estatísticas de espera do Service Broker](https://blogs.msdn.microsoft.com/sql_service_broker/2008/12/01/service-broker-wait-types).|
|BUILTIN_HASHKEY_MUTEX |Pode ocorrer depois de inicialização de instância, enquanto as estruturas de dados internos estiverem sendo inicializadas. Não ocorrerá antes que as estruturas de dados tiverem inicializado.| 
|CHANGE_TRACKING_WAITFORCHANGES |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|CHECK_PRINT_RECORD |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|CHECK_SCANNER_MUTEX |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|CHECK_TABLES_INITIALIZATION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|CHECK_TABLES_SINGLE_SCAN |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|CHECK_TABLES_THREAD_BARRIER |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
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
|CLRHOST_STATE_ACCESS |Ocorre quando há uma espera para adquirir acesso exclusivo às estruturas de dados de hospedagem de CLR. Esse tipo de espera ocorre ao configurar ou subdividir o runtime do CLR.| 
|CMEMPARTITIONED |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|CMEMTHREAD |Ocorre quando uma tarefa está aguardando um objeto de memória protegido por thread. O tempo de espera pode aumentar quando há contenção provocada por várias tarefas tentando alocar memória do mesmo objeto de memória.| 
|COLUMNSTORE_BUILD_THROTTLE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|COLUMNSTORE_COLUMNDATASET_SESSION_LIST |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|COMMIT_TABLE |Somente para uso interno.| 
|CONNECTION_ENDPOINT_LOCK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|COUNTRECOVERYMGR |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|CREATE_DATINISERVICE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|CXCONSUMER |Ocorre com planos de consulta paralelos quando um thread de consumidor aguarda um thread de produtor enviar linhas. Essa é uma parte normal da execução de consulta paralela. <br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2, [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Cu3),[!INCLUDE[ssSDS](../../includes/sssds-md.md)]|
|CXPACKET |Ocorre com planos de consulta paralelos ao sincronizar o iterador de troca do processador de consultas e ao produzir e consumir linhas. Se a espera for excessiva e não puder ser reduzida ajustando a consulta (como adicionando índices), ajuste o limite de custo para paralelismo ou reduza o grau de paralelismo.<br /> **Observação:** Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] o SP2, o [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Cu3 e o [!INCLUDE[ssSDS](../../includes/sssds-md.md)] esperas cxpacket se refere apenas à sincronização do iterador de troca do processador de consultas e à produção de linhas para threads de consumidor. Os threads de consumidor são rastreados separadamente no tipo de espera CXCONSUMER.| 
|CXROWSET_SYNC |Ocorre durante um exame de intervalo paralelo.| 
|DAC_INIT |Ocorre enquanto a conexão de administrador dedicada estiver inicializando.| 
|DBCC_SCALE_OUT_EXPR_CACHE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|DBMIRROR_DBM_EVENT |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|DBMIRROR_DBM_MUTEX |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|DBMIRROR_EVENTS_QUEUE |Ocorre quando o espelhamento de banco de dados aguarda o processamento de eventos.| 
|DBMIRROR_SEND |Ocorre quando uma tarefa aguarda que os registros acumulados de comunicações na camada de rede a serem apagados possam enviar mensagens. Indica que a camada de comunicações está começando a ser sobrecarregada e a afetar a taxa de transferência de dados de espelhamento de banco de dados.| 
|DBMIRROR_WORKER_QUEUE |Indica que a tarefa de trabalhador de espelhamento de banco de dados está aguardando mais trabalho.| 
|DBMIRRORING_CMD |Ocorre quando uma tarefa aguarda a liberação dos registros para o disco. Estima-se que esse estado de espera seja mantido por longos períodos de tempo.| 
|DBSEEDING_FLOWCONTROL |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|DBSEEDING_OPERATION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|DEADLOCK_ENUM_MUTEX |Ocorre quando o monitor de deadlock e o sys. dm_os_waiting_tasks tentam certificar-se de que SQL Server não está executando várias pesquisas de deadlock ao mesmo tempo.| 
|DEADLOCK_TASK_SEARCH |Um grande tempo de espera nesse recurso indica que o servidor está realizando consultas na parte superior de sys.dm_os_waiting_tasks e que essas consultas estão impedindo o monitor de deadlock de pesquisar deadlocks. Esse tipo de espera só é usado através de monitor de deadlock. Consultas na parte superior de sys.dm_os_waiting_tasks usam DEADLOCK_ENUM_MUTEX.| 
|DEBUG |Ocorre durante a depuração de CLR e Transact-SQL para sincronização interna.| 
|DIRECTLOGCONSUMER_LIST |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|DIRTY_PAGE_POLL |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|DIRTY_PAGE_SYNC |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|DIRTY_PAGE_TABLE_LOCK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|DISABLE_VERSIONING |Ocorre quando SQL Server sonda a versão do Gerenciador de transações para ver se o carimbo de data/hora da transação ativa mais antiga é posterior ao carimbo de data/hora de quando o estado começou a ser alterado. Se esse for o caso, todas as transações de instantâneo iniciadas antes de a instrução ALTER DATABASE ter sido executada serão finalizadas. Esse estado de espera é usado quando SQL Server desabilita o controle de versão usando a instrução ALTER DATABASE.| 
|DISKIO_SUSPEND |Ocorre quando uma tarefa estiver esperando para acessar um arquivo quando um backup externo está ativo. Isso é informado a cada processo de usuário de espera. Uma contagem maior que cinco por processo de usuário pode indicar que o backup externo está levando muito tempo para ser concluído.| 
|DISPATCHER_PRIORITY_QUEUE_SEMAPHORE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|DISPATCHER_QUEUE_SEMAPHORE |Ocorre quando um thread do pool de dispatcher está aguardando mais trabalho para processamento. Estima-se que o tempo para esse tipo de espera aumente quando o dispatcher estiver ocioso.| 
|DLL_LOADING_MUTEX |Ocorre uma vez ao aguardar a DLL do analisador XML ser carregada.| 
|DPT_ENTRY_LOCK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|DROP_DATABASE_TIMER_TASK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|DROPTEMP |Ocorre entre tentativas para descartar um objeto temporário caso a tentativa anterior tenha falhado. A duração da espera cresce bastante em cada tentativa de descarte com falha.| 
|DTC |Ocorre quando uma tarefa estiver esperando um evento usado para gerenciar a transição de estado. Esse estado controla quando a recuperação de transações do Microsoft Coordenador de Transações Distribuídas (MS DTC) ocorre depois que SQL Server recebe uma notificação informando que o serviço MS DTC tornou-se indisponível.| 
|DTC_ABORT_REQUEST |Ocorre em uma sessão de trabalhador de MS DTC quando a sessão estiver aguardando para obter a propriedade de uma transação de MS DTC. Depois que o MS DTC for proprietário da transação, a sessão poderá reverter a transação. Geralmente, a sessão esperará por outra sessão que está usando a transação.| 
|DTC_RESOLVE |Ocorre quando uma tarefa de recuperação está aguardando o banco de dados mestre em uma transação de banco de dados cruzado de forma que a tarefa possa consultar o resultado da transação.| 
|DTC_STATE |Ocorre quando uma tarefa está esperando um evento que protege as alterações no objeto de estado global de MS DTC. Esse estado deve ser mantido para intervalos de tempo muito curtos.| 
|DTC_TMDOWN_REQUEST |Ocorre em uma sessão de trabalho do MS DTC quando SQL Server recebe uma notificação informando que o serviço MS DTC não está disponível. Primeiro, o trabalhador aguardará o processo de recuperação de MS DTC iniciar. Em seguida, o trabalhador espera para obter o resultado da transação distribuída em que o trabalhador está trabalhando. Isso pode continuar até a conexão com o serviço de MS DTC ser restabelecida.| 
|DTC_WAITFOR_OUTCOME |Ocorre quando as tarefas de recuperação aguardam o MS DTC ficar ativo para ativar a resolução de transações preparadas.| 
|DTCNEW_ENLIST |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|DTCNEW_PREPARE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|DTCNEW_RECOVERY |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|DTCNEW_TM |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|DTCNEW_TRANSACTION_ENLISTMENT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|DTCPNTSYNC |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|DUMP_LOG_COORDINATOR |Ocorre quando uma tarefa principal está esperando uma subtarefa gerar dados. Em geral, esse estado não ocorre. Uma espera longa indica um bloqueio inesperado. A subtarefa deve ser investigada.| 
|DUMP_LOG_COORDINATOR_QUEUE |Somente para uso interno.| 
|DUMPTRIGGER |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|EC |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|EE_PMOLOCK |Ocorre durante a sincronização de certos tipos de alocações de memória durante execução de instrução.| 
|EE_SPECPROC_MAP_INIT |Ocorre durante sincronização da criação de tabela de hash de procedimento interno. Essa espera só pode ocorrer durante o acesso inicial da tabela de hash depois que a instância de SQL Server é iniciada.| 
|ENABLE_EMPTY_VERSIONING |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|ENABLE_VERSIONING |Ocorre quando SQL Server aguarda que todas as transações de atualização nesse banco de dados sejam concluídas antes de declarar o banco de dados pronto para fazer a transição para o estado permitido de isolamento de instantâneo. Esse estado é usado quando SQL Server habilita o isolamento de instantâneo usando a instrução ALTER DATABASE.| 
|ERROR_REPORTING_MANAGER |Ocorre durante a sincronização de várias inicializações de log de erros simultâneas.| 
|EXCHANGE |Ocorre durante a sincronização no iterador de troca de processador de consulta durante consultas paralelas.| 
|EXECSYNC |Ocorre durante consultas paralelas durante a sincronização em processador de consulta em áreas não relacionadas ao iterador de troca. Exemplos dessas áreas são bitmaps, LOBs (objetos binários grandes) e o iterador de spool. Os LOBs podem usar esse estado de espera frequentemente.| 
|EXECUTION_PIPE_EVENT_INTERNAL |Ocorre durante a sincronização entre o produtor e partes do consumidor de execução em lotes que são enviados por meio do contexto da conexão.| 
|EXTERNAL_RG_UPDATE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|EXTERNAL_SCRIPT_NETWORK_IO |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] até atual.| 
|EXTERNAL_SCRIPT_PREPARE_SERVICE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|EXTERNAL_SCRIPT_SHUTDOWN |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|EXTERNAL_WAIT_ON_LAUNCHER, |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|FABRIC_HADR_TRANSPORT_CONNECTION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|FABRIC_REPLICA_CONTROLLER_LIST |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|FABRIC_REPLICA_CONTROLLER_STATE_AND_CONFIG |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|FABRIC_REPLICA_PUBLISHER_EVENT_PUBLISH |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|FABRIC_REPLICA_PUBLISHER_SUBSCRIBER_LIST |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|FABRIC_WAIT_FOR_BUILD_REPLICA_EVENT_PROCESSING |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|FAILPOINT |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|FCB_REPLICA_READ |Ocorre quando as leituras de um arquivo esparso de instantâneo (ou um instantâneo temporário criado por DBCC) são sincronizadas.| 
|FCB_REPLICA_WRITE |Ocorre quando o envio ou a remoção de uma página de um arquivo esparso de instantâneo (ou de um instantâneo temporário criado por DBCC) é sincronizado.| 
|FEATURE_SWITCHES_UPDATE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|FFT_NSO_DB_KILL_FLAG |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FFT_NSO_DB_LIST |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FFT_NSO_FCB |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FFT_NSO_FCB_FIND |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FFT_NSO_FCB_PARENT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FFT_NSO_FCB_RELEASE_CACHED_ENTRIES |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FFT_NSO_FCB_STATE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|FFT_NSO_FILEOBJECT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FFT_NSO_TABLE_LIST |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FFT_NTFS_STORE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FFT_RECOVERY |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FFT_RSFX_COMM |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FFT_RSFX_WAIT_FOR_MEMORY |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FFT_STARTUP_SHUTDOWN |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FFT_STORE_DB |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FFT_STORE_ROWSET_LIST |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FFT_STORE_TABLE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FILE_VALIDATION_THREADS |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|FILESTREAM_CACHE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FILESTREAM_CHUNKER |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FILESTREAM_CHUNKER_INIT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FILESTREAM_FCB |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FILESTREAM_FILE_OBJECT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FILESTREAM_WORKITEM_QUEUE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FILETABLE_SHUTDOWN |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FOREIGN_REDO |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] até atual.| 
|FORWARDER_TRANSITION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
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
|FT_MASTER_MERGE_COORDINATOR |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FT_METADATA_MUTEX |Documentado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|FT_PROPERTYLIST_CACHE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|FT_RESTART_CRAWL |Ocorre quando um rastreamento de texto completo precisa ser reiniciado a partir do último ponto conhecido bom para recuperação de uma falha momentânea. A espera deixa as tarefas do trabalhador em execução na população para concluir a etapa atual ou sair dela.| 
|FULLTEXT GATHERER |Ocorre durante a sincronização de operações de texto completo.| 
|GDMA_GET_RESOURCE_OWNER |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|GHOSTCLEANUP_UPDATE_STATS |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|GHOSTCLEANUPSYNCMGR |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|GLOBAL_QUERY_CANCEL |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|GLOBAL_QUERY_CLOSE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|GLOBAL_QUERY_CONSUMER |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|GLOBAL_QUERY_PRODUCER |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|GLOBAL_TRAN_CREATE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|GLOBAL_TRAN_UCS_SESSION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|GUARDIAN |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|HADR_AG_MUTEX |Ocorre quando uma instrução DDL Always On ou o comando Windows Server failover clustering está aguardando acesso de leitura/gravação exclusivo para a configuração de um grupo de disponibilidade. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_AR_CRITICAL_SECTION_ENTRY |Ocorre quando uma instrução DDL Always On ou o comando Windows Server failover clustering está aguardando o acesso de leitura/gravação exclusivo para o estado de tempo de execução da réplica local do grupo de disponibilidade associado. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_AR_MANAGER_MUTEX |Ocorre quando um desligamento da réplica de disponibilidade está aguardando a inicialização ser concluída ou uma inicialização de réplica de disponibilidade está aguardando o desligamento ser concluído. Somente uso interno., <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_AR_UNLOAD_COMPLETED |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_ARCONTROLLER_NOTIFICATIONS_SUBSCRIBER_LIST |O publicador para um evento de réplica de disponibilidade (como uma alteração de estado ou alteração de configuração) está aguardando acesso de leitura/gravação exclusivo à lista de assinantes do evento. Somente uso interno., <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_BACKUP_BULK_LOCK |O banco de dados primário Always On recebeu uma solicitação de backup de um banco de dados secundário e está aguardando que o thread em segundo plano termine de processar a solicitação na aquisição ou liberação do bloqueio BulkOp. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_BACKUP_QUEUE |O thread de segundo plano de backup do banco de dados primário Always On está aguardando uma nova solicitação de trabalho do banco de dados secundário. (normalmente, isso ocorre quando o banco de dados primário está mantendo o log BulkOp e aguarda o banco de dados secundário indicar que o banco de dados primário pode liberar o bloqueio). <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_CLUSAPI_CALL |Um thread de SQL Server está aguardando para alternar do modo não preemptivo (agendado por SQL Server) para o modo Preemptive (agendado pelo sistema operacional) para invocar as APIs de clustering de failover do Windows Server. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_COMPRESSED_CACHE_SYNC |Aguardando o acesso ao cache de blocos de log compactados que é usado para evitar a compactação redundante dos blocos de log enviados a vários bancos de dados secundários. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_CONNECTIVITY_INFO |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_DATABASE_FLOW_CONTROL |Aguardando as mensagens serem enviadas ao parceiro quando o número máximo de mensagens enfileiradas tiver sido alcançado. Indica que os exames de log estão sendo executadas mais rapidamente que os envios da rede. Esse é um problema somente se os envios de rede forem mais lentos do que o esperado. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_DATABASE_VERSIONING_STATE |Ocorre na alteração de estado de controle de versão de um banco de dados secundário Always On. Essa espera é para estruturas de dados internas e geralmente é muito curta sem efeito direto sobre o acesso a dados. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_DATABASE_WAIT_FOR_RECOVERY |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|HADR_DATABASE_WAIT_FOR_RESTART |Aguardando o banco de dados reiniciar em Always On controle grupos de disponibilidade. Em condições normais, esse não é um problema de cliente porque esperas são esperadas aqui. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_DATABASE_WAIT_FOR_TRANSITION_TO_VERSIONING |Uma consulta em objetos em um banco de dados secundário legível de um grupo de disponibilidade Always On é bloqueada no controle de versão de linha enquanto aguarda a confirmação ou a reversão de todas as transações que estavam em andamento quando a réplica secundária foi habilitada para cargas de trabalho de leitura. Esse tipo de espera garante que as versões de linha estejam disponíveis antes da execução de uma consulta em isolamento de instantâneo. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_DB_COMMAND |Aguardando respostas a mensagens de conversação (que exigem uma resposta explícita do outro lado, usando a Always On infraestrutura de mensagens de conversação). Vários tipos de mensagem diferentes usam esse tipo de espera., <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_DB_OP_COMPLETION_SYNC |Aguardando respostas a mensagens de conversação (que exigem uma resposta explícita do outro lado, usando a Always On infraestrutura de mensagens de conversação). Vários tipos de mensagem diferentes usam esse tipo de espera., <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_DB_OP_START_SYNC |Uma Always On instrução DDL ou um comando Windows Server failover clustering está aguardando o acesso serializado a um banco de dados de disponibilidade e seu estado de tempo de execução. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_DBR_SUBSCRIBER |O publicador para um evento de réplica de disponibilidade (como uma alteração de estado ou alteração de configuração) está aguardando acesso de leitura/gravação para o estado de runtime de um assinante de evento que corresponda a um banco de dados de disponibilidade. Somente uso interno., <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_DBR_SUBSCRIBER_FILTER_LIST |O publicador para um evento de réplica de disponibilidade (como uma alteração de estado ou alteração de configuração) está aguardando acesso de leitura/gravação para a lista de assinantes do evento que correspondam aos bancos de dados de disponibilidade. Somente uso interno., <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_DBSEEDING |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|HADR_DBSEEDING_LIST |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|HADR_DBSTATECHANGE_SYNC |O controle de simultaneidade aguarda a atualização do estado interno da réplica de banco de dados. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_FABRIC_CALLBACK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|HADR_FILESTREAM_BLOCK_FLUSH |O Gerenciador de transporte de Always On FILESTREAM está aguardando até que o processamento de um bloco de log seja concluído. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_FILESTREAM_FILE_CLOSE |O Gerenciador de transporte de Always On FILESTREAM está aguardando até que o próximo arquivo FILESTREAM seja processado e seu identificador seja fechado. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_FILESTREAM_FILE_REQUEST |Um Always On réplica secundária está aguardando a réplica primária enviar todos os arquivos FILESTREAM solicitados durante a ação desfazer. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_FILESTREAM_IOMGR |O Gerenciador de transporte de Always On FILESTREAM está aguardando um bloqueio de R/W que protege o FILESTREAM Always On o Gerenciador de e/s durante a inicialização ou desligamento., <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_FILESTREAM_IOMGR_IOCOMPLETION |O Gerenciador de e/s de FILESTREAM Always On está aguardando a conclusão de e/s., <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_FILESTREAM_MANAGER |O Gerenciador de transporte de Always On FILESTREAM está aguardando o bloqueio de R/W que protege o FILESTREAM Always On o Gerenciador de transporte durante a inicialização ou o desligamento. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_FILESTREAM_PREPROC |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|HADR_GROUP_COMMIT |O processamento da confirmação de transação está aguardando uma confirmação de grupo de modo que vários registros de log de confirmação possam ser colocados em um único bloco de log. Essa espera é uma condição esperada que otimiza as operações de e/s de log, captura e envio. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_LOGCAPTURE_SYNC |Controle de simultaneidade ao redor da captura de log ou objeto de aplicação ao criar ou destruir exames. Essa é uma espera esperada quando os parceiros alteram o estado ou o status da conexão. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_LOGCAPTURE_WAIT |Aguardando os registros de log ficarem disponíveis. Pode ocorrer ao esperar novos registros de log serem gerados por conexões ou para a conclusão de E/S ao ler log não no cache. Essa é uma espera esperada se a verificação de log for exibida até o final do log ou se estiver lendo do disco. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_LOGPROGRESS_SYNC |O controle de simultaneidade aguarda ao atualizar o status de progresso de log das réplicas de banco de dados. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_NOTIFICATION_DEQUEUE |Uma tarefa em segundo plano que processa as notificações do Windows Server Failover Clustering está aguardando a próxima notificação. Somente uso interno., <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_NOTIFICATION_WORKER_EXCLUSIVE_ACCESS |O Gerenciador de réplica de disponibilidade Always On está aguardando o acesso serializado ao estado de tempo de execução de uma tarefa em segundo plano que processa as notificações de clustering de failover do Windows Server. Somente uso interno., <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_NOTIFICATION_WORKER_STARTUP_SYNC |Uma tarefa em segundo plano está aguardando a conclusão da inicialização de uma tarefa em segundo plano que processa as notificações do Windows Server Failover Clustering. Somente uso interno., <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_NOTIFICATION_WORKER_TERMINATION_SYNC |Uma tarefa em segundo plano está aguardando a conclusão de uma tarefa em segundo plano que processa as notificações do Windows Server Failover Clustering. Somente uso interno., <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_PARTNER_SYNC |Espera de controle de simultaneidade na lista de parceiros. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_READ_ALL_NETWORKS |Aguardando para obter acesso de leitura ou gravação para a lista de redes do WSFC. Somente para uso interno. Observação: o mecanismo mantém uma lista de redes WSFC que é usada em exibições de gerenciamento dinâmico (como sys. dm_hadr_cluster_networks) ou para validar Always On instruções Transact-SQL que fazem referência a informações de rede do WSFC. Essa lista é atualizada após a inicialização do mecanismo, as notificações relacionadas ao WSFC e a reinicialização interna de Always On (por exemplo, perder e reconhecer o quorum do WSFC). As tarefas serão geralmente bloqueadas quando uma atualização nessa lista estiver em andamento. , <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_RECOVERY_WAIT_FOR_CONNECTION |Aguardando o banco de dados secundário conectar-se ao banco de dados primário antes de executar a recuperação. Essa é uma espera esperada, que pode aumentar se a conexão com a primária estiver lenta para estabelecer., <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_RECOVERY_WAIT_FOR_UNDO |A recuperação de banco de dados está aguardando o banco de dados secundário concluir a fase de reversão e inicialização para devolvê-lo ao ponto de log comum com o banco de dados primário. Essa é uma espera esperada após failovers. O progresso de desfazer pode ser acompanhado por meio do monitor de sistema do Windows (perfmon.exe) e exibições de gerenciamento dinâmico. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_REPLICAINFO_SYNC |Aguardando controle de simultaneidade atualizar o estado da réplica atual., <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_SEEDING_CANCELLATION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|HADR_SEEDING_FILE_LIST |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|HADR_SEEDING_LIMIT_BACKUPS |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|HADR_SEEDING_SYNC_COMPLETION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|HADR_SEEDING_TIMEOUT_TASK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|HADR_SEEDING_WAIT_FOR_COMPLETION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|HADR_SYNC_COMMIT |Aguardando o processamento da confirmação de transação para os bancos de dados secundários sincronizados proteger o log. Esta espera também é refletida pelo contador de desempenho de Atraso na Transação. Esse tipo de espera é esperado para grupos de disponibilidade sincronizados e indica o tempo para enviar, gravar e confirmar o log para os bancos de dados secundários. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_SYNCHRONIZING_THROTTLE |Aguardando o processamento de confirmação de transação permitir que um banco de dados secundário de sincronização atualize o final primário do log para fazer a transição para o estado sincronizado. Essa é uma espera esperada quando um banco de dados secundário está sendo atualizado. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_TDS_LISTENER_SYNC |O sistema de Always On interno ou o Cluster WSFC solicitará que os ouvintes sejam iniciados ou interrompidos. O processamento desta solicitação é sempre assíncrono e há um mecanismo para remover solicitações redundantes. Também há momentos em que este processo é suspenso devido a alterações de configuração. Todas as esperas relacionadas com este mecanismo de sincronização de ouvinte usam este tipo de espera. Somente uso interno., <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_TDS_LISTENER_SYNC_PROCESSING |Usado no final de uma Always On instrução Transact-SQL que requer iniciar e/ou parar um ouvinte de grupo de disponibilidade. Como a operação iniciar/parar é feita de forma assíncrona, o thread do usuário será bloqueado usando esse tipo de espera até que a situação do ouvinte seja conhecida. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_THROTTLE_LOG_RATE_GOVERNOR |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|HADR_THROTTLE_LOG_RATE_MISMATCHED_SLO | Ocorre quando um secundário de replicação geográfica é configurado com o tamanho de computação inferior (SLO menor) do que o primário. Um banco de dados primário é limitado devido ao consumo de log atrasado pelo secundário. Isso é causado pelo banco de dados secundário com capacidade de computação insuficiente para acompanhar a taxa de alteração do banco de dados primário. <br /> **Aplica-se a**: banco de dados SQL do Azure| 
|HADR_THROTTLE_LOG_RATE_LOG_SIZE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|HADR_THROTTLE_LOG_RATE_SEEDING |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|HADR_THROTTLE_LOG_RATE_SEND_RECV_QUEUE_SIZE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|HADR_TIMER_TASK |Aguardando para obter o bloqueio no objeto de tarefa de temporizador e também é usado para as esperas reais entre os momentos em que o trabalho está sendo realizado. Por exemplo, para uma tarefa que é executada a cada 10 segundos, após uma execução, Always On grupos de disponibilidade aguarda cerca de 10 segundos para reagendar a tarefa e a espera é incluída aqui., <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_TRANSPORT_DBRLIST |Aguardando acesso à lista de réplica de banco de dados da camada de transporte. Usado para o SpinLock que concede acesso a ele. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_TRANSPORT_FLOW_CONTROL |Aguardando quando o número de mensagens de Always On não confirmadas pendentes está acima do limite de controle de fluxo de saída. Isso está em uma base réplica-para-réplica de disponibilidade (não está em uma base de banco de dados para banco de dados). <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_TRANSPORT_SESSION |Always On grupos de disponibilidade estão aguardando ao alterar ou acessar o estado de transporte subjacente. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_WORK_POOL |Espera de controle de simultaneidade no objeto de tarefa de trabalho em segundo plano de grupos de disponibilidade de Always On. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_WORK_QUEUE |Always On thread de trabalho em segundo plano de grupos de disponibilidade aguardando a atribuição de um novo trabalho. Essa é uma espera esperada quando há trabalhadores prontos aguardando um novo trabalho, que é o estado normal. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HADR_XRF_STACK_ACCESS |Acessando (pesquise, adicione e exclua) a pilha de bifurcação de recuperação estendida para um banco de dados de Always On disponibilidade. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HCCO_CACHE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|HK_RESTORE_FILEMAP |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|HKCS_PARALLEL_MIGRATION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|HKCS_PARALLEL_RECOVERY |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|HTBUILD |Ocorre com planos paralelos de modo de lote ao sincronizar a compilação da tabela de hash no lado de entrada de uma junção/agregação hash. Se a espera for excessiva e não puder ser reduzida ajustando a consulta (como adicionando índices), ajuste o limite de custo para paralelismo ou reduza o grau de paralelismo. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HTDELETE |Ocorre com planos paralelos de modo de lote ao sincronizar no final de uma junção/agregação hash. Se a espera for excessiva e não puder ser reduzida ajustando a consulta (como adicionando índices), ajuste o limite de custo para paralelismo ou reduza o grau de paralelismo. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|HTMEMO |Ocorre com planos paralelos de modo de lote ao sincronizar antes de examinar a tabela de hash para correspondências/não correspondências na junção/agregação hash. Se a espera for excessiva e não puder ser reduzida ajustando a consulta (como adicionando índices), ajuste o limite de custo para paralelismo ou reduza o grau de paralelismo. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|HTREINIT |Ocorre com planos paralelos de modo de lote ao sincronizar antes de redefinir uma junção/agregação hash para a próxima junção parcial. Se a espera for excessiva e não puder ser reduzida ajustando a consulta (como adicionando índices), ajuste o limite de custo para paralelismo ou reduza o grau de paralelismo. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|HTREPARTITION |Ocorre com planos paralelos de modo de lote ao sincronizar o reparticionamento da tabela de hash no lado de entrada de uma junção/agregação hash. Se a espera for excessiva e não puder ser reduzida ajustando a consulta (como adicionando índices), ajuste o limite de custo para paralelismo ou reduza o grau de paralelismo.<br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|HTTP_ENUMERATION |Ocorre na inicialização para enumerar os pontos de extremidade de HTTP para iniciar o HTTP.| 
|HTTP_START |Ocorre quando uma conexão está esperando que o HTTP conclua a inicialização.| 
|HTTP_STORAGE_CONNECTION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|IMPPROV_IOWAIT |Ocorre quando SQL Server aguarda a conclusão de uma e/s de carregamento em massa.| 
|INSTANCE_LOG_RATE_GOVERNOR |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|INTERNAL_TESTING |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|IO_AUDIT_MUTEX |Ocorre durante a sincronização de buffers de evento de rastreamento.| 
|IO_COMPLETION |Ocorre enquanto se espera as operações de E/S serem concluídas. Esse tipo de espera geralmente representa E/Ss de página sem-dados. As esperas de conclusão de e/s de página de dados aparecem como \_ \* esperas de PAGEIOLATCH.| 
|IO_QUEUE_LIMIT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|IO_RETRY |Ocorre quando uma operação de E/S, como uma leitura ou uma gravação no disco, falha devido a recursos insuficientes, e é tentada novamente.| 
|IOAFF_RANGE_QUEUE |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|KSOURCE_WAKEUP |Usado pela tarefa de controle de serviço ao aguardar solicitações do Gerenciador de Controle de Serviços. Esperas longas estão previstas e não indicam um problema.| 
|KTM_ENLISTMENT |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|KTM_RECOVERY_MANAGER |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|KTM_RECOVERY_RESOLUTION |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|LATCH_DT |Ocorre ao esperar uma trava de DT (destruir). Isso não inclui travas de buffer ou de marcação de transação. Uma lista de \_ \* esperas de trava está disponível em sys. dm_os_latch_stats. Observe que sys.dm_os_latch_stats agrupa LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX e LATCH_DT.| 
|LATCH_EX |Ocorre ao esperar uma trava de EX (exclusivo). Isso não inclui travas de buffer ou de marcação de transação. Uma lista de \_ \* esperas de trava está disponível em sys. dm_os_latch_stats. Observe que sys.dm_os_latch_stats agrupa LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX e LATCH_DT.| 
|LATCH_KP |Ocorre ao esperar uma trava de KP (manutenção). Isso não inclui travas de buffer ou de marcação de transação. Uma lista de \_ \* esperas de trava está disponível em sys. dm_os_latch_stats. Observe que sys.dm_os_latch_stats agrupa LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX e LATCH_DT.| 
|LATCH_NL |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|LATCH_SH |Ocorre ao esperar uma trava de SH (compartilhamento). Isso não inclui travas de buffer ou de marcação de transação. Uma lista de \_ \* esperas de trava está disponível em sys. dm_os_latch_stats. Observe que sys.dm_os_latch_stats agrupa LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX e LATCH_DT.| 
|LATCH_UP |Ocorre ao esperar uma trava de UP (atualização). Isso não inclui travas de buffer ou de marcação de transação. Uma lista de \_ \* esperas de trava está disponível em sys. dm_os_latch_stats. Observe que sys.dm_os_latch_stats agrupa LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX e LATCH_DT.| 
|LAZYWRITER_SLEEP |Ocorre quando as tarefas de gravador lentas são suspensas. É uma medição do tempo gasto por tarefas em segundo plano em espera. Não considere esse estado quando você estiver procurando pausas de usuário.| 
|LCK_M_BU |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização em Massa (BU).| 
|LCK_M_BU_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio BU (Atualização em Massa) com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_BU_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio BU (Atualização em Massa) com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_IS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Tentativa Compartilhada (IS).| 
|LCK_M_IS_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio IS (Tentativa Compartilhada) com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_IS_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio IS (Tentativa Compartilhada) com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_IU |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização da Tentativa (IU).| 
|LCK_M_IU_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio IU (Tentativa de Atualização) com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_IU_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio IU (Tentativa de Atualização) com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_IX |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Exclusivo da Tentativa (IX).| 
|LCK_M_IX_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio IX (Exclusivo da Tentativa) com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_IX_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio IX (Exclusivo da Tentativa) com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_RIn_NL |Ocorre quando uma tarefa está esperando adquirir um bloqueio NULL no valor de chave atual e um bloqueio Inserção de Intervalo entre a chave atual e a anterior. Um bloqueio NULL na chave é um bloqueio de liberação instantâneo.| 
|LCK_M_RIn_NL_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio NULL com Bloqueadores de Anulação no valor da chave atual e um bloqueio Inserção de Intervalo com Bloqueadores de Anulação entre a chave atual e a anterior. Um bloqueio NULL na chave é um bloqueio de liberação instantâneo. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_RIn_NL_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio NULL com Baixa Prioridade no valor da chave atual e um bloqueio Inserção de Intervalo com Baixa Prioridade entre a chave atual e a anterior. Um bloqueio NULL na chave é um bloqueio de liberação instantâneo. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_RIn_S |Ocorre quando uma tarefa está esperando adquirir um bloqueio compartilhado no valor de chave atual e um bloqueio Inserção de Intervalo entre a chave atual e a anterior.| 
|LCK_M_RIn_S_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio compartilhado com Bloqueadores de Anulação no valor da chave atual e um bloqueio Inserção de Intervalo com Bloqueadores de Anulação entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_RIn_S_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio compartilhado com Baixa Prioridade no valor da chave atual e um bloqueio Inserção de Intervalo com Baixa Prioridade entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_RIn_U |Uma tarefa que está esperando para adquirir um bloqueio Atualização no valor de chave atual e um bloqueio Inserção de Intervalo entre a chave atual e a anterior.| 
|LCK_M_RIn_U_ABORT_BLOCKERS |A tarefa está esperando para adquirir um bloqueio Atualização com Bloqueadores de Anulação no valor da chave atual e um bloqueio Inserção de Intervalo com Bloqueadores de Anulação entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_RIn_U_LOW_PRIORITY |A tarefa está esperando para adquirir um bloqueio Atualização com Baixa Prioridade no valor da chave atual e um bloqueio Inserção de Intervalo com Baixa Prioridade entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_RIn_X |Ocorre quando uma tarefa está esperando adquirir um bloqueio Exclusivo no valor de chave atual e um bloqueio Inserção de Intervalo entre a chave atual e a anterior.| 
|LCK_M_RIn_X_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Exclusivo com Bloqueadores de Anulação no valor da chave atual e um bloqueio Inserção de Intervalo com Bloqueadores de Anulação entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_RIn_X_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Exclusivo com Baixa Prioridade no valor da chave atual e um bloqueio Inserção de Intervalo com Baixa Prioridade entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_RS_S |Ocorre quando uma tarefa está esperando adquirir um bloqueio Compartilhado no valor de chave atual e um bloqueio Intervalo Compartilhado entre a chave atual e a anterior.| 
|LCK_M_RS_S_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Bloqueadores de Anulação no valor da chave atual e um bloqueio Intervalo Compartilhado com Bloqueadores de Anulação entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_RS_S_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Baixa Prioridade no valor da chave atual e um bloqueio Intervalo Compartilhado com Baixa Prioridade entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_RS_U |Ocorre quando uma tarefa está esperando adquirir um bloqueio Atualização no valor de chave atual e um bloqueio Atualização de Intervalo entre a chave atual e a anterior.| 
|LCK_M_RS_U_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização com Bloqueadores de Anulação no valor da chave atual e um bloqueio Intervalo de Atualização com Bloqueadores de Anulação entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_RS_U_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização com Baixa Prioridade no valor da chave atual e um bloqueio Intervalo de Atualização com Baixa Prioridade entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_RX_S |Ocorre quando uma tarefa está esperando adquirir um bloqueio Compartilhado no valor de chave atual e um bloqueio Intervalo Exclusivo entre a chave atual e a anterior.| 
|LCK_M_RX_S_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Bloqueadores de Anulação no valor da chave atual e um bloqueio Intervalo Exclusivo com Bloqueadores de Anulação entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_RX_S_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Baixa Prioridade no valor da chave atual e um bloqueio Intervalo Exclusivo com Baixa Prioridade entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_RX_U |Ocorre quando uma tarefa está esperando adquirir um bloqueio Atualização no valor de chave atual e um bloqueio Intervalo Exclusivo entre a chave atual e a anterior.| 
|LCK_M_RX_U_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização com Bloqueadores de Anulação no valor da chave atual e um bloqueio Intervalo Exclusivo com Bloqueadores de Anulação entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_RX_U_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização com Baixa Prioridade no valor da chave atual e um bloqueio Intervalo Exclusivo com Baixa Prioridade entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_RX_X |Ocorre quando uma tarefa está esperando adquirir um bloqueio Exclusivo no valor de chave atual e um bloqueio Intervalo Exclusivo entre a chave atual e a anterior.| 
|LCK_M_RX_X_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Exclusivo com Bloqueadores de Anulação no valor da chave atual e um bloqueio Intervalo Exclusivo com Bloqueadores de Anulação entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_RX_X_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Exclusivo com Baixa Prioridade no valor da chave atual e um bloqueio Intervalo Exclusivo com Baixa Prioridade entre a chave atual e a anterior. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_S |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado.| 
|LCK_M_S_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_S_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_SCH_M |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Modificação de Esquema.| 
|LCK_M_SCH_M_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Modificação de Esquema com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_SCH_M_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Modificação de Esquema com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_SCH_S |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhamento de Esquema.| 
|LCK_M_SCH_S_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhamento de Esquema com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_SCH_S_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhamento de Esquema com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_SIU |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Atualização da Tentativa.| 
|LCK_M_SIU_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Tentativa de Atualização com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_SIU_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Tentativa de Atualização com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_SIX |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Exclusivo da Tentativa.| 
|LCK_M_SIX_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Exclusivo da Tentativa com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_SIX_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Exclusivo da Tentativa com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_U |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização.| 
|LCK_M_U_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_U_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_UIX |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização com Exclusivo da Tentativa.| 
|LCK_M_UIX_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização com Exclusivo da Tentativa com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_UIX_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização com Exclusivo da Tentativa com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_X |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Exclusivo.| 
|LCK_M_X_ABORT_BLOCKERS |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Exclusivo com Bloqueadores de Anulação. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LCK_M_X_LOW_PRIORITY |Ocorre quando uma tarefa está esperando para adquirir um bloqueio Exclusivo com Baixa Prioridade. (Relacionado à opção de espera de baixa prioridade de ALTER TABLE e ALTER INDEX.) <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|LOG_POOL_SCAN |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|LOG_RATE_GOVERNOR |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|LOGBUFFER |Ocorre quando uma tarefa está esperando espaço no buffer de log para armazenar um registro de log. Consistentemente, valores altos podem indicar que os dispositivos de log não podem acompanhar a quantidade de log que está sendo gerada pelo servidor.| 
|LOGCAPTURE_LOGPOOLTRUNCPOINT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|LOGGENERATION |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|LOGMGR |Ocorre quando uma tarefa está aguardando que qualquer E/S de log pendente seja concluída antes de desativar o log durante o fechamento do banco de dados.| 
|LOGMGR_FLUSH |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|LOGMGR_PMM_LOG |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|LOGMGR_QUEUE |Ocorre enquanto a tarefa de gravador de log aguarda solicitações de trabalho.| 
|LOGMGR_RESERVE_APPEND |Ocorre quando uma tarefa está esperando para verificar se o truncamento de log libera espaço para logs, para que a tarefa possa gravar um novo registro de log. Considere aumentar o tamanho do(s) arquivo(s) de log para o banco de dados afetado para reduzir essa espera.| 
|LOGPOOL_CACHESIZE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|LOGPOOL_CONSUMER |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|LOGPOOL_CONSUMERSET |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|LOGPOOL_FREEPOOLS |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|LOGPOOL_MGRSET |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|LOGPOOL_REPLACEMENTSET |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|LOGPOOLREFCOUNTEDOBJECT_REFDONE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|LOWFAIL_MEMMGR_QUEUE |Ocorre ao aguardar que a memória esteja disponível para uso.| 
|MD_AGENT_YIELD |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|MD_LAZYCACHE_RWLOCK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|MEMORY_ALLOCATION_EXT |Ocorre ao alocar memória do pool de memória interno SQL Server ou do sistema operacional. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|MEMORY_GRANT_UPDATE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|METADATA_LAZYCACHE_RWLOCK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] somente. |  
|MIGRATIONBUFFER |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|MISCELLANEOUS |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|MISCELLANEOUS |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|MSQL_DQ |Ocorre quando uma tarefa está aguardando que uma operação de consulta distribuída seja concluída. Isso é usado para detectar deadlocks de aplicativo MARS (Vários Conjuntos de Resultados Ativos) potenciais. A espera termina quando a chamada de consulta distribuída é concluída.| 
|MSQL_XACT_MGR_MUTEX |Ocorre quando uma tarefa está aguardando para obter a propriedade do gerenciador de transações de sessão para executar uma operação de transação em nível de sessão.| 
|MSQL_XACT_MUTEX |Ocorre durante sincronização de uso de transação. Uma solicitação deve adquirir o mutex antes de usar a transação.| 
|MSQL_XP |Ocorre quando uma tarefa está esperando a finalização de um procedimento armazenado estendido. SQL Server usa esse estado de espera para detectar deadlocks de aplicativo MARS potenciais. A espera para quando a chamada do procedimento armazenado estendido termina.| 
|MSSEARCH |Ocorre durante chamadas de pesquisa de texto completo. Essa espera termina quando a operação de texto completo é concluída. Ela não indica contenção, mas a duração de operações de texto completo.| 
|NET_WAITFOR_PACKET |Ocorre quando uma conexão está esperando um pacote de rede durante uma leitura de rede.| 
|NETWORKSXMLMGRLOAD |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|NODE_CACHE_MUTEX |Somente para uso interno.| 
|OLEDB |Ocorre quando SQL Server chama o provedor de OLE DB de SQL Server Native Client. Esse tipo de espera não é usado para sincronização. Em vez disso, ele indica a duração de chamadas ao provedor OLE DB.| 
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
|PARALLEL_REDO_DRAIN_WORKER |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|PARALLEL_REDO_FLOW_CONTROL |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|PARALLEL_REDO_LOG_CACHE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|PARALLEL_REDO_TRAN_LIST |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|PARALLEL_REDO_TRAN_TURN |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|PARALLEL_REDO_WORKER_SYNC |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|PARALLEL_REDO_WORKER_WAIT_WORK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|PERFORMANCE_COUNTERS_RWLOCK |Somente para uso interno.| 
|PHYSICAL_SEEDING_DMV |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|POOL_LOG_RATE_GOVERNOR |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|PREEMPTIVE_ABR |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|PREEMPTIVE_AUDIT_ACCESS_EVENTLOG |Ocorre quando o agendador de Sistema operacional (SQLOS) [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] alterna para o modo preemptivo para gravar um evento de auditoria para o log de eventos do Windows. <br /> **Aplica-se a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] somente. |  
|PREEMPTIVE_AUDIT_ACCESS_SECLOG |Ocorre quando o agendador de Sistema operacional (SQLOS) alterna para o modo preemptivo para gravar um evento de auditoria para o log de segurança do Windows. <br /> **Aplica-se a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] somente. |  
|PREEMPTIVE_CLOSEBACKUPMEDIA |Ocorre quando o agendador de SQLOS alterna para o modo preventivo para fechar a mídia de backup.| 
|PREEMPTIVE_CLOSEBACKUPTAPE |Ocorre quando o agendador de SQLOS alterna para o modo preemptivo para fechar um dispositivo de backup em fita.| 
|PREEMPTIVE_CLOSEBACKUPVDIDEVICE |Ocorre quando o agendador de SQLOS alterna para o modo preemptivo para fechar um dispositivo de backup virtual.| 
|PREEMPTIVE_CLUSAPI_CLUSTERRESOURCECONTROL |Ocorre quando o agendador de Sistema operacional (SQLOS) alterna para o modo preemptivo para executar operações de cluster de failover do Windows.| 
|PREEMPTIVE_COM_COCREATEINSTANCE |Ocorre quando o agendador de SQLOS alterna para o modo preemptivo para criar um objeto COM.| 
|PREEMPTIVE_COM_COGETCLASSOBJECT |Somente para uso interno.| 
|PREEMPTIVE_COM_CREATEACCESSOR |Somente para uso interno.| 
|PREEMPTIVE_COM_DELETEROWS |Somente para uso interno.| 
|PREEMPTIVE_COM_GETCOMMANDTEXT |Somente para uso interno.| 
|PREEMPTIVE_COM_GETDATA |Somente para uso interno.| 
|PREEMPTIVE_COM_GETNEXTROWS |Somente para uso interno.| 
|PREEMPTIVE_COM_GETRESULT |Somente para uso interno.| 
|PREEMPTIVE_COM_GETROWSBYBOOKMARK |Somente para uso interno.| 
|PREEMPTIVE_COM_LBFLUSH |Somente para uso interno.| 
|PREEMPTIVE_COM_LBLOCKREGION |Somente para uso interno.| 
|PREEMPTIVE_COM_LBREADAT |Somente para uso interno.| 
|PREEMPTIVE_COM_LBSETSIZE |Somente para uso interno.| 
|PREEMPTIVE_COM_LBSTAT |Somente para uso interno.| 
|PREEMPTIVE_COM_LBUNLOCKREGION |Somente para uso interno.| 
|PREEMPTIVE_COM_LBWRITEAT |Somente para uso interno.| 
|PREEMPTIVE_COM_QUERYINTERFACE |Somente para uso interno.| 
|PREEMPTIVE_COM_RELEASE |Somente para uso interno.| 
|PREEMPTIVE_COM_RELEASEACCESSOR |Somente para uso interno.| 
|PREEMPTIVE_COM_RELEASEROWS |Somente para uso interno.| 
|PREEMPTIVE_COM_RELEASESESSION |Somente para uso interno.| 
|PREEMPTIVE_COM_RESTARTPOSITION |Somente para uso interno.| 
|PREEMPTIVE_COM_SEQSTRMREAD |Somente para uso interno.| 
|PREEMPTIVE_COM_SEQSTRMREADANDWRITE |Somente para uso interno.| 
|PREEMPTIVE_COM_SETDATAFAILURE |Somente para uso interno.| 
|PREEMPTIVE_COM_SETPARAMETERINFO |Somente para uso interno.| 
|PREEMPTIVE_COM_SETPARAMETERPROPERTIES |Somente para uso interno.| 
|PREEMPTIVE_COM_STRMLOCKREGION |Somente para uso interno.| 
|PREEMPTIVE_COM_STRMSEEKANDREAD |Somente para uso interno.| 
|PREEMPTIVE_COM_STRMSEEKANDWRITE |Somente para uso interno.| 
|PREEMPTIVE_COM_STRMSETSIZE |Somente para uso interno.| 
|PREEMPTIVE_COM_STRMSTAT |Somente para uso interno.| 
|PREEMPTIVE_COM_STRMUNLOCKREGION |Somente para uso interno.| 
|PREEMPTIVE_CONSOLEWRITE |Somente para uso interno.| 
|PREEMPTIVE_CREATEPARAM |Somente para uso interno.| 
|PREEMPTIVE_DEBUG |Somente para uso interno.| 
|PREEMPTIVE_DFSADDLINK |Somente para uso interno.| 
|PREEMPTIVE_DFSLINKEXISTCHECK |Somente para uso interno.| 
|PREEMPTIVE_DFSLINKHEALTHCHECK |Somente para uso interno.| 
|PREEMPTIVE_DFSREMOVELINK |Somente para uso interno.| 
|PREEMPTIVE_DFSREMOVEROOT |Somente para uso interno.| 
|PREEMPTIVE_DFSROOTFOLDERCHECK |Somente para uso interno.| 
|PREEMPTIVE_DFSROOTINIT |Somente para uso interno.| 
|PREEMPTIVE_DFSROOTSHARECHECK |Somente para uso interno.| 
|PREEMPTIVE_DTC_ABORT |Somente para uso interno.| 
|PREEMPTIVE_DTC_ABORTREQUESTDONE |Somente para uso interno.| 
|PREEMPTIVE_DTC_BEGINTRANSACTION |Somente para uso interno.| 
|PREEMPTIVE_DTC_COMMITREQUESTDONE |Somente para uso interno.| 
|PREEMPTIVE_DTC_ENLIST |Somente para uso interno.| 
|PREEMPTIVE_DTC_PREPAREREQUESTDONE |Somente para uso interno.| 
|PREEMPTIVE_FILESIZEGET |Somente para uso interno.| 
|PREEMPTIVE_FSAOLEDB_ABORTTRANSACTION |Somente para uso interno.| 
|PREEMPTIVE_FSAOLEDB_COMMITTRANSACTION |Somente para uso interno.| 
|PREEMPTIVE_FSAOLEDB_STARTTRANSACTION |Somente para uso interno.| 
|PREEMPTIVE_FSRECOVER_UNCONDITIONALUNDO |Somente para uso interno.| 
|PREEMPTIVE_GETRMINFO |Somente para uso interno.| 
|PREEMPTIVE_HADR_LEASE_MECHANISM |Always On agendamento do Gerenciador de concessão de grupos de disponibilidade para diagnósticos de Suporte da Microsoft. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PREEMPTIVE_HTTP_EVENT_WAIT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|PREEMPTIVE_HTTP_REQUEST |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|PREEMPTIVE_LOCKMONITOR |Somente para uso interno.| 
|PREEMPTIVE_MSS_RELEASE |Somente para uso interno.| 
|PREEMPTIVE_ODBCOPS |Somente para uso interno.| 
|PREEMPTIVE_OLE_UNINIT |Somente para uso interno.| 
|PREEMPTIVE_OLEDB_ABORTORCOMMITTRAN |Somente para uso interno.| 
|PREEMPTIVE_OLEDB_ABORTTRAN |Somente para uso interno.| 
|PREEMPTIVE_OLEDB_GETDATASOURCE |Somente para uso interno.| 
|PREEMPTIVE_OLEDB_GETLITERALINFO |Somente para uso interno.| 
|PREEMPTIVE_OLEDB_GETPROPERTIES |Somente para uso interno.| 
|PREEMPTIVE_OLEDB_GETPROPERTYINFO |Somente para uso interno.| 
|PREEMPTIVE_OLEDB_GETSCHEMALOCK |Somente para uso interno.| 
|PREEMPTIVE_OLEDB_JOINTRANSACTION |Somente para uso interno.| 
|PREEMPTIVE_OLEDB_RELEASE |Somente para uso interno.| 
|PREEMPTIVE_OLEDB_SETPROPERTIES |Somente para uso interno.| 
|PREEMPTIVE_OLEDBOPS |Somente para uso interno.| 
|PREEMPTIVE_OS_ACCEPTSECURITYCONTEXT |Somente para uso interno.| 
|PREEMPTIVE_OS_ACQUIRECREDENTIALSHANDLE |Somente para uso interno.| 
|PREEMPTIVE_OS_AUTHENTICATIONOPS |Somente para uso interno.| 
|PREEMPTIVE_OS_AUTHORIZATIONOPS |Somente para uso interno.| 
|PREEMPTIVE_OS_AUTHZGETINFORMATIONFROMCONTEXT |Somente para uso interno.| 
|PREEMPTIVE_OS_AUTHZINITIALIZECONTEXTFROMSID |Somente para uso interno.| 
|PREEMPTIVE_OS_AUTHZINITIALIZERESOURCEMANAGER |Somente para uso interno.| 
|PREEMPTIVE_OS_BACKUPREAD |Somente para uso interno.| 
|PREEMPTIVE_OS_CLOSEHANDLE |Somente para uso interno.| 
|PREEMPTIVE_OS_CLUSTEROPS |Somente para uso interno.| 
|PREEMPTIVE_OS_COMOPS |Somente para uso interno.| 
|PREEMPTIVE_OS_COMPLETEAUTHTOKEN |Somente para uso interno.| 
|PREEMPTIVE_OS_COPYFILE |Somente para uso interno.| 
|PREEMPTIVE_OS_CREATEDIRECTORY |Somente para uso interno.| 
|PREEMPTIVE_OS_CREATEFILE |Somente para uso interno.| 
|PREEMPTIVE_OS_CRYPTACQUIRECONTEXT |Somente para uso interno.| 
|PREEMPTIVE_OS_CRYPTIMPORTKEY |Somente para uso interno.| 
|PREEMPTIVE_OS_CRYPTOPS |Somente para uso interno.| 
|PREEMPTIVE_OS_DECRYPTMESSAGE |Somente para uso interno.| 
|PREEMPTIVE_OS_DELETEFILE |Somente para uso interno.| 
|PREEMPTIVE_OS_DELETESECURITYCONTEXT |Somente para uso interno.| 
|PREEMPTIVE_OS_DEVICEIOCONTROL |Somente para uso interno.| 
|PREEMPTIVE_OS_DEVICEOPS |Somente para uso interno.| 
|PREEMPTIVE_OS_DIRSVC_NETWORKOPS |Somente para uso interno.| 
|PREEMPTIVE_OS_DISCONNECTNAMEDPIPE |Somente para uso interno.| 
|PREEMPTIVE_OS_DOMAINSERVICESOPS |Somente para uso interno.| 
|PREEMPTIVE_OS_DSGETDCNAME |Somente para uso interno.| 
|PREEMPTIVE_OS_DTCOPS |Somente para uso interno.| 
|PREEMPTIVE_OS_ENCRYPTMESSAGE |Somente para uso interno.| 
|PREEMPTIVE_OS_FILEOPS |Somente para uso interno.| 
|PREEMPTIVE_OS_FINDFILE |Somente para uso interno.| 
|PREEMPTIVE_OS_FLUSHFILEBUFFERS |Somente para uso interno.| 
|PREEMPTIVE_OS_FORMATMESSAGE |Somente para uso interno.| 
|PREEMPTIVE_OS_FREECREDENTIALSHANDLE |Somente para uso interno.| 
|PREEMPTIVE_OS_FREELIBRARY |Somente para uso interno.| 
|PREEMPTIVE_OS_GENERICOPS |Somente para uso interno.| 
|PREEMPTIVE_OS_GETADDRINFO |Somente para uso interno.| 
|PREEMPTIVE_OS_GETCOMPRESSEDFILESIZE |Somente para uso interno.| 
|PREEMPTIVE_OS_GETDISKFREESPACE |Somente para uso interno.| 
|PREEMPTIVE_OS_GETFILEATTRIBUTES |Somente para uso interno.| 
|PREEMPTIVE_OS_GETFILESIZE |Somente para uso interno.| 
|PREEMPTIVE_OS_GETFINALFILEPATHBYHANDLE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|PREEMPTIVE_OS_GETLONGPATHNAME |Somente para uso interno.| 
|PREEMPTIVE_OS_GETPROCADDRESS |Somente para uso interno.| 
|PREEMPTIVE_OS_GETVOLUMENAMEFORVOLUMEMOUNTPOINT |Somente para uso interno.| 
|PREEMPTIVE_OS_GETVOLUMEPATHNAME |Somente para uso interno.| 
|PREEMPTIVE_OS_INITIALIZESECURITYCONTEXT |Somente para uso interno.| 
|PREEMPTIVE_OS_LIBRARYOPS |Somente para uso interno.| 
|PREEMPTIVE_OS_LOADLIBRARY |Somente para uso interno.| 
|PREEMPTIVE_OS_LOGONUSER |Somente para uso interno.| 
|PREEMPTIVE_OS_LOOKUPACCOUNTSID |Somente para uso interno.| 
|PREEMPTIVE_OS_MESSAGEQUEUEOPS |Somente para uso interno.| 
|PREEMPTIVE_OS_MOVEFILE |Somente para uso interno.| 
|PREEMPTIVE_OS_NETGROUPGETUSERS |Somente para uso interno.| 
|PREEMPTIVE_OS_NETLOCALGROUPGETMEMBERS |Somente para uso interno.| 
|PREEMPTIVE_OS_NETUSERGETGROUPS |Somente para uso interno.| 
|PREEMPTIVE_OS_NETUSERGETLOCALGROUPS |Somente para uso interno.| 
|PREEMPTIVE_OS_NETUSERMODALSGET |Somente para uso interno.| 
|PREEMPTIVE_OS_NETVALIDATEPASSWORDPOLICY |Somente para uso interno.| 
|PREEMPTIVE_OS_NETVALIDATEPASSWORDPOLICYFREE |Somente para uso interno.| 
|PREEMPTIVE_OS_OPENDIRECTORY |Somente para uso interno.| 
|PREEMPTIVE_OS_PDH_WMI_INIT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PREEMPTIVE_OS_PIPEOPS |Somente para uso interno.| 
|PREEMPTIVE_OS_PROCESSOPS |Somente para uso interno.| 
|PREEMPTIVE_OS_QUERYCONTEXTATTRIBUTES |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PREEMPTIVE_OS_QUERYREGISTRY |Somente para uso interno.| 
|PREEMPTIVE_OS_QUERYSECURITYCONTEXTTOKEN |Somente para uso interno.| 
|PREEMPTIVE_OS_REMOVEDIRECTORY |Somente para uso interno.| 
|PREEMPTIVE_OS_REPORTEVENT |Somente para uso interno.| 
|PREEMPTIVE_OS_REVERTTOSELF |Somente para uso interno.| 
|PREEMPTIVE_OS_RSFXDEVICEOPS |Somente para uso interno.| 
|PREEMPTIVE_OS_SECURITYOPS |Somente para uso interno.| 
|PREEMPTIVE_OS_SERVICEOPS |Somente para uso interno.| 
|PREEMPTIVE_OS_SETENDOFFILE |Somente para uso interno.| 
|PREEMPTIVE_OS_SETFILEPOINTER |Somente para uso interno.| 
|PREEMPTIVE_OS_SETFILEVALIDDATA |Somente para uso interno.| 
|PREEMPTIVE_OS_SETNAMEDSECURITYINFO |Somente para uso interno.| 
|PREEMPTIVE_OS_SQLCLROPS |Somente para uso interno.| 
|PREEMPTIVE_OS_SQMLAUNCH |Somente para uso interno. <br /> **Aplica-se a**: do [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] ao [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]. |  
|PREEMPTIVE_OS_VERIFYSIGNATURE |Somente para uso interno.| 
|PREEMPTIVE_OS_VERIFYTRUST |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|PREEMPTIVE_OS_VSSOPS |Somente para uso interno.| 
|PREEMPTIVE_OS_WAITFORSINGLEOBJECT |Somente para uso interno.| 
|PREEMPTIVE_OS_WINSOCKOPS |Somente para uso interno.| 
|PREEMPTIVE_OS_WRITEFILE |Somente para uso interno.| 
|PREEMPTIVE_OS_WRITEFILEGATHER |Somente para uso interno.| 
|PREEMPTIVE_OS_WSASETLASTERROR |Somente para uso interno.| 
|PREEMPTIVE_REENLIST |Somente para uso interno.| 
|PREEMPTIVE_RESIZELOG |Somente para uso interno.| 
|PREEMPTIVE_ROLLFORWARDREDO |Somente para uso interno.| 
|PREEMPTIVE_ROLLFORWARDUNDO |Somente para uso interno.| 
|PREEMPTIVE_SB_STOPENDPOINT |Somente para uso interno.| 
|PREEMPTIVE_SERVER_STARTUP |Somente para uso interno.| 
|PREEMPTIVE_SETRMINFO |Somente para uso interno.| 
|PREEMPTIVE_SHAREDMEM_GETDATA |Somente para uso interno.| 
|PREEMPTIVE_SNIOPEN |Somente para uso interno.| 
|PREEMPTIVE_SOSHOST |Somente para uso interno.| 
|PREEMPTIVE_SOSTESTING |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|PREEMPTIVE_SP_SERVER_DIAGNOSTICS |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PREEMPTIVE_STARTRM |Somente para uso interno.| 
|PREEMPTIVE_STREAMFCB_CHECKPOINT |Somente para uso interno.| 
|PREEMPTIVE_STREAMFCB_RECOVER |Somente para uso interno.| 
|PREEMPTIVE_STRESSDRIVER |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|PREEMPTIVE_TESTING |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|PREEMPTIVE_TRANSIMPORT |Somente para uso interno.| 
|PREEMPTIVE_UNMARSHALPROPAGATIONTOKEN |Somente para uso interno.| 
|PREEMPTIVE_VSS_CREATESNAPSHOT |Somente para uso interno.| 
|PREEMPTIVE_VSS_CREATEVOLUMESNAPSHOT |Somente para uso interno.| 
|PREEMPTIVE_XE_CALLBACKEXECUTE |Somente para uso interno.| 
|PREEMPTIVE_XE_CX_FILE_OPEN |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|PREEMPTIVE_XE_CX_HTTP_CALL |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|PREEMPTIVE_XE_DISPATCHER |Somente para uso interno.| 
|PREEMPTIVE_XE_ENGINEINIT |Somente para uso interno.| 
|PREEMPTIVE_XE_GETTARGETSTATE |Somente para uso interno.| 
|PREEMPTIVE_XE_SESSIONCOMMIT |Somente para uso interno.| 
|PREEMPTIVE_XE_TARGETFINALIZE |Somente para uso interno.| 
|PREEMPTIVE_XE_TARGETINIT |Somente para uso interno.| 
|PREEMPTIVE_XE_TIMERRUN |Somente para uso interno.| 
|PREEMPTIVE_XETESTING |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|PRINT_ROLLBACK_PROGRESS |Usado para aguardar enquanto os processos do usuário são finalizados em um banco de dados que passou por transição usando a cláusula de término ALTER DATABASE. Para obter mais informações, veja ALTER DATABASE (Transact-SQL).| 
|PRU_ROLLBACK_DEFERRED |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PWAIT_ALL_COMPONENTS_INITIALIZED |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PWAIT_COOP_SCAN |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PWAIT_DIRECTLOGCONSUMER_GETNEXT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|PWAIT_EVENT_SESSION_INIT_MUTEX |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PWAIT_FABRIC_REPLICA_CONTROLLER_DATA_LOSS |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|PWAIT_HADR_ACTION_COMPLETED |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PWAIT_HADR_CHANGE_NOTIFIER_TERMINATION_SYNC |Ocorre quando uma tarefa em segundo plano está aguardando o encerramento da tarefa em segundo plano que recebe (via sondagem) as notificações de clustering de failover do Windows Server. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PWAIT_HADR_CLUSTER_INTEGRATION |Uma operação de acréscimo, substituição e/ou remoção está aguardando para obter um bloqueio de gravação em uma Always On lista interna (como uma lista de redes, endereços de rede ou ouvintes de grupo de disponibilidade). Somente uso interno, <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PWAIT_HADR_FAILOVER_COMPLETED |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PWAIT_HADR_JOIN |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|PWAIT_HADR_OFFLINE_COMPLETED |Uma operação Always On remover grupo de disponibilidade está aguardando o grupo de disponibilidade de destino ficar offline antes de destruir objetos de clustering de failover do Windows Server. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PWAIT_HADR_ONLINE_COMPLETED |Um Always On operação de criação ou de grupo de disponibilidade de failover está aguardando o grupo de disponibilidade de destino ficar online., <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PWAIT_HADR_POST_ONLINE_COMPLETED |Uma operação Always On remover grupo de disponibilidade está aguardando o encerramento de qualquer tarefa em segundo plano que foi agendada como parte de um comando anterior. Por exemplo, pode haver uma tarefa em segundo plano que está fazendo a transição de bancos de dados de disponibilidade para a função primária. A dll remover grupo de disponibilidade deve aguardar a finalização desta tarefa em segundo plano para evitar condições de corrida. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PWAIT_HADR_SERVER_READY_CONNECTIONS |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PWAIT_HADR_WORKITEM_COMPLETED |Espera interna por um thread que espera uma tarefa de trabalho assíncrona ser concluída. Essa é uma espera esperada e é para uso de CSS. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PWAIT_HADRSIM |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|PWAIT_LOG_CONSOLIDATION_IO |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|PWAIT_LOG_CONSOLIDATION_POLL |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|PWAIT_MD_LOGIN_STATS |Ocorre durante a sincronização interna em metadados em estatísticas de logon. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PWAIT_MD_RELATION_CACHE |Ocorre durante a sincronização interna em metadados na tabela ou índice., <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PWAIT_MD_SERVER_CACHE |Ocorre durante a sincronização interna em metadados em servidores vinculados. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PWAIT_MD_UPGRADE_CONFIG |Ocorre durante a sincronização interna na atualização de configurações amplas do servidor. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PWAIT_PREEMPTIVE_APP_USAGE_TIMER |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|PWAIT_PREEMPTIVE_AUDIT_ACCESS_WINDOWSLOG |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PWAIT_QRY_BPMEMORY |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PWAIT_REPLICA_ONLINE_INIT_MUTEX |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PWAIT_RESOURCE_SEMAPHORE_FT_PARALLEL_QUERY_SYNC |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|PWAIT_SBS_FILE_OPERATION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|PWAIT_XTP_FSSTORAGE_MAINTENANCE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|PWAIT_XTP_HOST_STORAGE_WAIT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|QDS_ASYNC_CHECK_CONSISTENCY_TASK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|QDS_ASYNC_PERSIST_TASK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|QDS_ASYNC_PERSIST_TASK_START |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|QDS_ASYNC_QUEUE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|QDS_BCKG_TASK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|QDS_BLOOM_FILTER |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|QDS_CLEANUP_STALE_QUERIES_TASK_MAIN_LOOP_SLEEP |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|QDS_CTXS |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|QDS_DB_DISK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|QDS_DYN_VECTOR |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|QDS_EXCLUSIVE_ACCESS |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|QDS_HOST_INIT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|QDS_LOADDB |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|QDS_PERSIST_TASK_MAIN_LOOP_SLEEP |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|QDS_QDS_CAPTURE_INIT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|QDS_SHUTDOWN_QUEUE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|QDS_STMT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|QDS_STMT_DISK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|QDS_TASK_SHUTDOWN |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|QDS_TASK_START |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|QE_WARN_LIST_SYNC |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|QPJOB_KILL |Indica que uma atualização de estatística automática e assíncrona foi cancelada por uma chamada para KILL enquanto a atualização estava começando a ser executada. O thread de término está suspenso, esperando que ele inicie a escuta dos comandos KILL. Um valor bom é menos de um segundo.| 
|QPJOB_WAITFOR_ABORT |Indica que uma atualização assíncrona de estatísticas automática foi cancelada por uma chamada a KILL quando estava sendo executada. A atualização agora está concluída, mas está suspensa até que a coordenação de mensagens de thread de término seja concluída. Esse é um estado comum, mas raro, e deve ser bem curto. Um valor bom é menos de um segundo.| 
|QRY_MEM_GRANT_INFO_MUTEX |Ocorre quando o gerenciamento de memória de execução de consulta tenta controlar o acesso à lista de informações de concessão estáticas. Esse estado lista informações sobre as solicitações de memória em espera e concedidas atuais. É um estado de controle de acesso simples. Nunca deverá haver uma espera longa nesse estado. Se o mutex não for liberado, todas as novas consultas que usam memória deixarão de responder.| 
|QRY_PARALLEL_THREAD_MUTEX |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|QRY_PROFILE_LIST_MUTEX |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|QUERY_ERRHDL_SERVICE_DONE |Identificado apenas para fins informativos. Sem suporte. <br /> **Aplica-se a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] somente. |  
|QUERY_WAIT_ERRHDL_SERVICE |Identificado apenas para fins informativos.  Sem suporte. <br /> **Aplica-se a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] somente.  |  
|QUERY_EXECUTION_INDEX_SORT_EVENT_OPEN |Ocorre em determinados casos quando a criação de índice offline é executada em paralelo, e os diferentes threads de trabalho que estão classificando sincronizam o acesso aos arquivos de classificação.| 
|QUERY_NOTIFICATION_MGR_MUTEX |Ocorre durante a sincronização da fila de coleta de lixo do gerenciador de notificação de consulta.| 
|QUERY_NOTIFICATION_SUBSCRIPTION_MUTEX |Ocorre durante a sincronização de estado para transações em notificações de consulta.| 
|QUERY_NOTIFICATION_TABLE_MGR_MUTEX |Ocorre durante sincronização interna no gerenciador de notificação de consulta.| 
|QUERY_NOTIFICATION_UNITTEST_MUTEX |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|QUERY_OPTIMIZER_PRINT_MUTEX |Ocorre durante sincronização de produção de saída de diagnóstico do otimizador de consulta. Esse tipo de espera só ocorrerá se as configurações de diagnóstico tiverem sido habilitadas na direção do suporte a produtos da Microsoft.| 
|QUERY_TASK_ENQUEUE_MUTEX |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|QUERY_TRACEOUT |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|RBIO_WAIT_VLF |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|RBIO_RG_STORAGE |Ocorre quando um nó de computação de banco de dados de hiperescala está sendo limitado devido ao consumo de log atrasado no (s) servidor (es) de páginas. <br /> **Aplica-se a**: hiperescala do banco de dados SQL do Azure.|
|RBIO_RG_DESTAGE |Ocorre quando um nó de computação de banco de dados de hiperescala está sendo limitado devido ao consumo de log atrasado pelo armazenamento de log de longo prazo. <br /> **Aplica-se a**: hiperescala do banco de dados SQL do Azure.|
|RBIO_RG_REPLICA |Ocorre quando um nó de computação de banco de dados de hiperescala está sendo limitado devido ao consumo de log atrasado pelos nós de réplica secundária legíveis. <br /> **Aplica-se a**: hiperescala do banco de dados SQL do Azure.|
|RBIO_RG_LOCALDESTAGE |Ocorre quando um nó de computação de banco de dados de hiperescala está sendo limitado devido ao consumo de log atrasado pelo serviço de log. <br /> **Aplica-se a**: hiperescala do banco de dados SQL do Azure.|
|RECOVER_CHANGEDB |Ocorre durante a sincronização do status do banco de dados em espera passiva.| 
|RECOVERY_MGR_LOCK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|REDO_THREAD_PENDING_WORK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|REDO_THREAD_SYNC |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|REMOTE_BLOCK_IO |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|REMOTE_DATA_ARCHIVE_MIGRATION_DMV |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|REMOTE_DATA_ARCHIVE_SCHEMA_DMV |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|REMOTE_DATA_ARCHIVE_SCHEMA_TASK_QUEUE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|REPL_CACHE_ACCESS |Ocorre durante a sincronização em um cache de artigo de replicação. Durante essas esperas, o leitor de log de replicação entra em pausa e as instruções DDL (linguagem de definição de dados) em uma tabela publicada, são bloqueadas.| 
|REPL_HISTORYCACHE_ACCESS |Somente para uso interno.| 
|REPL_SCHEMA_ACCESS |Ocorre durante sincronização das informações de versão do esquema de replicação. Esse estado ocorre quando as instruções DDL são executadas no objeto replicado e quando o leitor de log gera ou consome esquema com controle de versão com base em uma ocorrência DDL. A contenção poderá ser vista nesse tipo de espera se você tiver muitos bancos de dados publicados em um único Publicador com replicação transacional e os bancos de dados publicados estiverem muito ativos.| 
|REPL_TRANFSINFO_ACCESS |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|REPL_TRANHASHTABLE_ACCESS |Somente para uso interno.| 
|REPL_TRANTEXTINFO_ACCESS |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|REPLICA_WRITES |Ocorre enquanto uma tarefa espera a conclusão de gravações de página em instantâneos de banco de dados ou réplicas de DBCC.| 
|REQUEST_DISPENSER_PAUSE |Ocorre quando uma tarefa está esperando a conclusão de todas as E/Ss pendentes, de forma que a E/S para um arquivo possa ser congelada para backup de instantâneo.| 
|REQUEST_FOR_DEADLOCK_SEARCH |Ocorre enquanto o monitor de deadlock espera iniciar a próxima pesquisa de deadlock. Essa espera é prevista entre as detecções de deadlock e, o tempo total maior nesse recurso, não significa que existe um problema.| 
|RESERVED_MEMORY_ALLOCATION_EXT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|RESMGR_THROTTLED |Ocorre quando uma nova solicitação chega e é suprimida com base na configuração de GROUP_MAX_REQUESTS.| 
|RESOURCE_GOVERNOR_IDLE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|RESOURCE_QUEUE |Ocorre durante a sincronização de várias filas de recurso internos.| 
|RESOURCE_SEMAPHORE |Ocorre quando uma solicitação de memória de consulta não pode ser concedida imediatamente devido a outras consultas simultâneas. Esperas e tempos de espera longos podem indicar número excessivo de consultas simultâneas ou valores de solicitação de memória excessivos.| 
|RESOURCE_SEMAPHORE_MUTEX |Ocorre enquanto uma consulta aguarda a sua solicitação de uma reserva de thread ser atendida. Também ocorre durante a sincronização de solicitações de compilação de consulta e concessão de memória.| 
|RESOURCE_SEMAPHORE_QUERY_COMPILE |Ocorre quando o número de compilações de consulta simultâneas atinge um limite de estrangulamento. Esperas e tempos de espera longos podem indicar compilações excessivas, recompilações ou planos que não sejam para cache.| 
|RESOURCE_SEMAPHORE_SMALL_QUERY |Ocorre quando uma solicitação de memória por meio de uma pequena consulta não pode ser concedida imediatamente devido a outras consultas simultâneas. O tempo de espera não deve exceder mais do que alguns segundos porque o servidor transfere a solicitação ao pool de memória de consulta principal se ele falhar ao conceder a memória solicitada dentro de alguns segundos. Esperas longas podem indicar número excessivo de pequenas consultas simultâneas enquanto o pool de memória principal está sendo bloqueado por consultas em espera. <br /> **Aplica-se a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] somente. |  
|RESTORE_FILEHANDLECACHE_ENTRYLOCK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|RESTORE_FILEHANDLECACHE_LOCK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|RG_RECONFIG |Somente para uso interno.| 
|ROWGROUP_OP_STATS |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|ROWGROUP_VERSION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|RTDATA_LIST |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|SATELLITE_CARGO |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|SATELLITE_SERVICE_SETUP |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|SATELLITE_TASK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|SBS_DISPATCH |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|SBS_RECEIVE_TRANSPORT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|SBS_TRANSPORT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|SCAN_CHAR_HASH_ARRAY_INITIALIZATION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|SEC_DROP_TEMP_KEY |Ocorre depois de uma falha ao tentar descartar uma chave de segurança temporária antes de uma nova tentativa.| 
|SECURITY_CNG_PROVIDER_MUTEX |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|SECURITY_CRYPTO_CONTEXT_MUTEX |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|SECURITY_DBE_STATE_MUTEX |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|SECURITY_KEYRING_RWLOCK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|SECURITY_MUTEX |Ocorre quando há uma espera por mutexes que controlam o acesso à lista global de provedores criptográficos de EKM (Gerenciamento Extensível de Chaves) e à lista de escopo de sessões de EKM.| 
|SECURITY_RULETABLE_MUTEX |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|SEMPLAT_DSI_BUILD |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|SEQUENCE_GENERATION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|SEQUENTIAL_GUID |Ocorre enquanto um novo GUID sequencial está sendo obtido.| 
|SERVER_IDLE_CHECK |Ocorre durante a sincronização do status de ociosidade da instância de SQL Server quando um monitor de recursos está tentando declarar uma instância de SQL Server como ociosa ou tentando acordar.| 
|SERVER_RECONFIGURE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|SESSION_WAIT_STATS_CHILDREN |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|SHARED_DELTASTORE_CREATION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|SHUTDOWN |Ocorre enquanto uma instrução de desligamento aguarda o encerramento de conexões ativas.| 
|SLEEP_BPOOL_FLUSH |Ocorre quando um ponto de verificação está estrangulando a emissão de E/Ss novas para evitar o enchimento do subsistema de disco.| 
|SLEEP_BUFFERPOOL_HELPLW |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|SLEEP_DBSTARTUP |Ocorre durante a inicialização do banco de dados enquanto aguarda a recuperação de todos os bancos de dados.| 
|SLEEP_DCOMSTARTUP |Ocorre uma vez no máximo durante SQL Server inicialização da instância enquanto aguarda a conclusão da inicialização do DCOM.| 
|SLEEP_MASTERDBREADY |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|SLEEP_MASTERMDREADY |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|SLEEP_MASTERUPGRADED |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|SLEEP_MEMORYPOOL_ALLOCATEPAGES |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|SLEEP_MSDBSTARTUP |Ocorre quando o SQL Trace aguarda o banco de dados msdb concluir a inicialização.| 
|SLEEP_RETRY_VIRTUALALLOC |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|SLEEP_SYSTEMTASK |Ocorre durante o início de uma tarefa em segundo plano enquanto aguarda tempdb concluir a inicialização.| 
|SLEEP_TASK |Ocorre quando uma tarefa suspensa espera a ocorrência de um evento genérico.| 
|SLEEP_TEMPDBSTARTUP |Ocorre enquanto uma tarefa espera tempdb completar a inicialização.| 
|SLEEP_WORKSPACE_ALLOCATEPAGE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|SLO_UPDATE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|SMSYNC |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|SNI_CONN_DUP |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|SNI_CRITICAL_SECTION |Ocorre durante a sincronização interna dentro de SQL Server componentes de rede.| 
|SNI_HTTP_WAITFOR_0_DISCON |Ocorre durante SQL Server desligamento, enquanto aguarda a saída de conexões HTTP pendentes.| 
|SNI_LISTENER_ACCESS |Ocorre ao aguardar que os nós NUMA (acesso não uniforme à memória) atualizem a alteração do estado. O acesso à alteração de estado é serializado.| 
|SNI_TASK_COMPLETION |Ocorre quando há uma espera para que todas as tarefas sejam concluídas durante uma alteração de estado de nó NUMA.| 
|SNI_WRITE_ASYNC |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|SOAP_READ |Ocorre ao aguardar pela conclusão de uma leitura de rede HTTP.| 
|SOAP_WRITE |Ocorre enquanto aguarda a conclusão de uma gravação de rede HTTP.| 
|SOCKETDUPLICATEQUEUE_CLEANUP |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|SOS_CALLBACK_REMOVAL |Ocorre enquanto executa a sincronização em uma lista de retorno de chamada para remover um retorno de chamada. Não se espera que esse contador seja alterado depois que a inicialização do servidor é concluída.| 
|SOS_DISPATCHER_MUTEX |Ocorre durante a sincronização interna do pool de dispatchers. Isto inclui o período de ajuste do pool.| 
|SOS_LOCALALLOCATORLIST |Ocorre durante a sincronização interna no gerenciador de memória do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. <br /> **Aplica-se a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] somente. |  
|SOS_MEMORY_TOPLEVELBLOCKALLOCATOR |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|SOS_MEMORY_USAGE_ADJUSTMENT |Ocorre quando o uso de memória está sendo ajustado entre pools.| 
|SOS_OBJECT_STORE_DESTROY_MUTEX |Ocorre durante sincronização interna em pools de memória na destruição de objetos do pool.| 
|SOS_PHYS_PAGE_CACHE |Contabiliza o tempo que um thread aguarda para obter o mutex necessário antes de alocar páginas físicas ou antes de retornar essas páginas para o sistema operacional. As esperas nesse tipo só aparecerão se a instância do SQL Server usar memória AWE., <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|SOS_PROCESS_AFFINITY_MUTEX |Ocorre durante a sincronização de acesso para processar configurações de afinidade.| 
|SOS_RESERVEDMEMBLOCKLIST |Ocorre durante a sincronização interna no Gerenciador de memória SQL Server. <br /> **Aplica-se a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] somente. |  
|SOS_SCHEDULER_YIELD |Ocorre quando uma tarefa cede o agendador para a execução de outras tarefas. Durante essa espera, a tarefa espera que seu quantum seja renovado.| 
|SOS_SMALL_PAGE_ALLOC |Ocorre durante a alocação e a liberação de memória que é gerenciada por alguns objetos de memória.| 
|SOS_STACKSTORE_INIT_MUTEX |Ocorre durante a sincronização da inicialização do repositório interno.| 
|SOS_SYNC_TASK_ENQUEUE_EVENT |Ocorre quando uma tarefa é iniciada em uma maneira síncrona. A maioria das tarefas na SQL Server são iniciadas de maneira assíncrona, na qual o controle retorna ao início imediatamente depois que a solicitação de tarefa é colocada na fila de trabalho.| 
|SOS_VIRTUALMEMORY_LOW |Ocorre quando uma alocação de memória espera um gerenciador de recursos liberar memória virtual.| 
|SOSHOST_EVENT |Ocorre quando um componente hospedado, como CLR, aguarda um SQL Server objeto de sincronização de evento.| 
|SOSHOST_INTERNAL |Ocorre durante a sincronização de retornos de chamada de gerenciador de memória usada por componentes hospedados, como CLR.| 
|SOSHOST_MUTEX |Ocorre quando um componente hospedado, como CLR, aguarda um objeto de sincronização de SQL Server mutex.| 
|SOSHOST_RWLOCK |Ocorre quando um componente hospedado, como CLR, aguarda um objeto de sincronização SQL Server Reader-Writer.| 
|SOSHOST_SEMAPHORE |Ocorre quando um componente hospedado, como CLR, aguarda um objeto de sincronização de semáforo SQL Server.| 
|SOSHOST_SLEEP |Ocorre quando uma tarefa hospedada entra em suspensão enquanto espera a ocorrência de um evento genérico. As tarefas hospedadas são usadas por componentes hospedados, como CLR.| 
|SOSHOST_TRACELOCK |Ocorre durante a sincronização de acesso para rastreamento de fluxos.| 
|SOSHOST_WAITFORDONE |Ocorre quando um componente hospedado, como CLR, aguarda a conclusão de uma tarefa.| 
|SP_PREEMPTIVE_SERVER_DIAGNOSTICS_SLEEP |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|SP_SERVER_DIAGNOSTICS_BUFFER_ACCESS |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|SP_SERVER_DIAGNOSTICS_INIT_MUTEX |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|SP_SERVER_DIAGNOSTICS_SLEEP |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|SQLCLR_APPDOMAIN |Ocorre enquanto CLR espera que um domínio de aplicativo conclua a inicialização.| 
|SQLCLR_ASSEMBLY |Ocorre enquanto aguarda o acesso à lista de assemblies carregados em appdomain.| 
|SQLCLR_DEADLOCK_DETECTION |Ocorre enquanto CLR aguarda a conclusão da detecção de deadlock.| 
|SQLCLR_QUANTUM_PUNISHMENT |Ocorre quando uma tarefa CLR é estrangulada porque excedeu seu quantum de execução. Esse estrangulamento é feito para reduzir o efeito dessa tarefa com muitos recursos em outras tarefas.| 
|SQLSORT_NORMMUTEX |Ocorre durante sincronização interna na inicialização das estruturas de classificação internas.| 
|SQLSORT_SORTMUTEX |Ocorre durante sincronização interna na inicialização das estruturas de classificação internas.| 
|SQLTRACE_BUFFER_FLUSH |Ocorre quando uma tarefa espera que, uma tarefa em segundo plano, libere buffers de rastreamento para o disco a cada quatro segundos. <br /> **Aplica-se a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] somente. |  
|SQLTRACE_FILE_BUFFER |Ocorre durante a sincronização em buffers de rastreamento durante um rastreamento de arquivo. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|SQLTRACE_FILE_READ_IO_COMPLETION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|SQLTRACE_FILE_WRITE_IO_COMPLETION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|SQLTRACE_INCREMENTAL_FLUSH_SLEEP |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|SQLTRACE_LOCK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] somente. |  
|SQLTRACE_PENDING_BUFFER_WRITERS |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|SQLTRACE_SHUTDOWN |Ocorre enquanto o desligamento de rastreamento aguarda a conclusão dos eventos de rastreamento pendentes.| 
|SQLTRACE_WAIT_ENTRIES |Ocorre enquanto uma fila de eventos do Rastreamento do SQL aguarda a chegada de pacotes na fila.| 
|SRVPROC_SHUTDOWN |Ocorre enquanto o processo de desligamento aguarda a liberação dos recursos internos para desligamento completo.| 
|STARTUP_DEPENDENCY_MANAGER |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|TDS_BANDWIDTH_STATE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|TDS_INIT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|TDS_PROXY_CONTAINER |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|TEMPOBJ |Ocorre quando os descartes de objetos temporários são sincronizados. Essa espera é rara e só acontecerá se uma tarefa solicitar acesso exclusivo para descartes de tabelas temporárias.| 
|TEMPORAL_BACKGROUND_PROCEED_CLEANUP |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|TERMINATE_LISTENER |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|THREADPOOL |Ocorre quando uma tarefa estiver esperando que um trabalhador seja processado no sistema. Isso pode indicar que a configuração máxima do trabalhador está muito baixa ou que as execuções em lotes estão demorando normalmente mais tempo, reduzindo o número de trabalhadores disponíveis para atender outros lotes.| 
|TIMEPRIV_TIMEPERIOD |Ocorre durante a sincronização interna do timer de Eventos Estendidos.| 
|TRACE_EVTNOTIF |Somente para uso interno.| 
|TRACEWRITE |Ocorre quando o provedor de rastreamento do conjunto de linhas de Rastreamento do SQL aguarda que um buffer livre ou um buffer com eventos seja processado.| 
|TRAN_MARKLATCH_DT |Ocorre ao esperar uma trava de modo de destruição em uma destruição de marcação de transação. Essas travas são usadas para sincronização de confirmações com transações marcadas.| 
|TRAN_MARKLATCH_EX |Ocorre ao esperar uma trava de modo exclusiva em uma transação marcada. Essas travas são usadas para sincronização de confirmações com transações marcadas.| 
|TRAN_MARKLATCH_KP |Ocorre ao esperar uma trava de modo de manutenção em uma transação marcada. Essas travas são usadas para sincronização de confirmações com transações marcadas.| 
|TRAN_MARKLATCH_NL |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|TRAN_MARKLATCH_SH |Ocorre ao esperar uma trava de modo compartilhado em uma transação marcada. Essas travas são usadas para sincronização de confirmações com transações marcadas.| 
|TRAN_MARKLATCH_UP |Ocorre ao esperar uma trava de modo de atualização em uma transação marcada. Essas travas são usadas para sincronização de confirmações com transações marcadas.| 
|TRANSACTION_MUTEX |Ocorre durante a sincronização de acesso a uma transação por meio de vários lotes.| 
|UCS_ENDPOINT_CHANGE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|UCS_MANAGER |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|UCS_MEMORY_NOTIFICATION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|UCS_SESSION_REGISTRATION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|UCS_TRANSPORT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|UCS_TRANSPORT_STREAM_CHANGE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|UTIL_PAGE_ALLOC |Ocorre quando exames de log de transação aguardam que memória esteja disponível durante pressão da memória.| 
|VDI_CLIENT_COMPLETECOMMAND |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|VDI_CLIENT_GETCOMMAND |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|VDI_CLIENT_OPERATION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|VDI_CLIENT_OTHER |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|VERSIONING_COMMITTING |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|VIA_ACCEPT |Ocorre quando uma conexão do provedor Virtual Interface Adapter (VIA) é concluída durante a inicialização.| 
|VIEW_DEFINITION_MUTEX |Ocorre durante a sincronização no acesso às definições de exibição em cache.| 
|WAIT_FOR_RESULTS |Ocorre ao esperar a ativação de uma notificação de consulta.| 
|WAIT_ON_SYNC_STATISTICS_REFRESH |Ocorre ao aguardar a conclusão da atualização de estatísticas síncrona antes da compilação da consulta e a execução ser retomada.<br /> **Aplica-se ao**: A partir do [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]|
|WAIT_SCRIPTDEPLOYMENT_REQUEST |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|WAIT_SCRIPTDEPLOYMENT_WORKER |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|WAIT_XLOGREAD_SIGNAL |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|WAIT_XTP_ASYNC_TX_COMPLETION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|WAIT_XTP_CKPT_AGENT_WAKEUP |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|WAIT_XTP_CKPT_CLOSE |Ocorre ao aguardar a conclusão de um ponto de verificação. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|WAIT_XTP_CKPT_ENABLED |Ocorre quando o ponto de verificação está desabilitado e aguardando a habilitação do ponto de verificação., <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|WAIT_XTP_CKPT_STATE_LOCK |Ocorre ao sincronizar a verificação do estado do ponto de verificação. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|WAIT_XTP_COMPILE_WAIT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|WAIT_XTP_GUEST |Ocorre quando o alocador de memória do banco de dados precisa parar de receber notificações de baixa memória. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|WAIT_XTP_HOST_WAIT |Ocorre quando as esperas são disparadas pelo mecanismo de banco de dados e implementadas pelo host. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|WAIT_XTP_OFFLINE_CKPT_BEFORE_REDO |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|WAIT_XTP_OFFLINE_CKPT_LOG_IO |Ocorre quando o ponto de verificação offline está aguardando a conclusão de uma e/s de leitura de log. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|WAIT_XTP_OFFLINE_CKPT_NEW_LOG |Ocorre quando o ponto de verificação offline está aguardando a verificação de novos registros de log. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|WAIT_XTP_PROCEDURE_ENTRY |Ocorre quando um procedimento de soltar está aguardando a conclusão de todas as execuções atuais do procedimento. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|WAIT_XTP_RECOVERY |Ocorre quando a recuperação de banco de dados está aguardando a conclusão da recuperação de objetos com otimização de memória. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|WAIT_XTP_SERIAL_RECOVERY |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|WAIT_XTP_SWITCH_TO_INACTIVE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|WAIT_XTP_TASK_SHUTDOWN |Ocorre ao aguardar a conclusão de um thread OLTP na memória. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|WAIT_XTP_TRAN_DEPENDENCY |Ocorre ao aguardar dependências de transação., <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|WAITFOR |Ocorre como resultado de uma instrução WAITFOR Transact-SQL. A duração da espera é determinada pelos parâmetros da instrução. Essa é uma espera iniciada pelo usuário.| 
|WAITFOR_PER_QUEUE |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|WAITFOR_TASKSHUTDOWN |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|WAITSTAT_MUTEX |Ocorre durante a sincronização de acesso à coleção de estatísticas usadas para popular sys.dm_os_wait_stats.| 
|WCC |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|WINDOW_AGGREGATES_MULTIPASS |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|WINFAB_API_CALL |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|WINFAB_REPLICA_BUILD_OPERATION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|WINFAB_REPORT_FAULT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|WORKTBL_DROP |Ocorre ao pausar antes de tentar novamente, após uma falha no descarte de uma tabela de trabalho.| 
|WRITE_COMPLETION |Ocorre quando uma operação de gravação está em andamento.| 
|WRITELOG |Ocorre ao aguardar que uma liberação de log seja concluída. As operações comuns que causam liberações de log são pontos de verificação e confirmações de transação.| 
|XACT_OWN_TRANSACTION |Ocorre enquanto se espera a aquisição da propriedade de uma transação.| 
|XACT_RECLAIM_SESSION |Ocorre enquanto se espera que o proprietário atual de uma sessão libere a propriedade da sessão.| 
|XACTLOCKINFO |Ocorre durante a sincronização de acesso à lista de bloqueios para uma transação. Além da própria transação, a lista de bloqueios é acessada por operações como detecção de deadlock e migração de bloqueio durante divisões de páginas.| 
|XACTWORKSPACE_MUTEX |Ocorre durante a sincronização de remoções de uma transação, bem como do número de bloqueios de banco de dados entre os membros registrados de uma transação.| 
|XDB_CONN_DUP_HASH |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|XDES_HISTORY |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|XDES_OUT_OF_ORDER_LIST |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|XDES_SNAPSHOT |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|XDESTSVERMGR |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|XE_BUFFERMGR_ALLPROCESSED_EVENT |Ocorre quando buffers de sessão de Eventos Estendidos são liberados para destinos. Essa espera ocorre em um thread em segundo plano.| 
|XE_BUFFERMGR_FREEBUF_EVENT |Ocorre quando uma destas condições é verdadeira:| 
|XE_CALLBACK_LIST |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|XE_CX_FILE_READ |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|XE_DISPATCHER_CONFIG_SESSION_LIST |Ocorre quando uma sessão de Eventos Estendidos que está usando destinos assíncronos é iniciada ou interrompida. Essa espera indica qualquer um dos seguintes:| 
|XE_DISPATCHER_JOIN |Ocorre quando um thread em segundo plano que é usado para sessões de Eventos Estendidos está sendo encerrado.| 
|XE_DISPATCHER_WAIT |Ocorre quando um thread em segundo plano que é usado para sessões de Eventos Estendidos está esperando o processamento de buffers de evento.| 
|XE_FILE_TARGET_TVF |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|XE_LIVE_TARGET_TVF |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.| 
|XE_MODULEMGR_SYNC |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|XE_OLS_LOCK |Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.| 
|XE_PACKAGE_LOCK_BACKOFF |Identificado apenas para fins informativos. Sem suporte. <br /> **Aplica-se a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] somente. |  
|XE_SERVICES_EVENTMANUAL |Somente para uso interno.| 
|XE_SERVICES_MUTEX |Somente para uso interno.| 
|XE_SERVICES_RWLOCK |Somente para uso interno.| 
|XE_SESSION_CREATE_SYNC |Somente para uso interno.| 
|XE_SESSION_FLUSH |Somente para uso interno.| 
|XE_SESSION_SYNC |Somente para uso interno.| 
|XE_STM_CREATE |Somente para uso interno.| 
|XE_TIMER_EVENT |Somente para uso interno.| 
|XE_TIMER_MUTEX |Somente para uso interno.| 
|XE_TIMER_TASK_DONE |Somente para uso interno.| 
|XIO_CREDENTIAL_MGR_RWLOCK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|XIO_CREDENTIAL_RWLOCK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|XIO_EDS_MGR_RWLOCK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|XIO_EDS_RWLOCK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|XIO_IOSTATS_BLOBLIST_RWLOCK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|XIO_IOSTATS_FCBLIST_RWLOCK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e posterior.| 
|XIO_LEASE_RENEW_MGR_RWLOCK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|XTP_HOST_DB_COLLECTION |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|XTP_HOST_LOG_ACTIVITY |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|XTP_HOST_PARALLEL_RECOVERY |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|XTP_PREEMPTIVE_TASK |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|XTP_TRUNCATION_LSN |Somente para uso interno. <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior.| 
|XTPPROC_CACHE_ACCESS |Ocorre quando para acessar todos os objetos de cache de procedimento armazenado compilados nativamente. <br /> **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.| 
|XTPPROC_PARTITIONED_STACK_CREATE |Ocorre ao alocar estruturas de cache de procedimento armazenado compiladas nativamente por nó NUMA (deve ser feito com um único thread) para um determinado procedimento. <br /> **Aplica-se a**: [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] e posterior.|

  
 Os XEvents a seguir estão relacionados à **opção** de partição e à recompilação de índice online. Para obter informações sobre a sintaxe, consulte [ALTER TABLE &#40;Transact-sql&#41;](../../t-sql/statements/alter-table-transact-sql.md) e [ALTER INDEX &#40;&#41;do Transact-SQL ](../../t-sql/statements/alter-index-transact-sql.md).  
  
-   lock_request_priority_state  
  
-   process_killed_by_abort_blockers  
  
-   ddl_with_wait_at_low_priority  
  
 Para uma matriz de compatibilidade de bloqueio, consulte [Sys. dm_tran_locks &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).  
  
## <a name="see-also"></a>Consulte também  
    
 [SQL Server exibições de gerenciamento dinâmico relacionadas ao sistema operacional &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys. dm_exec_session_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md)   
 [sys. dm_db_wait_stats &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-wait-stats-azure-sql-database.md)  
  
  


