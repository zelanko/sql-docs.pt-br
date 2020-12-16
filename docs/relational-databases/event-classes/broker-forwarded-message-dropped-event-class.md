---
description: classe de evento Broker:Forwarded Message Dropped
title: Classe de evento Broker:Forwarded Message Dropped | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Broker:Forwarded Message Dropped event class
ms.assetid: ec242d0b-77b0-45f5-8b12-186a14b173a8
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ccb035e127b6476ca18b5745dbaf58b66c8c929e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97476247"
---
# <a name="brokerforwarded-message-dropped-event-class"></a>classe de evento Broker:Forwarded Message Dropped

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera um evento Broker:Forwarded Message Dropped quando o Service Broker remove uma mensagem que deveria ser encaminhada.  
  
## <a name="brokerforwarded-message-dropped-event-class-data-columns"></a>Colunas de dados da classe de evento Broker:Forwarded Message Dropped  
  
|Coluna de dados|Type|Descrição|Número da coluna|Filtrável|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|**nvarchar**|O nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|BigintData1|**bigint**|Número de sequência da mensagem.|52|Não|  
|ClientProcessID|**int**|A ID atribuída pelo computador host ao processo em que está sendo executado o aplicativo cliente. Essa coluna de dados será populada se a ID do processo do cliente for fornecida pelo cliente.|9|Sim|  
|DatabaseID|**int**|A ID do banco de dados especificada pela instrução de *banco de dados* USE ou a ID do banco de dados padrão se nenhuma instrução de *banco de dados* USE tiver sido emitida para determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados Server Name for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DatabaseName|**nvarchar**|O nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|DBUserName|**nvarchar**|O identificador da instância do agente de onde se origina a mensagem.|40|Não|  
|Erro|**int**|O número da ID de mensagem em sys.messages para o texto no evento.|31|Não|  
|EventClass|**int**|O tipo de classe de evento capturado. Sempre 191 para Broker:Forwarded Message Dropped.|27|Não|  
|EventSequence|**int**|Número de sequência para esse evento.|51|Não|  
|FileName|**nvarchar**|O nome do serviço a que se destina a mensagem.|36|Não|  
|GUID|**uniqueidentifier**|A ID de conversa da caixa de diálogo. Esse identificador é transmitido como parte da mensagem e é compartilhado por ambos os lados da conversa.|54|Não|  
|HostName|**nvarchar**|O nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|IndexID|**int**|O número de saltos restantes para a mensagem encaminhada.|24|Não|  
|IntegerData|**int**|O número de fragmentos da mensagem encaminhada.|25|Não|  
|LoginSid|**imagem**|Número SID (identificação de segurança) do usuário que fez logon. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|NTDomainName|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|NTUserName|**nvarchar**|O nome do usuário proprietário da conexão que gerou este evento.|6|Sim|  
|ObjectId|**int**|O valor de vida útil da mensagem encaminhada.|22|Não|  
|ObjectName|**nvarchar**|O ID da mensagem encaminhada.|34|Não|  
|OwnerName|**nvarchar**|O identificador da instância do agente de destino da mensagem.|37|Não|  
|RoleName|**nvarchar**|A função do identificador de conversa. Um destes:<br /><br /> - Iniciador. Este Broker iniciou a conversa.<br /><br /> - Destino. Este Broker é o destino da conversa.|38|Não|  
|ServerName|**nvarchar**|O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|Severidade|**int**|Número de severidade do texto no evento.|29|Não|  
|SPID|**int**|A ID de processo do servidor atribuída pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao processo associado ao cliente.|12|Sim|  
|StartTime|**datetime**|O horário no qual o evento foi iniciado, quando disponível.|14|Sim|  
|Estado|**int**|Indica o local, dentro do código-fonte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que produziu o evento. Cada local que pode produzir esse evento tem um código de estado diferente. Um engenheiro de suporte da Microsoft pode usar esse código de estado para descobrir onde o evento foi produzido.|30|Não|  
|Êxito|**int**|O tempo em que a mensagem esteve ativa. Quando este valor é maior ou igual à vida útil, a mensagem é removida.|23|Não|  
|TargetLoginName|**nvarchar**|O endereço de rede para o qual a mensagem deveria ser encaminhada.|42|Não|  
|TargetUserName|**nvarchar**|O nome do serviço que iniciou a mensagem.|39|Não|  
|TextData|**ntext**|Descrição do motivo pelo qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] removeu a mensagem.|1|Sim|  
|ID da Transação|**bigint**|ID da transação atribuída pelo sistema.|4|Não|  
  
 A coluna TextData desse evento contém uma descrição do motivo que levou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a remover a mensagem.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
