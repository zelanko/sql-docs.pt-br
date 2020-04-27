---
title: Classe de evento OLEDB DataRead | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- OLEDB DataRead event class
ms.assetid: fb6869ba-3199-4e32-a650-60a5dda2571e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d12bf6f0e002b1f06bc96ff97608f88bd305b34b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62960770"
---
# <a name="oledb-dataread-event-class"></a>classe de evento OLEDB DataRead
  A classe de evento OLEDB DataRead ocorre quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chama um provedor OLE DB para consultas distribuídas e procedimentos armazenados remotos. Inclua essa classe de evento em rastreamentos que monitoram quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] faz uma chamada de solicitação de dados ao provedor OLE DB.  
  
 Quando a classe OLEDB DataRead é incluída em um rastreamento, a quantidade de sobrecarga gerada será alta. É recomendável limitar o uso dessa classe de evento a rastreamentos que monitorem problemas específicos em breves períodos de tempo.  
  
## <a name="oledb-dataread-event-class-data-columns"></a>Colunas de dados da classe de evento OLEDB DataRead  
  
|Nome da coluna de dados|Tipo de dados|DESCRIÇÃO|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|ClientProcessID|`int`|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|DatabaseID|`int`|A ID do banco de dados especificada pela instrução USE *database* ou a ID do banco de dados padrão se nenhuma instrução USE *database*tiver sido emitida para determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados ServerName for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DatabaseName|`nvarchar`|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|Duration|`bigint`|Período de tempo para concluir o evento Chamada OLE DB.|13|Não|  
|EndTime|`datetime`|Hora em que o evento terminou.|15|Sim|  
|Erro|`int`|Número de erro de um determinado evento. Geralmente é o número do erro armazenado na exibição de catálogo sys.messages.|31|Sim|  
|EventClass|`int`|Tipo de evento = 121.|27|Não|  
|EventSequence|`int`|Sequência de classe de evento OLE DB em lote.|51|Não|  
|EventSubClass|`int`|Tipo de subclasse de evento.<br /><br /> 0 = Iniciando<br /><br /> 1=Concluído|21|Não|  
|GroupID|`int`|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|HostName|`nvarchar`|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|IsSystem|`int`|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|LinkedServerName|`nvarchar`|Nome do servidor vinculado.|45|Sim|  
|LoginName|`nvarchar`|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no formato DOMÍNIO\Nomedeusuário).|11|Sim|  
|LoginSid|`image`|SID (identificador de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo sys.server_principals. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|MethodName|`nvarchar`|Nome do método de chamada.|47|Não|  
|NTDomainName|`nvarchar`|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|NTUserName|`nvarchar`|Nome do usuário do Windows.|6|Sim|  
|ProviderName|`nvarchar`|Nome do provedor OLE DB.|46|Sim|  
|RequestID|`int`|ID da solicitação que contém a instrução.|49|Sim|  
|SessionLoginName|`nvarchar`|Nome de logon do usuário que originou a sessão. Por exemplo, ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, SessionLoginName mostrará o Logon1 e LoginName mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|SPID|`Int`|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|StartTime|`datetime`|Hora de início do evento, se disponível.|14|Sim|  
|TextData|`nvarchar`|Parâmetros enviados e recebidos na chamada OLE DB.|1|Não|  
|TransactionID|`bigint`|ID da transação atribuída pelo sistema.|4|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [Eventos estendidos](../extended-events/extended-events.md)   
 [&#41;&#40;Transact-SQL de sp_trace_setevent](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Objetos de automação OLE em Transact-SQL](../stored-procedures/ole-automation-objects-in-transact-sql.md)  
  
  
