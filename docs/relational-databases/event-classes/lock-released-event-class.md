---
title: "Classe de evento Lock:Released | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "classe de evento Released"
ms.assetid: a150c300-72fa-4231-8f41-f1abd550a429
caps.latest.revision: 35
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 35
---
# Classe de evento Lock:Released
  A classe de evento Lock:Released indica que um bloqueio em um recurso, como uma página, foi liberado.  
  
 As classes de evento Lock:Acquired e Lock: Released podem ser usadas para monitorar quando os objetos estão sendo bloqueados, o tipo de bloqueio obtido, e por quanto tempo os bloqueios foram retidos. Os bloqueios retidos por longos períodos de tempo podem causar problemas de contenção e devem ser investigados. Por exemplo, um aplicativo pode estar adquirindo bloqueios em linhas em uma tabela, e em seguida esperando por uma entrada do usuário. Como a entrada do usuário pode levar muito tempo, os bloqueios podem bloquear outros usuários. Nesta instância, o aplicativo deveria ser reprojetado para fazer solicitações de bloqueios somente quando necessário e não exigir uma entrada do usuário quando forem adquiridos os bloqueios.  
  
## Bloqueio:Colunas de dados de classe de evento Released  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|BinaryData|**image**|Identificador de recurso bloqueado.|2|Sim|  
|ClientProcessID|**int**|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|DatabaseID|**int**|ID do banco de dados no qual o bloqueio foi liberado. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados ServerName for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|EventClass|**int**|Tipo de evento = 23.|27|Não|  
|EventSequence|**int**|Sequência de um determinado evento na solicitação.|51|Não|  
|GroupID|**int**|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|HostName|**nvarchar**|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|IntegerData2|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|55|Sim|  
|IsSystem|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|LoginName|**nvarchar**|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do Windows na forma de DOMAIN\nome_do_usuário).|11|Sim|  
|LoginSid|**image**|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo sys.server_principals. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|Modo|**int**|Modo resultante depois da liberação do bloqueio.<br /><br /> 0=NULL - Compatível com todos os outros modos de bloqueio (LCK_M_NL)<br /><br /> 1=Bloqueio de estabilidade do esquema (LCK_M_SCH_S)<br /><br /> 2=Bloqueio de modificação de esquema (LCK_M_SCH_M)<br /><br /> 3=Bloqueio compartilhado (LCK_M_S)<br /><br /> 4=Bloqueio de atualização (LCK_M_U)<br /><br /> 5=Bloqueio exclusivo (LCK_M_X)<br /><br /> 6=Bloqueio de tentativa compartilhada (LCK_M_IS)<br /><br /> 7=Bloqueio de atualização da tentativa (LCK_M_IU)<br /><br /> 8=Bloqueio exclusivo da tentativa (LCK_M_IX)<br /><br /> 9=Compartilhado com tentativa de atualizar (LCK_M_SIU)<br /><br /> 10=Compartilhado com tentativa exclusiva (LCK_M_SIX)<br /><br /> 11=Atualizar com tentativa exclusiva (LCK_M_UIX)<br /><br /> 12=Bloqueio de atualização em massa (LCK_M_BU)<br /><br /> 13=Intervalo de chaves compartilhado/compartilhado (LCK_M_RS_S)<br /><br /> 14=Intervalo de chaves compartilhado/atualizar (LCK_M_RS_U)<br /><br /> 15=Inserção de Intervalo de Chaves NULL (LCK_M_RI_NL)<br /><br /> 16=Inserção de Intervalo de Chaves Compartilhado (LCK_M_RI_S)<br /><br /> 17=Atualização de Inserção de Intervalo de Chaves (LCK_M_RI_S)<br /><br /> 18=Inserção de intervalo de chaves exclusivo (LCK_M_RI_X)<br /><br /> 19=Intervalo de chaves compartilhado exclusivo (LCK_M_RX_S)<br /><br /> 20=Atualização de intervalo de chaves exclusivo (LCK_M_RX_U)<br /><br /> 21=Intervalo de chaves exclusivo exclusivo (LCK_M_RX_X)|32|Sim|  
|NTDomainName|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|NTUserName|**nvarchar**|Nome do usuário do Windows.|6|Sim|  
|ObjectID|**int**|A ID atribuída pelo sistema do objeto que foi liberado, se disponível e aplicável.|22|Sim|  
|ObjectID2|**bigint**|Identificação do objeto ou entidade relacionada, se disponível e aplicável.|56|Sim|  
|OwnerID|**int**|1=TRANSACTION<br /><br /> 2=CURSOR<br /><br /> 3=SESSION<br /><br /> 4=SHARED_TRANSACTION_WORKSPACE<br /><br /> 5=EXCLUSIVE_TRANSACTION_WORKSPACE|58|Sim|  
|RequestID|**int**|ID da solicitação que contém a instrução.|49|Sim|  
|ServerName|**nvarchar**|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|SessionLoginName|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, SessionLoginName mostrará o Logon1 e LoginName mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|SPID|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|StartTime|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|TextData|**ntext**|Valor do texto dependente da classe de evento capturada no rastreamento.|1|Sim|  
|TransactionID|**bigint**|ID da transação atribuída pelo sistema.|4|Sim|  
|Tipo|**int**|1=NULL_RESOURCE<br /><br /> 2=DATABASE<br /><br /> 3=FILE<br /><br /> 5=OBJECT<br /><br /> 6=PAGE<br /><br /> 7=KEY<br /><br /> 8=EXTENT<br /><br /> 9=RID<br /><br /> 10=APPLICATION<br /><br /> 11=METADATA<br /><br /> 12=AUTONAMEDB<br /><br /> 13=HOBT<br /><br /> 14=ALLOCATION_UNIT|57|Sim|  
  
## Consulte também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Classe de evento Lock:Acquired](../../relational-databases/event-classes/lock-acquired-event-class.md)   
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)  
  
  