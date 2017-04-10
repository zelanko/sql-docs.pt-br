---
title: "Suporte de alta disponibilidade para bancos de dados OLTP na mem&#243;ria | Microsoft Docs"
ms.custom: ""
ms.date: "08/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2113a916-3b1e-496c-8650-7f495e492510
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# Suporte de alta disponibilidade para bancos de dados OLTP na mem&#243;ria
  Os bancos de dados que contêm tabelas com otimização de memória, com ou sem procedimentos armazenados compilados nativos, são totalmente compatíveis com Grupos de Disponibilidade AlwaysOn.  Não há nenhuma diferença na configuração e no suporte para bancos de dados que contêm objetos do [!INCLUDE[hek_2](../../includes/hek-2-md.md)] em comparação a aqueles sem.  
  
 Quando um banco de dados OLTP in-memory for implantado em uma configuração de Grupo de Disponibilidade AlwaysOn, as alterações nas tabelas com otimização de memória na réplica primária serão aplicadas à memória para as tabelas nas réplicas secundárias, quando REDO for aplicado. Isso significa que o failover para uma réplica secundária pode ser muito rápido, pois os dados já estão na memória. Além disso, as tabelas estão disponíveis para consultas em réplicas secundárias que foram configuradas para acesso de leitura.  
  
## Grupos de Disponibilidade AlwaysOn e bancos de dados OLTP in-memory  
 Configurar bancos de dados com componentes [!INCLUDE[hek_2](../../includes/hek-2-md.md)] fornece o seguinte:  
  
-   **Uma experiência totalmente integrada**   
    Você pode configurar seus bancos de dados que contêm tabelas com otimização de memória usando o mesmo assistente com o mesmo nível de suporte para réplicas secundárias síncronas e assíncronas. Além disso, o monitoramento de integridade é fornecido usando o já familiar painel do AlwaysOn no SQL Server Management Studio.  
  
-   **Tempo de Failover comparável**   
    As réplicas secundárias mantêm o estado na memória das tabelas duráveis com otimização de memória. No caso de failover automático ou forçado, o tempo de failover para o novo primário é comparável a tabelas de bases de disco, já que nenhuma recuperação é necessária. As tabelas com otimização de memória criadas como SCHEMA_ONLY têm suporte nesta configuração. No entanto, as alterações para essas tabelas não são registradas e, portanto, nenhum dado existirá nessas tabelas na réplica secundária.  
  
-   **Secundária Legível**   
    Você pode acessar e consultar tabelas com otimização de memória na réplica secundária se ela tiver sido configurada para acesso de leitura. No [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o carimbo de data/hora de leitura na réplica secundária está em sincronização próxima com o carimbo de data/hora de leitura na réplica primária, o que significa que as alterações na réplica primária se tornarão visíveis na secundária muito rapidamente. Esse comportamento de sincronização próxima é diferente do OLTP in-memory do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
## Instância de Clustering de Failover (FCI) e bancos de dados OLTP na memória  
 Para obter alta disponibilidade em uma configuração de armazenamento compartilhado, você pode configurar o clustering de failover nas instâncias com um ou mais bancos de dados com tabelas com otimização de memória. Você precisa considerar os seguintes fatores como parte da configuração de uma FCI.  
  
-   **Objetivo de tempo de recuperação**   
    O tempo de failover provavelmente será maior conforme as tabelas com otimização de memória devam ser carregadas na memória antes que o banco de dados seja disponibilizado.  
  
-   **Tabelas SCHEMA_ONLY**   
    Lembre-se de que as tabelas SCHEMA_ONLY estarão vazias e sem linhas após o failover. Isso é projetado e definido pelo aplicativo. E é exatamente o mesmo comportamento de quando você reinicia um banco de dados [!INCLUDE[hek_2](../../includes/hek-2-md.md)] com uma ou mais tabelas SCHEMA_ONLY.  
  
## Suporte para replicação de transação em OLTP na memória  
 As tabelas que atuam como assinantes de replicação transacional, com exceção da replicação transacional ponto a ponto, podem ser configuradas como tabelas com otimização de memória. Outras configurações de replicação não são compatíveis com tabelas com otimização de memória.  Para obter mais informações, veja [Replicação para assinantes de tabela com otimização de memória](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md).  
  
## Consulte também  
 [Grupos de Disponibilidade AlwaysOn (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Secundárias ativas: réplicas secundárias legíveis (Grupos de Disponibilidade AlwaysOn)](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Replicação para assinantes de tabela com otimização de memória](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)  
  
  