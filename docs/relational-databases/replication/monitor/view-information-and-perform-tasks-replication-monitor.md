---
title: Exibir informações e executar tarefas (Replication Monitor)
description: Saiba como exibir informações e executar várias tarefas usando o Replication Monitor no SSMS (SQL Server Management Studio).
ms.custom: seo-lt-2019
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
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
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 1a71ef96c559857e739b074915b219c38f036ff3
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322205"
---
# <a name="view-information-and-perform-tasks-using-replication-monitor"></a>Exibir informações e executar tarefas usando o Replication Monitor
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
O Replication Monitor fornece uma série de guias e opções para exibir informações e realizar diversas tarefas. Este artigo descreve os diferentes itens que podem ser exibidos e realizados ao usar o Replication Monitor. 


## <a name="for-a-publication"></a>Para uma publicação

### <a name="view-information"></a>Exibir informações
O Replication Monitor fornece as seguintes guias que incluem informações sobre a publicação selecionada:  
  
-   **Todas as Assinaturas** – essa guia exibe informações sobre todas as assinaturas para a publicação selecionada.  
  
-   **Agentes** – essa guia exibe informações sobre todos os agentes usados por uma publicação:   
    -   O Agente de Instantâneo, que é usado por todas as publicações.   
    -   O Agente de Leitor de Log, que é usado por todas as publicações transacionais.   
    -   O Agente de Leitor de Fila, que é usado pelas publicações transacionais que possuem atualização de assinaturas em fila.  
  
-   **Avisos** – essa guia permite especificar avisos e alertas para agentes.  
  
-   **Tokens do Rastreador** (somente replicação transacional) – essa guia permite medir a latência, o período decorrido entre a confirmação de uma transação no Editor e a confirmação da transação correspondente no Assinante.  
  
 Para obter mais informações sobre as opções de cada guia, selecione a guia no painel direito e, em seguida, selecione **Ajuda** na barra de menus. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
### <a name="perform-tasks"></a>Realizar tarefas
  
1.  Expanda um grupo de Editor no painel esquerdo, expanda um Editor e selecione uma publicação.   
2.  Para exibir e modificar as propriedades da publicação, clique com o botão direito do mouse na publicação e, em seguida, selecione **Propriedades**.    
3.  Para exibir informações sobre assinaturas, selecione a guia **Todas as Assinaturas**, clique com o botão direito do mouse na assinatura e selecione **Propriedades**. Também é possível acessar informações mais detalhadas e executar tarefas nessa guia. 
4.  Para exibir informações sobre agentes, selecione a guia **Agentes**. Também é possível acessar informações mais detalhadas e executar tarefas nessa guia. 
5.  Para exibir informações sobre advertências de agente e limites, selecione a guia **Avisos**. Para obter mais informações, consulte [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
6.  Para exibir informações sobre tokens de rastreamento, selecione a guia **Tokens de Rastreamento**. Para obter mais informações sobre como usar tokens de rastreamento, consulte [Medir a latência e validar as conexões para a replicação transacional](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md).  
  
## <a name="for-a-publisher"></a>Para um Editor 

### <a name="view-information"></a>Exibir informações
O Replication Monitor fornece as seguintes guias que exibem informações sobre o Publicador selecionado:   
-   **Publicações** – exibe informações sobre todas as publicações no Editor selecionado.   
-   **Lista de Observação de Assinatura** – exibe informações sobre as assinaturas de todas as publicações disponíveis no Editor selecionado que tenham erros, avisos ou o pior desempenho. Essa guia não é exibida para Distribuidores que executam as versões anteriores do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].    
-   Guia **Agentes** – exibe informações detalhadas sobre os agentes e trabalhos usados por todos os tipos de replicação. A guia também permite que você inicie e interrompa cada agente e trabalho. Para exibir mais informações sobre as opções de cada guia, clique na guia no painel direito e clique em **Ajuda** na barra de menus. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
### <a name="perform-tasks"></a>Realizar tarefas
  
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
    -   Para gerenciar os perfis do agente, clique com o botão direito do mouse no agente e então clique em **Perfil do Agente**. Para obter mais informações, consulte [Trabalhar com perfis do agente de replicação](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md).    
    -   Para iniciar um agente que não está sendo executado, clique com o botão direito do mouse no agente e então clique em **Iniciar Agente**.  
    -   Para interromper um agente que está sendo executado, clique com o botão direito do mouse no agente e então clique em **Interromper Agente**.  


## <a name="for-a-subscription"></a>Para uma assinatura 

