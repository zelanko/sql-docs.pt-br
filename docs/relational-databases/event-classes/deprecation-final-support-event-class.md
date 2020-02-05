---
title: Classe de evento Deprecation Final Support | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Deprecation Final Support event class
- deprecation [SQL Server], events final support
ms.assetid: 2b4d88d0-62be-45c0-bea8-c5900d553d31
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7c1f01d9a51a46090237a609cab538ea1ea92841
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68089618"
---
# <a name="deprecation-final-support-event-class"></a>Classe de evento Deprecation Final Support
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A classe de evento **Deprecation Final Support** ocorre quando é usado um recurso que será removido da próxima versão principal do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para que seus aplicativos tenham tempo de vida mais longo, não use recursos que provoquem a classe de evento **Deprecation Final Support** ou **Deprecation Announcement** . Modifique os aplicativos que usam recursos de substituição final o mais rápido possível.  
  
## <a name="deprecation-final-support-event-class-data-columns"></a>Colunas de dados da classe de evento Deprecation Final Support  
  
|Nome da coluna de dados|Tipo de dados|DESCRIÇÃO|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|ClientProcessID|**int**|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|DatabaseID|**int**|ID do banco de dados especificado pela instrução USE de *database* ou o banco de dados padrão se nenhuma instrução USE de *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DatabaseName|**nvarchar**|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|EventClass|**int**|Tipo de evento = 126.|27|Não|  
|EventSequence|**int**|Sequência de um determinado evento na solicitação.|51|Não|  
|HostName|**nvarchar**|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|IntegerData2|**int**|Deslocamento final (em bytes) da instrução que está sendo executada.|55|Sim|  
|IsSystem|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|LoginName|**nvarchar**|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no formato DOMÍNIO/nomedousuário).|11|Sim|  
|LoginSid|**imagem**|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo **sys.server_principals** . Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|NTDomainName|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|NTUserName|**nvarchar**|Nome do usuário do Windows.|6|Sim|  
|Deslocamento|**int**|O deslocamento inicial da instrução no lote ou procedimento armazenado.|61|Sim|  
|ObjectID|**int**|Número de identificação do recurso substituído.|22|Sim|  
|ObjectName|**nvarchar**|Nome do recurso preterido.|34|Sim|  
|RequestID|**int**|ID da solicitação que contém a instrução.|49|Sim|  
|ServerName|**nvarchar**|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|SessionLoginName|**nvarchar**|O nome de logon do usuário que originou a sessão. Por exemplo, para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, o **SessionLoginName** mostrará o Logon1 e o **LoginName** mostrará o Logon2. Esta coluna exibirá logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|SPID|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|SqlHandle|**imagem**|Identificador binário que pode ser usado para identificar lotes SQL ou procedimentos armazenados.|63|Sim|  
|StartTime|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|TextData|**ntext**|Valor do texto dependente da classe de evento capturada no rastreamento.|1|Sim|  
|TransactionID|**bigint**|ID da transação atribuída pelo sistema.|4|Sim|  
|XactSequence|**bigint**|Token que descreve a transação atual.|50|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Classe de evento Deprecation Announcement](../../relational-databases/event-classes/deprecation-announcement-event-class.md)   
 [Recursos do Mecanismo de Banco de Dados preteridos no SQL Server 2016](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)  
  
  
