---
title: Exibir informações e executar tarefas usando o Replication Monitor | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- viewing publication information
- publications [SQL Server replication], viewing information
- publications [SQL Server replication], Replication Monitor tasks
ms.assetid: 92e28a07-d6a7-461b-a0b3-bd9bc6afcbe5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 400db44d053caf131ef13947adbd0154875995cf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62667121"
---
# <a name="view-information-and-perform-tasks-using-replication-monitor"></a>Exibir informações e executar tarefas usando o Replication Monitor
O Replication Monitor fornece uma série de guias e opções para exibir informações e realizar diversas tarefas. Este artigo descreve os diferentes itens que podem ser exibidos e realizados ao usar o Replication Monitor.

## <a name="for-a-publication"></a>Para uma publicação

### <a name="view-information"></a>Exibir informações

  O Replication Monitor fornece as seguintes guias que incluem informações sobre a publicação selecionada:  
  
-   **Todas as assinaturas** – essa guia exibe informações sobre todas as assinaturas para a publicação selecionada.  
  
-   **Agentes** – essa guia exibe informações sobre todos os agentes usados por uma publicação:  
  
    -   O Agente de Instantâneo, que é usado por todas as publicações.    
    -   O Agente de Leitor de Log, que é usado por todas as publicações transacionais.    
    -   O Agente de Leitor de Fila, que é usado pelas publicações transacionais que possuem atualização de assinaturas em fila.  
  