### <a name="view-information"></a>Exibir informações
  O Replication Monitor fornece as seguintes guias que incluem informações sobre as assinaturas:    
-   **Todas as Assinaturas** – exibe informações sobre todas as assinaturas para a publicação selecionada.   
-   **Lista de Observação de Assinatura** – exibe informações sobre as assinaturas de todas as publicações disponíveis no Editor selecionado que tenham erros, avisos ou o pior desempenho. Essa guia não é exibida para Distribuidores que executam as versões anteriores do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Para obter mais informações sobre as opções de cada guia, clique na guia no painel direito e, em seguida, clique em **Ajuda** na barra de menus. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
### <a name="perform-tasks"></a>Realizar tarefas
  
1.  Expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e clique em uma publicação.   
2.  Para exibir informações sobre assinaturas, clique na guia **Todas as Assinaturas** . Para exibir somente as assinaturas em um determinado estado, por exemplo, em sincronização, selecione uma opção da lista suspensa **Mostrar** .    
3.  Para exibir e modificar as propriedades da assinatura, clique com o botão direito do mouse na assinatura  e, então, clique em **Propriedades**. Também é possível acessar informações mais detalhadas e executar tarefas nessa guia. 
  
### <a name="to-view-information-and-perform-tasks-for-subscriptions-in-the-subscription-watch-list-tab"></a>Para exibir informações e realizar tarefas para as assinaturas na guia Lista de Observação da Assinatura  
  
1.  Expanda um Grupo do publicador no painel esquerdo e clique em um Publicador.    
2.  Para exibir informações sobre assinaturas, clique na guia **Lista de Observação da Assinatura** .    
3.  Selecione o tipo de assinatura a ser exibido da lista suspensa **Mostrar \<Assinaturas <SubscriptionType>** . Para exibir somente as assinaturas em um determinado estado, por exemplo, em sincronização, selecione uma opção da lista suspensa **Mostrar** .    
4.  Para exibir e modificar as propriedades da assinatura, clique com o botão direito do mouse na assinatura  e, então, clique em **Propriedades**. Também é possível acessar informações mais detalhadas e executar tarefas nessa guia. 
  
  
## <a name="for-publication-agents"></a>Para Agentes de Publicação
O Replication Monitor fornece a guia **Agentes** , que inclui informações sobre os agentes associados com a publicação selecionada. O Agente de Distribuição e o Agente de Mesclagem estão associados a assinaturas. 
  
### <a name="view-information"></a>Exibir informações
 Essa guia exibe informações sobre os seguintes agentes:  
  
-   O Agente de Instantâneo, que é usado por todas as publicações.  
-   O Agente de Leitor de Log, que é usado por todas as publicações transacionais.  
-   O Agente de Leitor de Fila, que é usado pelas publicações transacionais habilitadas para atualização de assinaturas em fila. 
  
 Para exibir mais informações sobre as opções nessa guia, clique em **Ajuda** na barra de menu. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-publication"></a>Para exibir informações e executar tarefas para os agentes associados com uma publicação  
  
1.  Expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e clique em uma publicação.    
2.  Para exibir informações sobre agentes, clique na guia **Agentes** . Você também pode acessar informações mais detalhadas e realizar tarefas nesta guia:    
    -   Para exibir informações detalhadas sobre o agente (como mensagens informativas e qualquer mensagem de erro), clique com o botão direito do mouse no agente e então clique em **Exibir Detalhes**.  
    -   Para exibir informações detalhadas sobre o trabalho que executa o agente (como o cronograma, detalhes da etapa de trabalho e outras), clique com o botão direito do mouse no agente e então clique em **Propriedades**.    
    -   Para gerenciar os perfis do agente, clique com o botão direito do mouse no agente e então clique em **Perfil do Agente**. Para obter mais informações, consulte [Trabalhar com perfis do agente de replicação](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md).   
    -   Para iniciar um agente que não está sendo executado, clique com o botão direito do mouse no agente e então clique em **Iniciar Agente**.   
    -   Para interromper um agente que está sendo executado, clique com o botão direito do mouse no agente e então clique em **Interromper Agente**.  
  
## <a name="for-subscription-agents"></a>Para Agentes de Assinatura

### <a name="view-information"></a>Exibir informações
-   **Todas as Assinaturas** – exibe informações sobre todas as assinaturas para a publicação selecionada.  
  
-   **Lista de Observação de Assinatura** – destina-se a exibir informações sobre as assinaturas de todas as publicações disponíveis no Editor selecionado que tenham erros, avisos ou o pior desempenho. Essa guia não é exibida para Distribuidores que executam as versões anteriores do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Para obter mais informações sobre as opções de cada guia, clique na guia no painel direito e, em seguida, clique em **Ajuda** na barra de menus. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
### <a name="perform-tasks"></a>Realizar tarefas
  
