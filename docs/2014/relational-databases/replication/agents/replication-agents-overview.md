---
title: Visão geral dos agentes de replicação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Distribution Agent
- agents [SQL Server replication]
- Queue Reader Agent, about Queue Reader Agent
- Queue Reader Agent
- Merge Agent, about Merge Agent
- Log Reader Agent, about Log Reader Agent
- replication [SQL Server], agents and profiles
- Log Reader Agent
- Distribution Agent, about Distribution Agent
- agents [SQL Server replication], about agents
- Merge Agent
- Snapshot Agent, about Snapshot Agent
- Snapshot Agent
ms.assetid: a35ecd7d-f130-483c-87e3-ddc8927bb91b
caps.latest.revision: 41
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4fe3b25fb570d305ba176d89f2f21413c19665e1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37270762"
---
# <a name="replication-agents-overview"></a>Visão geral dos agentes de replicação.
  A replicação usa um número de programas autônomos, chamados agentes, para executar as tarefas associadas ao rastreamento de alterações e dados de distribuição. Por padrão, os agentes de replicação são executados como tarefas programadas sob o Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e o Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve ficar executando para os trabalhos a executar. Os agentes de replicação também podem ser executados a partir da linha de comando e por aplicativos que usam RMO (Replication Management Objects). Os agentes de replicação podem ser administrados a partir do Monitor de Replicação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
## <a name="sql-server-agent"></a>SQL Server Agent  
 O agente[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] hospeda e programa os agentes usados em replicação e fornece uma maneira fácil para executar os agentes de replicação. O agente[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] também controla e monitora operações fora de replicação. Para obter mais informações, consulte [Configure SQL Server Agent](../../../ssms/agent/sql-server-agent.md).  
  
> [!IMPORTANT]  
>  Por padrão, o serviço do agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é desabilitado quando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é instalado, a menos que você escolha explicitamente iniciar automaticamente o serviço durante a instalação. Para obter mais informações sobre como iniciar o serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent, consulte [Start, Stop, or Pause the SQL Server Agent Service](../../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md).  
  
## <a name="snapshot-agent"></a>Snapshot Agent  
 O Agente de Instantâneo normalmente é usado com todos os tipos de replicação. Ele prepara o esquema e os arquivos de dados iniciais das tabelas publicadas e de outros objetos, armazena os arquivos de instantâneo e registra as informações sobre a sincronização do banco de dados de distribuição. O Agente de Instantâneo executa no Distribuidor. Para obter mais informações, consulte [Replication Snapshot Agent](replication-snapshot-agent.md).  
  
## <a name="log-reader-agent"></a>Agente de Leitor de Log  
 The Agente de Leitor de Log é usado em replicação transacional. Ele move transações marcadas para replicação do log de transação no Publicador para o banco de dados de distribuição. Cada banco de dados publicado com o uso de replicação transacional possui seu próprio Agente de Leitor de Log que executa no Distribuidor e conecta ao Publicador (o distribuidor pode estar no mesmo computador do Publicador). Para obter mais informações, consulte [Replication Log Reader Agent](replication-log-reader-agent.md).  
  
## <a name="distribution-agent"></a>Agente de Distribuição  
 O Agente de Distribuição é usado com a replicação de instantâneo e com a replicação transacional. Ele aplica o instantâneo inicial ao Assinante e move as transações contidas no banco de dados de distribuição para os Assinantes. O Agente de Distribuição é executado no Distribuidor para assinaturas push ou no Assinante para assinaturas pull. Para obter mais informações, consulte [Replication Distribution Agent](replication-distribution-agent.md).  
  
## <a name="merge-agent"></a>Merge Agent  
 O Agente de Mesclagem é usado com replicação de mesclagem. Ele aplica o instantâneo inicial ao Assinante e move e reconcilia as alterações de dados incrementais que ocorrem. Cada assinatura de mesclagem possui seu próprio Agente de Mesclagem que se conecta ao Publicador e ao Assinante e atualiza os dois. O Agente de Mesclagem é executado no Distribuidor para assinaturas push ou no Assinante para assinaturas pull. Por padrão, o Agente de Mesclagem carrega alterações do Assinante ao Publicador e, em seguida, baixa as alterações do Publicador para o Assinante. Para obter mais informações, consulte [Replication Merge Agent](replication-merge-agent.md).  
  
## <a name="queue-reader-agent"></a>Queue Reader Agent  
 O Agente de Leitor de Fila é usado com a replicação transacional com a opção de atualização enfileirada. O agente executa no Distribuidor e move as alterações feitas no Assinante de volta para o Publicador. Diferente do Agente de Distribuição e do Agente de Mesclagem, somente uma instância do Agente de Leitor de Fila existe para atender a todos os Publicadores e publicações de um determinado banco de dados de distribuição. Para obter mais informações sobre o Agente de Leitor de Fila, consulte o [Replication Queue Reader Agent](replication-queue-reader-agent.md). Para obter mais informações sobre assinaturas atualizáveis, consulte [Updatable Subscriptions for Transactional Replication](../transactional/updatable-subscriptions-for-transactional-replication.md).  
  
## <a name="replication-maintenance-jobs"></a>Trabalhos de Manutenção de Replicação  
 A replicação possui diversos trabalhos de manutenção que executam manutenção programada e sob demanda. Para obter mais informações, consulte [Replication Agent Administration](replication-agent-administration.md) (Administração do agente de replicação).  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar e interromper um agente de replicação &#40;SQL Server Management Studio&#41;](start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [Executar trabalhos de manutenção de replicação &#40;SQL Server Management Studio&#41;](../administration/run-replication-maintenance-jobs-sql-server-management-studio.md)   
 [Conceitos dos executáveis do Agente de Replicação](../concepts/replication-agent-executables-concepts.md)   
 [Administração do agente de replicação](replication-agent-administration.md)  
  
  
