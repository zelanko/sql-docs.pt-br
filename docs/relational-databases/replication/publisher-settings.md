---
title: "Configura&#231;&#245;es do Publicador | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.publishersettings.f1"
helpviewer_keywords: 
  - "caixa de diálogo Configurações do Publicador"
ms.assetid: 4fb70427-082d-4179-82a1-34b235accc43
caps.latest.revision: 19
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 19
---
# Configura&#231;&#245;es do Publicador
  A caixa de diálogo **Configurações do Publicador** permite alterar configurações para Publicadores adicionados ao painel esquerdo no Replication Monitor.  
  
## Opções  
 **Conexão do Publicador**  
 Clique para iniciar o **conectar ao servidor** caixa de diálogo que permite que você exiba e altere as propriedades de conexão e credenciais Replication Monitor usa para se conectar a um publicador.  
  
 **Conexão do Distribuidor**  
 Exibido somente se o Publicador usar um Distribuidor remoto. Clique para iniciar a caixa de diálogo **Conectar ao Servidor** que permite que você visualize e altere as credenciais e propriedades de conexão que o Replication Monitor usa para se conectar a um Distribuidor remoto.  
  
 **Conectar automaticamente quando o Replication Monitor for iniciado**  
 Selecione para permitir que o Replication Monitor faça conexão automática com o Distribuidor e recupere informações de status para o Publicador selecionado na grade, na parte superior da caixa de diálogo. Se essa caixa de seleção estiver desmarcada, você deve conectar-se manualmente depois de iniciar o Replication Monitor: clique no publicador no painel esquerdo do Replication Monitor e, em seguida, clique em **conectar**.  
  
 **Atualizar automaticamente o status deste Publicador e de suas publicações**  
 Selecione para permitir que o Replication Monitor atualize automaticamente o status do Publicador selecionado na grade, na parte superior da caixa de diálogo. Se essa opção for selecionada, o Replication Monitor pesquisará no Distribuidor informações de status sobre o Publicador e suas publicações. O intervalo da sondagem é definido pela opção **Taxa de Atualização** . Para obter mais informações sobre atualização no Replication Monitor, consulte [cache, atualização e monitorar o desempenho da replicação](../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
 **Taxa de atualização**  
 Insira um valor (em segundos) para especificar a frequência de sondagem do Replication Monitor no Distribuidor, por status. Valores mais baixos resultam em sondagens mais frequentes, que podem afetar o desempenho no Distribuidor se você estiver monitorando um grande número de Publicadores. É recomendado que você teste seu sistema para determinar um valor apropriado. A configuração da **Taxa de Atualização** será também usada se você selecionar **Atualização Automática** em qualquer uma das janelas de detalhes no Replication Monitor.  
  
 **Mostrar este Publicador no grupo a seguir**  
 Selecione um grupo de Publicadores na lista. O Publicador é exibido nesse grupo no painel esquerdo. Grupos fornecem uma forma de organizar Publicadores e não causam nenhum efeito em funções de replicação.  
  
 **Novo grupo**  
 Clique para criar um novo grupo de Publicadores. Um grupo de Publicadores é um modo conveniente de organizar Publicadores no Replication Monitor. Grupos não afetam a replicação de dados ou a relação entre servidores em uma topologia de replicação.  
  
## Consulte também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Replicação de monitoramento](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  