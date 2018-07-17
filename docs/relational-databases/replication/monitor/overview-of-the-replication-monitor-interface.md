---
title: Visão geral da interface do Replication Monitor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor
- Replication Monitor, about Replication Monitor
ms.assetid: 078f0e34-7153-45c4-8725-778b5bef88da
caps.latest.revision: 41
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: be7f1fd32f7bc951dcab0aad992fd3900012d678
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37358838"
---
# <a name="overview-of-the-replication-monitor-interface"></a>Visão geral da interface do Replication Monitor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Replication Monitor apresenta uma exibição voltada para o Publicador ou para o Distribuidor de todas as atividades de replicação em um formato de dois painéis. Você adiciona um Publicador ao monitor no painel esquerdo e, no painel direito, o monitor exibe informações sobre o Publicador, suas publicações, as assinaturas para essas publicações e os diversos agentes de replicação. Além de apresentar informações sobre a topologia de replicação, o Replication Monitor permite que você execute várias tarefas, como iniciar e interromper agentes e validar dados.  
  
## <a name="viewing-information-for-the-entire-topology"></a>Exibindo informações para toda a topologia  
 O painel esquerdo da exibição do Replication Monitor  
  
-   Grupos do publicador, publicadores e publicações.  
  
-   Distribuidores, publicadores e publicações.  
  
 Você deve adicionar um Publicador antes de exibir quaisquer informações no Replication Monitor. Para obter mais informações, veja [Adicionar e remover Publicadores do Replication Monitor](../../../relational-databases/replication/monitor/add-and-remove-publishers-from-replication-monitor.md).  
  
 O painel esquerdo ajuda a responder as seguintes perguntas:  
  
-   Meu sistema de replicação está íntegro?  
  
     O sistema de replicação estará relativamente íntegro se não houver nenhum ícones de erro em nós no painel esquerdo. Para obter uma exibição mais completa da integridade do sistema, você também deve verificar a guia **Lista de Observação da Assinatura** que exibe informações sobre as assinaturas que talvez exijam atenção.  
  
-   Por que um agente não está executando?  
  
     Um agente não está em execução em um momento específico porque não está agendado para execução ou porque ocorreu um erro. Se tiver ocorrido um erro, será exibido um ícone de erro nos nós apropriados no painel esquerdo. Por exemplo, se o Agente de Instantâneo de uma publicação foi interrompido devido a um erro, um ícone de erro será exibido no Grupo do publicador, no Publicador e nos nós de publicação. A guia **Agentes** exibe informações resumidas sobre o Agente de Instantâneo para a publicação. Clique duas vezes no Agente de Instantâneo nessa guia para obter informações detalhadas sobre o erro.  
  
## <a name="viewing-information-and-performing-tasks-related-to-distributors"></a>Exibindo informações e executando tarefas relacionadas à distribuidores  
 O Replication Monitor exibe informações sobre Distribuidores em três guias:  
  
-   Guia**Publicações**   
  
     Essa guia fornece informações resumidas de todas as publicações de um Distribuidor.  
  
-   Guia**Lista de Observação da Assinatura**   
  
     Essa guia fornece informações sobre assinaturas do Distribuidor selecionado. Você pode filtrar a lista de assinaturas para ver erros, avisos e qualquer assinatura de desempenho insatisfatório. A guia também permite executar as seguintes tarefas: acessar propriedades da assinatura, acessar informações detalhadas sobre o agente ou agentes associados à assinatura; reiniciar assinaturas e validar assinaturas.  
  
     A guia **Lista de Observação da Assinatura** ajuda a responder as seguintes perguntas:  
  
    -   Quais assinaturas estão lentas?  
  
         Defina as opções nessa guia de forma que a grade exiba as assinaturas em ordem de desempenho relativo.  
  
    -   Meu sistema de replicação está íntegro?  
  
         A grade nessa guia exibe ícones de erro e advertência de qualquer assinatura que exija sua atenção.  
  
     Essa guia não está disponível para Distribuidores que estão executando versões do [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] ou anteriores.  
  
-   Guia**Agentes**   
  
     Essa guia exibe informações detalhadas sobre os agentes e trabalhos usados por todos os tipos de replicação. A guia também permite iniciar e interromper cada agente e trabalho.  
  
 O Replication Monitor também fornece um menu de contexto para o nó Distribuidor. Clique com o botão direito do mouse em um Distribuidor no painel esquerdo para executar as tarefas a seguir:  
  
-   Adicionar um Publicador ao Replication Monitor.  
  
-   Editar as configurações do Replication Monitor para o Distribuidor.  
  
-   Alternar para a exibição Grupo do Publicador.  
  
## <a name="viewing-information-and-performing-tasks-related-to-publishers"></a>Exibindo informações e executando tarefas relacionadas a Publicadores  
 O Replication Monitor exibe informações sobre Publicadores em três guias:  
  
-   Guia**Publicações**   
  
     Essa guia fornece informações resumidas de todas as publicações em um Publicador.  
  
