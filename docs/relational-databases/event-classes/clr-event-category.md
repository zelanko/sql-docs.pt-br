---
title: Categoria de eventos de CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- event classes [SQL Server], CLR event category
- SQL Server event classes, CLR event category
- CLR event category [SQL Server]
ms.assetid: a7c0cd60-3bec-42be-ad5e-473bd26a06d9
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e589b57de25a5240b32e254d9c8280810dc0b557
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67999630"
---
# <a name="clr-event-category"></a>Categoria de evento CLR
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A categoria de evento **CLR** inclui classes de evento que são geradas pela execução de objetos CLR (Common Language Runtime) [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] dentro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 
 ## <a name="assembly-load-event-class"></a>Classe de evento Assembly Load 
  A classe de evento **Assembly Load** ocorre quando uma solicitação para carregar um assembly é executada.  
  
 Inclua a classe de evento **Assembly Load** em rastreamentos onde você quiser monitorar cargas de assembly. Isso pode ser útil ao solucionar problemas de uma consulta que usa CLR (Common Language Runtime), ao solucionar problemas de um servidor que está executando consultas CLR lentamente ou ao monitorar um servidor de forma a coletar informações de usuários, bancos de dados ou de êxito, entre outras, sobre cargas de assembly.  
  
## <a name="assembly-load-event-class-data-columns"></a>Colunas de dados da classe de evento Assembly Load  
  
|Nome da coluna de dados|Tipo de dados|DESCRIÇÃO|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|O nome do aplicativo que pediu a carga.|10|Sim|  
|**ClientProcessID**|**int**|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|**DatabaseID**|**int**|ID do banco de dados especificado pela instrução de banco de dados USE ou o banco de dados padrão se nenhuma instrução de banco de dados USE tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**DatabaseName**|**nvarchar**|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|**EventSequence**|**int**|Sequência de um determinado evento na solicitação.|51|Não|  
|**GroupID**|**int**|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|**HostName**|**nvarchar**|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|**LoginName**|**nvarchar**|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no formato DOMÍNIO/nomedousuário).|11|Sim|  
|**LoginSID**|**imagem**|SID (identificador de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo **sys.server_principals** . Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**NTDomainName**|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**NTUserName**|**nvarchar**|Nome do usuário do Windows.|6|Sim|  
|**ObjectID**|**int**|ID do assembly.|22|Sim|  
|**ObjectName**|**nvarchar**|Nome completamente qualificado do assembly.|34|Sim|  
|**RequestID**|**int**|ID da solicitação que contém a instrução.|49|Sim|  
|**ServerName**|**nvarchar**|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|**SessionLoginName**|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, o **SessionLoginName** mostrará o Logon1 e o **LoginName** mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|**SPID**|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|**StartTime**|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|**Êxito**|**int**|Indica se a carga de assembly foi bem-sucedida (1) ou falhou (0).|23|Sim|  
|**TextData**|**ntext**|"Carga de assembly concluída com êxito" se a carga for bem-sucedida; caso contrário, "Falha no carregamento do assembly".|1|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)   
 [Assemblies &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)  
  
   
  
## <a name="see-also"></a>Consulte Também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
