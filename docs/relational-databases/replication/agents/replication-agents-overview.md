---
title: "Vis&#227;o geral dos agentes de replica&#231;&#227;o. | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Agente de Distribuição"
  - "agentes [replicação do SQL Server]"
  - "Queue Reader Agent, sobre o Queue Reader Agent"
  - "Queue Reader Agent"
  - "Agente de Mesclagem, sobre o Agente de Mesclagem"
  - "Agente de Leitor de Log, sobre o Agente de Leitor de Log"
  - "replicação [SQL Server], agentes e perfis"
  - "Agente de Leitor de Log"
  - "Agente de Distribuição, sobre o Agente de Distribuição"
  - "agentes [replicação do SQL Server], sobre os agentes"
  - "Agente de Mesclagem"
  - "Snapshot Agent, sobre o Snapshot Agent"
  - "Snapshot Agent"
ms.assetid: a35ecd7d-f130-483c-87e3-ddc8927bb91b
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# Vis&#227;o geral dos agentes de replica&#231;&#227;o.
  A replicação usa um número de programas autônomos, chamados agentes, para executar as tarefas associadas ao rastreamento de alterações e dados de distribuição. Por padrão, os agentes de replicação são executados como tarefas programadas sob o Agente[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e o Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve ficar executando para os trabalhos a executar. Os agentes de replicação também podem ser executados a partir da linha de comando e por aplicativos que usam RMO (Replication Management Objects). Os agentes de replicação podem ser administrados a partir do Monitor de Replicação do  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
## SQL Server Agent  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agente hospeda e programa os agentes usados na replicação e fornece uma maneira fácil de executar os agentes de replicação. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agente também controla e monitora operações fora da replicação. Para obter mais informações, consulte [Configure SQL Server Agent](../../../ssms/agent/configure-sql-server-agent.md).  
  
> [!IMPORTANT]  
>  Por padrão, o serviço do agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é desabilitado quando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é instalado, a menos que você escolha explicitamente iniciar automaticamente o serviço durante a instalação. Para obter mais informações sobre como iniciar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] serviço do agente, consulte [Iniciar, parar ou pausar o serviço SQL Server Agent](../../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md).  
  
## Snapshot Agent  
 O Agente de Instantâneo normalmente é usado com todos os tipos de replicação. Ele prepara o esquema e os arquivos de dados iniciais das tabelas publicadas e de outros objetos, armazena os arquivos de instantâneo e registra as informações sobre a sincronização do banco de dados de distribuição. O Agente de Instantâneo executa no Distribuidor. Para obter mais informações, consulte [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md).  
  
## Agente de Leitor de Log  
 The Agente de Leitor de Log é usado em replicação transacional. Ele move transações marcadas para replicação do log de transação no Publicador para o banco de dados de distribuição. Cada banco de dados publicado com o uso de replicação transacional possui seu próprio Agente de Leitor de Log que executa no Distribuidor e conecta ao Publicador (o distribuidor pode estar no mesmo computador do Publicador). Para obter mais informações, consulte [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md).  
  
## Agente de Distribuição  
 O Agente de Distribuição é usado com a replicação de instantâneo e com a replicação transacional. Ele aplica o instantâneo inicial ao Assinante e move as transações contidas no banco de dados de distribuição para os Assinantes. O Agente de Distribuição é executado no Distribuidor para assinaturas push ou no Assinante para assinaturas pull. Para obter mais informações, consulte [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md).  
  
## Merge Agent  
 O Agente de Mesclagem é usado com replicação de mesclagem. Ele aplica o instantâneo inicial ao Assinante e move e reconcilia as alterações de dados incrementais que ocorrem. Cada assinatura de mesclagem possui seu próprio Agente de Mesclagem que se conecta ao Publicador e ao Assinante e atualiza os dois. O Agente de Mesclagem é executado no Distribuidor para assinaturas push ou no Assinante para assinaturas pull. Por padrão, o Agente de Mesclagem carrega alterações do Assinante ao Publicador e, em seguida, baixa as alterações do Publicador para o Assinante. Para obter mais informações, consulte [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md).  
  
## Queue Reader Agent  
 O Agente de Leitor de Fila é usado com a replicação transacional com a opção de atualização enfileirada. O agente executa no Distribuidor e move as alterações feitas no Assinante de volta para o Publicador. Diferente do Agente de Distribuição e do Agente de Mesclagem, somente uma instância do Agente de Leitor de Fila existe para atender a todos os Publicadores e publicações de um determinado banco de dados de distribuição. Para obter mais informações sobre o Queue Reader Agent, consulte [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md). Para obter mais informações sobre assinaturas atualizáveis, consulte [assinaturas atualizáveis para replicação transacional](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
## Trabalhos de Manutenção de Replicação  
 A replicação possui diversos trabalhos de manutenção que executam manutenção programada e sob demanda. Para obter mais informações, consulte [Administração do agente de replicação](../../../relational-databases/replication/agents/replication-agent-administration.md).  
  
## Consulte também  
 [Iniciar e parar um agente de replicação e 40; SQL Server Management Studio e 41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [Executar trabalhos de manutenção de replicação & #40. SQL Server Management Studio e 41;](../../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md)   
 [Conceitos dos executáveis do Replication Agent](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [Administração do agente de replicação](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  