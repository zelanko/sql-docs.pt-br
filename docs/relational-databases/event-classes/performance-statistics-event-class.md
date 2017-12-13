---
title: Classe de evento Performance Statistics | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: event-classes
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Performance Statistics event class
ms.assetid: da9cd2c4-6fdd-4ada-b74f-105e3541393c
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 952bad5b2f70ce0d1c22579ea50708cd48e6b9a0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="performance-statistics-event-class"></a>classe de evento Performance Statistics
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] A classe de evento Performance Statistics pode ser usada para monitorar o desempenho de consultas, procedimentos armazenados e gatilhos que são executados. Cada uma das seis subclasses de evento indica um evento no tempo de vida de consultas, procedimentos armazenados e gatilhos no sistema. Usando a combinação dessas subclasses de evento e as exibições de gerenciamento dinâmico sys.dm_exec_query_stats, sys.dm_exec_procedure_stats e sys.dm_exec_trigger_stats associadas, você pode reconstituir o histórico de desempenho de qualquer consulta, procedimento armazenado ou gatilho específico.  
  
## <a name="performance-statistics-event-class-data-columns"></a>Colunas de dados da classe de evento Performance Statistics  
 As tabelas a seguir descrevem as colunas de dados da classe de evento associada a cada uma das seguintes subclasses de evento: EventSubClass 0, EventSubClass 1, EventSubClass 2, EventSubClass 3, EventSubClass 4 e EventSubClass 5.  
  
### <a name="eventsubclass-0"></a>EventSubClass 0  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|NULL|52|Sim|  
|BinaryData|**image**|NULL|2|Sim|  
|DatabaseID|**int**|ID do banco de dados especificado pela instrução USE de *database* ou o banco de dados padrão se nenhuma instrução USE de *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados ServerName for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|EventSequence|**int**|Sequência de um determinado evento na solicitação.|51|Não|  
|EventSubClass|**int**|Tipo de subclasse de evento.<br /><br /> 0 = Novo texto SQL de lote que atualmente não está presente no cache.<br /><br /> Os seguintes tipos de EventSubClass são gerados no rastreamento para lotes ad hoc.<br /><br /> Para lotes ad hoc com *n* número de consultas:<br /><br /> 1 do tipo 0|21|Sim|  
|IntegerData2|**Int**|NULL|55|Sim|  
|ObjectID|**Int**|NULL|22|Sim|  
|Deslocamento|**Int**|NULL|61|Sim|  
|PlanHandle|**Image**|NULL|65|Sim|  
|SessionLoginName|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, SessionLoginName mostrará o Logon1 e LoginName mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|SPID|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|SqlHandle|**image**|Identificador SQL que pode ser usado para obter o texto SQL do lote usando a exibição de gerenciamento dinâmico dm_exec_sql_text.|63|Sim|  
|StartTime|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|TextData|**ntext**|Texto SQL do lote.|1|Sim|  
  
### <a name="eventsubclass-1"></a>EventSubClass 1  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|O número cumulativo de vezes que esse plano foi recompilado.|52|Sim|  
|BinaryData|**image**|O XML binário do plano compilado.|2|Sim|  
|DatabaseID|**int**|ID do banco de dados especificado pela instrução USE de *database* ou o banco de dados padrão se nenhuma instrução USE de *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados ServerName for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|EventSequence|**int**|Sequência de um determinado evento na solicitação.|51|Não|  
|SessionLoginName|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, SessionLoginName mostrará o Logon1 e LoginName mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|EventSubClass|**int**|Tipo de subclasse de evento.<br /><br /> 1 = Foram compiladas consultas dentro de um procedimento armazenado.<br /><br /> Os seguintes tipos de EventSubClass são gerados no rastreamento para procedimentos armazenados.<br /><br /> Para procedimentos armazenados com o número de consultas *n* número de consultas:<br /><br /> *n* número de tipo 1|21|Sim|  
|IntegerData2|**Int**|Término da instrução do procedimento armazenado.<br /><br /> -1 para o término do procedimento armazenado.|55|Sim|  
|ObjectID|**int**|ID de objeto atribuída pelo sistema.|22|Sim|  
|Deslocamento|**int**|O deslocamento inicial da instrução no lote ou procedimento armazenado.|61|Sim|  
|SPID|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|SqlHandle|**image**|Identificador SQL que pode ser usado para obter o texto SQL do procedimento armazenado usando a exibição de gerenciamento dinâmico dm_exec_sql_text.|63|Sim|  
|StartTime|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|TextData|**ntext**|NULL|1|Sim|  
|PlanHandle|**image**|O identificador do plano compilado para o procedimento armazenado. Isso pode ser usado para obter o plano XML usando a exibição de gerenciamento dinâmico sys.dm_exec_query_plan.|65|Sim|  
|ObjectType|**Int**|Um valor que representa o tipo do objeto envolvido no evento.<br /><br /> 8272 = procedimento armazenado|28|Sim|  
|BigintData2|**bigint**|Memória total, em quilobytes, usada durante a compilação.|53|Sim|  
|CPU|**Int**|Tempo total de CPU, em milissegundos, gasto durante a compilação.|18|Sim|  
|Duration|**Int**|Tempo total, em milissegundos, gasto durante a compilação.|13|Sim|  
|IntegerData|**Int**|O tamanho, em quilobytes, do plano compilado.|25|Sim|  
  
