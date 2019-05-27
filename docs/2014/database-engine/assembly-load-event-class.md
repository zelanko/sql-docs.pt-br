---
title: Classe de evento assembly Load | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Assembly Load event class
ms.assetid: cfb0b69d-4ce0-4067-a3df-d82775e57886
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 17a2c847e906616c4555d37e641f76eeb73391ab
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66065255"
---
# <a name="assembly-load-event-class"></a>Classe de evento Assembly Load
  A classe de evento **Assembly Load** ocorre quando uma solicitação para carregar um assembly é executada.  
  
 Inclua a classe de evento **Assembly Load** em rastreamentos onde você quiser monitorar cargas de assembly. Isso pode ser útil ao solucionar problemas de uma consulta que usa CLR (Common Language Runtime), ao solucionar problemas de um servidor que está executando consultas CLR lentamente ou ao monitorar um servidor de forma a coletar informações de usuários, bancos de dados ou de êxito, entre outras, sobre cargas de assembly.  
  
## <a name="assembly-load-event-class-data-columns"></a>Colunas de dados da classe de evento Assembly Load  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|O nome do aplicativo que pediu a carga.|10|Sim|  
|**ClientProcessID**|**int**|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|**DatabaseID**|**int**|ID do banco de dados especificado pela instrução de banco de dados USE ou o banco de dados padrão se nenhuma instrução de banco de dados USE tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**DatabaseName**|**nvarchar**|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|**EventSequence**|**int**|Sequência de um determinado evento na solicitação.|51|Não |  
|**GroupID**|**int**|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|**HostName**|**nvarchar**|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|**LoginName**|**nvarchar**|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows no formato DOMÍNIO/nomedousuário).|11|Sim|  
|**LoginSID**|**image**|SID (identificador de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo **sys.server_principals** . Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**NTDomainName**|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**NTUserName**|**nvarchar**|Nome do usuário do Windows.|6|Sim|  
|**ObjectID**|**int**|ID do assembly.|22|Sim|  
|**ObjectName**|**nvarchar**|Nome completamente qualificado do assembly.|34|Sim|  
|**RequestID**|**int**|ID da solicitação que contém a instrução.|49|Sim|  
|**ServerName**|**nvarchar**|Nome da instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|**SessionLoginName**|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, para se conectar ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, o **SessionLoginName** mostrará o Logon1 e o **LoginName** mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|**SPID**|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|**StartTime**|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|**Êxito**|**int**|Indica se a carga de assembly foi bem-sucedida (1) ou falhou (0).|23|Sim|  
|**TextData**|**ntext**|"Carga de assembly concluída com êxito" se a carga for bem-sucedida; caso contrário, "Falha no carregamento do assembly".|1|Sim|  
  
## <a name="see-also"></a>Consulte também  
 [Eventos estendidos](../relational-databases/extended-events/extended-events.md)   
 [Assemblies &#40;Mecanismo de Banco de Dados&#41;](../relational-databases/clr-integration/assemblies-database-engine.md)  
  
  
