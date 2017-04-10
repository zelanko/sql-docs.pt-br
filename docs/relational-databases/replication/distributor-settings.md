---
title: "Configura&#231;&#245;es de distribuidor | Microsoft Docs"
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
  - "sql13.rep.monitor.DistributorSettings.f1"
helpviewer_keywords: 
  - "caixa de diálogo Configurações de Distribuidor"
ms.assetid: 8276a521-bdd1-4783-bdb6-7ab43499c0ca
caps.latest.revision: 10
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 10
---
# Configura&#231;&#245;es de distribuidor
  A caixa de diálogo **Configurações do Distribuidor** permite alterar configurações para Distribuidores que foram adicionados ao painel esquerdo no Replication Monitor.  
  
## Opções  
 **Conectar automaticamente quando o Replication Monitor for iniciado**  
 Selecione para permitir que o Monitor de Replicação conecte-se ao Distribuidor e recupere informações de status.  
  
 **Conexão**  
 Clique para exibir o **conectar ao servidor** caixa de diálogo. Isso permite que você visualize e altere as credenciais e propriedades de conexão que o Replication Monitor usa para se conectar ao Distribuidor.  
  
 **Atualizar automaticamente o status deste Distribuidor e de suas publicações**  
 Selecione para permitir que o Monitor de Replicação atualize automaticamente o status para o Distribuidor. Se essa opção for selecionada, o Replication Monitor pesquisará no Distribuidor informações de status com base no intervalo de sondagem pela opção **Taxa de atualização** . Para obter mais informações sobre atualização no Replication Monitor, consulte [Caching, Refresh, and Replication Monitor Performance](../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
 **Taxa de atualização**  
 Insira um valor (em segundos) para especificar a frequência de sondagem do Replication Monitor no Distribuidor, por status. Valores inferiores resultam em sondagem mais frequente. Isto poderá afetar o desempenho no Distribuidor se você estiver monitorando muitos Publicadores. Recomendamos que você teste seu sistema para determinar um valor apropriado. A configuração da **Taxa de Atualização** será também usada se você selecionar **Atualização Automática** em qualquer uma das janelas de detalhes no Replication Monitor.  
  
 **Mostre para todos os Publicadores deste Distribuidor no grupo a seguir**  
 Selecione um grupo de Publicadores na lista. O Publicador é exibido nesse grupo no painel esquerdo. Grupos fornecem uma forma de organizar Publicadores e não afetam a maneira como a replicação funciona.  
  
 **Novo grupo**  
 Clique para criar um novo grupo de Publicadores. Um grupo de Publicadores é um modo conveniente de organizar Publicadores no Replication Monitor. Grupos não afetam a replicação de dados ou a relação entre servidores em uma topologia de replicação.  
  
## Consulte também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Replicação de monitoramento](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  