1.  Expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e clique em uma publicação.    
2.  Clique na guia **Todas as Assinaturas** para exibir informações sobre as assinaturas. Você também pode acessar informações mais detalhadas e realizar tarefas nesta guia:   
    -   Para exibir informações detalhadas sobre o agente associado a uma assinatura, clique com o botão direito do mouse na assinatura e então clique em **Exibir Detalhes**. As informações detalhadas incluem: histórico do agente e mensagens de erro, estatísticas de desempenho da replicação transacional e estatísticas no nível de sincronização da replicação de mesclagem.  
  
         As guias na janela de detalhes aberta dependem do tipo de assinatura: para as assinaturas de instantâneos, a guia é **Histórico do Distribuidor para o Assinante**, para as assinaturas transacionais, as guias são **Histórico do Publicador para o Distribuidor**, **Histórico do Distribuidor para o Assinante**e **Comandos Não Distribuídos**, para as assinaturas de mesclagem, a guia é **Histórico de Sincronização**.  
  
    -   Para sincronizar uma assinatura push, clique com o botão direito do mouse na assinatura, e, depois, clique em **Iniciar Sincronização**.    
    -   Para reinicializar uma assinatura, clique com o botão direito do mouse na assinatura, e, depois, clique em **Reinicializar Assinatura**.    
    -   Para validar uma única assinatura de mesclagem, clique com o botão direito do mouse na assinatura, e, então, clique em **Validar Assinatura**. Para validar todas as assinaturas em uma publicação de mesclagem, clique com o botão direito do mouse na publicação e clique em **Validar Todas as Assinaturas**; para validar todas as assinaturas em uma publicação transacional, clique com o botão direito do mouse na publicação e clique em **Validar Assinaturas**.    
    -   Para gerenciar os perfis do agente, clique com o botão direito do mouse no agente e então clique em **Perfil do Agente**. Para obter mais informações, consulte [Trabalhar com perfis do agente de replicação](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md).  
  
### <a name="subscription-watch-list-tab"></a>Guia Lista de Observação da Assinatura 
  
1.  Expanda um Grupo do publicador no painel esquerdo e clique em um Publicador.    
2.  Clique na guia **Lista de Observação da Assinatura** , para exibir informações sobre assinaturas. Você também pode acessar informações mais detalhadas e realizar tarefas nesta guia:   
    -   Para exibir informações detalhadas sobre o agente associado a uma assinatura, clique com o botão direito do mouse na assinatura e então clique em **Exibir Detalhes**. As informações detalhadas incluem: histórico do agente e mensagens de erro, estatísticas de desempenho da replicação transacional e estatísticas no nível de sincronização da replicação de mesclagem.    
         As guias na janela de detalhes aberta dependem do tipo de assinatura: para as assinaturas de instantâneos, a guia é **Histórico do Distribuidor para o Assinante**; para as assinaturas transacionais, as guias são **Histórico do Publicador para o Distribuidor**, **Histórico do Distribuidor para o Assinante**e **Desempenho**; para as assinaturas de mesclagem, a guia é **Histórico de Sincronização**.  
  
    -   Para sincronizar uma assinatura push, clique com o botão direito do mouse na assinatura, e, depois, clique em **Iniciar Sincronização**.    
    -   Para reinicializar uma assinatura, clique com o botão direito do mouse na assinatura, e, depois, clique em **Reinicializar Assinatura**.    
    -   Para validar uma única assinatura de mesclagem, clique com o botão direito do mouse na assinatura, e, então, clique em **Validar Assinatura**. Para validar todas as assinaturas em uma publicação de mesclagem, clique com o botão direito do mouse na publicação e clique em **Validar Todas as Assinaturas**; para validar todas as assinaturas em uma publicação transacional, clique com o botão direito do mouse na publicação e clique em **Validar Assinaturas**.    
    -   Para gerenciar os perfis do agente, clique com o botão direito do mouse no agente e então clique em **Perfil do Agente**. Para obter mais informações, consulte [Trabalhar com perfis do agente de replicação](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md).  

    


## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar as propriedades da publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Exibir e modificar propriedades de assinatura push](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Exibir e modificar propriedades de assinatura pull](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)  
 [Definir limites e avisos no Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)   
 [Administração do agente de replicação](../../../relational-databases/replication/agents/replication-agent-administration.md)    
  
  
