---
title: Classe de evento Database Mirroring State Change | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- event notifications [SQL Server], database mirroring
- database mirroring [SQL Server], event notifications
- Database Mirroring State Change event class
ms.assetid: f936a99e-2a81-4768-8177-5c969bbe2e04
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a15a70999431af9969589a8d4ca771f0d92463d9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48062246"
---
# <a name="database-mirroring-state-change-event-class"></a>classe de evento Database Mirroring State Change
  A classe de evento **Database Mirroring State Change** indica quando muda o estado de um banco de dados espelho. Inclua esta classe de evento em rastreamentos que monitorem as condições de bancos de dados espelhados.  
  
 Quando a classe de evento **Database Mirroring State Change** é incluída em um rastreamento, a sobrecarga relativa é baixa. A sobrecarga poderá ser maior se o estado dos bancos de dados espelhados aumentar.  
  
## <a name="data-database-mirroring-state-change-event-class-data-columns"></a>Colunas de dados da classe de evento Database Mirroring State Change  
  
|Nome da coluna de dados|Tipo de Dados|Description|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|ID do banco de dados especificado pela instrução USE de *database* ou o banco de dados padrão se nenhuma instrução USE de *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**DatabaseName**|**nvarchar**|Nome do banco de dados espelho.|35|Sim|  
|**EventClass**|**int**|Tipo de evento = 167.|27|não|  
|**EventSequence**|**int**|Sequência de classe de evento em lote.|51|não|  
|**IntegerData**|**int**|ID de estado anterior.|25|Sim|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|**LoginSid**|**image**|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo **sys.server_principals** . Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**RequestID**|**int**|ID da solicitação que contém a instrução.|49|Sim|  
|**ServerName**|**nvarchar**|Nome da instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|não|  
|**SessionLoginName**|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, o **SessionLoginName** mostrará o Logon1 e o **LoginName** mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|**SPID**|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|**StartTime**|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|**Estado**|**Int**|ID do novo estado de espelhamento:<br /><br /> 0 = Notificação nula<br /><br /> 1 = Principal sincronizado com testemunha<br /><br /> 2 = Principal sincronizado sem testemunha<br /><br /> 3 = Espelho sincronizado com testemunha<br /><br /> 4 = Espelho sincronizado sem testemunha<br /><br /> 5 = Conexão com principal perdida<br /><br /> 6 = Conexão com espelho perdida<br /><br /> 7 = Failover manual<br /><br /> 8 = Failover automático<br /><br /> 9 = Espelhamento suspenso<br /><br /> 10 = Sem quorum<br /><br /> 11 = Sincronizando espelho<br /><br /> 12 = Principal em execução exposto|30|Sim|  
|**TextData**|**ntext**|Descrição da alteração de estado.|1|Sim|  
|**TransactionID**|**bigint**|ID da transação atribuída pelo sistema.|4|Sim|  
  
## <a name="see-also"></a>Consulte também  
 [Eventos estendidos](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
