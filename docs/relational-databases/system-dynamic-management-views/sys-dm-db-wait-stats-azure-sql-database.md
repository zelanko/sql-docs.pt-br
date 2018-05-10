---
title: sys.DM db_wait_stats (banco de dados do SQL Azure) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_wait_stats_TSQL
- dm_db_wait_stats
- sys.dm_db_wait_stats
- sys.dm_db_wait_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_wait_stats dynamic management view
- dm_db_wait_stats
ms.assetid: 00abd0a5-bae0-4d71-b173-f7a14cddf795
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: b40388c60180630b1b6e64a3dc73b47a343f4264
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmdbwaitstats-azure-sql-database"></a>sys.DM db_wait_stats (banco de dados do SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre todas as esperas encontradas por threads executados durante a operação. É possível usar essa exibição agregada para diagnosticar problemas de desempenho com o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e também com consultas e lotes específicos.  
  
 Tipos específicos de horas de espera durante execução de consulta podem indicar gargalos ou pontos de pausa dentro da consulta. Da mesma forma, os tempos de espera altos ou as contagens de espera em todo o servidor podem indicar gargalos nas interações de consulta de interação na instância do servidor. Por exemplo, as esperas de bloqueio indicam a contenção de dados por consultas; as esperas de trava de ES de página indicam tempos de resposta de ES lentos; as esperas de atualização de trava de página indicam layout de arquivo incorreto.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|wait_type|**nvarchar(60)**|Nome do tipo de espera. Para obter mais informações, consulte [tipos de espera](#WaitTypes), mais adiante neste tópico.|  
|waiting_tasks_count|**bigint**|Número de esperas nesse tipo de espera. O contador é incrementado no início de cada espera.|  
|wait_time_ms|**bigint**|Tempo de espera total para esse tipo de espera em milissegundos. Essa hora é inclusiva de signal_wait_time_ms.|  
|max_wait_time_ms|**bigint**|Tempo de espera máximo neste tipo de espera.|  
|signal_wait_time_ms|**bigint**|Diferença entre a hora em que o thread de espera foi sinalizado e quando ele começou a ser executado.|  
  
## <a name="remarks"></a>Remarks  
  
-   Essa exibição de gerenciamento dinâmico exibe dados apenas para o banco de dados atual.  
  
-   Essa exibição de gerenciamento dinâmico mostra a hora para as esperas concluídas. Ela não mostra as esperas atuais.  
  
-   Os contadores são redefinidos como zero sempre que o banco de dados é movido ou fica offline.  
  
-   Não será considerado que um thread de trabalho do SQL Server esteja sendo esperado se qualquer um dos seguintes for verdadeiro:  
  
    -   Um recurso fica disponível.  
  
    -   Uma fila não está vazia.  
  
    -   Um processo externo termina.  
  
-   Essas estatísticas não são persistidas em eventos de failover do banco de dados SQL e todos os dados são cumulativos desde a última vez em que as estatísticas foram redefinidas.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE no servidor.  
  
##  <a name="WaitTypes"></a> Tipos de esperas  
 Esperas de recurso  
 As esperas de recurso ocorrem quando um trabalhador solicita acesso a um recurso que não está disponível porque esse recurso está sendo usado por outro trabalhador ou ainda não foi disponibilizado. Exemplos de esperas de recurso são bloqueios, travas, rede e esperas de E/S de disco. Bloqueio e trava são esperas em objetos de sincronização.  
  
 Esperas de fila  
 As esperas de fila acontecem quando um trabalhador está inativo, aguardando atribuição de trabalho. As esperas de fila são geralmente vistas com tarefas em segundo plano de sistema, como monitor de deadlocks e tarefas de limpeza de registro excluídas. Essas tarefas aguardarão as solicitações de trabalho serem colocadas em uma fila de trabalho. Esperas de fila também poderão ficar periodicamente ativas mesmo se nenhum pacote novo tiver sido colocado na fila.  
  
 Esperas externas  
 As esperas externas ocorrem quando um trabalhador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está aguardando um evento externo, como uma chamada de procedimento armazenado estendido ou consulta de servidor vinculada, terminar Quando você diagnostica os problemas de bloqueio, lembre-se de que as esperas externas nem sempre indicam que o trabalhador está ocioso, porque ele pode estar ativamente executando algum código externo.  
  
 Embora o thread já não esteja mais aguardando, ele não precisa iniciar a execução imediatamente. Isso ocorre porque esse thread é colocado primeiro na fila de trabalhadores executáveis e deve aguardar a execução de um quantum no agendador.  
  
 Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os contadores de tempo de espera são **bigint** valores e, portanto, não são tão suscetíveis à substituição de contador quanto os contadores equivalentes em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A tabela a seguir lista os tipos de espera encontrados por tarefas.  
  
|Tipo de espera|Description|  
|---------------|-----------------|  
|ABR|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|ASSEMBLY_LOAD|Ocorre durante o acesso exclusivo ao carregamento do assembly.|  
|ASYNC_DISKPOOL_LOCK|Ocorre quando há uma tentativa de sincronizar threads paralelos que estão executando tarefas, como criação ou inicialização de um arquivo.|  
|ASYNC_IO_COMPLETION|Ocorre quando uma tarefa estiver esperando a conclusão de E/Ss.|  
|ASYNC_NETWORK_IO|Ocorre em gravações de rede quando a tarefa é bloqueada por trás da rede. Verifique se o cliente está processando dados do servidor.|  
|AUDIT_GROUPCACHE_LOCK|Ocorre quando há uma espera em um bloqueio que controla o acesso a um cache especial. O cache contém informações sobre as auditorias que estão sendo usadas para auditar cada grupo de ações de auditoria.|  
|AUDIT_LOGINCACHE_LOCK|Ocorre quando há uma espera em um bloqueio que controla o acesso a um cache especial. O cache contém informações sobre as auditorias que estão sendo usadas para auditar grupos de ações de auditoria de logon.|  
|AUDIT_ON_DEMAND_TARGET_LOCK|Ocorre quando há uma espera em um bloqueio que é usado para garantir a inicialização única dos destinos do Evento Estendido relacionados à auditoria.|  
|AUDIT_XE_SESSION_MGR|Ocorre quando há uma espera em um bloqueio que é usado para sincronizar o início e a interrupção de sessões de Eventos Estendidos relacionadas à auditoria.|  
|BACKUP|Ocorre quando uma tarefa é bloqueada como parte do processamento do backup.|  
|BACKUP_OPERATOR|Ocorre quando uma tarefa está aguardando uma montagem de fita. Para exibir o status da fita, consulte [sys.DM io_backup_tapes](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md). Se uma operação de montagem não estiver pendente, esse tipo de espera poderá indicar um problema de hardware na unidade de fita.|  
|BACKUPBUFFER|Ocorre quando uma tarefa de backup estiver aguardando dados ou um buffer para armazenar dados nele. Esse tipo não é comum, exceto quando uma tarefa estiver aguardando uma montagem de fita.|  
|BACKUPIO|Ocorre quando uma tarefa de backup estiver aguardando dados ou um buffer para armazenar dados nele. Esse tipo não é comum, exceto quando uma tarefa estiver aguardando uma montagem de fita.|  
|BACKUPTHREAD|Ocorre quando uma tarefa estiver esperando a conclusão da tarefa de backup. Os tempos de espera podem ser longos, de alguns minutos até várias horas. Se a tarefa sendo aguardada estiver em um processo de E/S, esse tipo não indicará um problema.|  
|BAD_PAGE_PROCESS|Ocorre quando o registrador de página suspeita em segundo plano estiver tentando evitar a execução mais que cada cinco segundos. Páginas suspeitas em excesso causam a execução frequente do registrador.|  
|BROKER_CONNECTION_RECEIVE_TASK|Ocorre ao aguardar o acesso para receber uma mensagem em um ponto de extremidade de conexão. O acesso de recepção para o ponto de extremidade é serializado.|  
|BROKER_ENDPOINT_STATE_MUTEX|Ocorre quando houver contenção para acessar o estado de um ponto de extremidade de conexão [!INCLUDE[ssSB](../../includes/sssb-md.md)]. O acesso ao estado das alterações é serializado.|  
|BROKER_EVENTHANDLER|Ocorre quando uma tarefa estiver aguardando o manipulador de eventos principal do [!INCLUDE[ssSB](../../includes/sssb-md.md)]. Isso deve ocorrer muito brevemente.|  
|BROKER_INIT|Ocorre ao inicializar [!INCLUDE[ssSB](../../includes/sssb-md.md)] em cada banco de dados ativo. Isso deve ocorrer raramente.|  
|BROKER_MASTERSTART|Ocorre quando uma tarefa estiver aguardando o manipulador de eventos principal do [!INCLUDE[ssSB](../../includes/sssb-md.md)] para iniciar. Isso deve ocorrer muito brevemente.|  
|BROKER_RECEIVE_WAITFOR|Ocorre quando RECEIVE WAITFOR estiver aguardando. Isso será comum se nenhuma mensagem estiver pronta para ser recebida.|  
|BROKER_REGISTERALLENDPOINTS|Ocorre durante a inicialização de um ponto de extremidade de conexão do [!INCLUDE[ssSB](../../includes/sssb-md.md)]. Isso deve ocorrer muito brevemente.|  
|BROKER_SERVICE|Ocorre quando a lista de destino do [!INCLUDE[ssSB](../../includes/sssb-md.md)] que está associada a um serviço de destino é atualizada ou priorizada novamente.|  
|BROKER_SHUTDOWN|Ocorre quando há um desligamento planejado do [!INCLUDE[ssSB](../../includes/sssb-md.md)]. Isso deve ocorrer muito brevemente, se ocorrer.|  
|BROKER_TASK_STOP|Ocorre quando o manipulador de tarefa da fila do [!INCLUDE[ssSB](../../includes/sssb-md.md)] tenta desligar a tarefa. A verificação do estado é serializada e deve estar em um estado de execução antecipadamente.|  
|BROKER_TO_FLUSH|Ocorre quando o liberador lento do [!INCLUDE[ssSB](../../includes/sssb-md.md)] libera os objetos de transmissão na memória para uma tabela de trabalho.|  
|BROKER_TRANSMITTER|Ocorre quando o transmissor [!INCLUDE[ssSB](../../includes/sssb-md.md)] está aguardando o trabalho.|  
|BUILTIN_HASHKEY_MUTEX|Pode ocorrer depois de inicialização de instância, enquanto as estruturas de dados internos estiverem sendo inicializadas. Não ocorrerá antes que as estruturas de dados tiverem inicializado.|  
|CHECK_PRINT_RECORD|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|CHECKPOINT_QUEUE|Ocorre enquanto a tarefa de ponto de verificação aguarda a próxima solicitação de ponto de verificação.|  
|CHKPT|Ocorre na inicialização de servidor para informar ao thread de ponto de verificação que ele pode iniciar.|  
|CLEAR_DB|Ocorre durante operações que alteram o estado de um banco de dados, como abrir ou fechar um banco de dados.|  
|CLR_AUTO_EVENT|Ocorre quando uma tarefa executa o CLR (Common Language Runtime) e aguarda o início de um determinado evento automático. Esperas longas são comuns e não indicam um problema.|  
|CLR_CRST|Ocorre quando uma tarefa está executando o CLR e aguarda a apresentação de uma seção crítica da tarefa que está, atualmente, sendo usada por outra tarefa.|  
|CLR_JOIN|Ocorre quando uma tarefa executa o CLR e aguarda o término de outra tarefa. Esse estado de espera quando há uma junção entre tarefas.|  
|CLR_MANUAL_EVENT|Ocorre quando uma tarefa está executando o CLR atualmente e está aguardando um evento manual específico a ser iniciado.|  
|CLR_MEMORY_SPY|Ocorre durante uma espera na aquisição de bloqueio para uma estrutura de dados que é usada para registrar todas as alocações de memória virtual provenientes do CLR. A estrutura de dados será bloqueada para manter sua integridade se houver acesso paralelo.|  
|CLR_MONITOR|Ocorre quando uma tarefa está executando o CLR atualmente e aguardando para obter um bloqueio no monitor.|  
|CLR_RWLOCK_READER|Ocorre quando uma tarefa executa o CLR e aguarda um bloqueio de leitor.|  
|CLR_RWLOCK_WRITER|Ocorre quando uma tarefa executa o CLR e aguarda um bloqueio de gravador.|  
|CLR_SEMAPHORE|Ocorre quando uma tarefa executa o CLR e aguarda um semáforo.|  
|CLR_TASK_START|Ocorre enquanto aguarda a inicialização de uma tarefa de CLR ser concluída.|  
|CLRHOST_STATE_ACCESS|Ocorre quando há uma espera para adquirir acesso exclusivo às estruturas de dados de hospedagem de CLR. Esse tipo de espera ocorre ao configurar ou subdividir o tempo de execução do CLR.|  
|CMEMTHREAD|Ocorre quando uma tarefa está aguardando um objeto de memória protegido por thread. O tempo de espera pode aumentar quando há contenção provocada por várias tarefas tentando alocar memória do mesmo objeto de memória.|  
|CXPACKET|Ocorre ao tentar sincronizar o iterador de troca do processador de consulta. A redução do grau de paralelismo poderá ser considerada se a contenção nesse tipo de espera se tornar um problema.|  
|CXROWSET_SYNC|Ocorre durante um exame de intervalo paralelo.|  
|DAC_INIT|Ocorre enquanto a conexão de administrador dedicada estiver inicializando.|  
|DBMIRROR_DBM_EVENT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|DBMIRROR_DBM_MUTEX|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|DBMIRROR_EVENTS_QUEUE|Ocorre quando o espelhamento de banco de dados aguarda o processamento de eventos.|  
|DBMIRROR_SEND|Ocorre quando uma tarefa aguarda que os registros acumulados de comunicações na camada de rede a serem apagados possam enviar mensagens. Indica que a camada de comunicações está começando a ser sobrecarregada e a afetar a taxa de transferência de dados de espelhamento de banco de dados.|  
|DBMIRROR_WORKER_QUEUE|Indica que a tarefa de trabalhador de espelhamento de banco de dados está aguardando mais trabalho.|  
|DBMIRRORING_CMD|Ocorre quando uma tarefa aguarda a liberação dos registros para o disco. Estima-se que esse estado de espera seja mantido por longos períodos de tempo.|  
|DEADLOCK_ENUM_MUTEX|Ocorre quando o monitor de deadlock e sys.dm_os_waiting_tasks tentam verificar se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não está executando várias pesquisas de deadlock ao mesmo tempo.|  
|DEADLOCK_TASK_SEARCH|Um grande tempo de espera nesse recurso indica que o servidor está realizando consultas na parte superior de sys.dm_os_waiting_tasks e que essas consultas estão impedindo o monitor de deadlock de pesquisar deadlocks. Esse tipo de espera só é usado através de monitor de deadlock. Consultas na parte superior de sys.dm_os_waiting_tasks usam DEADLOCK_ENUM_MUTEX.|  
|DEBUG|Ocorre durante depuração de [!INCLUDE[tsql](../../includes/tsql-md.md)] e CLR para sincronização interna.|  
|DISABLE_VERSIONING|Ocorre quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pesquisa a versão do gerenciador de transações para verificar se o carimbo de data e hora da versão ativa mais recente é posterior ao carimbo de data/hora quando o estado começou a mudar. Se esse for o caso, todas as transações de instantâneo iniciadas antes de a instrução ALTER DATABASE ter sido executada serão finalizadas. Esse estado de espera é usado quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desabilita o controle de versão usando a instrução ALTER DATABASE.|  
|DISKIO_SUSPEND|Ocorre quando uma tarefa estiver esperando para acessar um arquivo quando um backup externo está ativo. Isso é informado a cada processo de usuário de espera. Uma contagem maior que cinco por processo de usuário pode indicar que o backup externo está levando muito tempo para ser concluído.|  
|DISPATCHER_QUEUE_SEMAPHORE|Ocorre quando um thread do pool de dispatcher está aguardando mais trabalho para processamento. Estima-se que o tempo para esse tipo de espera aumente quando o dispatcher estiver ocioso.|  
|DLL_LOADING_MUTEX|Ocorre uma vez ao aguardar a DLL do analisador XML ser carregada.|  
|DROPTEMP|Ocorre entre tentativas para descartar um objeto temporário caso a tentativa anterior tenha falhado. A duração da espera cresce bastante em cada tentativa de descarte com falha.|  
|DTC|Ocorre quando uma tarefa estiver esperando um evento usado para gerenciar a transição de estado. Esse estado controla quando a recuperação das transações de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC) ocorre após [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] receber a notificação de que o serviço MS DTC se tornou indisponível.<br /><br /> Esse estado também descreve uma tarefa em espera quando uma confirmação de uma transação de MS DTC é iniciada por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aguarda a conclusão de uma confirmação de MS DTC.|  
|DTC_ABORT_REQUEST|Ocorre em uma sessão de trabalhador de MS DTC quando a sessão estiver aguardando para obter a propriedade de uma transação de MS DTC. Depois que o MS DTC for proprietário da transação, a sessão poderá reverter a transação. Geralmente, a sessão esperará por outra sessão que está usando a transação.|  
|DTC_RESOLVE|Ocorre quando uma tarefa de recuperação está aguardando o banco de dados mestre em uma transação de banco de dados cruzado de forma que a tarefa possa consultar o resultado da transação.|  
|DTC_STATE|Ocorre quando uma tarefa está esperando um evento que protege as alterações no objeto de estado global de MS DTC. Esse estado deve ser mantido para intervalos de tempo muito curtos.|  
|DTC_TMDOWN_REQUEST|Ocorre em uma sessão de trabalhador de MS DTC quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recebe notificação que o serviço de MS DTC não está disponível. Primeiro, o trabalhador aguardará o processo de recuperação de MS DTC iniciar. Em seguida, o trabalhador espera para obter o resultado da transação distribuída em que o trabalhador está trabalhando. Isso pode continuar até a conexão com o serviço de MS DTC ser restabelecida.|  
|DTC_WAITFOR_OUTCOME|Ocorre quando as tarefas de recuperação aguardam o MS DTC ficar ativo para ativar a resolução de transações preparadas.|  
|DUMP_LOG_COORDINATOR|Ocorre quando uma tarefa principal está esperando uma subtarefa gerar dados. Em geral, esse estado não ocorre. Uma espera longa indica um bloqueio inesperado. A subtarefa deve ser investigada.|  
|DUMPTRIGGER|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|EC|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|EE_PMOLOCK|Ocorre durante a sincronização de certos tipos de alocações de memória durante execução de instrução.|  
|EE_SPECPROC_MAP_INIT|Ocorre durante sincronização da criação de tabela de hash de procedimento interno. Essa espera só pode acontecer durante o acesso inicial da tabela de hash depois que a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciada.|  
|ENABLE_VERSIONING|Ocorre quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aguarda a finalização de todas as transações de atualização neste banco de dados, antes de declarar o banco de dados pronto para o estado permitido de isolamento de instantâneo. Esse estado é usado quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ativa o isolamento de instantâneo usando a instrução ALTER DATABASE.|  
|ERROR_REPORTING_MANAGER|Ocorre durante a sincronização de várias inicializações de log de erros simultâneas.|  
|EXCHANGE|Ocorre durante a sincronização no iterador de troca de processador de consulta durante consultas paralelas.|  
|EXECSYNC|Ocorre durante consultas paralelas durante a sincronização em processador de consulta em áreas não relacionadas ao iterador de troca. Exemplos dessas áreas são bitmaps, LOBs (objetos binários grandes) e o iterador de spool. Os LOBs podem usar esse estado de espera frequentemente.|  
|EXECUTION_PIPE_EVENT_INTERNAL|Ocorre durante a sincronização entre o produtor e partes do consumidor de execução em lotes que são enviados por meio do contexto da conexão.|  
|FAILPOINT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|FCB_REPLICA_READ|Ocorre quando as leituras de um arquivo esparso de instantâneo (ou um instantâneo temporário criado por DBCC) são sincronizadas.|  
|FCB_REPLICA_WRITE|Ocorre quando o envio ou a remoção de uma página de um arquivo esparso de instantâneo (ou de um instantâneo temporário criado por DBCC) é sincronizado.|  
|FS_FC_RWLOCK|Ocorre quando há uma espera pelo coletor de lixo do FILESTREAM para proceder de uma das seguintes maneiras:<br /><br /> Desabilitar a coleta de lixo (usada por backup e restauração).<br /><br /> Executar um ciclo do coletor de lixo do FILESTREAM.|  
|FS_GARBAGE_COLLECTOR_SHUTDOWN|Ocorre quando o coletor de lixo do FILESTREAM está aguardando que tarefas de limpeza sejam concluídas.|  
|FS_HEADER_RWLOCK|Ocorre quando há uma espera para adquirir acesso ao cabeçalho do FILESTREAM de um contêiner de dados do FILESTREAM para ler ou atualizar o conteúdo no arquivo de cabeçalho do FILESTREAM (Filestream.hdr).|  
|FS_LOGTRUNC_RWLOCK|Ocorre quando há uma espera para adquirir acesso ao truncamento de log do FILESTREAM para proceder de uma das seguintes maneiras:<br /><br /> Desabilitar temporariamente o truncamento de log do FILESTREAM (FSLOG) (usado pelo backup e pela restauração).<br /><br /> Executar um ciclo de truncamento de FSLOG.|  
|FSA_FORCE_OWN_XACT|Ocorre quando uma operação de E/S de arquivo do FILESTREAM precisa associar-se à transação associada, mas a transação pertence a outra sessão no momento.|  
|FSAGENT|Ocorre quando uma operação de E/S de arquivo FILESTREAM está aguardando um recurso do agente do FILESTREAM que está sendo usado por outra operação de E/S de arquivo.|  
|FSTR_CONFIG_MUTEX|Ocorre quando há uma espera para que outra reconfiguração de recurso do FILESTREAM seja concluída.|  
|FSTR_CONFIG_RWLOCK|Ocorre quando há uma espera para serializar o acesso aos parâmetros de configuração do FILESTREAM.|  
|FT_METADATA_MUTEX|Documentado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.|  
|FT_RESTART_CRAWL|Ocorre quando um rastreamento de texto completo precisa ser reiniciado a partir do último ponto conhecido bom para recuperação de uma falha momentânea. A espera deixa as tarefas do trabalhador em execução na população para concluir a etapa atual ou sair dela.|  
|FULLTEXT GATHERER|Ocorre durante a sincronização de operações de texto completo.|  
|GUARDIAN|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|HTTP_ENUMERATION|Ocorre na inicialização para enumerar os pontos de extremidade de HTTP para iniciar o HTTP.|  
|HTTP_START|Ocorre quando uma conexão está esperando que o HTTP conclua a inicialização.|  
|IMPPROV_IOWAIT|Ocorre quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aguarda que uma E/S de carregamento em massa seja concluída.|  
|INTERNAL_TESTING|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|IO_AUDIT_MUTEX|Ocorre durante a sincronização de buffers de evento de rastreamento.|  
|IO_COMPLETION|Ocorre enquanto se espera as operações de E/S serem concluídas. Esse tipo de espera geralmente representa E/Ss de página sem-dados. As esperas de conclusão de E/S da página de dados são exibidas como esperas PAGEIOLATCH_*.|  
|IO_QUEUE_LIMIT|Ocorre quando a fila E/S assíncrona para o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] tem muitas pendências de E/S. Tarefas tentando emitir outra E/S são bloqueadas neste tipo de espera até que o número de E/S pendentes caia abaixo do limite. O limite é proporcional às DTUs atribuídas ao banco de dados.|  
|IO_RETRY|Ocorre quando uma operação de E/S, como uma leitura ou uma gravação no disco, falha devido a recursos insuficientes, e é tentada novamente.|  
|IOAFF_RANGE_QUEUE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|KSOURCE_WAKEUP|Usado pela tarefa de controle de serviço ao aguardar solicitações do Gerenciador de Controle de Serviços. Esperas longas estão previstas e não indicam um problema.|  
|KTM_ENLISTMENT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|KTM_RECOVERY_MANAGER|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|KTM_RECOVERY_RESOLUTION|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|LATCH_DT|Ocorre ao esperar uma trava de DT (destruir). Isso não inclui travas de buffer ou de marcação de transação. Uma listagem de esperas de LATCH_* está disponível em sys.dm_os_latch_stats. Observe que sys.dm_os_latch_stats agrupa LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX e LATCH_DT.|  
|LATCH_EX|Ocorre ao esperar uma trava de EX (exclusivo). Isso não inclui travas de buffer ou de marcação de transação. Uma listagem de esperas de LATCH_* está disponível em sys.dm_os_latch_stats. Observe que sys.dm_os_latch_stats agrupa LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX e LATCH_DT.|  
|LATCH_KP|Ocorre ao esperar uma trava de KP (manutenção). Isso não inclui travas de buffer ou de marcação de transação. Uma listagem de esperas de LATCH_* está disponível em sys.dm_os_latch_stats. Observe que sys.dm_os_latch_stats agrupa LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX e LATCH_DT.|  
|LATCH_NL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|LATCH_SH|Ocorre ao esperar uma trava de SH (compartilhamento). Isso não inclui travas de buffer ou de marcação de transação. Uma listagem de esperas de LATCH_* está disponível em sys.dm_os_latch_stats. Observe que sys.dm_os_latch_stats agrupa LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX e LATCH_DT.|  
|LATCH_UP|Ocorre ao esperar uma trava de UP (atualização). Isso não inclui travas de buffer ou de marcação de transação. Uma listagem de esperas de LATCH_* está disponível em sys.dm_os_latch_stats. Observe que sys.dm_os_latch_stats agrupa LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX e LATCH_DT.|  
|LAZYWRITER_SLEEP|Ocorre quando as tarefas lazywriter são suspensas. É uma medição do tempo gasto por tarefas em segundo plano em espera. Não considere esse estado quando você estiver procurando pausas de usuário.|  
|LCK_M_BU|Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização em Massa (BU). Para uma matriz de compatibilidade de bloqueio, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_IS|Ocorre quando uma tarefa está esperando para adquirir um bloqueio Tentativa Compartilhada (IS). Para uma matriz de compatibilidade de bloqueio, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_IU|Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização da Tentativa (IU). Para uma matriz de compatibilidade de bloqueio, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_IX|Ocorre quando uma tarefa está esperando para adquirir um bloqueio Exclusivo da Tentativa (IX). Para uma matriz de compatibilidade de bloqueio, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_RIn_NL|Ocorre quando uma tarefa está esperando adquirir um bloqueio NULL no valor de chave atual e um bloqueio Inserção de Intervalo entre a chave atual e a anterior. Um bloqueio NULL na chave é um bloqueio de liberação instantâneo. Para uma matriz de compatibilidade de bloqueio, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_RIn_S|Ocorre quando uma tarefa está esperando adquirir um bloqueio compartilhado no valor de chave atual e um bloqueio Inserção de Intervalo entre a chave atual e a anterior. Para uma matriz de compatibilidade de bloqueio, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_RIn_U|Uma tarefa que está esperando para adquirir um bloqueio Atualização no valor de chave atual e um bloqueio Inserção de Intervalo entre a chave atual e a anterior. Para uma matriz de compatibilidade de bloqueio, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_RIn_X|Ocorre quando uma tarefa está esperando adquirir um bloqueio Exclusivo no valor de chave atual e um bloqueio Inserção de Intervalo entre a chave atual e a anterior. Para uma matriz de compatibilidade de bloqueio, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_RS_S|Ocorre quando uma tarefa está esperando adquirir um bloqueio Compartilhado no valor de chave atual e um bloqueio Intervalo Compartilhado entre a chave atual e a anterior. Para uma matriz de compatibilidade de bloqueio, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_RS_U|Ocorre quando uma tarefa está esperando adquirir um bloqueio Atualização no valor de chave atual e um bloqueio Atualização de Intervalo entre a chave atual e a anterior. Para uma matriz de compatibilidade de bloqueio, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_RX_S|Ocorre quando uma tarefa está esperando adquirir um bloqueio Compartilhado no valor de chave atual e um bloqueio Intervalo Exclusivo entre a chave atual e a anterior. Para uma matriz de compatibilidade de bloqueio, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_RX_U|Ocorre quando uma tarefa está esperando adquirir um bloqueio Atualização no valor de chave atual e um bloqueio Intervalo Exclusivo entre a chave atual e a anterior. Para uma matriz de compatibilidade de bloqueio, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_RX_X|Ocorre quando uma tarefa está esperando adquirir um bloqueio Exclusivo no valor de chave atual e um bloqueio Intervalo Exclusivo entre a chave atual e a anterior. Para uma matriz de compatibilidade de bloqueio, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_S|Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado. Para uma matriz de compatibilidade de bloqueio, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_SCH_M|Ocorre quando uma tarefa está esperando para adquirir um bloqueio Modificação de Esquema. Para uma matriz de compatibilidade de bloqueio, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_SCH_S|Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhamento de Esquema. Para uma matriz de compatibilidade de bloqueio, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_SIU|Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Atualização da Tentativa. Para uma matriz de compatibilidade de bloqueio, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_SIX|Ocorre quando uma tarefa está esperando para adquirir um bloqueio Compartilhado com Exclusivo da Tentativa. Para uma matriz de compatibilidade de bloqueio, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_U|Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização. Para uma matriz de compatibilidade de bloqueio, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_UIX|Ocorre quando uma tarefa está esperando para adquirir um bloqueio Atualização com Exclusivo da Tentativa. Para uma matriz de compatibilidade de bloqueio, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LCK_M_X|Ocorre quando uma tarefa está esperando para adquirir um bloqueio Exclusivo. Para uma matriz de compatibilidade de bloqueio, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).|  
|LOG_RATE_GOVERNOR|Ocorre quando o BD está esperando a cota para gravação no log.|  
|LOGBUFFER|Ocorre quando uma tarefa está esperando espaço no buffer de log para armazenar um registro de log. Consistentemente, valores altos podem indicar que os dispositivos de log não podem acompanhar a quantidade de log que está sendo gerada pelo servidor.|  
|LOGGENERATION|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|LOGMGR|Ocorre quando uma tarefa está aguardando que qualquer E/S de log pendente seja concluída antes de desativar o log durante o fechamento do banco de dados.|  
|LOGMGR_FLUSH|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|LOGMGR_QUEUE|Ocorre enquanto a tarefa de gravador de log aguarda solicitações de trabalho.|  
|LOGMGR_RESERVE_APPEND|Ocorre quando uma tarefa está esperando para verificar se o truncamento de log libera espaço para logs, para que a tarefa possa gravar um novo registro de log. Considere aumentar o tamanho do(s) arquivo(s) de log para o banco de dados afetado para reduzir essa espera.|  
|LOWFAIL_MEMMGR_QUEUE|Ocorre ao aguardar que a memória esteja disponível para uso.|  
|MSQL_DQ|Ocorre quando uma tarefa está aguardando que uma operação de consulta distribuída seja concluída. Isso é usado para detectar deadlocks de aplicativo MARS (Vários Conjuntos de Resultados Ativos) potenciais. A espera termina quando a chamada de consulta distribuída é concluída.|  
|MSQL_XACT_MGR_MUTEX|Ocorre quando uma tarefa está aguardando para obter a propriedade do gerenciador de transações de sessão para executar uma operação de transação em nível de sessão.|  
|MSQL_XACT_MUTEX|Ocorre durante sincronização de uso de transação. Uma solicitação deve adquirir o mutex antes de usar a transação.|  
|MSQL_XP|Ocorre quando uma tarefa está esperando a finalização de um procedimento armazenado estendido. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa este estado de espera para detectar deadlocks de aplicativo MARS potenciais. A espera para quando a chamada do procedimento armazenado estendido termina.|  
|MSSEARCH|Ocorre durante chamadas de pesquisa de texto completo. Essa espera termina quando a operação de texto completo é concluída. Ela não indica contenção, mas a duração de operações de texto completo.|  
|NET_WAITFOR_PACKET|Ocorre quando uma conexão está esperando um pacote de rede durante uma leitura de rede.|  
|OLEDB|Ocorre quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chama o provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Cliente OLE DB. Esse tipo de espera não é usado para sincronização. Em vez disso, ele indica a duração de chamadas ao provedor OLE DB.|  
|ONDEMAND_TASK_QUEUE|Ocorre enquanto uma tarefa em segundo plano aguarda solicitações de tarefa de sistema de alta prioridade. Os tempos de espera longos indicam que não houve nenhuma solicitação de alta prioridade a ser processada e que isso não deve causar nenhuma preocupação.|  
|PAGEIOLATCH_DT|Ocorre quando uma tarefa está esperando em uma trava por um buffer que está em uma solicitação de E/S. A solicitação de trava está no modo Destruição. Esperas longas podem indicar problemas no subsistema de disco.|  
|PAGEIOLATCH_EX|Ocorre quando uma tarefa está esperando em uma trava por um buffer que está em uma solicitação de E/S. A solicitação de trava está em modo Exclusivo. Esperas longas podem indicar problemas no subsistema de disco.|  
|PAGEIOLATCH_KP|Ocorre quando uma tarefa está esperando em uma trava por um buffer que está em uma solicitação de E/S. A solicitação de trava está no modo Manutenção. Esperas longas podem indicar problemas no subsistema de disco.|  
|PAGEIOLATCH_NL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|PAGEIOLATCH_SH|Ocorre quando uma tarefa está esperando em uma trava por um buffer que está em uma solicitação de E/S. A solicitação de trava está no modo Compartilhado. Esperas longas podem indicar problemas no subsistema de disco.|  
|PAGEIOLATCH_UP|Ocorre quando uma tarefa está esperando em uma trava por um buffer que está em uma solicitação de E/S. A solicitação de trava está no modo Atualização. Esperas longas podem indicar problemas no subsistema de disco.|  
|PAGELATCH_DT|Ocorre quando uma tarefa está esperando em uma trava por um buffer que não está em uma solicitação de E/S. A solicitação de trava está no modo Destruição.|  
|PAGELATCH_EX|Ocorre quando uma tarefa está esperando em uma trava por um buffer que não está em uma solicitação de E/S. A solicitação de trava está em modo Exclusivo.|  
|PAGELATCH_KP|Ocorre quando uma tarefa está esperando em uma trava por um buffer que não está em uma solicitação de E/S. A solicitação de trava está no modo Manutenção.|  
|PAGELATCH_NL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|PAGELATCH_SH|Ocorre quando uma tarefa está esperando em uma trava por um buffer que não está em uma solicitação de E/S. A solicitação de trava está no modo Compartilhado.|  
|PAGELATCH_UP|Ocorre quando uma tarefa está esperando em uma trava por um buffer que não está em uma solicitação de E/S. A solicitação de trava está no modo Atualização.|  
|PARALLEL_BACKUP_QUEUE|Ocorre ao serializar a saída produzida por RESTORE HEADERONLY, RESTORE FILELISTONLY ou RESTORE LABELONLY.|  
|PREEMPTIVE_ABR|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|PREEMPTIVE_AUDIT_ACCESS_EVENTLOG|Ocorre quando o agendador de Sistema operacional (SQLOS) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alterna para o modo preemptivo para gravar um evento de auditoria para o log de eventos do Windows.|  
|PREEMPTIVE_AUDIT_ACCESS_SECLOG|Ocorre quando o agendador de Sistema operacional (SQLOS) alterna para o modo preemptivo para gravar um evento de auditoria para o log de segurança do Windows.|  
|PREEMPTIVE_CLOSEBACKUPMEDIA|Ocorre quando o agendador de SQLOS alterna para o modo preventivo para fechar a mídia de backup.|  
|PREEMPTIVE_CLOSEBACKUPTAPE|Ocorre quando o agendador de SQLOS alterna para o modo preemptivo para fechar um dispositivo de backup em fita.|  
|PREEMPTIVE_CLOSEBACKUPVDIDEVICE|Ocorre quando o agendador de SQLOS alterna para o modo preemptivo para fechar um dispositivo de backup virtual.|  
|PREEMPTIVE_CLUSAPI_CLUSTERRESOURCECONTROL|Ocorre quando o agendador de Sistema operacional (SQLOS) alterna para o modo preemptivo para executar operações de cluster de failover do Windows.|  
|PREEMPTIVE_COM_COCREATEINSTANCE|Ocorre quando o agendador de SQLOS alterna para o modo preemptivo para criar um objeto COM.|  
|PREEMPTIVE_HADR_LEASE_MECHANISM|Grupos de disponibilidade AlwaysOn para diagnóstico de CSS de agendamento do Gerenciador de concessão.|  
|PREEMPTIVE_SOSTESTING|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|PREEMPTIVE_STRESSDRIVER|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|PREEMPTIVE_TESTING|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|PREEMPTIVE_XETESTING|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|PRINT_ROLLBACK_PROGRESS|Usado para aguardar enquanto os processos do usuário são finalizados em um banco de dados que passou por transição usando a cláusula de término ALTER DATABASE. Para obter mais informações, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).|  
|PWAIT_HADR_CHANGE_NOTIFIER_TERMINATION_SYNC|Ocorre quando uma tarefa em segundo plano está aguardando a conclusão de uma tarefa em segundo plano que recebe (via sondagem) as notificações do Windows Server Failover Clustering.  Somente para uso interno.|  
|PWAIT_HADR_CLUSTER_INTEGRATION|Um acréscimo, substituir e/ou Remover operação está aguardando para obter um bloqueio de gravação em um AlwaysOn lista interna (como uma lista de redes, endereços de rede ou ouvintes de grupo de disponibilidade).  Somente para uso interno.|  
|PWAIT_HADR_OFFLINE_COMPLETED|Uma AlwaysOn drop operação grupo de disponibilidade está aguardando o grupo de disponibilidade de destino ficar offline antes de destruir os objetos de cluster de Failover do Windows Server.|  
|PWAIT_HADR_ONLINE_COMPLETED|Um sempre em criar ou operação de failover do grupo de disponibilidade está aguardando o grupo de disponibilidade de destino ficar online.|  
|PWAIT_HADR_POST_ONLINE_COMPLETED|Uma AlwaysOn drop operação grupo de disponibilidade está aguardando o término de uma tarefa em segundo plano que foi agendada como parte de um comando anterior. Por exemplo, pode haver uma tarefa em segundo plano que está fazendo a transição de bancos de dados de disponibilidade para a função primária. O DROP AVAILABILITY GROUP DDL deve aguardar esta tarefa em segundo plano ser finalizada para evitar situações de competição.|  
|PWAIT_HADR_WORKITEM_COMPLETED|Espera interna por um thread que espera uma tarefa de trabalho assíncrona ser concluída. Essa é uma espera prevista e deve ser usada pelo CSS.|  
|PWAIT_MD_LOGIN_STATS|Ocorre durante a sincronização interna nos metadados nas estatísticas de logon.|  
|PWAIT_MD_RELATION_CACHE|Ocorre durante a sincronização interna nos metadados na tabela ou no índice.|  
|PWAIT_MD_SERVER_CACHE|Ocorre durante a sincronização interna nos metadados em servidores vinculados.|  
|PWAIT_MD_UPGRADE_CONFIG|Ocorre durante a sincronização interna ao atualizar as configurações de servidor amplas.|  
|PWAIT_METADATA_LAZYCACHE_RWLOCk|Ocorre durante a sincronização interna no cache de metadados junto com o índice de iteração ou estatísticas em uma tabela.|  
|QPJOB_KILL|Indica que uma atualização de estatística automática e assíncrona foi cancelada por uma chamada para KILL enquanto a atualização estava começando a ser executada. O thread de término está suspenso, esperando que ele inicie a escuta dos comandos KILL. Um valor bom é menos de um segundo.|  
|QPJOB_WAITFOR_ABORT|Indica que uma atualização assíncrona de estatísticas automática foi cancelada por uma chamada a KILL quando estava sendo executada. A atualização agora está concluída, mas está suspensa até que a coordenação de mensagens de thread de término seja concluída. Esse é um estado comum, mas raro, e deve ser bem curto. Um valor bom é menos de um segundo.|  
|QRY_MEM_GRANT_INFO_MUTEX|Ocorre quando o gerenciamento de memória de execução de consulta tenta controlar o acesso à lista de informações de concessão estáticas. Esse estado lista informações sobre as solicitações de memória em espera e concedidas atuais. É um estado de controle de acesso simples. Nunca deverá haver uma espera longa nesse estado. Se o mutex não for liberado, todas as novas consultas que usam memória deixarão de responder.|  
|QUERY_ERRHDL_SERVICE_DONE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|QUERY_EXECUTION_INDEX_SORT_EVENT_OPEN|Ocorre em determinados casos quando a criação de índice offline é executada em paralelo, e os diferentes threads de trabalho que estão classificando sincronizam o acesso aos arquivos de classificação.|  
|QUERY_NOTIFICATION_MGR_MUTEX|Ocorre durante a sincronização da fila de coleta de lixo do gerenciador de notificação de consulta.|  
|QUERY_NOTIFICATION_SUBSCRIPTION_MUTEX|Ocorre durante a sincronização de estado para transações em notificações de consulta.|  
|QUERY_NOTIFICATION_TABLE_MGR_MUTEX|Ocorre durante sincronização interna no gerenciador de notificação de consulta.|  
|QUERY_NOTIFICATION_UNITTEST_MUTEX|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|QUERY_OPTIMIZER_PRINT_MUTEX|Ocorre durante sincronização de produção de saída de diagnóstico do otimizador de consulta. Esse tipo de espera só ocorrerá se as configurações de diagnóstico estiverem habilitadas sob a direção do Suporte ao Produto da [!INCLUDE[msCoName](../../includes/msconame-md.md)].|  
|QUERY_TRACEOUT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|QUERY_WAIT_ERRHDL_SERVICE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|RECOVER_CHANGEDB|Ocorre durante a sincronização do status do banco de dados em espera passiva.|  
|REPL_CACHE_ACCESS|Ocorre durante a sincronização em um cache de artigo de replicação. Durante essas esperas, o leitor de log de replicação entra em pausa e as instruções DDL (linguagem de definição de dados) em uma tabela publicada, são bloqueadas.|  
|REPL_SCHEMA_ACCESS|Ocorre durante sincronização das informações de versão do esquema de replicação. Esse estado ocorre quando as instruções DDL são executadas no objeto replicado e quando o leitor de log gera ou consome esquema com controle de versão com base em uma ocorrência DDL.|  
|REPLICA_WRITES|Ocorre enquanto uma tarefa espera a conclusão de gravações de página em instantâneos de banco de dados ou réplicas de DBCC.|  
|REQUEST_DISPENSER_PAUSE|Ocorre quando uma tarefa está esperando a conclusão de todas as E/Ss pendentes, de forma que a E/S para um arquivo possa ser congelada para backup de instantâneo.|  
|REQUEST_FOR_DEADLOCK_SEARCH|Ocorre enquanto o monitor de deadlock espera iniciar a próxima pesquisa de deadlock. Essa espera é prevista entre as detecções de deadlock e, o tempo total maior nesse recurso, não significa que existe um problema.|  
|RESMGR_THROTTLED|Ocorre quando uma nova solicitação chega e é suprimida com base na configuração de GROUP_MAX_REQUESTS.|  
|RESOURCE_QUEUE|Ocorre durante a sincronização de várias filas de recurso internos.|  
|RESOURCE_SEMAPHORE|Ocorre quando uma solicitação de memória de consulta não pode ser concedida imediatamente devido a outras consultas simultâneas. Esperas e tempos de espera longos podem indicar número excessivo de consultas simultâneas ou valores de solicitação de memória excessivos.|  
|RESOURCE_SEMAPHORE_MUTEX|Ocorre enquanto uma consulta aguarda a sua solicitação de uma reserva de thread ser atendida. Também ocorre durante a sincronização de solicitações de compilação de consulta e concessão de memória.|  
|RESOURCE_SEMAPHORE_QUERY_COMPILE|Ocorre quando o número de compilações de consulta simultâneas atinge um limite de estrangulamento. Esperas e tempos de espera longos podem indicar compilações excessivas, recompilações ou planos que não sejam para cache.|  
|RESOURCE_SEMAPHORE_SMALL_QUERY|Ocorre quando uma solicitação de memória por meio de uma pequena consulta não pode ser concedida imediatamente devido a outras consultas simultâneas. O tempo de espera não deve exceder mais do que alguns segundos porque o servidor transfere a solicitação ao pool de memória de consulta principal se ele falhar ao conceder a memória solicitada dentro de alguns segundos. Esperas longas podem indicar número excessivo de pequenas consultas simultâneas enquanto o pool de memória principal está sendo bloqueado por consultas em espera.|  
|SE_REPL_CATCHUP_THROTTLE|Ocorre quando a transação aguarda o andamento de um dos secundários de banco de dados.|  
|SE_REPL_COMMIT_ACK|Ocorre quando a transação aguarda o reconhecimento da confirmação de quorum das réplicas secundárias.|  
|SE_REPL_COMMIT_TURN|Ocorre quando a transação aguarda a confirmação após receber os reconhecimentos da confirmação de quorum.|  
|SE_REPL_ROLLBACK_ACK|Ocorre quando a transação aguarda o reconhecimento da reversão de quorum das réplicas secundárias.|  
|SE_REPL_SLOW_SECONDARY_THROTTLE|Ocorre quando o thread está aguardando uma das réplicas secundárias do banco de dados.|  
|SEC_DROP_TEMP_KEY|Ocorre depois de uma falha ao tentar descartar uma chave de segurança temporária antes de uma nova tentativa.|  
|SECURITY_MUTEX|Ocorre quando há uma espera por mutexes que controlam o acesso à lista global de provedores criptográficos de EKM (Gerenciamento Extensível de Chaves) e à lista de escopo de sessões de EKM.|  
|SEQUENTIAL_GUID|Ocorre enquanto um novo GUID sequencial está sendo obtido.|  
|SERVER_IDLE_CHECK|Ocorre durante a sincronização do status ocioso da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando um monitor de recursos está tentando declarar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como ociosa ou tentando ativá-la.|  
|SHUTDOWN|Ocorre enquanto uma instrução de desligamento aguarda o encerramento de conexões ativas.|  
|SLEEP_BPOOL_FLUSH|Ocorre quando um ponto de verificação está estrangulando a emissão de E/Ss novas para evitar o enchimento do subsistema de disco.|  
|SLEEP_DBSTARTUP|Ocorre durante a inicialização do banco de dados enquanto aguarda a recuperação de todos os bancos de dados.|  
|SLEEP_DCOMSTARTUP|Ocorre uma vez no máximo durante inicialização de instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enquanto aguarda a conclusão da inicialização de DCOM.|  
|SLEEP_MSDBSTARTUP|Ocorre quando o SQL Trace aguarda o banco de dados msdb concluir a inicialização.|  
|SLEEP_SYSTEMTASK|Ocorre durante o início de uma tarefa em segundo plano enquanto aguarda tempdb concluir a inicialização.|  
|SLEEP_TASK|Ocorre quando uma tarefa suspensa espera a ocorrência de um evento genérico.|  
|SLEEP_TEMPDBSTARTUP|Ocorre enquanto uma tarefa espera tempdb completar a inicialização.|  
|SNI_CRITICAL_SECTION|Ocorre durante a sincronização interna nos componentes de rede do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|SNI_HTTP_WAITFOR_0_DISCON|Ocorre durante o desligamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao aguardar o encerramento de conexões HTTP pendentes.|  
|SNI_LISTENER_ACCESS|Ocorre ao aguardar que os nós NUMA (acesso não uniforme à memória) atualizem a alteração do estado. O acesso à alteração de estado é serializado.|  
|SNI_TASK_COMPLETION|Ocorre quando há uma espera para que todas as tarefas sejam concluídas durante uma alteração de estado de nó NUMA.|  
|SOAP_READ|Ocorre ao aguardar pela conclusão de uma leitura de rede HTTP.|  
|SOAP_WRITE|Ocorre enquanto aguarda a conclusão de uma gravação de rede HTTP.|  
|SOS_CALLBACK_REMOVAL|Ocorre enquanto executa a sincronização em uma lista de retorno de chamada para remover um retorno de chamada. Não se espera que esse contador seja alterado depois que a inicialização do servidor é concluída.|  
|SOS_DISPATCHER_MUTEX|Ocorre durante a sincronização interna do pool de dispatchers. Isto inclui o período de ajuste do pool.|  
|SOS_LOCALALLOCATORLIST|Ocorre durante a sincronização interna no gerenciador de memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|SOS_MEMORY_USAGE_ADJUSTMENT|Ocorre quando o uso de memória está sendo ajustado entre pools.|  
|SOS_OBJECT_STORE_DESTROY_MUTEX|Ocorre durante sincronização interna em pools de memória na destruição de objetos do pool.|  
|SOS_PROCESS_AFFINITY_MUTEX|Ocorre durante a sincronização de acesso para processar configurações de afinidade.|  
|SOS_RESERVEDMEMBLOCKLIST|Ocorre durante a sincronização interna no gerenciador de memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|SOS_SCHEDULER_YIELD|Ocorre quando uma tarefa cede o agendador para a execução de outras tarefas. Durante essa espera, a tarefa espera que seu quantum seja renovado.|  
|SOS_SMALL_PAGE_ALLOC|Ocorre durante a alocação e a liberação de memória que é gerenciada por alguns objetos de memória.|  
|SOS_STACKSTORE_INIT_MUTEX|Ocorre durante a sincronização da inicialização do repositório interno.|  
|SOS_SYNC_TASK_ENQUEUE_EVENT|Ocorre quando uma tarefa é iniciada em uma maneira síncrona. A maioria das tarefas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são iniciadas de maneira assíncrona, em que o controle retorna ao iniciador logo após a solicitação de tarefa ter sido colocada na fila de trabalhos.|  
|SOS_VIRTUALMEMORY_LOW|Ocorre quando uma alocação de memória espera um gerenciador de recursos liberar memória virtual.|  
|SOSHOST_EVENT|Ocorre quando um componente hospedado, como CLR, espera um objeto de sincronização de evento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|SOSHOST_INTERNAL|Ocorre durante a sincronização de retornos de chamada de gerenciador de memória usada por componentes hospedados, como CLR.|  
|SOSHOST_MUTEX|Ocorre quando um componente hospedado, como CLR, espera um objeto de sincronização de mutex do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|SOSHOST_RWLOCK|Ocorre quando um componente hospedado, como CLR, espera um objeto de sincronização de leitor-gravador de evento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|SOSHOST_SEMAPHORE|Ocorre quando um componente hospedado, como CLR, espera um objeto de sincronização de semáforo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|SOSHOST_SLEEP|Ocorre quando uma tarefa hospedada entra em suspensão enquanto espera a ocorrência de um evento genérico. As tarefas hospedadas são usadas por componentes hospedados, como CLR.|  
|SOSHOST_TRACELOCK|Ocorre durante a sincronização de acesso para rastreamento de fluxos.|  
|SOSHOST_WAITFORDONE|Ocorre quando um componente hospedado, como CLR, aguarda a conclusão de uma tarefa.|  
|SQLCLR_APPDOMAIN|Ocorre enquanto CLR espera que um domínio de aplicativo conclua a inicialização.|  
|SQLCLR_ASSEMBLY|Ocorre enquanto aguarda o acesso à lista de assemblies carregados em appdomain.|  
|SQLCLR_DEADLOCK_DETECTION|Ocorre enquanto CLR aguarda a conclusão da detecção de deadlock.|  
|SQLCLR_QUANTUM_PUNISHMENT|Ocorre quando uma tarefa CLR é estrangulada porque excedeu seu quantum de execução. Esse estrangulamento é feito para reduzir o efeito dessa tarefa com muitos recursos em outras tarefas.|  
|SQLSORT_NORMMUTEX|Ocorre durante sincronização interna na inicialização das estruturas de classificação internas.|  
|SQLSORT_SORTMUTEX|Ocorre durante sincronização interna na inicialização das estruturas de classificação internas.|  
|SQLTRACE_BUFFER_FLUSH|Ocorre quando uma tarefa espera que, uma tarefa em segundo plano, libere buffers de rastreamento para o disco a cada quatro segundos.|  
|SQLTRACE_LOCK|Ocorre durante sincronização em buffers de rastreamento durante um rastreamento de arquivo.|  
|SQLTRACE_SHUTDOWN|Ocorre enquanto o desligamento de rastreamento aguarda a conclusão dos eventos de rastreamento pendentes.|  
|SQLTRACE_WAIT_ENTRIES|Ocorre enquanto uma fila de eventos do Rastreamento do SQL aguarda a chegada de pacotes na fila.|  
|SRVPROC_SHUTDOWN|Ocorre enquanto o processo de desligamento aguarda a liberação dos recursos internos para desligamento completo.|  
|TEMPOBJ|Ocorre quando os descartes de objetos temporários são sincronizados. Essa espera é rara e só acontecerá se uma tarefa solicitar acesso exclusivo para descartes de tabelas temporárias.|  
|THREADPOOL|Ocorre quando uma tarefa estiver esperando que um trabalhador seja processado no sistema. Isso pode indicar que a configuração máxima do trabalhador está muito baixa ou que as execuções em lotes estão demorando normalmente mais tempo, reduzindo o número de trabalhadores disponíveis para atender outros lotes.|  
|TIMEPRIV_TIMEPERIOD|Ocorre durante a sincronização interna do timer de Eventos Estendidos.|  
|TRACEWRITE|Ocorre quando o provedor de rastreamento do conjunto de linhas de Rastreamento do SQL aguarda que um buffer livre ou um buffer com eventos seja processado.|  
|TRAN_MARKLATCH_DT|Ocorre ao esperar uma trava de modo de destruição em uma destruição de marcação de transação. Essas travas são usadas para sincronização de confirmações com transações marcadas.|  
|TRAN_MARKLATCH_EX|Ocorre ao esperar uma trava de modo exclusiva em uma transação marcada. Essas travas são usadas para sincronização de confirmações com transações marcadas.|  
|TRAN_MARKLATCH_KP|Ocorre ao esperar uma trava de modo de manutenção em uma transação marcada. Essas travas são usadas para sincronização de confirmações com transações marcadas.|  
|TRAN_MARKLATCH_NL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|TRAN_MARKLATCH_SH|Ocorre ao esperar uma trava de modo compartilhado em uma transação marcada. Essas travas são usadas para sincronização de confirmações com transações marcadas.|  
|TRAN_MARKLATCH_UP|Ocorre ao esperar uma trava de modo de atualização em uma transação marcada. Essas travas são usadas para sincronização de confirmações com transações marcadas.|  
|TRANSACTION_MUTEX|Ocorre durante a sincronização de acesso a uma transação por meio de vários lotes.|  
|UTIL_PAGE_ALLOC|Ocorre quando exames de log de transação aguardam que memória esteja disponível durante pressão da memória.|  
|VIA_ACCEPT|Ocorre quando uma conexão do provedor Virtual Interface Adapter (VIA) é concluída durante a inicialização.|  
|VIEW_DEFINITION_MUTEX|Ocorre durante a sincronização no acesso às definições de exibição em cache.|  
|WAIT_FOR_RESULTS|Ocorre ao esperar a ativação de uma notificação de consulta.|  
|WAITFOR|Ocorre como resultado de uma instrução WAITFOR [!INCLUDE[tsql](../../includes/tsql-md.md)]. A duração da espera é determinada pelos parâmetros da instrução. Essa é uma espera iniciada pelo usuário.|  
|WAITFOR_TASKSHUTDOWN|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|WAITSTAT_MUTEX|Ocorre durante a sincronização de acesso à coleção de estatísticas usadas para popular sys.dm_os_wait_stats.|  
|WCC|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|WORKTBL_DROP|Ocorre ao pausar antes de tentar novamente, após uma falha no descarte de uma tabela de trabalho.|  
|WRITE_COMPLETION|Ocorre quando uma operação de gravação está em andamento.|  
|WRITELOG|Ocorre ao aguardar que uma liberação de log seja concluída. As operações comuns que causam liberações de log são pontos de verificação e confirmações de transação.|  
|XACT_OWN_TRANSACTION|Ocorre enquanto se espera a aquisição da propriedade de uma transação.|  
|XACT_RECLAIM_SESSION|Ocorre enquanto se espera que o proprietário atual de uma sessão libere a propriedade da sessão.|  
|XACTLOCKINFO|Ocorre durante a sincronização de acesso à lista de bloqueios para uma transação. Além da própria transação, a lista de bloqueios é acessada por operações como detecção de deadlock e migração de bloqueio durante divisões de páginas.|  
|XACTWORKSPACE_MUTEX|Ocorre durante a sincronização de remoções de uma transação, bem como do número de bloqueios de banco de dados entre os membros registrados de uma transação.|  
|XE_BUFFERMGR_ALLPROCESSED_EVENT|Ocorre quando buffers de sessão de Eventos Estendidos são liberados para destinos. Essa espera ocorre em um thread em segundo plano.|  
|XE_BUFFERMGR_FREEBUF_EVENT|Ocorre quando uma destas condições é verdadeira:<br /><br /> Uma sessão de Eventos Estendidos é configurada para nenhuma perda de evento e todos os buffers na sessão estão atualmente cheios. Isso pode indicar que os buffers para uma sessão de Eventos Estendidos são muito pequenos ou devem ser particionados.<br /><br /> As auditorias apresentam um atraso. Isso pode indicar um gargalo de disco na unidade onde as auditorias são gravadas.|  
|XE_DISPATCHER_CONFIG_SESSION_LIST|Ocorre quando uma sessão de Eventos Estendidos que está usando destinos assíncronos é iniciada ou interrompida. Essa espera indica qualquer um dos seguintes:<br /><br /> Uma sessão de Eventos Estendidos está sendo registrada com um pool de thread em segundo plano.<br /><br /> O pool de thread em segundo plano está calculando o número necessário de threads com base na carga atual.|  
|XE_DISPATCHER_JOIN|Ocorre quando um thread em segundo plano que é usado para sessões de Eventos Estendidos está sendo encerrado.|  
|XE_DISPATCHER_WAIT|Ocorre quando um thread em segundo plano que é usado para sessões de Eventos Estendidos está esperando o processamento de buffers de evento.|  
|XE_MODULEMGR_SYNC|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|XE_OLS_LOCK|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|XE_PACKAGE_LOCK_BACKOFF|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|FT_COMPROWSET_RWLOCK|O texto completo está pendente na operação de metadados de fragmento. Documentado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.|  
|FT_IFTS_RWLOCK|O texto completo está pendente na sincronização interna. Documentado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.|  
|FT_IFTS_SCHEDULER_IDLE_WAIT|Tipo de espera de suspensão do agendador de texto completo. O agendador está ocioso.|  
|FT_IFTSHC_MUTEX|O texto completo está pendente em uma operação de controle fdhost. Documentado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.|  
|FT_IFTSISM_MUTEX|O texto completo está pendente na operação de comunicação. Documentado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.|  
|FT_MASTER_MERGE|O texto completo está pendente na operação de mesclagem mestre. Documentado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.|  
  
  
