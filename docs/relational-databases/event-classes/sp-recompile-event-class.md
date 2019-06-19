---
title: Classe de evento SP:Recompile | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- SP:Recompile event class
ms.assetid: 526c8eae-a07b-4d0e-b91e-8e537835d77d
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b6d6a152ad6251b35fa5b6dac9b2654e08f1ed30
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62446772"
---
# <a name="sprecompile-event-class"></a>classe de evento SP:Recompile
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A classe de evento SP:Recompile indica que um procedimento armazenado, gatilho ou função definida pelo usuário foi recompilado. Recompilações relatadas por essa classe de evento ocorrem ao nível de instrução.  
  
 O modo preferencial para rastrear recompilações em nível de instrução é usar a classe de evento SQL:StmtRecompile. A classe de evento SP:Recompile foi preterida. Para obter mais informações, consulte [SQL:StmtRecompile Event Class](../../relational-databases/event-classes/sql-stmtrecompile-event-class.md).  
  
## <a name="sprecompile-event-class-data-columns"></a>Colunas de dados da classe de evento SP:Recompile  
  
|Nome da coluna de dados|**Data type**|Descrição|ID da coluna|Filtrável|  
|----------------------|-------------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|Nome do aplicativo cliente que criou a conexão para uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|ClientProcessID|**int**|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo.|9|Sim|  
|DatabaseID|**int**|ID do banco de dados em que o procedimento armazenado está sendo executado. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DatabaseName|**nvarchar**|Nome do banco de dados no qual o procedimento armazenado está sendo executado.|35|Sim|  
|EventClass|**int**|Tipo de evento = 37.|27|Não|  
|EventSequence|**int**|A sequência de determinado evento dentro da solicitação.|51|Não|  
|EventSubClass|**int**|Tipo de subclasse de evento. Indica a razão para recompilação.<br /><br /> 1 = Esquema alterado<br /><br /> 2 = Estatísticas alteradas<br /><br /> 3 = Recompile DNR<br /><br /> 4 = Opção de conjunto alterada<br /><br /> 5 = Tabela temporária alterada<br /><br /> 6 = Conjunto de linhas remoto alterado<br /><br /> 7 = Para procurar permanente alterado<br /><br /> 8 = Ambiente de notificação de consulta alterado<br /><br /> 9 = Exibição MPI alterada<br /><br /> 10 = Opções de cursor alteradas<br /><br /> 11 = Opção With Recompile|21|Sim|  
|GroupID|**int**|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|HostName|**nvarchar**|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|IntegerData2|**int**|Deslocamento final da instrução dentro do procedimento armazenado ou lote que levou à recompilação. O deslocamento final é -1 se a instrução for a última instrução em seu lote.|55|Sim|  
|IsSystem|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|LoginName|**nvarchar**|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no formato DOMÍNIO/nomedousuário).|11|Sim|  
|LoginSid|**imagem**|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo sys.server_principals. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|NestLevel|**int**|O nível de aninhamento do procedimento armazenado.|29|Sim|  
|NTDomainName|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|NTUserName|**nvarchar**|Nome do usuário do Windows.|6|Sim|  
|ObjectID|**int**|ID do procedimento armazenado, atribuído pelo sistema.|22|Sim|  
|ObjectName|**nvarchar**|Nome do objeto que acionou a recompilação.|34|Sim|  
|ObjectType|**int**|Valor que representa o tipo do objeto envolvido no evento. Para obter mais informações, consulte [ObjectType Trace Event Column](../../relational-databases/event-classes/objecttype-trace-event-column.md).|28|Sim|  
|Deslocamento|**int**|Deslocamento inicial da instrução dentro do procedimento armazenado ou lote que levou à recompilação.|61|Sim|  
|RequestID|**int**|ID da solicitação que contém a instrução.|49|Sim|  
|ServerName|**nvarchar**|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|SessionLoginName|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, SessionLoginName mostrará o Logon1 e LoginName mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|SPID|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|SqlHandle|**varbinary**|Hash de 64 bits com base no texto de uma consulta ad hoc ou na ID de objeto e banco de dados de um objeto SQL. Esse valor pode ser transmitido a sys.dm_exec_sql_text para recuperar o texto SQL associado.|63|Sim|  
|StartTime|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|TextData|**ntext**|Texto da instrução Transact-SQL que levou a uma recompilação em nível de instrução.|1|Sim|  
|TransactionID|**bigint**|ID da transação atribuída pelo sistema.|4|Sim|  
|XactSequence|**bigint**|Token usado para descrever a transação atual.|50|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [SQL:StmtRecompile Event Class](../../relational-databases/event-classes/sql-stmtrecompile-event-class.md)  
  
  
