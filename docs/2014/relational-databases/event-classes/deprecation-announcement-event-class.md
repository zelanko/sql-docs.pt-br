---
title: Classe de evento Deprecation Announcement | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- deprecation [SQL Server], events announced stage
- Deprecation Announcement event class
ms.assetid: 46fc578f-3c97-477f-879c-8a1b2cfd9d58
author: stevestein
ms.author: sstein
ms.openlocfilehash: c622d4d0c39d685b7808c6c4cf1bebbe7f455b12
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85053046"
---
# <a name="deprecation-announcement-event-class"></a>classe de evento Deprecation Announcement
  A classe de evento **Deprecation Announcement** ocorre quando você usa um recurso que será removido de uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas não será removido da próxima versão principal. Para que seus aplicativos tenham tempo de vida mais longo, evite usar recursos que provocam a classe de evento **Deprecation Announcement** ou a **Deprecation Final Support** .  
  
## <a name="deprecation-announcement-event-class-data-columns"></a>Colunas de dados da classe de evento Deprecation Announcement  
  
|Nome da coluna de dados|Tipo de dados|DESCRIÇÃO|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|ClientProcessID|`int`|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|DatabaseID|`int`|ID do banco de dados especificado pela instrução USE de *database* ou o banco de dados padrão se nenhuma instrução USE de *database* tiver sido emitida para uma determinada instância. O [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados `ServerName` for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DatabaseName|`nvarchar`|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|EventClass|`int`|Tipo de evento = 125.|27|Não|  
|EventSequence|`int`|Sequência de um determinado evento na solicitação.|51|Não|  
|HostName|`nvarchar`|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|IntegerData2|`int`|Deslocamento final (em bytes) da instrução que está sendo executada.|55|Sim|  
|IsSystem|`int`|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|LoginName|`nvarchar`|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no formato DOMÍNIO/nomedousuário).|11|Sim|  
|LoginSid|`image`|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo sys.server_principals. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|NTDomainName|`nvarchar`|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|NTUserName|`nvarchar`|Nome do usuário do Windows.|6|Sim|  
|ObjectID|`int`|Número de identificação do recurso substituído.|22|Sim|  
|ObjectName|`nvarchar`|Nome do recurso preterido.|34|Sim|  
|Deslocamento|`int`|O deslocamento inicial da instrução no lote ou procedimento armazenado.|61|Sim|  
|RequestID|`int`|ID da solicitação que contém a instrução.|49|Sim|  
|ServerName|`nvarchar`|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|SessionLoginName|`nvarchar`|Nome de logon do usuário que originou a sessão. Por exemplo, se você se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando Login1 e executar uma instrução como Login2, `SessionLoginName` mostrará Login1 e `LoginName` mostrará Login2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|SPID|`int`|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|SqlHandle|`image`|Identificador binário que pode ser usado para identificar lotes SQL ou procedimentos armazenados.|63|Sim|  
|StartTime|`datetime`|Hora de início do evento, se disponível.|14|Sim|  
|TextData|`ntext`|Valor do texto dependente da classe de evento capturada no rastreamento.|1|Sim|  
|TransactionID|`bigint`|ID da transação atribuída pelo sistema.|4|Sim|  
|XactSequence|`bigint`|Token que descreve a transação atual.|50|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_trace_setevent](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Classe de evento reprovation final support](deprecation-final-support-event-class.md)   
 [Recursos do Mecanismo de Banco de Dados preteridos no SQL Server 2014](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)  
  
  
