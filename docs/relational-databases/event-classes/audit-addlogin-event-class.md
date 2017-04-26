---
title: Classe de evento Audit Addlogin | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Audit Addlogin event class
ms.assetid: 6e0633dc-889e-49ef-bace-3c50958db2dd
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: defdcbd68e38e097908dbded5dd28448f09f17fd
ms.lasthandoff: 04/11/2017

---
# <a name="audit-addlogin-event-class"></a>Classe de evento Audit Addlogin
  A classe de evento **Audit Addlogin** ocorre quando um logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é adicionado ou removido.  
  
 Se você definir propriedades adicionais quando o logon for adicionado, como um banco de dados padrão, as informações sobre essas propriedades serão encontradas na coluna **TextData** desse evento. Se você definir essas propriedades enquanto adiciona um logon, o evento **Audit Login Change Property** não ocorrerá.  
  
 Este evento de auditoria refere-se aos procedimentos armazenados **sp_addlogin** e **sp_droplogin** .  
  
 Essa classe de evento poderá ser removida em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. É recomendável que, em vez disso, você use a classe de evento **Audit Sever Principal** .  
  
## <a name="audit-addlogin-event-class-data-columns"></a>Colunas de dados da classe de evento Audit Addlogin  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|**ClientProcessID**|**int**|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|**DatabaseID**|**int**|ID do banco de dados especificado pela instrução USE de *database* ou o banco de dados padrão se nenhuma instrução USE de *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**DatabaseName**|**nvarchar**|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|**EventClass**|**int**|Tipo de evento = 104.|27|Não|  
|**EventSequence**|**int**|Sequência de um determinado evento na solicitação.|51|Não|  
|**EventSubClass**|**int**|Tipo de subclasse de evento.<br /><br /> 1=Add<br /><br /> 2=Drop|21|Sim|  
|**HostName**|**nvarchar**|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|**LoginName**|**nvarchar**|Nome do logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no formato DOMÍNIO\nomedeusuário).|11|Sim|  
|**LoginSid**|**image**|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo **sys.server_principals** . Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**NTDomainName**|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**NTUserName**|**nvarchar**|Nome do usuário do Windows.|6|Sim|  
|**RequestID**|**int**|ID da solicitação que contém a instrução.|49|Sim|  
|**ServerName**|**nvarchar**|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|**SessionLoginName**|**Nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, o **SessionLoginName** mostrará o Logon1 e o **LoginName** mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|**SPID**|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|**StartTime**|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|**Êxito**|**Int**|1 = êxito. 0 = falha. Por exemplo, o valor 1 indica êxito em uma verificação de permissões e o valor 0 indica falha nessa verificação.|23|Sim|  
|**TargetLoginName**|**nvarchar**|O nome do logon que será adicionado ou descartado.|42|Sim|  
|**TargetLoginSid**|**image**|O número de identificação de segurança (SID) do logon de destino (se transmitido como um parâmetro).|43|Sim|  
|**TransactionID**|**bigint**|ID da transação atribuída pelo sistema.|4|Sim|  
|**XactSequence**|**bigint**|Token usado para descrever a transação atual.|50|Sim|  
  
## <a name="see-also"></a>Consulte também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Classe de evento Audit Login Change Property](../../relational-databases/event-classes/audit-login-change-property-event-class.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_droplogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [Classe de evento Audit Server Principal Management](../../relational-databases/event-classes/audit-server-principal-management-event-class.md)  
  
  
