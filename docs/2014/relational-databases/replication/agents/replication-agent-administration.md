---
title: Administração do agente de replicação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 00fc90be42bddd7feb43d96c9110def4db60835c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721798"
---
# <a name="replication-agent-administration"></a>Administração do agente de replicação
  Agentes de replicação executam muitas tarefas associadas com replicação, incluindo a criação de cópias de esquema e dados, a detecção de atualizações no Publicador ou Assinante e a distribuição de modificações entre os servidores. Por padrão, os agentes de replicação [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] são executados sob etapas de trabalho do Agent. Os agentes são simplesmente executáveis, assim eles podem também ser chamados diretamente da linha de comando e dos scripts em lote. Cada agente de replicação suporta um jogo de parâmetros de tempo de execução usados para controlar o seu trabalho; esses parâmetros são especificados no perfil do agente ou na linha de comando.  
  
> [!IMPORTANT]  
>  Por padrão, o serviço do agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é desabilitado quando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é instalado, a menos que você escolha explicitamente iniciar automaticamente o serviço durante a instalação.  
  
 Arquivos de agente de Replicação ficam situados em [!INCLUDE[ssInstallPathVar](../../../includes/ssinstallpathvar-md.md)]\COM. A tabela seguinte lista a replicação de nomes executáveis e nomes de arquivo. Clique no link para um agente exibir sua referência de parâmetro.  
  
|Agente executável|Nome do Arquivo|  
|----------------------|---------------|  
|[Replication Snapshot Agent](replication-snapshot-agent.md)|snapshot.exe|  
|[Replication Distribution Agent](replication-distribution-agent.md)|distrib.exe|  
|[Agente do Leitor de Log de Replicação](replication-log-reader-agent.md)|logread.exe|  
|[Agente de Leitor de Fila de Replicação](replication-queue-reader-agent.md)|qrdrsvc.exe|  
|[Replication Merge Agent](replication-merge-agent.md)|replmerg.exe|  
  
 Além dos agentes de replicação, a replicação tem vários trabalhos que executam manutenção programada e sob demanda.  
  
 **Para executar agentes e trabalhos de manutenção**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]e o Replication Monitor: [Iniciar e parar um agente de replicação &#40;SQL Server Management Studio&#41;](start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
-   Programação de replicação: [Conceitos dos executáveis do agente de replicação](../concepts/replication-agent-executables-concepts.md)  
  
## <a name="agent-profiles"></a>Perfis de Agente  
 Um conjunto de perfis de agente é instalado no distribuidor quando a replicação é configurada. Um perfil de agente contém um conjunto de parâmetros que são usados sempre que um agente é executado: cada agente faz logon no distribuidor durante seu processo de inicialização e consulta os parâmetros em seu perfil. A replicação fornece um perfil padrão para cada agente e perfis adicionais predefinidos para o Log Reader Agent, o Distribution Agent e o Merge Agent. Além dos perfis fornecidos, você pode criar perfis adaptados às exigências de seu aplicativo. Para saber mais, confira [Replication Agent Profiles](replication-agent-profiles.md).  
  
 Para obter informações sobre como especificar parâmetros de linha de comando diretamente, consulte [Conceitos dos executáveis do agente de replicação](../concepts/replication-agent-executables-concepts.md).  
  
## <a name="monitoring-replication-agents"></a>Monitorando agentes de replicação  
 O Replication Monitor lhe permite exibir informações e executar tarefas associadas com cada agente de replicação. A lista a seguir inclui cada agente, as guias no Replication Monitor onde pode ser localizado e um link para um tópico que explica como acessar essas guias:  
  
-   Os agentes a seguir estão associados às publicações no Replication Monitor:  
  
    -   Snapshot Agent  
  
    -   Agente de Leitor de Log  
  
    -   Queue Reader Agent  
  
     Acesse informações e tarefas associadas a esses agentes por meio da guia **agentes** . Para obter mais informações, consulte [Exibir informações e executar tarefas usando o Replication Monitor](../monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
-   Os agentes a seguir estão associados às assinaturas no Replication Monitor:  
  
    -   Agente de Distribuição  
  
    -   Merge Agent  
  
     Acesse as informações e as tarefas associadas a esses agentes por meio das seguintes guias: **Lista de Observação da Assinatura** (disponível para cada Publicador) ou a guia **Todas as Assinaturas** (disponível para cada publicação). Para obter mais informações, confira [Exibir informações e executar tarefas usando o Replication Monitor](../monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
## <a name="independent-and-shared-agents"></a>Agente independente e compartilhado  
 Um agente independente é um agente que presta serviço a uma assinatura. Um agente compartilhado presta serviço a múltiplas assinaturas usando a mesma necessidade de sincronização do agente compartilhado, por padrão elas esperam em uma fila, e o agente compartilhado presta serviço a elas uma de cada vez. A latência é reduzida ao usar os agentes independentes porque o agente está pronto sempre que a assinatura precisa ser sincronizada. A replicação de mesclagem sempre usa agentes independentes, e a replicação transacional usa agentes independentes por padrão para publicações criadas no Assistente para Novas Publicações (nas versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], por padrão a replicação transacional usava agentes compartilhados).  
  
## <a name="replication-maintenance-jobs"></a>Trabalhos de Manutenção de Replicação  
 A replicação usa os seguintes trabalhos para executar manutenção programada e sob demanda.  
  
|Trabalho de limpeza|DESCRIÇÃO|Cronograma padrão|  
|------------------|-----------------|----------------------|  
|Limpeza do histórico do agente: Distribuição|Remove o histórico do agente de replicação do banco de dados de distribuição.|Executa a cada dez minutos|  
|Limpeza de distribuição: Distribuição|Remove transações replicadas do banco de dados de distribuição. Desativa assinaturas que não foram sincronizadas dentro do período máximo de retenção da distribuição.|Executa a cada dez minutos|  
|Limpeza de assinaturas expiradas|Detecta e remove assinaturas expiradas dos bancos de dados de publicação.|Executa diariamente à 1h00.|  
|Reinicializar as assinaturas que possuem falhas de validação de dados|Detectar todas as assinaturas que têm falhas de validação de dados marcando-as para reinicialização. A próxima vez que o Merge Agent ou que o Distribution Agent executarem, um instantâneo novo será aplicado aos Assinantes.|Nenhum cronograma padrão (desativado por padrão).|  
|Verificação dos agentes de replicação|Detecta agentes de replicação que não estão ativamente fazendo log no histórico. Comunica ao log do evento do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows se uma etapa do trabalho falhar.|Executa a cada dez minutos.|  
|Atualizador de monitoração de replicação para distribuição|Atualiza as consultas armazenadas usadas pelo Replication Monitor.|Executa continuamente.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorando a Replicação](../monitoring-replication.md)  
  
  
