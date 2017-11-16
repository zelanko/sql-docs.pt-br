---
title: Classe de evento Broker:Message Undeliverable | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Broker:Message Undeliverable event class
ms.assetid: f532b7c9-ca34-4bac-8dc3-53f9895fd6af
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1ff63d8d6824a29bb26dd960b74a6b810a227f50
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="brokermessage-undeliverable-event-class"></a>Classe de evento Broker:Message Undeliverable
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera um evento **Broker:Message Undeliverable** quando o Service Broker não pode reter uma mensagem recebida que deveria ter sido entregue a um serviço nessa instância. Para mensagens que deveriam ter sido encaminhadas, veja [Classe de evento Broker:Forwarded Message Dropped](../../relational-databases/event-classes/broker-forwarded-message-dropped-event-class.md).  
  
## <a name="brokermessage-undeliverable-event-class-data-columns"></a>Colunas de dados da classe de evento Broker:Message Undeliverable  
  
|Coluna de dados|Tipo|Descrição|Número da coluna|Filtrável|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**Nome do Aplicativo**|**nvarchar**|O nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|**BigintData1**|**bigint**|O número de sequência da mensagem sem possibilidade de entrega.|52|Não|  
|**BigintData2**|**bigint**|O número de sequência da última mensagem reconhecida com êxito.|53|Não|  
|**ClientProcessID**|**int**|A ID atribuída pelo computador host ao processo em que está sendo executado o aplicativo cliente. Essa coluna de dados será populada se a ID do processo do cliente for fornecida pelo cliente.|9|Sim|  
|**DatabaseID**|**int**|A ID do banco de dados especificada pela instrução USE *database* ou a ID do banco de dados padrão se nenhuma instrução USE *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**Erro**|**int**|O número da ID de mensagem em **sys.messages** para o texto no evento.|31|Não|  
|**EventClass**|**int**|O tipo de classe de evento capturado. Sempre **160** para **Broker:MessageUndeliverable**.|27|Não|  
|**EventSequence**|**int**|Número de sequência para esse evento.|51|Não|  
|**EventSubClass**|**nvarchar**|Indica se a mensagem sem possibilidade de entrega era uma mensagem sequenciada. Um de dois valores:<br /><br /> **Mensagem Sequenciada**. A mensagem sem possibilidade de entrega era uma mensagem sequenciada.<br /><br /> **Mensagem Não Sequenciada**. A mensagem sem possibilidade de entrega não era uma mensagem sequenciada.|21|Sim|  
|**GUID**|**uniqueidentifier**|A ID da conversa a que pertence a mensagem sem possibilidade de entrega. Esse identificador é transmitido como parte da mensagem e é compartilhado por ambos os lados da conversa.|54|Não|  
|**HostName**|**nvarchar**|O nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|**IntegerData**|**int**|O número de fragmento da mensagem sem possibilidade de entrega.|25|Não|  
|**IntegerData2**|**int**|O número de fragmento de mensagem que a mensagem sem possibilidade de entrega estava reconhecendo.|55|Não|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Não|  
|**LoginName**|**nvarchar**|O nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do Windows na forma DOMÍNIO/Nomedeusuário).|11|Não|  
|**LoginSid**|**image**|Número SID (identificação de segurança) do usuário que fez logon. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**NTDomainName**|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**NTUserName**|**nvarchar**|O nome do usuário proprietário da conexão que gerou este evento.|6|Sim|  
|**ObjectName**|**nvarchar**|O identificador de conversa do diálogo.|34|Não|  
|**RoleName**|**nvarchar**|A função do identificador de conversa. É **initiator** (iniciador) ou **target**(destino).|38|Não|  
|**ServerName**|**nvarchar**|O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|**Severity**|**int**|Número de severidade do texto no evento.|29|Não|  
|**SPID**|**int**|A ID de processo do servidor atribuída pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao processo associado ao cliente.|12|Sim|  
|**StartTime**|**datetime**|O horário no qual o evento foi iniciado, quando disponível.|14|Sim|  
|**Estado**|**int**|Indica o local, dentro do código-fonte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que produziu o evento. Cada local que pode produzir esse evento tem um código de estado diferente. Um engenheiro de suporte Microsoft pode usar esse código de estado para descobrir onde o evento foi produzido.|30|Não|  
|**TextData**|**ntext**|O motivo pelo qual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não conseguiu entregar a mensagem.|1|Sim|  
|**TransactionID**|**bigint**|ID da transação atribuída pelo sistema.|4|Não|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