-   **Avisos** (para os distribuidores que executam [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e posteriores)   
    -   Essa guia permite especificar avisos e alertas para agentes.  
  
-   **Tokens de rastreamento** (somente replicação transacional, para [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] distribuidores que executam e posteriores)  
  
     Essa guia permite medir a latência, o período decorrido entre a confirmação de uma transação no Publicador e a confirmação da transação correspondente no Assinante.  
  
 Para obter mais informações sobre as opções de cada guia, clique na guia no painel direito e, em seguida, clique em **Ajuda** na barra de menus. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
### <a name="perform-tasks"></a>Realizar tarefas
  
1.  Expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e clique em uma publicação.    
2.  Para exibir e modificar as propriedades da publicação, clique com o botão direito do mouse na publicação e, em seguida, clique em **Propriedades**.    
3.  Para exibir informações sobre assinaturas, clique na guia **Todas as Assinaturas** .  
  
     Para exibir e modificar as propriedades da assinatura, clique com o botão direito do mouse na assinatura  e, então, clique em **Propriedades**. Você também pode acessar informações mais detalhadas e executar tarefas nessa guia. Para obter mais informações, consulte [Exibir informações e executar tarefas usando o Replication Monitor](view-information-and-perform-tasks-replication-monitor.md).  
  
4.  Para exibir informações sobre agentes, clique na guia **agentes** . Você também pode acessar informações mais detalhadas e executar tarefas nessa guia. Para obter mais informações, consulte [Exibir informações e executar tarefas usando o Replication Monitor](view-information-and-perform-tasks-replication-monitor.md).    
5.  Para exibir informações sobre limites e avisos do agente, clique na guia **avisos** . Para obter mais informações, consulte [definir limites e avisos no Replication Monitor](set-thresholds-and-warnings-in-replication-monitor.md).   
6.  Para exibir informações sobre tokens de rastreamento, clique na guia **tokens de rastreamento** . Para obter mais informações sobre como usar tokens de rastreamento, consulte [medir latência e validar conexões para replicação transacional](measure-latency-and-validate-connections-for-transactional-replication.md).  
  
## <a name="for-a-publisher"></a>Para um Editor
  O Replication Monitor fornece as seguintes guias que exibem informações sobre o Publicador selecionado:  
  
-   **Publicações** – essa guia exibe informações sobre todas as publicações no Publicador selecionado.  
  
-   **Lista de observação da assinatura** -esta guia destina-se a exibir informações sobre assinaturas de todas as publicações disponíveis no Publicador selecionado que têm erros, avisos ou o desempenho mais baixo. Essa guia não é exibida para Distribuidores que executam as versões anteriores do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
-   Guia **agentes** – essa guia exibe informações detalhadas sobre os agentes e trabalhos que são usados por todos os tipos de replicação. A guia também permite que você inicie e interrompa cada agente e trabalho.  
  
 Para exibir mais informações sobre as opções de cada guia, clique na guia no painel direito e clique em **Ajuda** na barra de menus. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
### <a name="view-information-and-perform-tasks"></a>Exibir informações e executar tarefas
  
1.  Expanda um Grupo do publicador no painel esquerdo e clique em um Publicador.    
2.  Para exibir informações sobre todas as publicações, clique na guia **Publicações** .    
3.  Para exibir informações sobre assinaturas, clique na guia **Lista de Observação da Assinatura** . Você também pode acessar informações mais detalhadas e realizar tarefas a partir dessa guia:    
    -   Para exibir informações detalhadas sobre o agente associado a uma assinatura, clique com o botão direito do mouse na assinatura e então clique em **Exibir Detalhes**.    
    -   Para exibir as propriedades de uma assinatura, clique com o botão direito do mouse na assinatura e então clique em **Propriedades**.    
    -   Para sincronizar uma assinatura push, clique com o botão direito do mouse na assinatura, e, depois, clique em **Iniciar Sincronização**.    
    -   Para reinicializar uma assinatura, clique com o botão direito do mouse na assinatura, e, depois, clique em **Reinicializar Assinatura**.   
4.  Para exibir informações sobre agentes, clique na guia **Agentes** . Você também pode acessar informações mais detalhadas e realizar tarefas nesta guia:    
    -   Para exibir informações detalhadas sobre o agente (como mensagens informativas e qualquer mensagem de erro), clique com o botão direito do mouse no agente e então clique em **Exibir Detalhes**.    
    -   Para exibir informações detalhadas sobre o trabalho que executa o agente (como o cronograma, detalhes da etapa de trabalho e outras), clique com o botão direito do mouse no agente e então clique em **Propriedades**.    
    -   Para gerenciar os perfis do agente, clique com o botão direito do mouse no agente e então clique em **Perfil do Agente**. Para obter mais informações, consulte [Trabalhar com perfis do agente de replicação](../agents/replication-agent-profiles.md).    
    -   Para iniciar um agente que não está sendo executado, clique com o botão direito do mouse no agente e então clique em **Iniciar Agente**.    
    -   Para interromper um agente que está sendo executado, clique com o botão direito do mouse no agente e então clique em **Interromper Agente**.  
  
## <a name="for-a-subscription"></a>Para uma assinatura 

  O Replication Monitor fornece as seguintes guias que incluem informações sobre as assinaturas:  
  
-   **Todas as assinaturas** – essa guia exibe informações sobre todas as assinaturas para a publicação selecionada.  
  
-   **Lista de observação da assinatura** -esta guia destina-se a exibir informações sobre assinaturas de todas as publicações disponíveis no Publicador selecionado que têm erros, avisos ou o desempenho mais baixo. Essa guia não é exibida para Distribuidores que executam as versões anteriores do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Para obter mais informações sobre as opções de cada guia, clique na guia no painel direito e, em seguida, clique em **Ajuda** na barra de menus. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
### <a name="all-subscriptions-tab"></a>Guia todas as assinaturas  
  
1.  Expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e clique em uma publicação.   
2.  Para exibir informações sobre assinaturas, clique na guia **Todas as Assinaturas** . Para exibir somente as assinaturas em um determinado estado, por exemplo, em sincronização, selecione uma opção da lista suspensa **Mostrar** .   
3.  Para exibir e modificar as propriedades da assinatura, clique com o botão direito do mouse na assinatura  e, então, clique em **Propriedades**. Você também pode acessar informações mais detalhadas e executar tarefas nessa guia. Para obter mais informações, consulte [Exibir informações e executar tarefas usando o Replication Monitor](view-information-and-perform-tasks-replication-monitor.md).  
  
### <a name="subscription-watch-list-tab"></a>Guia Lista de Observação da Assinatura  
  
1.  Expanda um Grupo do publicador no painel esquerdo e clique em um Publicador.   
2.  Para exibir informações sobre assinaturas, clique na guia **Lista de Observação da Assinatura** .  
3.  Selecione o tipo de assinatura a ser exibido da lista suspensa **Mostrar \<Assinaturas <SubscriptionType>** . Para exibir somente as assinaturas em um determinado estado, por exemplo, em sincronização, selecione uma opção da lista suspensa **Mostrar** .    
4.  Para exibir e modificar as propriedades da assinatura, clique com o botão direito do mouse na assinatura  e, então, clique em **Propriedades**. Você também pode acessar informações mais detalhadas e executar tarefas nessa guia. Para obter mais informações, consulte [Exibir informações e executar tarefas usando o Replication Monitor](view-information-and-perform-tasks-replication-monitor.md).  

## <a name="for-publication-agents"></a>Para Agentes de Publicação

  O Replication Monitor fornece a guia **Agentes** , que inclui informações sobre os agentes associados com a publicação selecionada. As Agente de Distribuição e Agente de Mesclagem estão associadas a assinaturas; para obter mais informações, consulte [Exibir informações e executar tarefas usando o Replication Monitor](view-information-and-perform-tasks-replication-monitor.md).  
  
 Essa guia exibe informações sobre os seguintes agentes:    
-   O Agente de Instantâneo, que é usado por todas as publicações.    
-   O Agente de Leitor de Log, que é usado por todas as publicações transacionais.    
-   O Agente de Leitor de Fila, que é usado pelas publicações transacionais habilitadas para atualização de assinaturas em fila.  
  
 Para exibir mais informações sobre as opções nessa guia, clique em **Ajuda** na barra de menu. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
### <a name="view-information-and-perform-tasks"></a>Exibir informações e executar tarefas 
  
1.  Expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e clique em uma publicação.    
2.  Para exibir informações sobre agentes, clique na guia **Agentes** . Você também pode acessar informações mais detalhadas e realizar tarefas nesta guia:  
  
    -   Para exibir informações detalhadas sobre o agente (como mensagens informativas e qualquer mensagem de erro), clique com o botão direito do mouse no agente e então clique em **Exibir Detalhes**.    
    -   Para exibir informações detalhadas sobre o trabalho que executa o agente (como o cronograma, detalhes da etapa de trabalho e outras), clique com o botão direito do mouse no agente e então clique em **Propriedades**.    
    -   Para gerenciar os perfis do agente, clique com o botão direito do mouse no agente e então clique em **Perfil do Agente**. Para obter mais informações, consulte [Trabalhar com perfis do agente de replicação](../agents/replication-agent-profiles.md).  
    -   Para iniciar um agente que não está sendo executado, clique com o botão direito do mouse no agente e então clique em **Iniciar Agente**.  
      -   Para interromper um agente que está sendo executado, clique com o botão direito do mouse no agente e então clique em **Interromper Agente**.  

## <a name="for-subscription-agents"></a>Para Agentes de Assinatura

### <a name="view-information-and-perform-tasks"></a>Exibir informações e executar tarefas
  O Replication Monitor fornece duas guias que permitem acesso às informações sobre o(s) agente(s) associado(s) a uma assinatura:  
  
-   **Todas as assinaturas** – essa guia exibe informações sobre todas as assinaturas para a publicação selecionada.  
  
-   **Lista de observação da assinatura** -esta guia destina-se a exibir informações sobre assinaturas de todas as publicações disponíveis no Publicador selecionado que têm erros, avisos ou o desempenho mais baixo. Essa guia não é exibida para Distribuidores que executam as versões anteriores do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Para obter mais informações sobre as opções de cada guia, clique na guia no painel direito e, em seguida, clique em **Ajuda** na barra de menus. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
### <a name="view-information-and-perform-tasks"></a>Exibir informações e executar tarefas 
  
1.  Expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e clique em uma publicação.   
2.  Clique na guia **Todas as Assinaturas** para exibir informações sobre as assinaturas. Você também pode acessar informações mais detalhadas e realizar tarefas nesta guia:  
  
    -   Para exibir informações detalhadas sobre o agente associado a uma assinatura, clique com o botão direito do mouse na assinatura e então clique em **Exibir Detalhes**. As informações detalhadas incluem: histórico do agente e mensagens de erro, estatísticas de desempenho da replicação transacional e estatísticas no nível de sincronização da replicação de mesclagem.    
         As guias na janela de detalhes aberta dependem do tipo de assinatura: para as assinaturas de instantâneos, a guia é **Histórico do Distribuidor para o Assinante**, para as assinaturas transacionais, as guias são **Histórico do Publicador para o Distribuidor**, **Histórico do Distribuidor para o Assinante**e **Comandos Não Distribuídos**, para as assinaturas de mesclagem, a guia é **Histórico de Sincronização**.    
    -   Para sincronizar uma assinatura push, clique com o botão direito do mouse na assinatura, e, depois, clique em **Iniciar Sincronização**.    
    -   Para reinicializar uma assinatura, clique com o botão direito do mouse na assinatura, e, depois, clique em **Reinicializar Assinatura**.    
    -   Para validar uma única assinatura de mesclagem, clique com o botão direito do mouse na assinatura, e, então, clique em **Validar Assinatura**. Para validar todas as assinaturas em uma publicação de mesclagem, clique com o botão direito do mouse na publicação e clique em **Validar Todas as Assinaturas**; para validar todas as assinaturas em uma publicação transacional, clique com o botão direito do mouse na publicação e clique em **Validar Assinaturas**.    
    -   Para gerenciar os perfis do agente, clique com o botão direito do mouse no agente e então clique em **Perfil do Agente**. Para obter mais informações, consulte [Trabalhar com perfis do agente de replicação](../agents/replication-agent-profiles.md).  
  
### <a name="view-information-and-perform-tasks"></a>Exibir informações e executar tarefas
  
1.  Expanda um Grupo do publicador no painel esquerdo e clique em um Publicador.   
2.  Clique na guia **Lista de Observação da Assinatura** , para exibir informações sobre assinaturas. Você também pode acessar informações mais detalhadas e realizar tarefas nesta guia:    
    -   Para exibir informações detalhadas sobre o agente associado a uma assinatura, clique com o botão direito do mouse na assinatura e então clique em **Exibir Detalhes**. As informações detalhadas incluem: histórico do agente e mensagens de erro, estatísticas de desempenho da replicação transacional e estatísticas no nível de sincronização da replicação de mesclagem.    
         As guias na janela de detalhes aberta dependem do tipo de assinatura: para as assinaturas de instantâneos, a guia é **Histórico do Distribuidor para o Assinante**; para as assinaturas transacionais, as guias são **Histórico do Publicador para o Distribuidor**, **Histórico do Distribuidor para o Assinante**e **Desempenho**; para as assinaturas de mesclagem, a guia é **Histórico de Sincronização**.    
    -   Para sincronizar uma assinatura push, clique com o botão direito do mouse na assinatura, e, depois, clique em **Iniciar Sincronização**.    
    -   Para reinicializar uma assinatura, clique com o botão direito do mouse na assinatura, e, depois, clique em **Reinicializar Assinatura**.    
    -   Para validar uma única assinatura de mesclagem, clique com o botão direito do mouse na assinatura, e, então, clique em **Validar Assinatura**. Para validar todas as assinaturas em uma publicação de mesclagem, clique com o botão direito do mouse na publicação e clique em **Validar Todas as Assinaturas**; para validar todas as assinaturas em uma publicação transacional, clique com o botão direito do mouse na publicação e clique em **Validar Assinaturas**.    
    -   Para gerenciar os perfis do agente, clique com o botão direito do mouse no agente e então clique em **Perfil do Agente**. Para obter mais informações, consulte [Trabalhar com perfis do agente de replicação](../agents/replication-agent-profiles.md).  
  

## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar as propriedades da publicação](../publish/view-and-modify-publication-properties.md)   
 [Monitorando a Replicação](../monitoring-replication.md)  
  