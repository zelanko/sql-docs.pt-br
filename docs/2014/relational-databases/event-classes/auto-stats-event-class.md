---
title: Classe de evento Auto Stats | Microsoft Docs
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
- Auto Stats event class
ms.assetid: cd613fce-01e1-4d8f-86cc-7ffbf0759f9e
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 796f417d3dae943334b6cdadc62c633dcbe18baf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37213016"
---
# <a name="auto-stats-event-class"></a>Classe de evento Auto Stats
  A classe de evento **Auto Stats** indica que ocorreu uma atualização automática de estatísticas de índice e coluna.  
  
## <a name="auto-stats-event-class-data-columns"></a>Colunas de dados da classe de evento Auto Stats  
  
|Nome da coluna de dados|Tipo de dados|Description|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|**ClientProcessID**|**int**|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|**DatabaseID**|**int**|O identificador do banco de dados especificado pela instrução USE *database* ou o banco de dados padrão se nenhuma instrução USE *database* tiver sido emitida para determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**DatabaseName**|**nvarchar**|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|**Duration**|**bigint**|Período de tempo (em microssegundos) utilizado pelo evento.|13|Sim|  
|**EndTime**|**datetime**|Horário em que o evento foi encerrado.|15|Sim|  
|**Erro**|**int**|Número de erro de um determinado evento. Geralmente é o número do erro armazenado na exibição de catálogo **sys.messages** .|31|Sim|  
|**EventClass**|**int**|Tipo de evento = 58.|27|não|  
|**EventSequence**|**int**|Sequência de um determinado evento na solicitação.|51|não|  
|**EventSubClass**|**int**|Tipo de subclasse de eventos:<br /><br /> 1: estatísticas criadas/atualizadas de forma síncrona; **TextData** coluna indica as estatísticas e se elas foram criadas ou atualizadas.<br /><br /> 2: atualização de estatísticas assíncronas; trabalho enfileirado.<br /><br /> 3: atualização de estatísticas assíncronas; trabalho iniciando.<br /><br /> 4: atualização de estatísticas assíncronas; trabalho concluído.|21|Sim|  
|**GroupID**|**int**|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|**HostName**|**nvarchar**|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|**IndexID**|**int**|ID da entrada de índice/estatísticas do objeto afetado pelo evento. Para determinar a ID de índice de um objeto, utilize a coluna **index_id** da exibição do catálogo **sys.indexes** .|24|Sim|  
|**IntegerData**|**int**|Número de coleções de estatísticas que foram atualizadas com êxito.|25|Sim|  
|**IntegerData2**|**int**|Número de sequência do trabalho.|55|Sim|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|**LoginName**|**nvarchar**|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do Windows na forma de DOMAIN\nome_do_usuário).|11|Sim|  
|**LoginSid**|**image**|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo **sys.server_principals** . Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**NTDomainName**|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**NTUserName**|**nvarchar**|Nome do usuário do Windows.|6|Sim|  
|**ObjectID**|**int**|ID de objeto atribuída pelo sistema.|22|Sim|  
|**RequestID**|**int**|O ID da solicitação que contém a instrução.|49|Sim|  
|**ServerName**|**nvarchar**|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|não|  
|**SessionLoginName**|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, o **SessionLoginName** mostrará o Logon1 e o **LoginName** mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|**SPID**|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|**StartTime**|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|**Êxito**|**int**|0 = erro.<br /><br /> 1 = êxito.<br /><br /> 2 = ignorado devido a estrangulamento do servidor (MSDE).|23|Sim|  
|**TextData**|**ntext**|O conteúdo dessa coluna depende se as estatísticas são atualizadas de forma síncrona (**EventSubClass** 1) ou assíncrona (**EventSubClass** 2, 3 ou 4):<br /><br /> 1: lista as estatísticas que foram atualizadas/criadas<br /><br /> 2, 3 ou 4: NULL; a coluna **IndexID** é populada com a ID de índice/estatísticas das estatísticas atualizadas.|1|Sim|  
|**TransactionID**|**bigint**|ID da transação atribuída pelo sistema.|4|Sim|  
|**Tipo**|**int**|Tipo de trabalho.|57|Sim|  
  
## <a name="see-also"></a>Consulte também  
 [Eventos estendidos](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
