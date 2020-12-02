---
description: Classe de evento Audit Server Starts and Stops
title: Classe de evento Audit Server Starts and Stops | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Audit Server Starts and Stops event class
ms.assetid: 8ddb55af-c77b-4d07-b803-a97320c0804e
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: db0ef3200e1c7517d2c96d48f4dbb4f619225655
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126738"
---
# <a name="audit-server-starts-and-stops-event-class"></a>Classe de evento Audit Server Starts and Stops
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  A classe de evento **Audit Server Starts and Stops** ocorre quando o estado do serviço [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é modificado.  
  
## <a name="audit-server-starts-and-stops-event-class-data-columns"></a>Colunas de dados da classe de evento Audit Server Starts and Stops  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|**ClientProcessID**|**int**|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|**EventClass**|**int**|Tipo de evento = 18.|27|Não|  
|**EventSequence**|**int**|Sequência de um determinado evento na solicitação.|51|Não|  
|**EventSubClass**|**int**|Tipo de subclasse de evento.<br /><br /> 1=Shutdown<br /><br /> 2=Started<br /><br /> 3=Paused<br /><br /> 4=Continue|21|Sim|  
|**HostName**|**nvarchar**|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|**LoginName**|**nvarchar**|Nome do logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no formato DOMÍNIO\nomedeusuário).|11|Sim|  
|**LoginSid**|**imagem**|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo **sys.server_principals** . Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**NTDomainName**|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**NTUserName**|**nvarchar**|Nome do usuário do Windows.|6|Sim|  
|**RequestID**|**int**|ID da solicitação que contém a instrução.|49|Sim|  
|**ServerName**|**nvarchar**|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|**SessionLoginName**|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, o **SessionLoginName** mostrará o Logon1 e o **LoginName** mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|**SPID**|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|**StartTime**|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|**Êxito**|**int**|1 = êxito. 0 = falha. Por exemplo, o valor 1 indica êxito em uma verificação de permissões e o valor 0 indica falha nessa verificação.|23|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Gerenciar os serviços do Mecanismo de Banco de Dados](../../database-engine/configure-windows/manage-the-database-engine-services.md)  
  
  
