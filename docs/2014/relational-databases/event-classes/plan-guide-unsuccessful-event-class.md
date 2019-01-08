---
title: Classe de evento Plan Guide Unsuccessful | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Plan Guide Unsuccessful event class
ms.assetid: ef9759f8-5613-4884-9257-86b609313f69
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f6ce753ceaa0cc0ee16b395918390a4402cf5f39
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52788752"
---
# <a name="plan-guide-unsuccessful-event-class"></a>classe de evento Plan Guide Unsuccessful
  A classe de evento Plan Guide Unsuccessful indica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pôde produzir um plano de execução para uma consulta ou lote que continha uma guia de plano. Em vez disso, o plano foi compilado sem usar a guia de plano. O evento dispara quando as seguintes condições forem verdadeiras:  
  
-   O lote/módulo na definição da guia de plano corresponde ao lote que está sendo executado.  
  
-   A consulta na definição da guia de plano corresponde à consulta que está sendo executada.  
  
-   As dicas na definição da guia de plano, inclusive a dica USE PLAN, não foram aplicadas com êxito à consulta. Ou seja, o plano de consulta compilado não pôde honrar as dicas especificadas e o plano foi compilado sem usar a guia de plano.  
  
 Uma guia de plano inválida poderia fazer esse evento disparar. Valide o guia de plano usado pela consulta ou lote com a função [sys.fn_validate_plan_guide](/sql/relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql) e corrija o erro relatado por essa função.  
  
 Esse evento é incluído no modelo de ajuste do [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] .  
  
## <a name="plan-guide-unsuccessful-event-class-data-columns"></a>Colunas de dados da classe de evento Plan Guide Unsuccessful  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|ClientProcessID|`int`|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|DatabaseID|`int`|ID do banco de dados especificado pela instrução USE *database* ou o banco de dados padrão se nenhuma instrução USE *database* tiver sido emitida para uma instância especificada. [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados ServerName for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DatabaseName|`nvarchar`|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|EventClass|`int`|Tipo de evento = 218.|27|Não|  
|EventSequence|`int`|A sequência de um evento específico dentro da solicitação.|51|Não|  
|HostName|`nvarchar`|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|IsSystem|`int`|Indica se o evento ocorreu em um processo do sistema ou do usuário: 1 = sistema, 0 = usuário.|60|Sim|  
|LoginName|`nvarchar`|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no formato DOMAIN\\*username*).|11|Sim|  
|LoginSid|`image`|Número SID (identificação de segurança) do usuário que fez logon. É possível localizar essas informações em [sys.server_principals](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql) ou nas exibições de catálogo [sys.sql_logins](/sql/relational-databases/system-catalog-views/sys-sql-logins-transact-sql) . Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|NTDomainName|`nvarchar`|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|NTUserName|`nvarchar`|Nome do usuário do Windows.|6|Sim|  
|ObjectID|`int`|ID do objeto do módulo que estava sendo compilado quando a guia de plano foi aplicada. Se a guia de plano não foi aplicada a um módulo, essa coluna será definida como NULL.|22|Sim|  
|RequestID|`int`|A ID da solicitação que contém a instrução.|49|Sim|  
|ServerName|`nvarchar`|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|SessionLoginName|`nvarchar`|Nome de logon do usuário que originou a sessão. Por exemplo, ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, SessionLoginName mostrará o Logon1 e LoginName mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|SPID|`int`|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|StartTime|`datetime`|Hora de início do evento, se disponível.|14|Sim|  
|TextData|`ntext`|Nome do guia de plano.|1|Sim|  
|TransactionID|`bigint`|ID da transação atribuída pelo sistema.|4|Sim|  
|XactSequence|`bigint`|Token que descreve a transação atual.|50|Sim|  
  
## <a name="see-also"></a>Consulte também  
 [Classe de evento Plan Guide Successful](plan-guide-successful-event-class.md)   
 [Eventos estendidos](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [sys.fn_validate_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
