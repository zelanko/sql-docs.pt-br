---
title: Classe de evento Broker:Corrupted Message | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Corrupted Message event class
ms.assetid: 084bf198-2138-438e-bdc7-4ff1e04300f7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 710112cfd4ab902c4c92a87602f6e362f3078d93
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85030529"
---
# <a name="brokercorrupted-message-event-class"></a>classe de evento Broker:Corrupted Message
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria um evento **Broker:Corrupted Message** quando o Service Broker recebe uma mensagem corrompida.  
  
## <a name="brokercorrupted-message-event-class-data-columns"></a>Colunas de dados da classe de evento Broker:Corrupted Message  
  
|Coluna de dados|Type|DESCRIÇÃO|Número da coluna|Filtrável|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|O nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|**BigintData1**|**bigint**|O número de sequência da mensagem.|52|Não|  
|**BinaryData**|**imagem**|O corpo da mensagem.|2|Sim|  
|**ClientProcessID**|**int**|A ID atribuída pelo computador host ao processo em que está sendo executado o aplicativo cliente. Essa coluna de dados será populada se a ID do processo do cliente for fornecida pelo cliente.|9|Sim|  
|**DatabaseID**|**int**|A ID do banco de dados especificada pela instrução USE *database* ou a ID do banco de dados padrão se nenhuma instrução USE *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**Erro**|**int**|O número da ID de mensagem em **sys.messages** para o texto no evento.|31|Não|  
|**EventClass**|**int**|O tipo de classe de evento capturado. Sempre **161** para **Broker:Corrupted Message**.|27|Não|  
|**EventSequence**|**int**|Número de sequência para esse evento.|51|Não|  
|**FileName**|**nvarchar**|O endereço de rede do ponto de extremidade remoto.|36|Não|  
|**GUID**|**uniqueidentifier**|A ID da conversa a que pertence a mensagem corrompida. Esse identificador é transmitido como parte da mensagem e é compartilhado por ambos os lados da conversa.|54|Não|  
|**Nome do Host**|**nvarchar**|O nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|**IntegerData**|**int**|O número de fragmento da mensagem.|25|Sim|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Não|  
|**LoginSid**|**imagem**|Número SID (identificação de segurança) do usuário que fez logon. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**NTDomainName**|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**NTUserName**|**nvarchar**|O nome do usuário proprietário da conexão que gerou este evento.|6|Sim|  
|**ObjectName**|**nvarchar**|O nome do serviço do outro lado da conversa e a cadeia de caracteres de conexão que o banco de dados remoto usou para se conectar a esse banco de dados.|34|Não|  
|**RoleName**|**nvarchar**|A função do ponto de extremidade que recebe essa mensagem. Um dos seguintes valores:<br /><br /> **iniciador**:<br />                  O ponto de extremidade receptor é o iniciador da conversa.<br /><br /> **destino**:<br />                  O ponto de extremidade receptor é o destino da conversa.|38|Não|  
|**ServerName**|**nvarchar**|O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|**Severidade**|**int**|A severidade do erro que fez com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] descartasse a mensagem.|29|Não|  
|**SPID**|**int**|A ID de processo do servidor atribuída pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao processo associado ao cliente.|12|Sim|  
|**StartTime**|**datetime**|O horário no qual o evento foi iniciado, quando disponível.|14|Sim|  
|**State**|**int**|Indica o local, dentro do código-fonte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que produziu o evento. Cada local que pode produzir esse evento tem um código de estado diferente. Um engenheiro de suporte da Microsoft pode usar esse código de estado para descobrir onde o evento foi produzido.|30|Não|  
|**TextData**|**ntext**|Descrição do dano detectado.|1|Sim|  
|**ID da transação**|**bigint**|ID da transação atribuída pelo sistema.|4|Não|  
  
 A coluna **TextData** desse evento contém uma mensagem que descreve o problema com a mensagem.  
  
  
