---
title: Classe de evento Missing Column Statistics | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Missing Column Statistics event class
ms.assetid: b9321143-3f29-4a19-8471-7085669282ef
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c9c4cdf1a3918bdf7e222d22b6e2cd9629caddc8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37298496"
---
# <a name="missing-column-statistics-event-class"></a>Classe de evento Missing Column Statistics
  A classe de evento Missing Column Statistics indica que as estatísticas de coluna que podiam ter sido úteis para o otimizador, não estão disponíveis.  
  
 Para determinar se há estatísticas ausentes para uma coluna usada pela consulta, monitore a classe de evento Missing Column Statistics. Isso pode fazer com que o otimizador escolha um plano de consulta menos eficiente do que seria esperado.  
  
## <a name="missing-column-statistics-event-class-data-columns"></a>Colunas de dados da classe de evento Missing Column Statistics  
  
|Nome da coluna de dados|Tipo de dados|Description|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|ClientProcessID|`int`|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|DatabaseID|`int`|ID do banco de dados especificado pela instrução USE de *database* ou o banco de dados padrão se nenhuma instrução USE de *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados ServerName for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DatabaseName|`nvarchar`|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|EventClass|`int`|Tipo de evento=79.|27|não|  
|EventSequence|`int`|Sequência de um determinado evento na solicitação.|51|não|  
|GroupID|`int`|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|HostName|`nvarchar`|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|IsSystem|`int`|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|LoginName|`nvarchar`|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no formato DOMÍNIO/nomedousuário).|11|Sim|  
|LoginSid|`image`|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo sys.server_principals. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|NTDomainName|`nvarchar`|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|NTUserName|`nvarchar`|Nome do usuário do Windows.|6|Sim|  
|RequestID|`int`|ID da solicitação que contém a instrução.|49|Sim|  
|ServerName|`nvarchar`|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|não|  
|SessionLoginName|`nvarchar`|Nome de logon do usuário que originou a sessão. Por exemplo, ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, SessionLoginName mostrará o Logon1 e LoginName mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|SPID|`int`|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|StartTime|`datetime`|Hora de início do evento, se disponível.|14|Sim|  
|TextData|`ntext`|Lista das colunas com estatísticas ausentes.|1|Sim|  
|TransactionID|`bigint`|ID da transação atribuída pelo sistema.|4|Sim|  
|XactSequence|`bigint`|Token que descreve a transação atual.|50|Sim|  
  
## <a name="see-also"></a>Consulte também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql)   
 [Monitorar e responder a eventos](../../ssms/agent/monitor-and-respond-to-events.md)  
  
  
