---
title: Classe de evento SP:Completed | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SP:Completed event class
ms.assetid: 7636a433-5d32-4562-8f5a-694f8e2beeca
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8ed4a766035c7fffe237cf4cee20e8fea64ed001
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="spcompleted-event-class"></a>Classe de evento SP:Completed
  A classe de evento SP:Completed indica que o procedimento armazenado completou a execução.  
  
## <a name="spcompleted-event-class-data-columns"></a>Colunas de dados da classe de evento SP:Completed  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|ClientProcessID|**int**|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|DatabaseID|**int**|ID do banco de dados em que o procedimento armazenado está sendo executado. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DatabaseName|**nvarchar**|Nome do banco de dados no qual o procedimento armazenado está sendo executado.|35|Sim|  
|Duration|**bigint**|Período de tempo (em microssegundos) utilizado pelo evento.|13|Sim|  
|EndTime|**datetime**|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting.|15|Sim|  
|EventClass|**int**|Tipo de evento = 43.|27|Não|  
|EventSequence|**int**|Sequência de um determinado evento na solicitação.|51|Não|  
|GroupID|**int**|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|HostName|**nvarchar**|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|IsSystem|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|LineNumber|**int**|Exibe o número da linha da instrução de execução que chamou esse procedimento armazenado.|5|Sim|  
|LoginName|**nvarchar**|Nome do logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no formato DOMÍNIO\nomedeusuário).|11|Sim|  
|LoginSid|**image**|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo sys.server_principals. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|NestLevel|**int**|O nível de aninhamento do procedimento armazenado.|29|Sim|  
|NTDomainName|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|NTUserName|**nvarchar**|Nome do usuário do Windows.|6|Sim|  
|ObjectID|**int**|ID do procedimento armazenado, atribuído pelo sistema.|22|Sim|  
|ObjectName|**nvarchar**|Nome do objeto que está sendo referenciado.|34|Sim|  
|ObjectType|**int**|Tipo de procedimento armazenado chamado. Esse valor corresponde à coluna do tipo na exibição do catálogo sys.objects. Para obter valores, consulte [Coluna de evento de rastreamento ObjectType](../../relational-databases/event-classes/objecttype-trace-event-column.md).|28|Sim|  
|RequestID|**int**|ID da solicitação que contém a instrução.|49|Sim|  
|RowCounts|**bigint**|Número de linhas para todas as instruções dentro deste procedimento armazenado.|48|Sim|  
|ServerName|**nvarchar**|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|SessionLoginName|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, SessionLoginName mostrará o Logon1 e LoginName mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|SourceDatabaseID|**int**|ID do banco de dados em que o objeto existe.|62|Sim|  
|SPID|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|StartTime|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|TextData|**ntext**|Texto da chamada de procedimento armazenado.|1|Sim|  
|TransactionID|**bigint**|ID da transação atribuída pelo sistema.|4|Sim|  
|XactSequence|**bigint**|Token que descreve a transação atual.|50|Sim|  
  
## <a name="see-also"></a>Consulte também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
