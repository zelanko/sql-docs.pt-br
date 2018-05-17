---
title: Administração do agente de replicação | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Snapshot Agent, administering
- Log Reader Agent, administering
- Queue Reader Agent, administering
- shared agents [SQL Server replication]
- Merge Agent, administering
- Distribution Agent, administering
- agents [SQL Server replication], administering
- replication cleanup jobs [SQL Server]
- administering replication, agents
- replication [SQL Server], administering
- independent agents [SQL Server replication]
ms.assetid: f27186b8-b1b2-4da0-8b2b-91f632c2ab7e
caps.latest.revision: 48
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b2607af48ae1f542ce314a0aebca1ec3463921fe
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="replication-agent-administration"></a>Administração do agente de replicação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Agentes de replicação executam muitas tarefas associadas com replicação, incluindo a criação de cópias de esquema e dados, a detecção de atualizações no Publicador ou Assinante e a distribuição de modificações entre os servidores. Por padrão, agentes de replicação são executados sob as etapas de trabalho do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent. Os agentes são simplesmente executáveis, assim eles podem também ser chamados diretamente da linha de comando e dos scripts em lote. Cada agente de replicação suporta um jogo de parâmetros de tempo de execução usados para controlar o seu trabalho; esses parâmetros são especificados no perfil do agente ou na linha de comando.  
  
> [!IMPORTANT]  
>  Por padrão, o serviço do agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é desabilitado quando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é instalado, a menos que você escolha explicitamente iniciar automaticamente o serviço durante a instalação.  
  
 Arquivos de agente de Replicação ficam situados em [!INCLUDE[ssInstallPathVar](../../../includes/ssinstallpathvar-md.md)]\COM. A tabela seguinte lista a replicação de nomes executáveis e nomes de arquivo. Clique no link para um agente exibir sua referência de parâmetro.  
  
|Agente executável|Nome do Arquivo|  
|----------------------|---------------|  
|[Agente de Instantâneo de Replicação](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|snapshot.exe|  
|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|distrib.exe|  
|[Agente do Leitor de Log de Replicação](../../../relational-databases/replication/agents/replication-log-reader-agent.md)|logread.exe|  
|[Agente de Leitor de Fila de Replicação](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)|qrdrsvc.exe|  
|[Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)|replmerg.exe|  
  
 Além dos agentes de replicação, a replicação tem vários trabalhos que executam manutenção programada e sob demanda.  
  
 **Para executar os agentes e trabalhos de manutenção**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] e Replication Monitor: [Iniciar e interromper um agente de replicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)  
  
-   Programação de replicação: [Conceitos dos executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
## <a name="agent-profiles"></a>Perfis de Agente  
 Um conjunto de perfis de agente é instalado no distribuidor quando a replicação é configurada. Um perfil de agente contém um conjunto de parâmetros que são usados sempre que um agente é executado: cada agente faz logon no distribuidor durante seu processo de inicialização e consulta os parâmetros em seu perfil. A replicação fornece um perfil padrão para cada agente e perfis adicionais predefinidos para o Log Reader Agent, o Distribution Agent e o Merge Agent. Além dos perfis fornecidos, você pode criar perfis adaptados às exigências de seu aplicativo. Para saber mais, confira [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 Para obter informações sobre como especificar parâmetros de linha de comando diretamente, consulte [Conceitos dos executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## <a name="monitoring-replication-agents"></a>Monitorando agentes de replicação  
 O Replication Monitor lhe permite exibir informações e executar tarefas associadas com cada agente de replicação. A lista a seguir inclui cada agente, as guias no Replication Monitor onde pode ser localizado e um link para um tópico que explica como acessar essas guias:  
  
-   Os agentes a seguir estão associados às publicações no Replication Monitor:  
  
    -   Snapshot Agent  
  
    -   Agente de Leitor de Log  
  
    -   Queue Reader Agent  
  
     Acesse as informações e as tarefas associadas a esses agentes por meio da guia **Agentes** . Para mais informações, consulte [Exibir informações e executar tarefas para os agentes associados a uma publicação &#40;Replication Monitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
-   Os agentes a seguir estão associados às assinaturas no Replication Monitor:  
  
    -   Agente de Distribuição  
  
    -   Merge Agent  
  
     Acesse as informações e as tarefas associadas a esses agentes por meio das seguintes guias: **Lista de Observação da Assinatura** (disponível para cada Publicador) ou a guia **Todas as Assinaturas** (disponível para cada publicação). Para obter mais informações, consulte [View Information and Perform Tasks for the Agents Associated With a Subscription &#40;Replication Monitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md) [Exibir informações e executar tarefas para os agentes associados a uma assinatura (Replication Monitor)].  
  
## <a name="independent-and-shared-agents"></a>Agente independente e compartilhado  
 Um agente independente é um agente que presta serviço a uma assinatura. Um agente compartilhado presta serviço a múltiplas assinaturas usando a mesma necessidade de sincronização do agente compartilhado, por padrão elas esperam em uma fila, e o agente compartilhado presta serviço a elas uma de cada vez. A latência é reduzida ao usar os agentes independentes porque o agente está pronto sempre que a assinatura precisa ser sincronizada. A replicação de mesclagem sempre usa agentes independentes, e a replicação transacional usa agentes independentes por padrão para publicações criadas no Assistente para Novas Publicações (nas versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], por padrão a replicação transacional usava agentes compartilhados).  
  
## <a name="replication-maintenance-jobs"></a>Trabalhos de Manutenção de Replicação  
 A replicação usa os seguintes trabalhos para executar manutenção programada e sob demanda.  
  
|Limpar o trabalho|Description|Cronograma padrão|  
|------------------|-----------------|----------------------|  
|Limpeza do histórico do agente: Distribuição|Remove o histórico do agente de replicação do banco de dados de distribuição.|Executa a cada dez minutos|  
|Limpeza de distribuição: Distribuição|Remove transações replicadas do banco de dados de distribuição. |Executa a cada dez minutos|  
|Limpeza de assinaturas expiradas|Detecta e remove assinaturas expiradas dos bancos de dados de publicação. No distribuidor, desativa assinaturas que não foram sincronizadas dentro do período máximo de retenção da distribuição.|Executa diariamente à 1h00.| 
|Reinicializar as assinaturas que possuem falhas de validação de dados|Detectar todas as assinaturas que têm falhas de validação de dados marcando-as para reinicialização. A próxima vez que o Merge Agent ou que o Distribution Agent executarem, um instantâneo novo será aplicado aos Assinantes.|Nenhum cronograma padrão (desativado por padrão).|  
|Verificação dos agentes de replicação|Detecta agentes de replicação que não estão ativamente fazendo log no histórico. Comunica ao log do evento do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows se uma etapa do trabalho falhar.|Executa a cada dez minutos.|  
|Atualizador de monitoração de replicação para distribuição|Atualiza as consultas armazenadas usadas pelo Replication Monitor.|Executa continuamente.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorando a Replicação](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