### <a name="eventsubclass-2"></a>EventSubClass 2  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|O número cumulativo de vezes que esse plano foi recompilado.|52|Sim|  
|BinaryData|**image**|O XML binário do plano compilado.|2|Sim|  
|DatabaseID|**int**|ID do banco de dados especificado pela instrução USE de *database* ou o banco de dados padrão se nenhuma instrução USE de *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados ServerName for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|EventSequence|**int**|Sequência de um determinado evento na solicitação.|51|Não|  
|SessionLoginName|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, SessionLoginName mostrará o Logon1 e LoginName mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|EventSubClass|**int**|Tipo de subclasse de evento.<br /><br /> 2 = Consultas dentro um instrução SQL ad hoc foram compiladas.<br /><br /> Os seguintes tipos de EventSubClass são gerados no rastreamento para lotes ad hoc.<br /><br /> Para lotes ad hoc com *n* número de consultas:<br /><br /> *n* número de tipo 2|21|Sim|  
|IntegerData2|**Int**|Término da instrução dentro do lote.<br /><br /> -1 para o término do lote.|55|Sim|  
|ObjectID|**Int**|N/A|22|Sim|  
|Deslocamento|**Int**|Deslocamento inicial da instrução do lote.<br /><br /> 0 para o início do lote.|61|Sim|  
|SPID|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|SqlHandle|**image**|Identificador SQL. Esse identificador pode ser usado para obter o texto SQL do lote usando a exibição de gerenciamento dinâmico sys.dm_exec_sql_text.|63|Sim|  
|StartTime|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|TextData|**ntext**|NULL|1|Sim|  
|PlanHandle|**image**|O identificador de plano do plano compilado para o lote. Esse identificador pode ser usado para obter o plano XML do lote usando a exibição de gerenciamento dinâmico dm_exec_query_plan.|65|Sim|  
|BigintData2|**bigint**|Memória total, em quilobytes, usada durante a compilação.|53|Sim|  
|CPU|**Int**|Tempo total de CPU, em milissegundos, gasto durante a compilação.|18|Sim|  
|Duration|**Int**|Tempo total, em milissegundos, gasto durante a compilação.|13|Sim|  
|IntegerData|**Int**|O tamanho, em quilobytes, do plano compilado.|25|Sim|  
  
### <a name="eventsubclass-3"></a>EventSubClass 3  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|O número cumulativo de vezes que esse plano foi recompilado.|52|Sim|  
|BinaryData|**image**|NULL|2|Sim|  
|DatabaseID|**int**|ID do banco de dados especificado pela instrução USE de *database* ou o banco de dados padrão se nenhuma instrução USE de *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados ServerName for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|EventSequence|**int**|Sequência de um determinado evento na solicitação.|51|Não|  
|SessionLoginName|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, SessionLoginName mostrará o Logon1 e LoginName mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|EventSubClass|**int**|Tipo de subclasse de evento.<br /><br /> 3 = Uma consulta armazenada em cache foi destruída e os dados históricos do desempenho associados ao plano serão destruídos.<br /><br /> Os seguintes tipos de EventSubClass são gerados no rastreamento.<br /><br /> Para lotes ad hoc com *n* número de consultas:<br /><br /> 1 de tipo 3 quando a consulta é liberada do cache<br /><br /> Para procedimentos armazenados com o número de consultas *n* número de consultas:<br /><br /> 1 de tipo 3 quando a consulta é liberada do cache.|21|Sim|  
|IntegerData2|**Int**|Fim da instrução no procedimento armazenado ou lote.<br /><br /> -1 para o final do procedimento armazenado ou lote.|55|Sim|  
|ObjectID|**Int**|NULL|22|Sim|  
|Deslocamento|**int**|O deslocamento inicial da instrução no lote ou procedimento armazenado.<br /><br /> 0 para o início do procedimento armazenado ou lote.|61|Sim|  
|SPID|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|SqlHandle|**image**|Identificador SQL que pode ser usado para obter o texto SQL do procedimento armazenado ou do lote usando a exibição de gerenciamento dinâmico dm_exec_sql_text.|63|Sim|  
|StartTime|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|TextData|**ntext**|QueryExecutionStats|1|Sim|  
|PlanHandle|**image**|O identificador de plano do plano compilado para o procedimento armazenado ou lote. Esse identificador pode ser usado para obter o plano XML usando a exibição de gerenciamento dinâmico dm_exec_query_plan.|65|Sim|  
|GroupID|**int**|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
  
