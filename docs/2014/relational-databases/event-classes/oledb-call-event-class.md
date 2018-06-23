---
title: Classe de evento OLEDB Call | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
topic_type:
- apiref
helpviewer_keywords:
- OLEDB Call event class
ms.assetid: e1be1e90-98cc-47a3-addd-59d4aeca6547
caps.latest.revision: 37
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 98ee5b7ecc2f2705278211df9432db1020b224bd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006847"
---
# <a name="oledb-call-event-class"></a>classe de evento OLEDB Call
  A classe de evento **OLEDB Call** ocorre quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chama um provedor OLE DB para consultas distribuídas e procedimentos armazenados remotamente.  
  
 Inclua a classe de evento **OLEDB Call** em rastreamentos para monitorar apenas as chamadas que não requerem dados ou chamadas que não são feitas pelo método **QueryInterface** . Quando a classe de evento **OLEDB Call** é incluída no rastreamento, a quantidade de sobrecarga gerada depende da frequência com que as chamadas do provedor OLE DB ocorrem em relação ao banco de dados durante o rastreamento. Se chamadas ocorrerem com frequência, o rastreamento poderá impedir significativamente o desempenho.  
  
## <a name="oledb-call-event-class-data-columns"></a>Coluna de dados da classe de evento OLEDB Call  
  
|Nome da coluna de dados|Tipo de dados|Description|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|ClientProcessID|`Int`|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|DatabaseID|`Int`|ID do banco de dados especificado pela instrução USE de *database* ou o banco de dados padrão se nenhuma instrução USE de *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DatabaseName|`nvarchar`|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|Duração|`Bigint`|Período de tempo para concluir o evento Chamada OLE DB.|13|não|  
|EndTime|`Datetime`|Hora em que o evento foi encerrado.|15|Sim|  
|Erro|`int`|Número de erro de um determinado evento. Geralmente é o número do erro armazenado na exibição de catálogo sys.messages.|31|Sim|  
|EventClass|`Int`|Tipo de evento = 119.|27|não|  
|EventSequence|`Int`|Sequência de classe de evento OLE DB em lote.|51|não|  
|EventSubClass|`Int`|0 = Iniciando<br /><br /> 1=Concluído|21|não|  
|GroupID|`int`|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|HostName|`nvarchar`|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|IsSystem|`int`|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|LinkedServerName|`nvarchar`|Nome do servidor vinculado.|45|Sim|  
|LoginName|`nvarchar`|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no formato DOMÍNIO\Nomedeusuário).|11|Sim|  
|LoginSid|`Image`|SID (identificador de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo sys.server_principals. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|MethodName|`nvarchar`|Nome do método OLE DB.|47|Sim|  
|NTDomainName|`nvarchar`|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|NTUserName|`nvarchar`|Nome do usuário do Windows.|6|Sim|  
|ProviderName|`nvarchar`|Nome do provedor OLE DB.|46|Sim|  
|RequestID|`Int`|ID da solicitação que contém a instrução.|49|Sim|  
|SessionLoginName|`nvarchar`|Nome de logon do usuário que originou a sessão. Por exemplo, se você se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando Login1 e executar uma instrução como Login2, `SessionLoginName` mostrará Login1 e `LoginName` mostrará Login2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|SPID|`Int`|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|StartTime|`datetime`|Hora de início do evento, se disponível.|14|Sim|  
|TextData|`nvarchar`|Parâmetros enviados e recebidos na chamada OLE DB.|1|não|  
|TransactionID|`bigint`|ID da transação atribuída pelo sistema.|4|Sim|  
  
## <a name="see-also"></a>Consulte também  
 [Eventos estendidos](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Objetos Automation no Transact-SQL](../stored-procedures/ole-automation-objects-in-transact-sql.md)  
  
  
