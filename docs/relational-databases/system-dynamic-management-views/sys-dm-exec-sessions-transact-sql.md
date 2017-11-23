---
title: exec_sessions (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/21/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_exec_sessions_TSQL
- sys.dm_exec_sessions
- dm_exec_sessions
- sys.dm_exec_sessions_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_sessions dynamic management view
ms.assetid: 2b7e8e0c-eea0-431e-819f-8ccd12ec8cfa
caps.latest.revision: "60"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 4119f0283be2bf4a0b145e59ec930eea4496d666
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecsessions-transact-sql"></a>sys.dm_exec_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma linha por sessão autenticada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. sys.dm_exec_sessions é uma exibição de escopo de servidor que mostra informações sobre todas as conexões de usuário ativas e tarefas internas. Essas informações contêm a versão de cliente, o nome do programa cliente, a hora do logon do cliente, o usuário do logon, a configuração da sessão atual, etc. Use sys.dm_exec_sessions para exibir primeiro a carga do sistema atual e identificar uma sessão de interesse e, depois, para obter mais informações sobre essa sessão usando outras exibições ou funções de gerenciamento dinâmicas.  
  
 As exibições de gerenciamento dinâmico sys.DM exec_connections, sys.DM exec_sessions e sys.DM exec_requests mapeiam para o [sys. sysprocesses](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md) tabela do sistema.  
  
> **Observação:** chamá-la de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_exec_sessions**.  
  
|Nome da coluna|Tipo de dados|Descrição e informações específicas da versão|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|Identifica a sessão associada a cada conexão primária ativa. Não permite valor nulo.|  
|login_time|**datetime**|Hora em que sessão foi estabelecida. Não permite valor nulo.|  
|host_name|**nvarchar (128)**|Nome da estação de trabalho cliente específica de uma sessão. O valor é NULL para sessões internas. Permite valor nulo.<br /><br /> **Observação de segurança:** o aplicativo cliente fornece o nome da estação de trabalho e pode fornecer dados imprecisos. Não confie em HOST_NAME como um recurso de segurança.|  
|program_name|**nvarchar (128)**|Nome do programa cliente que iniciou a sessão. O valor é NULL para sessões internas. Permite valor nulo.|  
|host_process_id|**int**|ID do processo do programa cliente que iniciou a sessão. O valor é NULL para sessões internas. Permite valor nulo.|  
|client_version|**int**|Versão de protocolo TDS da interface usada pelo cliente para conexão com o servidor. O valor é NULL para sessões internas. Permite valor nulo.|  
|client_interface_name|**nvarchar (32)**|Nome da biblioteca/driver está sendo usado pelo cliente para se comunicar com o servidor. O valor é NULL para sessões internas. Permite valor nulo.|  
|security_id|**varbinary(85)**|Identificador de segurança do Microsoft Windows associado ao logon. Não permite valor nulo.|  
|login_name|**nvarchar (128)**|Nome do logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no qual a sessão está sendo executada atualmente. Para o nome de logon original que criou a sessão, consulte original_login_name. Pode ser um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticado nome de logon ou um nome de usuário de domínio autenticado do Windows. Não permite valor nulo.|  
|nt_domain|**nvarchar (128)**|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Domínio de Windows do cliente se a sessão estiver usando Autenticação do Windows ou uma conexão confiável. Esse valor é NULL para sessões internas e usuários que não têm domínio. Permite valor nulo.|  
|nt_user_name|**nvarchar (128)**|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Nome do usuário do Windows do cliente se a sessão estiver usando Autenticação do Windows ou uma conexão confiável. Esse valor é NULL para sessões internas e usuários que não têm domínio. Permite valor nulo.|  
|status|**nvarchar (30)**|Status da sessão. Valores possíveis:<br /><br /> **Executando** -executando uma ou mais solicitações no momento<br /><br /> **Em suspensão** -não há solicitações em execução no momento<br /><br /> **Inativo** – sessão foi reiniciada devido a pooling de conexão e está agora no estado de pré-logon.<br /><br /> **Pré-conexão** -sessão está no classificador do administrador de recursos.<br /><br /> Não permite valor nulo.|  
|context_info|**varbinary(128)**|Valor CONTEXT_INFO da sessão. As informações de contexto são definidas pelo usuário usando o [SET CONTEXT_INFO](../../t-sql/statements/set-context-info-transact-sql.md) instrução. Permite valor nulo.|  
|cpu_time|**int**|Tempo da CPU, em milissegundos, usado por essa sessão. Não permite valor nulo.|  
|memory_usage|**int**|Número de páginas de 8 KB de memória usado por essa sessão. Não permite valor nulo.|  
|total_scheduled_time|**int**|Tempo total, em milissegundos, para o qual a sessão (solicitações internas) era programada para execução. Não permite valor nulo.|  
|total_elapsed_time|**int**|Tempo, em milissegundos, desde que a sessão foi estabelecida. Não permite valor nulo.|  
|endpoint_id|**int**|ID do ponto de extremidade associado à sessão. Não permite valor nulo.|  
|last_request_start_time|**datetime**|Hora de início da última solicitação na sessão. Inclui a solicitação em execução no momento. Não permite valor nulo.|  
|last_request_end_time|**datetime**|Hora da última conclusão de uma solicitação na sessão. Permite valor nulo.|  
|reads|**bigint**|Número de leituras executadas por solicitações durante esta sessão. Não permite valor nulo.|  
|writes|**bigint**|Número de gravações executadas por solicitações durante esta sessão. Não permite valor nulo.|  
|logical_reads|**bigint**|Número de leituras lógicas executadas na sessão. Não permite valor nulo.|  
|is_user_process|**bit**|0 se a sessão for uma sessão do sistema. Caso contrário, será 1. Não permite valor nulo.|  
|text_size|**int**|Configuração de TEXTSIZE da sessão. Não permite valor nulo.|  
|language|**nvarchar (128)**|Configuração de LANGUAGE da sessão. Permite valor nulo.|  
|date_format|**nvarchar(3)**|Configuração de DATEFORMAT da sessão. Permite valor nulo.|  
|date_first|**smallint**|Configuração de DATEFIRST da sessão. Não permite valor nulo.|  
|quoted_identifier|**bit**|Configuração de QUOTED_IDENTIFIER da sessão. Não permite valor nulo.|  
|arithabort|**bit**|Configuração de ARITHABORT da sessão. Não permite valor nulo.|  
|ansi_null_dflt_on|**bit**|Configuração de ANSI_NULL_DFLT_ON da sessão. Não permite valor nulo.|  
|ansi_defaults|**bit**|Configuração de ANSI_DEFAULTS da sessão. Não permite valor nulo.|  
|ansi_warnings|**bit**|Configuração de ANSI_WARNINGS da sessão. Não permite valor nulo.|  
|ansi_padding|**bit**|Configuração de ANSI_PADDING da sessão. Não permite valor nulo.|  
|ansi_nulls|**bit**|Configuração de ANSI_NULLS da sessão. Não permite valor nulo.|  
|concat_null_yields_null|**bit**|Configuração de CONCAT_NULL_YIELDS_NULL da sessão. Não permite valor nulo.|  
|transaction_isolation_level|**smallint**|Nível de isolamento da transação da sessão.<br /><br /> 0 = Não Especificado<br /><br /> 1 = Leitura Não Confirmada<br /><br /> 2 = Leitura Confirmada<br /><br /> 3 = Repetível<br /><br /> 4 = Serializável<br /><br /> 5 = Instantâneo<br /><br /> Não permite valor nulo.|  
|lock_timeout|**int**|Configuração de LOCK_TIMEOUT da sessão. O valor está em milissegundos. Não permite valor nulo.|  
|deadlock_priority|**int**|Configuração de DEADLOCK_PRIORITY da sessão. Não permite valor nulo.|  
|row_count|**bigint**|Número de linhas retornadas na sessão até este ponto. Não permite valor nulo.|  
|prev_error|**int**|ID do último erro retornado na sessão. Não permite valor nulo.|  
|original_security_id|**varbinary(85)**|Identificador de segurança do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows associada a original_login_name. Não permite valor nulo.|  
|original_login_name|**nvarchar (128)**|Nome do logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que o cliente usou para criar esta sessão. Pode ser um nome de logon autenticado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um nome de usuário de domínio autenticado pelo Windows ou um usuário do banco de dados independente. Observe que a sessão pode ter passado por muitas alternâncias de contexto implícitas ou explícitas após a conexão inicial. Por exemplo, se [EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md) é usado. Não permite valor nulo.|  
|last_successful_logon|**datetime**|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Hora do último logon efetuado com êxito para original_login_name antes de a sessão atual ter sido iniciada.|  
|last_unsuccessful_logon|**datetime**|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Hora da última tentativa de logon para original_login_name antes de a sessão atual ter sido iniciada.|  
|unsuccessful_logons|**bigint**|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número de tentativas de logon malsucedidas para original_login_name entre last_successful_logon e login_time.|  
|group_id|**int**|ID do grupo de carga de trabalho a que pertence esta sessão. Não permite valor nulo.|  
|database_id|**smallint**|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> ID do banco de dados atual para cada sessão.|  
|authenticating_database_id|**int**|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> ID do banco de dados que está autenticando a entidade. Para Logons, o valor será 0. Para usuários de bancos de dados independentes, o valor será a ID do banco de dados independente.|  
|open_transaction_count|**int**|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número de transações abertas por sessão.|  
|pdw_node_id|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões  
Todos podem ver suas próprias informações de sessão.  
**[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]:** Requer `VIEW SERVER STATE` permissão em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] para ver todas as sessões no servidor.  
**[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]:** Requer `VIEW DATABASE STATE` para ver todas as conexões com o banco de dados atual. `VIEW DATABASE STATE`não podem ser concedidos a `master` banco de dados. 
  
  
## <a name="remarks"></a>Comentários  
 Quando o **conformidade de critérios comuns habilitada** opção de configuração de servidor estiver habilitada, as estatísticas de logon são exibidas nas seguintes colunas.  
  
