---
description: classe de evento Broker:Message Classify
title: Classe de evento Broker:Message Classify | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Broker:Message Classify event class
ms.assetid: e51f3351-1239-4c41-b87c-1dd86968e027
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7e5e8e0bc84e26798716ba1635580b81dbfc08c8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88331072"
---
# <a name="brokermessage-classify-event-class"></a>classe de evento Broker:Message Classify

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera um evento **Broker:Message Classify** quando o Broker Service determina o roteamento de uma mensagem.  
  
## <a name="brokermessage-classify-event-class-data-columns"></a>Colunas de dados da classe de evento Broker:Message Classify  
  
|Coluna de dados|Tipo de dados|Descrição|Número da coluna|Filtrável|  
|-----------------|---------------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|O nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|**ClientProcessID**|**int**|A ID atribuída pelo computador host ao processo em que está sendo executado o aplicativo cliente. Essa coluna de dados será populada se a ID do processo do cliente for fornecida pelo cliente.|9|Sim|  
|**DatabaseID**|**int**|A ID do banco de dados especificada pela instrução USE *database* ou a ID do banco de dados padrão se nenhuma instrução USE *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**EventClass**|**int**|O tipo de classe de evento capturado. Sempre **141** para **Broker:Message Classify**.|27|Não|  
|**EventSequence**|**int**|Número de sequência para esse evento.|51|Não|  
|**EventSubClass**|**nvarchar**|O tipo de subclasse de evento, fornecendo mais informações sobre cada classe de evento. Essa coluna pode conter os valores a seguir.<br /><br /> **Local**: a rota escolhida tem o endereço LOCAL.<br /><br /> **Remoto**:                 a rota escolhida tem um endereço diferente de LOCAL.<br /><br /> **Atrasado**:                a mensagem está atrasada porque o encaminhamento está desabilitado ou porque não existe rota correspondente.|21|Sim|  
|**FileName**|**nvarchar**|O nome do serviço para o qual se destina a mensagem.|36|Não|  
|**GUID**|**uniqueidentifier**|A ID de conversa da caixa de diálogo. Esse identificador é transmitido como parte da mensagem e é compartilhado por ambos os lados da conversa.|54|Não|  
|**HostName**|**nvarchar**|O nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Não|  
|**LoginSid**|**imagem**|Número SID (identificação de segurança) do usuário que fez logon. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**NTDomainName**|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**NTUserName**|**nvarchar**|O nome do usuário proprietário da conexão que gerou este evento.|6|Sim|  
|**OwnerName**|**nvarchar**|O identificador do Broker ao qual a mensagem se destina.|37|Não|  
|**RoleName**|**nvarchar**|Indica se a mensagem foi recebida da rede ou se originou nessa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|38|Não|  
|**ServerName**|**nvarchar**|O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|**SPID**|**int**|A ID de processo do servidor atribuída pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao processo associado ao cliente.|12|Sim|  
|**Start Time**|**datetime**|O horário no qual o evento foi iniciado, quando disponível.|14|Sim|  
|**TargetUserName**|**nvarchar**|O endereço de rede do próximo Broker de salto.|39|Não|  
|**TransactionID**|**bigint**|ID da transação atribuída pelo sistema.|4|Não|  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
