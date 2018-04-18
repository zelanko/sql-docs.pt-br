---
title: sp_trace_setevent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_trace_setevent_TSQL
- sp_trace_setevent
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_setevent
ms.assetid: 7662d1d9-6d0f-443a-b011-c901a8b77a44
caps.latest.revision: 49
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: bf4e3f645a8480104fcb6f67790563fbb05d0480
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sptracesetevent-transact-sql"></a>sp_trace_setevent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona ou remove um evento ou coluna de eventos a um rastreamento. **sp_trace_setevent** pode ser executado apenas em rastreamentos existentes que são interrompidos (*status* é **0**). Um erro será retornado se armazenados por esse procedimento é executado em um rastreamento que não existe ou cujo *status* não é **0**.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use Eventos Estendidos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_trace_setevent [ @traceid = ] trace_id   
          , [ @eventid = ] event_id  
          , [ @columnid = ] column_id  
          , [ @on = ] on  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@traceid=** ] *trace_id*  
 É a ID do rastreamento a ser modificado. *trace_id* é **int**, sem padrão. O usuário emprega este *trace_id* valor para identificar, modificar e controlar o rastreamento.  
  
 [  **@eventid=** ] *event_id*  
 É a ID do evento a ser ativado. *event_id* é **int**, sem padrão.  
  
 Esta tabela lista os eventos que podem ser adicionados ou removidos de um rastreamento.  
  