-   last_successful_logon  
  
-   last_unsuccessful_logon  
  
-   unsuccessful_logons  
  
 Se essa opção não for habilitada, essas colunas retornarão valores nulos. Para obter mais informações sobre como configurar este servidor a opção de configuração, consulte [conformidade de critérios comuns habilitado a opção de configuração de servidor](../../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md).  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Em/Aplicar|Relação|  
|----------|--------|---------------|------------------|  
|sys.dm_exec_sessions|[sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|session_id|Um para zero ou um para muitos|  
|sys.dm_exec_sessions|[sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)|session_id|Um para zero ou um para muitos|  
|sys.dm_exec_sessions|[sys.dm_tran_session_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-session-transactions-transact-sql.md)|session_id|Um para zero ou um para muitos|  
|sys.dm_exec_sessions|[sys.DM exec_cursors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)(session_id &#124; 0)|session_id CROSS APPLY<br /><br /> OUTER APPLY|Um para zero ou um para muitos|  
|sys.dm_exec_sessions|[sys.dm_db_session_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)|session_id|Um para um|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-finding-users-that-are-connected-to-the-server"></a>A. Localizando usuários conectados ao servidor  
 O exemplo a seguir localiza os usuários conectados ao servidor e retorna o número de sessões de cada usuário.  
  
```tsql  
SELECT login_name ,COUNT(session_id) AS session_count   
FROM sys.dm_exec_sessions   
GROUP BY login_name;  
```  
  
### <a name="b-finding-long-running-cursors"></a>B. Localizando cursores demorados  
 O exemplo a seguir localiza os cursores abertos para mais um intervalo de tempo especificado, que criou os cursores e em qual sessão os cursores estão.  
  
```tsql  
USE master;  
GO  
SELECT creation_time ,cursor_id   
    ,name ,c.session_id ,login_name   
FROM sys.dm_exec_cursors(0) AS c   
JOIN sys.dm_exec_sessions AS s   
   ON c.session_id = s.session_id   
WHERE DATEDIFF(mi, c.creation_time, GETDATE()) > 5;  
```  
  
### <a name="c-finding-idle-sessions-that-have-open-transactions"></a>C. Localizando sessões inativas que têm transações abertas  
 O exemplo a seguir localiza sessões que têm transações abertas e estão ociosas. Uma sessão ociosa é a que não tem nenhuma solicitação em execução no momento.  
  
```tsql  
SELECT s.*   
FROM sys.dm_exec_sessions AS s  
WHERE EXISTS   
    (  
    SELECT *   
    FROM sys.dm_tran_session_transactions AS t  
    WHERE t.session_id = s.session_id  
    )  
    AND NOT EXISTS   
    (  
    SELECT *   
    FROM sys.dm_exec_requests AS r  
    WHERE r.session_id = s.session_id  
    );  
```  
  
### <a name="d-finding-information-about-a-queries-own-connection"></a>D. Localizando informações sobre a própria conexão de consultas  
 Consulta típica para reunir informações sobre a própria conexão de consultas.  
  
```tsql  
SELECT   
    c.session_id, c.net_transport, c.encrypt_option,   
    c.auth_scheme, s.host_name, s.program_name,   
    s.client_interface_name, s.login_name, s.nt_domain,   
    s.nt_user_name, s.original_login_name, c.connect_time,   
    s.login_time   
FROM sys.dm_exec_connections AS c  
JOIN sys.dm_exec_sessions AS s  
    ON c.session_id = s.session_id  
WHERE c.session_id = @@SPID;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico &#40; relacionadas à execução Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  



