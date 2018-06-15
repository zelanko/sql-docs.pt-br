---
title: Exibir informações e executar tarefas para agentes de assinatura | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- agents [SQL Server replication], viewing information
- viewing replication agent information
- agents [SQL Server replication], tasks in Replication Monitor
ms.assetid: fbb59d31-2424-4552-9195-0da8d83e755f
caps.latest.revision: 37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f98dd86491561fb67197a02e228ec1b151e6e3ea
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32960611"
---
# <a name="view-information-and-perform-tasks-for-subscription-agents"></a>Exibir informações e executar tarefas para agentes de assinatura
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O Replication Monitor fornece duas guias que permitem acesso às informações sobre o(s) agente(s) associado(s) a uma assinatura:  
  
-   **Todas as Assinaturas**  
  
     Essa guia exibe informações sobre todas as assinaturas para a publicação selecionada.  
  
-   **Lista de Observação da Assinatura**  
  
     Essa guia destina-se a exibir informações sobre as assinaturas de todas as publicações disponíveis no Publicador selecionado que tenham erros, avisos ou o pior desempenho. Essa guia não é exibida para Distribuidores que executam as versões anteriores do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Para obter mais informações sobre as opções de cada guia, clique na guia no painel direito e, em seguida, clique em **Ajuda** na barra de menus. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-subscription-all-subscriptions-tab"></a>Para exibir informações e executar tarefas para os agentes associados a uma assinatura (guia Todas as Assinaturas)  
  
1.  Expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e clique em uma publicação.  
  
2.  Clique na guia **Todas as Assinaturas** para exibir informações sobre as assinaturas. Você também pode acessar informações mais detalhadas e realizar tarefas nesta guia:  
  
    -   Para exibir informações detalhadas sobre o agente associado a uma assinatura, clique com o botão direito do mouse na assinatura e então clique em **Exibir Detalhes**. As informações detalhadas incluem: histórico do agente e mensagens de erro, estatísticas de desempenho da replicação transacional e estatísticas no nível de sincronização da replicação de mesclagem.  
  
         As guias na janela de detalhes aberta dependem do tipo de assinatura: para as assinaturas de instantâneos, a guia é **Histórico do Distribuidor para o Assinante**, para as assinaturas transacionais, as guias são **Histórico do Publicador para o Distribuidor**, **Histórico do Distribuidor para o Assinante**e **Comandos Não Distribuídos**, para as assinaturas de mesclagem, a guia é **Histórico de Sincronização**.  
  
    -   Para sincronizar uma assinatura push, clique com o botão direito do mouse na assinatura, e, depois, clique em **Iniciar Sincronização**.  
  
    -   Para reinicializar uma assinatura, clique com o botão direito do mouse na assinatura, e, depois, clique em **Reinicializar Assinatura**.  
  
    -   Para validar uma única assinatura de mesclagem, clique com o botão direito do mouse na assinatura, e, então, clique em **Validar Assinatura**. Para validar todas as assinaturas em uma publicação de mesclagem, clique com o botão direito do mouse na publicação e clique em **Validar Todas as Assinaturas**; para validar todas as assinaturas em uma publicação transacional, clique com o botão direito do mouse na publicação e clique em **Validar Assinaturas**.  
  
    -   Para gerenciar os perfis do agente, clique com o botão direito do mouse no agente e então clique em **Perfil do Agente**. Para obter mais informações, consulte [Trabalhar com perfis do agente de replicação](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md).  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-subscription-subscription-watch-list-tab"></a>Para exibir as informações e executar tarefas nos agentes associados a uma assinatura (guia Lista de Observação da Assinatura)  
  
1.  Expanda um Grupo do publicador no painel esquerdo e clique em um Publicador.  
  
2.  Clique na guia **Lista de Observação da Assinatura** , para exibir informações sobre assinaturas. Você também pode acessar informações mais detalhadas e realizar tarefas nesta guia:  
  
    -   Para exibir informações detalhadas sobre o agente associado a uma assinatura, clique com o botão direito do mouse na assinatura e então clique em **Exibir Detalhes**. As informações detalhadas incluem: histórico do agente e mensagens de erro, estatísticas de desempenho da replicação transacional e estatísticas no nível de sincronização da replicação de mesclagem.  
  
         As guias na janela de detalhes aberta dependem do tipo de assinatura: para as assinaturas de instantâneos, a guia é **Histórico do Distribuidor para o Assinante**; para as assinaturas transacionais, as guias são **Histórico do Publicador para o Distribuidor**, **Histórico do Distribuidor para o Assinante**e **Desempenho**; para as assinaturas de mesclagem, a guia é **Histórico de Sincronização**.  
  
    -   Para sincronizar uma assinatura push, clique com o botão direito do mouse na assinatura, e, depois, clique em **Iniciar Sincronização**.  
  
    -   Para reinicializar uma assinatura, clique com o botão direito do mouse na assinatura, e, depois, clique em **Reinicializar Assinatura**.  
  
    -   Para validar uma única assinatura de mesclagem, clique com o botão direito do mouse na assinatura, e, então, clique em **Validar Assinatura**. Para validar todas as assinaturas em uma publicação de mesclagem, clique com o botão direito do mouse na publicação e clique em **Validar Todas as Assinaturas**; para validar todas as assinaturas em uma publicação transacional, clique com o botão direito do mouse na publicação e clique em **Validar Assinaturas**.  
  
    -   Para gerenciar os perfis do agente, clique com o botão direito do mouse no agente e então clique em **Perfil do Agente**. Para obter mais informações, consulte [Trabalhar com perfis do agente de replicação](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir informações e realizar tarefas para uma assinatura &#40;Replication Monitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [Monitorando a Replicação](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