|Número do evento|Nome do evento|Description|  
|------------------|----------------|-----------------|  
|0-9|Reservado|Reservado|  
|10|RPC:Completed|Ocorre quando uma RPC (chamada de procedimento remoto) é concluída.|  
|11|RPC:Starting|Ocorre quando uma RPC é iniciada.|  
|12|SQL:BatchCompleted|Ocorre quando um lote [!INCLUDE[tsql](../../includes/tsql-md.md)] é concluído.|  
|13|SQL:BatchStarting|Ocorre quando um lote [!INCLUDE[tsql](../../includes/tsql-md.md)] é iniciado.|  
|14|Audit Login|Ocorre quando um usuário faz logon com êxito no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|15|Audit Logout|Ocorre quando um usuário faz logoff do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|16|Attention|Ocorre quando eventos de atenção, como solicitações de interrupção de cliente ou conexões de cliente interrompidas, acontecem.|  
|17|ExistingConnection|Detecta toda a atividade dos usuários conectados ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes do início do rastreamento.|  
|18|Audit Server Starts and Stops|Ocorre quando o estado de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é modificado.|  
|19|DTCTransaction|Rastreia as transações do MS DTC ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator) entre dois ou mais bancos de dados.|  
|20|Audit Login Failed|Indica que uma tentativa de logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um cliente falhou.|  
|21|EventLog|Indica que os eventos foram registrados no log de aplicativo do Windows.|  
|22|ErrorLog|Indica que eventos de erro foram registrados no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|23|Lock:Released|Indica que um bloqueio em um recurso, como uma página, foi liberado.|  
|24|Lock:Acquired|Indica a aquisição de um bloqueio em um recurso, como uma página de dados.|  
|25|Lock:Deadlock|Indica que duas transações simultâneas fizeram deadlock uma na outra ao tentar obter bloqueios incompatíveis em recursos de propriedade da outra transação.|  
|26|Lock:Cancel|Indica que a aquisição de um bloqueio em um recurso foi cancelada (por exemplo, devido a um deadlock).|  
|27|Lock:Timeout|Indica que uma solicitação para um bloqueio em um recurso, como uma página, expirou por causa de outra transação que estava mantendo um bloqueio no recurso necessário. Tempo limite é determinado pelo @@LOCK_TIMEOUT de função e pode ser definido com a instrução SET LOCK_TIMEOUT.|  
|28|Degree of Parallelism Event (7.0 Insert)|Acontece antes de uma instrução SELECT, INSERT ou UPDATE ser executada.|  
|29-31|Reservado|Use o Evento 28 em vez disso.|  
|32|Reservado|Reservado|  
|33|Exceção|Indica que uma exceção ocorreu no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|34|SP:CacheMiss|Indica quando um procedimento armazenado não é localizado no cache de procedimento.|  
|35|SP:CacheInsert|Indica quando um item é inserido no cache de procedimento.|  
|36|SP:CacheRemove|Indica quando um item é removido do cache de procedimento.|  
|37|SP:Recompile|Indica que um procedimento armazenado foi recompilado.|  
|38|SP:CacheHit|Indica quando um procedimento armazenado é localizado no cache de procedimento.|  
|39|Preterido|Preterido|  
|40|SQL:StmtStarting|Ocorre quando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] é iniciada.|  
|41|SQL:StmtCompleted|Ocorre quando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] é concluída.|  
|42|SP:Starting|Indica quando o procedimento armazenado é iniciado.|  
|43|SP:Completed|Indica quando o procedimento armazenado é concluído.|  
|44|SP:StmtStarting|Indica que a execução de uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] em um procedimento armazenado foi iniciada.|  
|45|SP:StmtCompleted|Indica que a execução de uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] em um procedimento armazenado foi concluída.|  
|46|Object:Created|Indica que um objeto foi criado, tal como para as instruções CREATE INDEX, CREATE TABLE e CREATE DATABASE.|  
|47|Object:Deleted|Indica que um objeto foi excluído, tal como nas instruções DROP INDEX e DROP TABLE.|  
|48|Reservado||  
|49|Reservado||  
|50|SQL Transaction|Rastreia as seguintes instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]: BEGIN TRAN, COMMIT TRAN, SAVE TRAN e ROLLBACK TRAN.|  
|51|Scan:Started|Indica quando foi iniciada uma verificação de tabela ou de índice.|  
|52|Scan:Stopped|Indica quando foi interrompida uma verificação de tabela ou de índice.|  
|53|CursorOpen|Indica quando um cursor é aberto em uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] por ODBC, OLE DB ou DB-Library.|  
|54|TransactionLog|Rastreia quando as transações são gravadas no log de transações.|  
|55|Hash Warning|Indica que uma operação de hash (por exemplo, junção hash, agregação de hash, união de hash e distinção de hash) que não está sendo processada em uma partição de buffer foi revertida para um plano alternativo. Isso pode ocorrer por causa de profundidade de recursão, distorção de dados, sinalizadores de rastreamento ou contagem de bits.|  
|56-57|Reservado||  
|58|Auto Stats|Indica que ocorreu uma atualização automática de estatísticas de índice.|  
|59|Lock:Deadlock Chain|Produzido para cada um dos eventos que resultam no deadlock.|  
|60|Lock:Escalation|Indica que um bloqueio mais refinado foi convertido em um bloqueio mais rústico (por exemplo, um bloqueio de página escalonado ou convertido em um bloqueio TABLE ou HoBT).|  
|61|OLE DB Errors|Indica que ocorreu um erro OLE DB.|  
|62-66|Reservado||  
|67|Execution Warnings|Indicam qualquer aviso que ocorreu durante a execução de uma instrução ou um procedimento armazenado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|68|Showplan Text (Unencoded)|Exibe a árvore de plano da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] executada.|  
|69|Sort Warnings|Indica operações de classificação que não cabem na memória. Isso não inclui operações de classificação envolvendo a criação de índices, mas somente operações de classificação em uma consulta (como uma cláusula ORDER BY usada em uma instrução SELECT).|  
|70|CursorPrepare|Indica quando um cursor em uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] está pronto para ser usado por ODBC, OLE DB ou DB-Library.|  
|71|Prepare SQL|ODBC, OLE DB ou DB-Library preparou uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] ou instruções para uso.|  
|72|Exec Prepared SQL|ODBC, OLE DB ou DB-Library executou uma instrução ou instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] preparadas.|  
|73|Unprepare SQL|ODBC, OLE DB ou DB-Library despreparou (excluiu) uma instrução ou instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] preparadas.|  
|74|CursorExecute|Um cursor anteriormente preparado em uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] por ODBC, OLE DB ou DB-Library é executado.|  
|75|CursorRecompile|Um cursor aberto em uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] por ODBC, OLE DB, ou DB-Library foi recompilado diretamente ou devido a uma alteração de esquema.<br /><br /> Disparado para cursores ANSI e não ANSI.|  
|76|CursorImplicitConversion|Um cursor em uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] é convertido de um tipo para outro pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Disparado para cursores ANSI e não ANSI.|  
|77|CursorUnprepare|Um cursor preparado em uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] é despreparado (excluído) por ODBC, OLE DB ou DB-Library.|  
|78|CursorClose|Um cursor anteriormente aberto em uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] por ODBC, OLE DB, ou DB-Library foi fechado.|  
|79|Missing Column Statistics|Estatísticas de coluna que podem ter sido úteis para o otimizador não estão disponíveis.|  
|80|Missing Join Predicate|A consulta que está sendo executada não tem nenhum predicado de junção. Isso pode resultar em uma consulta de longa execução.|  
|81|Server Memory Change|O uso de memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aumentou ou diminuiu em 1 megabyte (MB) ou em 5 por cento da memória máxima de servidor, o que for maior.|  
|82-91|User Configurable (0-9)|Dados de evento definidos pelo usuário.|  
|92|Data File Auto Grow|Indica que um arquivo de dados foi automaticamente estendido pelo servidor.|  
|93|Log File Auto Grow|Indica que um arquivo de log foi automaticamente estendido pelo servidor.|  
|94|Data File Auto Shrink|Indica que um arquivo de dados foi automaticamente reduzido pelo servidor.|  
|95|Log File Auto Shrink|Indica que um arquivo de log foi automaticamente reduzido pelo servidor.|  
|96|Showplan Text|Exibe a árvore de plano de consulta da instrução SQL a partir do otimizador de consulta. Observe que o **TextData** coluna não contém o plano de execução para este evento.|  
|97|Showplan All|Exibe o plano de consulta com detalhes completos de tempo de compilação da instrução SQL executada. Observe que o **TextData** coluna não contém o plano de execução para este evento.|  
|98|Showplan Statistics Profile|Exibe o plano de consulta com detalhes completos de tempo de execução da instrução SQL executada. Observe que o **TextData** coluna não contém o plano de execução para este evento.|  
|99|Reservado||  
|100|RPC Output Parameter|Produz valores de saída dos parâmetros para todo RPC.|  
|101|Reservado||  
|102|Audit Database Scope GDR|Ocorre sempre que GRANT, DENY, REVOKE é emitido para uma permissão de instrução por qualquer usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ações somente de banco de dados, como conceder permissões em um banco de dados.|  
|103|Evento Audit Object GDR|Ocorre sempre que um GRANT, DENY, REVOKE para uma permissão de objeto é emitido por qualquer usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|104|Evento Audit AddLogin|Ocorre quando um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon é adicionado ou removido; para **sp_addlogin** e **sp_droplogin**.|  
|105|Evento Audit Login GDR|Ocorre quando um direito de logon é adicionado ou removido; para **sp_grantlogin**, **sp_revokelogin**, e **sp_denylogin**.|  
|106|Evento Audit Login Change Property|Ocorre quando uma propriedade de um logon, exceto senhas, é modificada; para **sp_defaultdb** e **sp_defaultlanguage**.|  
|107|Evento Audit Login Change Password|Ocorre quando uma senha de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é alterada.<br /><br /> As senhas não são registradas.|  
|108|Evento Audit Add Login to Server Role|Ocorre quando um logon é adicionado ou removido de uma função de servidor fixa; para **sp_addsrvrolemember**, e **sp_dropsrvrolemember**.|  
|109|Evento Audit Add DB User|Ocorre quando um logon é adicionado ou removido como um usuário de banco de dados (Windows ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) para um banco de dados; para **sp_grantdbaccess**, **sp_revokedbaccess**, **sp_adduser**, e **sp_dropuser**.|  
|110|Evento Audit Add Member to DB Role|Ocorre quando um logon é adicionado ou removido como um usuário de banco de dados (fixa ou definida pelo usuário) para um banco de dados; para **sp_addrolemember**, **sp_droprolemember**, e **sp_changegroup**.|  
|111|Evento Audit Add Role|Ocorre quando um logon é adicionado ou removido como um usuário de banco de dados para um banco de dados; para **sp_addrole** e **sp_droprole**.|  
|112|Evento Audit App Role Change Password|Ocorre quando uma senha de uma função de aplicativo é alterada.|  
|113|Evento Audit Statement Permission|Ocorre quando uma permissão de instrução (como CREATE TABLE) é usada.|  
|114|Evento Audit Schema Object Access|Ocorre quando uma permissão de objeto (como SELECT) é usada, com êxito ou não.|  
|115|Audit Backup/Restore Event|Ocorre quando um comando BACKUP ou RESTORE é emitido.|  
|116|Evento Audit DBCC|Ocorre quando comandos DBCC são emitidos.|  
|117|Evento Audit Change Audit|Ocorre quando são feitas modificações de rastreamento de auditoria.|  
|118|Evento Audit Object Derived Permission|Ocorre quando um comando de objeto CREATE, ALTER e DROP é emitido.|  
|119|Evento OLEDB Call|Ocorre quando as chamadas de provedor OLE DB são feitas para consultas distribuídas e procedimentos armazenados remotos.|  
|120|Evento OLEDB QueryInterface|Ocorre quando OLE DB **QueryInterface** chamadas são feitas para consultas distribuídas e procedimentos armazenados remotos.|  
|121|Evento OLEDB DataRead|Ocorre quando uma chamada de solicitação de dados é feita ao provedor OLE DB.|  
|122|Showplan XML|Ocorre quando uma instrução SQL é executada. Inclua este evento para identificar operadores de plano de execução. Cada evento é armazenado em um documento XML bem formado. Observe que o **binário** coluna para este evento contém o plano de execução codificado. Use o SQL Server Profiler para abrir o rastreamento e exibir o plano de execução.|  
|123|SQL:FullTextQuery|Ocorre quando uma consulta de texto completo é executada.|  
|124|Broker:Conversation|Relata o progresso de uma conversa do [!INCLUDE[ssSB](../../includes/sssb-md.md)].|  
|125|Deprecation Announcement|Ocorre quando é usado um recurso que será removido de uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|126|Deprecation Final Support|Ocorre quando é usado um recurso que será removido da próxima versão principal do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|127|Evento Exchange Spill|Ocorre quando buffers de comunicação em um plano de consulta paralelo foram temporariamente gravados para o **tempdb** banco de dados.|  
|128|Evento Audit Database Management|Ocorre quando um banco de dados é criado, alterado ou descartado.|  
|129|Evento Audit Database Object Management|Ocorre quando uma instrução CREATE, ALTER ou DROP é executada em objetos de banco de dados, como esquemas.|  
|130|Evento Audit Database Principal Management|Ocorre quando os principais, como usuários, são criados, alterados ou descartados de um banco de dados.|  
|131|Evento Audit Schema Object Management|Ocorre quando objetos de servidor são criados, alterados ou descartados.|  
|132|Evento Audit Server Principal Impersonation|Ocorre quando há uma representação no escopo de servidor, como EXECUTE LOGIN AS.|  
|133|Evento Audit Database Principal Impersonation|Ocorre quando uma representação acontece no escopo de banco de dados, como EXECUTE AS USER ou SETUSER.|  
|134|Evento Audit Server Object Take Ownership|Ocorre quando o proprietário é alterado para objetos no escopo de servidor.|  
|135|Evento Audit Database Object Take Ownership|Ocorre quando acontece uma alteração de proprietário para objetos no escopo de banco de dados.|  
|136|Broker:Conversation Group|Ocorre quando o [!INCLUDE[ssSB](../../includes/sssb-md.md)] cria um novo grupo de conversa ou descarta um existente.|  
|137|Blocked Process Report|Ocorre quando um processo foi bloqueado para mais do que um período especificado. Não inclui processos do sistema ou processos que estão aguardando em recursos não detectáveis por deadlock. Use **sp_configure** para configurar o limite e a frequência em que os relatórios são gerados.|  
|138|Broker:Connection|Relata o status de uma conexão de transporte administrada pelo [!INCLUDE[ssSB](../../includes/sssb-md.md)].|  
|139|Broker:Forwarded Message Sent|Ocorre quando o [!INCLUDE[ssSB](../../includes/sssb-md.md)] encaminha uma mensagem.|  
|140|Broker:Forwarded Message Dropped|Ocorre quando o [!INCLUDE[ssSB](../../includes/sssb-md.md)] descarta uma mensagem destinada a ser encaminhada.|  
|141|Broker:Message Classify|Ocorre quando o [!INCLUDE[ssSB](../../includes/sssb-md.md)] determina o roteamento para uma mensagem.|  
|142|Broker:Transmission|Indica que erros ocorreram na camada de transporte do [!INCLUDE[ssSB](../../includes/sssb-md.md)]. O número do erro e os valores de estado indicam a origem do erro.|  
|143|Broker:Queue Disabled|Indica que uma mensagem suspeita foi detectada porque havia cinco reversões de transação sucessivas em uma fila do [!INCLUDE[ssSB](../../includes/sssb-md.md)]. O evento contém a ID do banco de dados e a ID de fila da fila que contém a mensagem suspeita.|  
|144-145|Reservado||  
|146|Showplan XML Statistics Profile|Ocorre quando uma instrução SQL é executada. Identifica os operadores de plano de execução e exibe dados de tempo de compilação completos. Observe que o **binário** coluna para este evento contém o plano de execução codificado. Use o SQL Server Profiler para abrir o rastreamento e exibir o plano de execução.|  
|148|Deadlock Graph|Ocorre quando uma tentativa para adquirir um bloqueio é cancelada porque a tentativa fazia parte de um deadlock e foi escolhida como a vítima de deadlock. Fornece uma descrição XML de um deadlock.|  
|149|Broker:Remote Message Acknowledgement|Ocorre quando o [!INCLUDE[ssSB](../../includes/sssb-md.md)] envia ou recebe uma confirmação de mensagem.|  
|150|Trace File Close|Ocorre quando um arquivo de rastreamento é fechado durante a sua substituição.|  
|151|Reservado||  
|152|Audit Change Database Owner|Ocorre quando a instrução ALTER AUTHORIZATION é usada para alterar o proprietário de um banco de dados e as permissões são marcadas para fazer isso.|  
|153|Evento Audit Schema Object Take Ownership|Ocorre quando a instrução ALTER AUTHORIZATION é usada para atribuir um proprietário a um objeto e as permissões para fazer isso estão marcadas.|  
|154|Reservado||  
|155|FT:Crawl Started|Ocorre quando um rastreamento (população) de texto completo é iniciado. Use para verificar se uma solicitação de rastreamento está sendo selecionada por tarefas de trabalhado.|  
|156|FT:Crawl Stopped|Ocorre quando um rastreamento (população) de texto completo é interrompido. As interrupções acontecem quando um rastreamento é concluído com êxito ou quando ocorre um erro fatal.|  
|157|FT:Crawl Aborted|Ocorre quando uma exceção é encontrada em um rastreamento de texto completo. Em geral, provoca a interrupção do rastreamento de texto completo.|  
|158|Audit Broker Conversation|Relata mensagens de auditoria relacionadas à segurança de diálogo do [!INCLUDE[ssSB](../../includes/sssb-md.md)].|  
|159|Audit Broker Login|Relata mensagens de auditoria relacionadas à segurança de transporte do [!INCLUDE[ssSB](../../includes/sssb-md.md)].|  
|160|Broker:Message Undeliverable|Ocorre quando o [!INCLUDE[ssSB](../../includes/sssb-md.md)] não pode reter uma mensagem recebida que deve ser entregue a um serviço.|  
|161|Broker:Corrupted Message|Ocorre quando o [!INCLUDE[ssSB](../../includes/sssb-md.md)] recebe uma mensagem corrompida.|  
|162|User Error Message|Exibe mensagens de erro que os usuários veem no caso de um erro ou uma exceção.|  
|163|Broker:Activation|Ocorre quando um monitor de fila inicia um procedimento armazenado de ativação, envia uma notificação QUEUE_ACTIVATION ou quando um procedimento armazenado de ativação iniciado por um monitor de fila é encerrado.|  
|164|Object:Altered|Ocorre quando um objeto de banco de dados é alterado.|  
|165|Performance statistics|Ocorre quando um plano de consulta compilado foi armazenado em cache pela primeira vez, recompilado ou removido do cache do plano.|  
|166|SQL:StmtRecompile|Ocorre quando uma recompilação do nível de instrução acontece.|  
|167|Database Mirroring State Change|Ocorre quando o estado de um banco de dados espelho é alterado.|  
|168|Showplan XML For Query Compile|Ocorre quando uma instrução SQL é compilada. Exibe os dados de tempo de compilação completos. Observe que o **binário** coluna para este evento contém o plano de execução codificado. Use o SQL Server Profiler para abrir o rastreamento e exibir o plano de execução.|  
|169|Showplan All For Query Compile|Ocorre quando uma instrução SQL é compilada. Exibe dados concluídos, o tempo de compilação. Use para identificar operadores de plano de execução.|  
|170|Evento Audit Server Scope GDR|Indica que ocorreu um evento de concessão, recusa ou revogação para permissões no escopo de servidor, tal como criar um logon.|  
|171|Evento Audit Server Object GDR|Indica que ocorreu um evento de concessão, negação ou revogação para um objeto de esquema, tal como uma tabela ou função.|  
|172|Evento Audit Database Object GDR|Indica que ocorreu um evento de concessão, negação ou revogação para objetos de banco de dados, tal como assemblies e esquemas.|  
|173|Evento Audit Server Operation|Ocorre quando são usadas operações de Segurança Auditoria, tal como alterar configurações, recursos, acesso externo ou autorização.|  
|175|Evento Audit Server Alter Trace|Ocorre quando uma instrução verifica a permissão ALTER TRACE.|  
|176|Evento Audit Server Object Management|Ocorre quando objetos de servidor são criados, alterados ou descartados.|  
|177|Evento Audit Server Principal Management|Ocorre quando principais são criados, alterados ou descartados.|  
|178|Evento Audit Database Operation|Ocorre quando ocorrem operações de banco de dados, tal como ponto de verificação ou notificação de consulta de assinatura.|  
|180|Evento Audit Database Object Access|Ocorre quando são acessados objetos de banco de dados, tal como esquemas.|  
|181|TM: Begin Tran starting|Ocorre quando uma solicitação BEGIN TRANSACTION é iniciada.|  
|182|TM: Begin Tran completed|Ocorre quando uma solicitação BEGIN TRANSACTION é concluída.|  
|183|TM: Promote Tran starting|Ocorre quando uma solicitação PROMOTE TRANSACTION é iniciada.|  
|184|TM: Promote Tran completed|Ocorre quando uma solicitação PROMOTE TRANSACTION é concluída.|  
|185|TM: Commit Tran starting|Ocorre quando uma solicitação COMMIT TRANSACTION é iniciada.|  
|186|TM: Commit Tran completed|Ocorre quando uma solicitação COMMIT TRANSACTION é concluída.|  
|187|TM: Rollback Tran starting|Ocorre quando uma solicitação ROLLBACK TRANSACTION é iniciada.|  
|188|TM: Rollback Tran completed|Ocorre quando uma solicitação ROLLBACK TRANSACTION é concluída.|  
|189|Lock: Timeout (timeout > 0)|Ocorre quando uma solicitação para um bloqueio em um recurso, como uma página, expira.|  
|190|Progress Report: Online Index Operation|Relata o progresso de uma operação de criação de índice online quando o processo de criação está sendo executado.|  
|191|TM: Save Tran starting|Ocorre quando uma solicitação SAVE TRANSACTION é iniciada.|  
|192|TM: Save Tran completed|Ocorre quando uma solicitação SAVE TRANSACTION é concluída.|  
|193|Background Job Error|Ocorre quando um trabalho em segundo plano é terminado de maneira anormal.|  
|194|OLEDB Provider Information|Ocorre quando uma consulta distribuída é executada e coleta informações que correspondem à conexão de provedor.|  
|195|Mount Tape|Ocorre quando uma solicitação de montagem de fita é recebida.|  
|196|Assembly Load|Ocorre quando acontece uma solicitação para carregar um assembly CLR.|  
|197|Reservado||  
|198|XQuery Static Type|Ocorre quando uma expressão XQuery é executada. Essa classe de evento fornece o tipo estático da expressão XQuery.|  
|199|QN: subscription|Ocorre quando um registro de consulta não pode ser assinado. O **TextData** coluna contém informações sobre o evento.|  
|200|QN: parameter table|Informações sobre assinaturas ativas são armazenadas em tabelas de parâmetro internas. Esta classe de evento ocorre quando uma tabela de parâmetro é criada ou excluída. Normalmente, essas tabelas são criadas ou excluídas quando o banco de dados é reiniciado. O **TextData** coluna contém informações sobre o evento.|  
|201|QN: template|Um modelo de consulta representa uma classe de consultas de assinatura. Normalmente, as consultas de mesma classe são idênticas com exceção dos valores de parâmetro. Essa classe de evento ocorre quando uma nova solicitação de assinatura se enquadra em uma classe já existente de (Match), uma nova classe (Create) ou uma classe Drop, que indica a limpeza de modelos para classes de consulta sem assinaturas ativas. O **TextData** coluna contém informações sobre o evento.|  
|202|QN: dynamics|Rastreia atividades internas de notificações de consulta. O **TextData** coluna contém informações sobre o evento.|  
|212|Aviso de bitmap|Indica quando os filtros do bitmap foram desabilitados em uma consulta.|  
|213|Database Suspect Data Page|Indica quando uma página é adicionada para o **suspect_pages** tabela **msdb**.|  
|214|Limite de CPU excedido|Indica quando o Administrador de Recursos detecta que uma consulta excedeu o valor do limite de CPU em (REQUEST_MAX_CPU_TIME_SEC).|  
|215|Indica quando uma função do gatilho LOGON ou do classificador Administrador de Recursos inicia a execução.|Indica quando uma função do gatilho LOGON ou do classificador Administrador de Recursos inicia a execução.|  
|216|PreConnect:Completed|Indica quando uma função do gatilho LOGON ou do classificador Administrador de Recursos conclui a execução.|  
|217|Guia de plano bem-sucedido|Indica que o SQL Server produziu com sucesso um plano de execução para uma consulta ou lote, que continha um guia de plano.|  
|218|Guia de plano malsucedido|Indica que o SQL Server não pôde produzir um plano de execução, para uma consulta ou lote, que continha um guia de plano. O SQL Server tentou gerar um plano de execução para esta consulta ou lote sem aplicar o guia de plano. Um guia de plano inválido pode ser a causa deste problema. Você pode validar o guia de plano usando a função de sistema sys.fn_validate_plan_guide.|  
|235|Audit Fulltext||  
  
 [  **@columnid=** ] *column_id*  
 É a ID da coluna a ser adicionada para o evento. *column_id* é **int**, sem padrão.  
  
 A tabela a seguir lista as colunas que podem ser adicionadas a um evento.  
  
