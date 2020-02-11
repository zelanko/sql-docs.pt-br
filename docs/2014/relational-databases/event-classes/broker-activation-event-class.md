---
title: Classe de evento Broker:Activation | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Activation event class
ms.assetid: 481d5b13-657e-4b51-8783-ccac3595bd45
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f2562f3931f98c040bb3dc475e3863bb6396dbbf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62664342"
---
# <a name="brokeractivation-event-class"></a>classe de evento Broker:Activation
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera um evento **Broker:Activation** quando um monitor de fila inicia um procedimento armazenado de ativação, envia uma notificação QUEUE_ACTIVATION ou quando um procedimento armazenado de ativação iniciado por um monitor de fila é encerrado.  
  
## <a name="brokeractivation-event-class-data-columns"></a>Colunas de dados da classe de evento Broker:Activation  
  
|Coluna de dados|Type|DESCRIÇÃO|Número da coluna|Filtrável|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ClientProcessID**|`int`|A ID atribuída pelo computador host ao processo em que está sendo executado o aplicativo cliente. Essa coluna de dados será populada se a ID do processo do cliente for fornecida pelo cliente.|9|Sim|  
|**DatabaseID**|`int`|A ID do banco de dados especificada pela instrução de *banco de dados* USE ou a ID do banco de dados padrão se nenhuma instrução de *banco de dados*USE tiver sido emitida para determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**EventClass**|`int`|O tipo de classe de evento capturado. Sempre **163** para **Broker:Activation**.|27|Não|  
|**EventSequence**|`int`|Número de sequência para esse evento.|51|Não|  
|**EventSubClass**|`nvarchar`|A ação específica que este evento informa. Um dos seguintes valores:<br /><br /> **início**: <br />                O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] iniciou um procedimento armazenado de ativação.<br /><br /> **encerrado**: o procedimento armazenado de ativação saiu normalmente.<br /><br /> **anulado**: o procedimento armazenado de ativação foi encerrado com um erro.|21|Não|  
|**HostName**|`nvarchar`|O nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|**IntegerData**|`int`|O número de tarefas ativas nesta fila.|25|Não|  
|**IsSystem**|`int`|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Não|  
|**LoginSid**|`image`|Número SID (identificação de segurança) do usuário que fez logon. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**NTDomainName**|`nvarchar`|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**NTUserName**|`nvarchar`|O nome do usuário proprietário da conexão que gerou este evento.|6|Sim|  
|**ObjectID**|`int`|A fila associada a este evento.|22|Não|  
|**ServerName**|`nvarchar`|O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|**SPID**|`int`|A ID de processo do servidor atribuída pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao processo associado ao cliente.|12|Sim|  
|**StartTime**|`datetime`|O horário no qual o evento foi iniciado, quando disponível.|14|Sim|  
|**TransactionID**|`bigint`|ID da transação atribuída pelo sistema.|4|Não|  
  
  
