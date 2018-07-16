---
title: Classe de evento Audit Server Principal Management | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
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
- Audit Server Principal Management event class
ms.assetid: 7894850c-91fe-47c0-a03c-baacbc10d29c
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b10ddece7d37ce0ff447b31a6ca5a1f3b76b7a35
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37176103"
---
# <a name="audit-server-principal-management-event-class"></a>Classe de evento Audit Server Principal Management
  A classe de evento **Audit Server Principal Management** ocorre quando entidades do servidor são criadas, alteradas ou descartadas.  
  
## <a name="audit-server-principal-management-event-class-data-columns"></a>Colunas de dados da classe de evento Audit Server Principal Management  
  
|Nome da coluna de dados|Tipo de dados|Description|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|Nome do aplicativo cliente que criou a conexão para uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|**DatabaseID**|**int**|ID do banco de dados especificado pela instrução USE de *database* ou o banco de dados padrão se nenhuma instrução USE de *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**DatabaseName**|**nvarchar**|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|**DBUserName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do cliente.|40|Sim|  
|**EventSequence**|**int**|Sequência de um determinado evento na solicitação.|51|não|  
|**EventSubClass**|**int**|Tipo de subclasse de evento.<br /><br /> 1=Create<br /><br /> 2=Alter<br /><br /> 3=Drop<br /><br /> 4=Dump<br /><br /> 5=Disable<br /><br /> 6=Enable<br /><br /> 11=Load|21|Sim|  
|**HostName**|**nvarchar**|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|**LoginSid**|**image**|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo **sys.server_principals** . Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**NTDomainName**|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**NTUserName**|**nvarchar**|Nome do usuário do Windows.|6|Sim|  
|**ObjectName**|**nvarchar**|Nome do objeto que está sendo referenciado.|34|Sim|  
|**ObjectType**|**int**|Valor que representa o tipo do objeto envolvido no evento. Esse valor corresponde à coluna do tipo na exibição de catálogo **sys.objects** . Para obter valores, consulte [Coluna de evento de rastreamento ObjectType](objecttype-trace-event-column.md).|28|Sim|  
|**OwnerName**|**nvarchar**|Nome de usuário de banco de dados do proprietário do objeto.|37|Sim|  
|**RequestID**|**int**|ID da solicitação que contém a instrução.|49|Sim|  
|**ServerName**|**nvarchar**|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|não|  
|**SessionLoginName**|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, o **SessionLoginName** mostrará o Logon1 e o **LoginName** mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|**SPID**|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|**StartTime**|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|**Êxito**|**int**|1 = êxito. 0 = falha. Por exemplo, o valor 1 indica êxito em uma verificação de permissões e o valor 0 indica falha nessa verificação.|23|Sim|  
|**XactSequence**|**bigint**|Token usado para descrever a transação atual.|50|Sim|  
  
## <a name="see-also"></a>Consulte também  
 [Eventos estendidos](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
