---
title: "Adicionar Publicador | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.addpublisher.f1"
helpviewer_keywords: 
  - "caixa de diálogo Adicionar Publicador"
ms.assetid: 4b57e298-655f-42c2-82bc-25cdad94a194
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# Adicionar Publicador
  A caixa de diálogo **Adicionar Publicador** permite a adição de um ou mais publicadores no painel esquerdo do Replication Monitor. Depois de adicionar um Publicador, selecioná-lo no painel esquerdo mostrará informações sobre o Publicador no painel à direita.  
  
## Opções  
 **Adicionar**  
 Clique para selecionar um tipo de editor para adicionar, que inicia o **conectar ao servidor** caixa de diálogo. As opções são:  
  
-   **Adicionar Editor SQL Server…**  
  
     Conectar-se ao Editor usando a caixa de diálogo **Conectar ao Servidor** .  
  
-   **Adicionar Editor Oracle…**  
  
     Conecte-se ao Distribuidor da [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com Editor Oracle usando a caixa de diálogo **Conectar ao Servidor** .  
  
-   **Especificar um Distribuidor e Adicionar seus Publicadores…**  
  
     Conecte-se ao Distribuidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associado a um ou mais Publicadores usando a caixa de diálogo **Conectar ao Servidor** .  
  
 Depois de se conectar com êxito ao Publicador ou ao Distribuidor, o nome de cada publicador e seu distribuidor serão exibidos na grade, na parte superior da caixa de diálogo.  
  
> [!NOTE]  
>  O Distribuidor e o Publicador geralmente são executados na mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas o Distribuidor pode ser executado em outra instância (essa configuração é referenciada como Distribuidor remoto).  
  
 **Remover**  
 Selecione um publicador na grade, na parte superior da caixa de diálogo e clique em **Remover** para remover o editor da lista de editores a ser adicionado.  
  
> [!NOTE]  
>  Esse botão não pode ser usado para remover um Publicador já exibido no Replication Monitor. Para remover um publicador já exibido com o botão direito no painel esquerdo do Replication Monitor e clique em Editor **Remover**.  
  
 **Conectar automaticamente quando o Replication Monitor for iniciado**  
 Selecione para permitir que o Replication Monitor faça conexão automática com o Distribuidor e recupere informações de status para o Publicador selecionado na grade, na parte superior da caixa de diálogo. Se essa caixa de seleção estiver desmarcada, você deve conectar-se manualmente depois de iniciar o Replication Monitor: clique no publicador no painel esquerdo do Replication Monitor e, em seguida, clique em **conectar**.  
  
 **Atualizar automaticamente o status deste Publicador e de suas publicações**  
 Selecione para permitir que o Replication Monitor atualize automaticamente o status do Publicador selecionado na grade, na parte superior da caixa de diálogo. Se essa opção for selecionada, o Replication Monitor pesquisará no Distribuidor informações de status sobre o Publicador e suas publicações. O intervalo da sondagem é definido pela opção **Taxa de Atualização** . Para obter mais informações sobre atualização no Replication Monitor, consulte [cache, atualização e monitorar o desempenho da replicação](../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
 **Taxa de atualização**  
 Insira um valor (em segundos) para especificar a frequência de sondagem do Replication Monitor no Distribuidor, por status. Valores mais baixos resultam em sondagens mais frequentes, que podem afetar o desempenho no Distribuidor se você estiver monitorando um grande número de Publicadores. É recomendado que você teste seu sistema para determinar um valor apropriado. A configuração da **Taxa de Atualização** será também usada se você selecionar **Atualização Automática** em qualquer uma das janelas de detalhes no Replication Monitor.  
  
 **Mostrar este Publicador no grupo a seguir**  
 Selecione um grupo de Publicadores na lista. O Publicador é exibido nesse grupo no painel esquerdo. Grupos fornecem uma forma de organizar Publicadores e não causam nenhum efeito em funções de replicação. Se nenhum grupo estiver definido ou você quer criar um novo, clique em **Novo Grupo**.  
  
 **Novo grupo**  
 Clique para criar um novo grupo de Publicadores. Um grupo de Publicadores é um modo conveniente de organizar Publicadores no Replication Monitor. Grupos não afetam a replicação de dados ou a relação entre servidores em uma topologia de replicação.  
  
## Consulte também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Replicação de monitoramento](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  