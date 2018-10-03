---
title: Exibir informações e executar tarefas para os agentes associados com uma assinatura (Replication Monitor) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], viewing information
- viewing replication agent information
- agents [SQL Server replication], tasks in Replication Monitor
ms.assetid: fbb59d31-2424-4552-9195-0da8d83e755f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 872053f2f48518fc3586369c46677e21287866a3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48111286"
---
# <a name="view-information-and-perform-tasks-for-the-agents-associated-with-a-subscription-replication-monitor"></a>Exibir informações e executar tarefas para os agentes associados a uma assinatura (Replication Monitor)
  O Replication Monitor fornece duas guias que permitem acesso às informações sobre o(s) agente(s) associado(s) a uma assinatura:  
  
-   **Todas as Assinaturas**  
  
     Essa guia exibe informações sobre todas as assinaturas para a publicação selecionada.  
  
-   **Lista de Observação da Assinatura**  
  
     Essa guia destina-se a exibir informações sobre as assinaturas de todas as publicações disponíveis no Publicador selecionado que tenham erros, avisos ou o pior desempenho. Essa guia não é exibida para Distribuidores que executam as versões anteriores do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Para obter mais informações sobre as opções de cada guia, clique na guia no painel direito e, em seguida, clique em **Ajuda** na barra de menus. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-subscription-all-subscriptions-tab"></a>Para exibir informações e executar tarefas para os agentes associados a uma assinatura (guia Todas as Assinaturas)  
  
1.  Expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e clique em uma publicação.  
  
2.  Clique na guia **Todas as Assinaturas** para exibir informações sobre as assinaturas. Você também pode acessar informações mais detalhadas e realizar tarefas nesta guia:  
  
    -   Para exibir informações detalhadas sobre o agente associado a uma assinatura, clique com o botão direito do mouse na assinatura e então clique em **Exibir Detalhes**. As informações detalhadas incluem: histórico do agente e mensagens de erro, estatísticas de desempenho da replicação transacional e estatísticas no nível de sincronização da replicação de mesclagem.  
  
         As guias na janela de detalhes aberta dependem do tipo de assinatura: para as assinaturas de instantâneos, a guia é **Histórico do Distribuidor para o Assinante**, para as assinaturas transacionais, as guias são **Histórico do Publicador para o Distribuidor**, **Histórico do Distribuidor para o Assinante**e **Comandos Não Distribuídos**, para as assinaturas de mesclagem, a guia é **Histórico de Sincronização**.  
  
    -   Para sincronizar uma assinatura push, clique com o botão direito do mouse na assinatura, e, depois, clique em **Iniciar Sincronização**.  
  
    -   Para reinicializar uma assinatura, clique com o botão direito do mouse na assinatura, e, depois, clique em **Reinicializar Assinatura**.  
  
    -   Para validar uma única assinatura de mesclagem, clique com o botão direito do mouse na assinatura, e, então, clique em **Validar Assinatura**. Para validar todas as assinaturas em uma publicação de mesclagem, clique com o botão direito do mouse na publicação e clique em **Validar Todas as Assinaturas**; para validar todas as assinaturas em uma publicação transacional, clique com o botão direito do mouse na publicação e clique em **Validar Assinaturas**.  
  
    -   Para gerenciar os perfis do agente, clique com o botão direito do mouse no agente e então clique em **Perfil do Agente**. Para obter mais informações, consulte [Trabalhar com perfis do agente de replicação](../agents/replication-agent-profiles.md).  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-subscription-subscription-watch-list-tab"></a>Para exibir as informações e executar tarefas nos agentes associados a uma assinatura (guia Lista de Observação da Assinatura)  
  
1.  Expanda um Grupo do publicador no painel esquerdo e clique em um Publicador.  
  
2.  Clique na guia **Lista de Observação da Assinatura** , para exibir informações sobre assinaturas. Você também pode acessar informações mais detalhadas e realizar tarefas nesta guia:  
  
    -   Para exibir informações detalhadas sobre o agente associado a uma assinatura, clique com o botão direito do mouse na assinatura e então clique em **Exibir Detalhes**. As informações detalhadas incluem: histórico do agente e mensagens de erro, estatísticas de desempenho da replicação transacional e estatísticas no nível de sincronização da replicação de mesclagem.  
  
         As guias na janela de detalhes aberta dependem do tipo de assinatura: para as assinaturas de instantâneos, a guia é **Histórico do Distribuidor para o Assinante**; para as assinaturas transacionais, as guias são **Histórico do Publicador para o Distribuidor**, **Histórico do Distribuidor para o Assinante**e **Desempenho**; para as assinaturas de mesclagem, a guia é **Histórico de Sincronização**.  
  
    -   Para sincronizar uma assinatura push, clique com o botão direito do mouse na assinatura, e, depois, clique em **Iniciar Sincronização**.  
  
    -   Para reinicializar uma assinatura, clique com o botão direito do mouse na assinatura, e, depois, clique em **Reinicializar Assinatura**.  
  
    -   Para validar uma única assinatura de mesclagem, clique com o botão direito do mouse na assinatura, e, então, clique em **Validar Assinatura**. Para validar todas as assinaturas em uma publicação de mesclagem, clique com o botão direito do mouse na publicação e clique em **Validar Todas as Assinaturas**; para validar todas as assinaturas em uma publicação transacional, clique com o botão direito do mouse na publicação e clique em **Validar Assinaturas**.  
  
    -   Para gerenciar os perfis do agente, clique com o botão direito do mouse no agente e então clique em **Perfil do Agente**. Para obter mais informações, consulte [Trabalhar com perfis do agente de replicação](../agents/replication-agent-profiles.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibir informações e realizar tarefas para uma assinatura &#40;Replication Monitor&#41;](view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [Monitorando a Replicação](../monitoring-replication.md)  
  
  
