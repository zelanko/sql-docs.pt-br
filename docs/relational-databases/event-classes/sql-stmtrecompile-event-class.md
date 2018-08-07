---
title: Classe de evento SQL:StmtRecompile | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL:StmtRecompile event class
ms.assetid: 3a134751-3e93-4fe8-bf22-1e0561189293
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 531161ab7ce88510d87b1735b522b72a46138841
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39539086"
---
# <a name="sqlstmtrecompile-event-class"></a>classe de evento SQL:StmtRecompile
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A classe de evento SQL:StmtRecompile indica recompilações em nível de instrução causadas por todos os tipos de lotes: procedimentos armazenados, gatilhos lotes ad hoc e consultas. Consultas podem ser submetidas usando-se sp_executesql, SQL dinâmico, métodos Preparar, métodos Executar ou interfaces semelhantes. A classe de evento SQL:StmtRecompile deve ser usada, em vez da classe de evento SP:Recompile.  
  
## <a name="sqlstmtrecompile-event-class-data-columns"></a>Colunas de dados de classes de evento SQL:StmtRecompile  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|Nome do aplicativo cliente que criou a conexão para uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|ClientProcessID|**int**|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo.|9|Sim|  
|DatabaseID|**int**|ID do banco de dados em que o procedimento armazenado está sendo executado. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DatabaseName|**nvarchar**|Nome do banco de dados no qual o procedimento armazenado está sendo executado.|35|Sim|  
|EventSequence|**int**|A sequência de um evento na solicitação.|51|não|  
|EventSubClass|**int**|Descreve a causa da recompilação:<br /><br /> 1 = Esquema alterado<br /><br /> 2 = Estatísticas alteradas<br /><br /> 3 = Compilação adiada<br /><br /> 4 = Opção fixa alterada<br /><br /> 5 = Tabela temporária alterada<br /><br /> 6 = Conjunto de linhas remoto alterado<br /><br /> 7 = Permissões For Browse alteradas<br /><br /> 8 = Ambiente de notificação de consulta alterado<br /><br /> 9 = Exibição particionada alterada<br /><br /> 10 = Opções de cursor alteradas<br /><br /> 11 = Opção (recompilar) solicitada|21|Sim|  
|GroupID|**int**|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|HostName|**nvarchar**|Nome do computador no qual o cliente está sendo executado que enviou essa instrução. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|IntegerData2|**int**|Deslocamento final da instrução dentro do procedimento armazenado ou lote que levou à recompilação. O deslocamento final é -1 se a instrução for a última instrução em seu lote.|55|Sim|  
|IsSystem|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário.<br /><br /> 1 = sistema<br /><br /> 0 = usuário|60|Sim|  
|LineNumber|**int**|Número de sequência dessa instrução dentro do lote, se aplicável.|5|Sim|  
|LoginName|**nvarchar**|Nome do logon que enviou esse lote.|11|Sim|  
|LoginSid|**imagem**|SID (identificador de segurança) do usuário conectado no momento. Você pode encontrar essas informações na exibição de catálogo sys.server_principals. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|NestLevel|**int**|O nível aninhando da chamada de procedimento armazenado. Por exemplo, o procedimento armazenado my_proc_a chama my_proc_b. Nesse caso, my_proc_a tem um NESTLEVEL de 1, my_proc_b tem um NESTLEVEL de 2.|29|Sim|  
|NTDomainName|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|NTUserName|**nvarchar**|Nome de usuário do Windows do usuário conectado.|6|Sim|  
|ObjectID|**int**|Identificador atribuído pelo sistema do objeto que contém a instrução que levou à recompilação. Esse objeto pode ser um procedimento armazenado, gatilho ou função definida pelo usuário. Para lotes ad hoc ou SQL preparado, ObjectID e ObjectName retornam um valor NULL.|22|Sim|  
|ObjectName|**nvarchar**|Nome do objeto identificado por ObjectID.|34|Sim|  
|ObjectType|**int**|Valor que representa o tipo do objeto envolvido no evento. Para obter mais informações, consulte [ObjectType Trace Event Column](../../relational-databases/event-classes/objecttype-trace-event-column.md).|28|Sim|  
|Deslocamento|**int**|Deslocamento inicial da instrução dentro do procedimento armazenado ou lote que levou à recompilação.|61|Sim|  
|RequestID|**int**|ID da solicitação que contém a instrução.|49|Sim|  
|ServerName|**nvarchar**|Nome do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreado.|26|não|  
|SessionLoginName|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, SessionLoginName mostrará o Logon1 e LoginName mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|SPID|**int**|ID de processo do servidor da conexão.|12|Sim|  
|SqlHandle|**varbinary**|Hash de 64 bits com base no texto de uma consulta ad hoc ou na ID de objeto e banco de dados de um objeto SQL. Esse valor pode ser transmitido a sys.dm_exec_sql_text para recuperar o texto SQL associado.|63|não|  
|StartTime|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|TextData|**ntext**|Texto da instrução Transact-SQL recompilado.|1|Sim|  
|TransactionID|**bigint**|ID da transação atribuída pelo sistema.|4|Sim|  
|XactSequence|**bigint**|Token que descreve a transação atual.|50|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [Classe de evento SP:Recompile](../../relational-databases/event-classes/sp-recompile-event-class.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