### <a name="eventsubclass-4"></a>EventSubClass 4  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|NULL|52|Sim|  
|BinaryData|**image**|NULL|2|Sim|  
|DatabaseID|**Int**|ID do banco de dados em que o procedimento armazenado específico reside.|3|Sim|  
|EventSequence|**int**|Sequência de um determinado evento na solicitação.|51|Não|  
|SessionLoginName|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, SessionLoginName mostrará o Logon1 e LoginName mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|EventSubClass|**int**|Tipo de subclasse de evento.<br /><br /> 4 = Um procedimento armazenado em cache foi removido do cache e os dados de histórico de desempenho associados a ele estão prestes a serem destruídos.|21|Sim|  
|IntegerData2|**Int**|NULL|55|Sim|  
|ObjectID|**Int**|Identificação do procedimento armazenado. É igual à coluna object_id em sys.procedures.|22|Sim|  
|Deslocamento|**Int**|NULL|61|Sim|  
|SPID|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|SqlHandle|**image**|Identificador SQL que pode ser usado para obter o texto SQL do procedimento armazenado que foi executado usando a exibição de gerenciamento dinâmico dm_exec_sql_text.|63|Sim|  
|StartTime|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|TextData|**ntext**|ProcedureExecutionStats|1|Sim|  
|PlanHandle|**image**|O identificador do plano compilado para o procedimento armazenado. Esse identificador pode ser usado para obter o plano XML usando a exibição de gerenciamento dinâmico dm_exec_query_plan.|65|Sim|  
|GroupID|**int**|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
  
### <a name="eventsubclass-5"></a>EventSubClass 5  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BigintData1|**bigint**|NULL|52|Sim|  
|BinaryData|**image**|NULL|2|Sim|  
|DatabaseID|**Int**|Identificação do banco de dados no qual o gatilho específico reside.|3|Sim|  
|EventSequence|**int**|Sequência de um determinado evento na solicitação.|51|Não|  
|SessionLoginName|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, SessionLoginName mostrará o Logon1 e LoginName mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|EventSubClass|**int**|Tipo de subclasse de evento.<br /><br /> 5 = Um gatilho armazenado em cache foi removido do cache e os dados de histórico de desempenho associados a ele estão prestes a serem destruídos.|21|Sim|  
|IntegerData2|**Int**|NULL|55|Sim|  
|ObjectID|**Int**|Identificação do gatilho. É igual à coluna object_id nas exibições do catálogo sys.triggers/sys.server_triggers.|22|Sim|  
|Deslocamento|**Int**|NULL|61|Sim|  
|SPID|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|SqlHandle|**image**|Identificador SQL que pode ser usado para obter o texto SQL do gatilho usando a exibição de gerenciamento dinâmico dm_exec_sql_text.|63|Sim|  
|StartTime|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|TextData|**ntext**|TriggerExecutionStats|1|Sim|  
|PlanHandle|**image**|O identificador do plano compilado para o gatilho. Esse identificador pode ser usado para obter o plano XML usando a exibição de gerenciamento dinâmico dm_exec_query_plan.|65|Sim|  
|GroupID|**int**|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
  
## <a name="see-also"></a>Consulte também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Classe de evento Showplan XML for Query Compile](../../relational-databases/event-classes/showplan-xml-for-query-compile-event-class.md)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  