-   Guia**Lista de Observação da Assinatura**   
  
     O objetivo dessa guia é exibir informações sobre assinaturas de todas as publicações disponíveis no Publicador selecionado. Você pode filtrar a lista de assinaturas para ver erros, avisos e qualquer assinatura de desempenho insatisfatório. A guia também permite: acessar as propriedades da assinatura; acessar informações detalhadas sobre o agente ou agentes associados com uma assinatura; reiniciar assinaturas e validar assinaturas.  
  
     A guia **Lista de Observação da Assinatura** ajuda a responder as seguintes perguntas:  
  
    -   Quais assinaturas estão lentas?  
  
         Defina as opções nessa guia de forma que a grade exiba as assinaturas em ordem de desempenho relativo.  
  
    -   Meu sistema de replicação está íntegro?  
  
         A grade nessa guia exibe ícones de erro e advertência de qualquer assinatura que exija sua atenção.  
  
     Essa guia não é exibida para Distribuidores que executam versões anteriores ao [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
-   Guia**Agentes**   
  
     Essa guia exibe informações detalhadas sobre os agentes e trabalhos usados por todos os tipos de replicação. A guia também permite que você inicie e interrompa cada agente e trabalho.  
  
 Para obter mais informações, consulte [Exibir informações e executar tarefas para um Publicador &#40;Replication Monitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md).  
  
 O Replication Monitor também fornece um menu de contexto para o nó Publicador. Clique com o botão direito do mouse em um Publicador no painel esquerdo para:  
  
-   Editar as configurações do Replication Monitor para o Publicador  
  
-   Remover o Publicador do Replication Monitor  
  
-   Exibir e editar perfis de agente  
  
-   Conectar-se ou desconectar-se do Distribuidor que armazena informações sobre o Publicador  
  
## <a name="viewing-information-and-performing-tasks-related-to-publications"></a>Exibindo informações e executando tarefas relacionadas a publicações  
 O Replication Monitor exibe informações sobre publicações em três guias e várias janelas de detalhes:  
  
-   Guia**Todas as Assinaturas**   
  
     Essa guia exibe informações sobre todas as assinaturas para a publicação selecionada. Por padrão, essa guia é classificada por ordem de prioridade: erros, avisos e, em seguida, em ordem crescente de desempenho, com qualquer assinatura de baixo desempenho na parte superior.  
  
     A guia **Todas as Assinaturas** ajuda a responder as seguintes perguntas:  
  
    -   Quais assinaturas estão lentas?  
  
         Defina as opções nessa guia de forma que a grade exiba as assinaturas em ordem de desempenho relativo.  
  
    -   Meu sistema de replicação está íntegro?  
  
         A grade nessa guia exibe ícones de erro e advertência de qualquer assinatura que exija sua atenção.  
  
-   Guia**Agentes**   
  
     Essa guia exibe informações sobre os agentes que são usados pela replicação. Essa guia exibe informações sobre os seguintes agentes:  
  
    -   O Agente de Instantâneo, que é usado por todas as publicações.  
  
    -   O Agente de Leitor de Log, que é usado por todas as publicações transacionais.  
  
    -   O Agente de Leitor de Fila, que é usado pelas publicações transacionais habilitadas para atualização de assinaturas em fila.  
  
     A guia também permite que você execute as seguintes tarefas: acessar informações detalhadas sobre cada agente e iniciar e interromper cada agente. Para obter mais informações sobre os agentes associados a assinaturas (Agente de Distribuição e Agente de Mesclagem), consulte a seção “Exibindo informações e tarefas de desempenho relacionadas a assinaturas”, neste tópico.  
  
-   Guia**Avisos**   
  
     Esta guia permite especificar avisos e alertas para agentes. Para obter mais informações, consulte [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
-   Guia**Tokens de Rastreamento** (somente para replicação transacional)  
  
     Essa guia permite medir a latência, o período decorrido entre a confirmação de uma transação no Publicador e a confirmação da transação correspondente no Assinante.  
  
     Essa guia ajuda a responder a seguinte pergunta:  
  
    -   Quanto tempo uma transação confirmada agora, levará para alcançar um Assinante em replicação transacional?  
  
         Exiba o período total para uma transação viajar pelo sistema e também o compare com os intervalos anteriores.  
  
     Essa guia não é exibida para Distribuidores que executam o [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] ou versões anteriores. Para obter mais informações sobre tokens de rastreamento, consulte [Medir a latência e validar as conexões para a replicação transacional](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md).  
  
-   Janelas de detalhes para agentes associados a uma publicação. Os seguintes agentes são associados a publicações:  
  
    -   O Agente de Instantâneo, que é usado por todas as publicações.  
  
    -   O Agente de Leitor de Log, que é usado por todas as publicações transacionais.  
  
    -   O Agente de Leitor de Fila, que é usado pelas publicações transacionais habilitadas para atualização de assinaturas em fila.  
  
     Clique duas vezes em um agente no Replication Monitor para acessar informações em uma janela de detalhes. Além dos agentes listados acima, existem agentes associados a assinaturas: o Agente de Distribuição para assinaturas em instantâneos e publicações transacionais; e o Agente de Mesclagem para assinaturas em publicações de mesclagem. Para obter mais informações, consulte a seção “Exibindo informações e desempenhando tarefas relacionadas a assinaturas” neste tópico.  
  
     As janelas de detalhes do agente fornecem informações sobre sessões dos agentes, inclusive hora de início, hora de término, duração e ações executadas em uma sessão. Elas ajudam a responder a seguinte pergunta:  
  
    -   Por que um agente não está executando?  
  
         As mensagens de erro disponíveis fornecem informações detalhadas sobre o motivo de o agente não estar em execução e fornece o ponto inicial para solução de problemas com agentes associados a uma publicação.  
  
 Para obter mais informações, consulte [Exibir informações e executar tarefas para uma publicação &#40;Replication Monitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md) e [Exibir informações e executar tarefas para os agentes associados a uma publicação &#40;Replication Monitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
 O Replication Monitor também fornece um menu de contexto para o nó de publicações. Clique com o botão direito do mouse em uma publicação no painel esquerdo para:  
  
-   Reiniciar todas as assinaturas em uma publicação  
  
-   Validar todas as assinaturas em uma publicação  
  
-   Gerar um instantâneo para uma publicação  
  
-   Exibir e editar as propriedades da publicação  
  
## <a name="viewing-information-and-performing-tasks-related-to-subscriptions"></a>Exibindo informações e executando tarefas relacionadas a assinaturas  
 O Replication Monitor exibe informações sobre assinaturas em várias guias diferentes. Clique duas vezes em uma assinatura no Replication Monitor para acessar essas guias em uma janela de detalhes. Todas as guias são úteis para responder a pergunta "Por que um agente não está em execução?" As mensagens de erro disponíveis fornecem informações detalhadas sobre o motivo de o agente não estar em execução e fornece um ponto inicial para solução de problemas com agentes associados a uma assinatura.  
  
-   **Guia Todas as Assinaturas** e **guia Lista de Observação da Assinatura**  
  
     Essas guias foram descritas anteriormente neste tópico.  
  
-   Guia**Histórico do Publicador para o Distribuidor** (somente replicação transacional)  
  
     Essa guia exibe informações sobre o Agente de Leitor de Log para uma publicação (a guia é idêntica à janela de detalhes do Agente de Leitor de Log).  
  
-   Guia**Histórico do Distribuidor para o Assinante** (replicação de instantâneo e replicação transacional)  
  
     Essa guia exibe informações sobre o Agente de Distribuição de uma assinatura.  
  
-   Guia**Comandos Não Distribuídos** (somente replicação transacional)  
  
     Essa guia exibe informações sobre o número de comandos no banco de dados de distribuição que não foram entregues ao Assinante selecionado e o tempo estimado para entrega desses comandos. A guia ajuda a responder a pergunta "Quanto minha assinatura está atrasada?" Essa guia não é exibida para Distribuidores que executam versões anteriores ao SQL Server 2005.  
  
-   Guia**Histórico de Sincronização** (somente replicação de mesclagem)  
  
     Essa guia exibe informações sobre o Agente de Mesclagem para uma assinatura. Essa guia ajuda a responder a seguinte pergunta:  
  
    -   Por que minha assinatura de mesclagem está lenta?  
  
         Essa guia fornece estatísticas detalhadas para cada artigo processado durante a sincronização, inclusive o tempo gasto em cada fase de processamento (carregar alterações, baixar alterações e assim por diante). Ela pode ajudar a definir tabelas específicas que estão provocando lentidão e é o melhor local para a solução de problemas de desempenho com assinaturas de mesclagem.  
  
 Para obter mais informações, consulte [Exibir informações e executar tarefas para uma assinatura &#40;Replication Monitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md) e [Exibir informações e executar tarefas para os agentes associados a uma assinatura &#40;Replication Monitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
## <a name="viewing-information-and-performing-tasks-related-to-agent-profiles"></a>Exibindo informações e executando tarefas relacionadas a perfis de agente  
 O Replication Monitor inclui várias caixas de diálogo para gerenciar os perfis de agente. Os perfis de agente são conjuntos de parâmetros para um agente que determinam seu comportamento. Para obter mais informações, consulte [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md). As caixas de diálogo são:  
  
-   **Perfis de Agente**  
  
     Essa caixa de diálogo permite: alterar as propriedades dos perfis, criar e excluir perfis, especificar um perfil padrão e especificar que todos os agentes de um tipo específico (como os Agente de Instantâneos) devem usar um determinado perfil.  
  
-   **Propriedades de \<AgentProfileName>**  
  
     Essa caixa de diálogo permite exibir e editar os parâmetros de configuração em um perfil.  
  
-   **Novo Perfil de Agente**  
  
     Essa caixa de diálogo permite criar um novo perfil, com a inclusão opcional dos valores de um perfil existente.  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorando a Replicação](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