|Número da coluna|Nome da coluna|Description|  
|-------------------|-----------------|-----------------|  
|1|**TextData**|Valor de texto dependente da classe de evento capturada no rastreamento.|  
|2|**BinaryData**|Valor binário dependente da classe de evento capturada no rastreamento.|  
|3|**DatabaseID**|ID do banco de dados especificado pelo uso *banco de dados* instrução ou o banco de dados padrão se nenhum uso *banco de dados* instrução for emitida para uma determinada conexão.<br /><br /> O valor para um banco de dados pode ser determinado usando a função DB_ID.|  
|4|**TransactionID**|ID da transação atribuída pelo sistema.|  
|5|**LineNumber**|O número da linha que contém o erro. No caso de eventos que envolvem instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] , como **SP:StmtStarting**, **LineNumber** contém o número de linha da instrução no procedimento armazenado ou lote.|  
|6|**NTUserName**|Nome de usuário do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.|  
|7|**NTDomainName**|O domínio do Windows ao qual o usuário pertence.|  
|8|**HostName**|Nome do computador cliente que originou a solicitação.|  
|9|**ClientProcessID**|ID atribuída pelo computador cliente ao processo no qual o aplicativo cliente está sendo executado.|  
|10|**ApplicationName**|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|  
|11|**LoginName**|Nome de logon do cliente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|12|**SPID**|ID de processo de servidor atribuída pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao processo associado ao cliente.|  
|13|**Duration**|Tempo decorrido (em milhões de segundos) utilizado pelo evento. Esta coluna de dados não é populada pelo evento Hash Warning.|  
|14|**StartTime**|Horário de início do evento, quando disponível.|  
|15|**EndTime**|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como **SQL:BatchStarting** ou **SP:Starting**. Ele também não é preenchido com o **Hash Warning** eventos.|  
|16|**Reads**|Número de leituras lógicas do disco executadas pelo servidor em nome do evento. Esta coluna não é populada pelo **bloqueio: liberado** eventos.|  
|17|**Writes**|Número de gravações no disco físico executadas pelo servidor em nome do evento.|  
|18|**CPU**|Tempo da CPU (em milissegundos) usado pelo evento.|  
|19|**Permissões**|Representa o bitmap de permissões; usada pela Security Auditing.|  
|20|**Severity**|Nível de severidade de uma exceção.|  
|21|**EventSubClass**|Tipo de subclasse de evento. Essa coluna de dados não é populada para todas as classes de evento.|  
|22|**ObjectID**|ID de objeto atribuída pelo sistema.|  
|23|**Êxito**|Êxito da tentativa de uso de permissões; usada para auditoria.<br /><br /> **1** = êxito**0** = falha|  
|24|**IndexID**|ID do índice no objeto afetado pelo evento. Para determinar a ID do índice de um objeto, use a coluna **indid** da tabela do sistema **sysindexes** .|  
|25|**IntegerData**|O valor inteiro dependente da classe de evento capturada no rastreamento.|  
|26|**ServerName**|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], *servername* ou *NomedoServidor \ NomedaInstância*, que está sendo rastreado.|  
|27|**EventClass**|Tipo de classe de evento que está sendo registrada.|  
|28|**ObjectType**|Tipo de objeto, como tabela, função ou procedimento armazenado.|  
|29|**NestLevel**|O nível de aninhamento no qual esse procedimento armazenado está sendo executado. Consulte [@@NESTLEVEL &#40;Transact-SQL&#41;](../../t-sql/functions/nestlevel-transact-sql.md).|  
|30|**Estado**|Estado do servidor, no caso de um erro.|  
|31|**Erro**|Número de erro.|  
|32|**Modo**|Modo de bloqueio do bloqueio adquirido. Esta coluna não é populada pelo **bloqueio: liberado** eventos.|  
|33|**Handle**|Identificador do objeto mencionado no evento.|  
|34|**ObjectName**|Nome do objeto acessado.|  
|35|**DatabaseName**|Nome do banco de dados especificado no uso *banco de dados* instrução.|  
|36|**FileName**|Nome lógico do nome de arquivo modificado.|  
|37|**OwnerName**|Nome do proprietário do objeto referenciado.|  
|38|**RoleName**|Nome do banco de dados ou da função em todo o servidor direcionados por uma instrução.|  
|39|**TargetUserName**|Nome de usuário do destino de alguma ação.|  
|40|**DBUserName**|Nome de usuário do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do cliente.|  
|41|**LoginSid**|SID (identificador de segurança) do usuário que fez logon.|  
|42|**TargetLoginName**|Nome de logon do destino de alguma ação.|  
|43|**TargetLoginSid**|SID do logon que é o destino de alguma ação.|  
|44|**ColumnPermissions**|Status de permissões em nível de coluna; usado pela Security Auditing.|  
|45|**LinkedServerName**|Nome do servidor vinculado.|  
|46|**ProviderName**|Nome do provedor OLE DB.|  
|47|**MethodName**|Nome do método OLE DB.|  
|48|**RowCounts**|Número de linhas no lote.|  
|49|**RequestID**|ID da solicitação que contém a instrução.|  
|50|**XactSequence**|Token usado para descrever a transação atual.|  
|51|**EventSequence**|Número de sequência para esse evento.|  
|52|**BigintData1**|**bigint** valor, que é dependente da classe de evento capturada no rastreamento.|  
|53|**BigintData2**|**bigint** valor, que é dependente da classe de evento capturada no rastreamento.|  
|54|**GUID**|Valor GUID, que é dependente da classe de evento capturada no rastreamento.|  
|55|**IntegerData2**|Valor inteiro, que é dependente da classe de evento capturada no rastreamento.|  
|56|**ObjectID2**|ID do objeto relacionado ou entidade, se disponível.|  
|57|**Tipo**|Valor inteiro, que é dependente da classe de evento capturada no rastreamento.|  
|58|**OwnerID**|Tipo o objeto que possui o bloqueio. Apenas para eventos de bloqueio.|  
|59|**ParentName**|Nome do esquema que contém o objeto.|  
|60|**IsSystem**|Indica se o evento ocorreu em um processo do sistema ou do usuário.<br /><br /> **1** = sistema<br /><br /> **0** = usuário.|  
|61|**Deslocamento**|O deslocamento inicial da instrução no lote ou procedimento armazenado.|  
|62|**SourceDatabaseID**|ID do banco de dados no qual existe a fonte do objeto.|  
|63|**SqlHandle**|Hash de 64 bits com base no texto de uma consulta ad hoc ou na ID de objeto e banco de dados de um objeto SQL. Esse valor pode ser passado a **sys.dm_exec_sql_text()** para recuperar o texto SQL associado.|  
|64|**SessionLoginName**|O nome de logon do usuário que originou a sessão. Por exemplo, se você se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando **Login1** e executar uma instrução como **Login2**, **SessionLoginName** irá exibir **Login1**, enquanto que **LoginName** exibirá **Login2**. Esta coluna de dados exibe logons tanto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , quanto do Windows.|  
  
 **[ @on=]** *on*  
 Especifica se o evento deve ser ON (1) ou OFF (0). *em* é **bit**, sem padrão.  
  
 Se *na* é definido como **1**, e *column_id* for NULL, em seguida, o evento é definido como ON e todas as colunas são limpas. Se *column_id* não for nulo, então a coluna é definida como ON para o evento.  
  
 Se *na* é definido como **0**, e *column_id* for NULL, o evento será transformado OFF e todas as colunas são limpas. Se *column_id* não for nulo, então a coluna for ativada OFF.  
  
 Esta tabela ilustra a interação entre **@on** e **@columnid**.  
  
|@on|@columnid|Resultado|  
|---------|---------------|------------|  
|ON (**1**)|NULL|Evento é definido como ON.<br /><br /> Todas as colunas são limpas.|  
||NOT NULL|A coluna é definida como ON para o evento especificado.|  
|OFF (**0**)|NULL|O evento é definido como OFF.<br /><br /> Todas as colunas são limpas.|  
||NOT NULL|A coluna é definida como OFF para o evento especificado.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 A tabela a seguir descreve os valores de código que os usuários podem obter após a conclusão do procedimento armazenado.  
  
|Código de retorno|Description|  
|-----------------|-----------------|  
|0|Nenhum erro.|  
|1|Erro desconhecido.|  
|2|O rastreamento está sendo executado no momento. Alterar o rastreamento nesse momento resultará em um erro.|  
|3|O evento especificado não é válido. O evento pode não existir ou não é um apropriado para o procedimento de loja.|  
|4|A coluna especificada não é válida.|  
|9|O identificador de rastreamento especificado não é válido.|  
|11|A coluna especificada é usada internamente e não pode ser removida.|  
|13|Memória insuficiente. Retornado quando não há memória suficiente para executar a ação especificada.|  
|16|A função não é válida para este rastreamento.|  
  
## <a name="remarks"></a>Remarks  
 **sp_trace_setevent** executa muitas das ações anteriormente executadas por procedimentos armazenados estendidos disponíveis em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use **sp_trace_setevent** em vez do seguinte:  
  
-   **xp_trace_addnewqueue**  
  
-   **xp_trace_eventclassrequired**  
  
-   **xp_trace_seteventclassrequired**  
  
 Os usuários devem executar **sp_trace_setevent** para cada coluna adicionada para cada evento. Durante cada execução, se **@on** é definido como **1**, **sp_trace_setevent** adiciona o evento especificado à lista de eventos de rastreamento. Se **@on** é definido como **0**, **sp_trace_setevent** remove o evento especificado da lista.  
  
 Os parâmetros de rastreamento de SQL todos os procedimentos armazenados (**sp_trace_xx**) são rigorosamente tipados. Se esses parâmetros não forem chamados com os tipos de dados com parâmetro de entrada corretos, como especificado na descrição do argumento, o procedimento armazenado retornará um erro.  
  
 Para obter um exemplo de como usar procedimentos armazenados de rastreamento, veja [Criar um rastreamento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ter a permissão ALTER TRACE.  
  
## <a name="see-also"></a>Consulte também  
 [sys.fn_trace_geteventinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [sp_trace_generateevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [Referência de classe de evento do SQL Server](../../relational-databases/event-classes/sql-server-event-class-reference.md)   
 [Rastreamento do SQL](../../relational-databases/sql-trace/sql-trace.md)  
  
  
