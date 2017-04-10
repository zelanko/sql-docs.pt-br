---
title: "Sincronizar dados | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "sincronização [replicação do SQL Server], sobre a sincronização"
  - "sincronização de replicação de mesclagem [replicação do SQL Server]"
  - "scripts [replicação do SQL Server], sincronização e"
  - "sincronização [replicação do SQL Server]"
  - "replicação de instantâneo [SQL Server], sincronização"
  - "replicação transacional, sincronização"
  - "assinaturas [replicação do SQL Server], sincronizando"
  - "execução de script sob demanda"
  - "replicação [SQL Server], sincronização"
  - "scripts [replicação do SQL Server]"
ms.assetid: 724802f7-7d69-46d3-a330-bd8aa7f53114
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Sincronizar dados
  Sincronizando dados se refere ao processo de alterações de dados e esquemas sendo propagadas entre o Publicador e os Assinantes após o instantâneo inicial ter sido aplicado ao Assinante. A sincronização pode acontecer:  
  
-   Continuamente, o que é típico para replicação transacional.  
  
-   Sob demanda, o que é típico para replicação de mesclagem.  
  
-   Em um agendamento, o que é típico para replicação de instantâneo.  
  
 Quando uma assinatura é sincronizada, diferentes processos acontecem baseados no tipo de replicação que você está usando:  
  
-   Replicação de instantâneo A sincronização significa que o Agente de Distribuição reaplicou o instantâneo ao Assinante para que o esquema e os dados no banco de dados da assinatura sejam consistentes com o bando de dados da publicação.  
  
     Se alterações nos dados ou no esquema tiverem sido feitas no Publicador, um novo instantâneo deve ser gerado para propagar as modificações ao Assinante.  
  
-   Replicação transacional. A sincronização significa que o Agente de Distribuição transfere atualizações, inserções, exclusões e quaisquer outras modificações do banco de dados de distribuição ao Assinante.  
  
-   Replicação de mesclagem. A sincronização significa que o Agente de Mesclagem carrega alterações do Assinante ao Publicador e depois baixa as alterações do Publicador ao Assinante. Conflitos, se houver, são detectados e resolvidos. Os dados são convergidos e o Publicador e todos os Assinantes eventualmente acabam com os mesmos valores de dados. Se os conflitos forem detectados e resolvidos, o trabalho que foi confirmado por alguns usuários é alterado para resolver o conflito de acordo com a política que você definir.  
  
 Publicações de instantâneo atualizam completamente o esquema no Assinante cada vez que ocorrer uma sincronização, assim todas as alterações de esquema são aplicadas ao Assinante. Replicação transacional e replicação de mesclagem também oferecem suporte às alterações de esquema mais comuns. Para obter mais informações, consulte [fazer alterações de esquema em bancos de dados de publicação](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
 Para sincronizar uma inscrição de envio, consulte [sincronizar uma assinatura Push](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
 Para sincronizar uma assinatura pull, consulte [sincronizar uma assinatura Pull](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
 Para definir agendas de sincronização, consulte [especificar agendas de sincronização](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
 **Para exibir e resolver conflitos de sincronização**  
  
-   [! INCLUIR [ssManStudioFull] (... / Token/ssManStudioFull_md.md)]: [View and Resolve Data Conflicts for Merge Publications &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view and resolve data conflicts for merge publications.md)  
  
-   [! INCLUIR [ssManStudioFull] (... / Token/ssManStudioFull_md.md)]: [View Data Conflicts for Transactional Publications &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
## Executando código durante sincronização  
 A replicação suporta dois métodos de execução de código durante a sincronização  
  
-   A execução de script sob demanda tem suporte para replicação transacional e replicação de mesclagem. Usando em execução de script sob demanda, você pode especificar um script SQL para ser executado durante a sincronização. O script é copiado para o assinante e executado usando **sqlcmd** no início do processo de sincronização. O script não tem acesso às alterações replicadas enquanto elas são aplicadas ao Assinante. Para obter mais informações, consulte [Executar Scripts durante a sincronização e 40; Programação Transact-SQL de replicação e 41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md).  
  
-   Manipuladores de lógica de negócios possuem suporte para replicação de mesclagem. Usando a estrutura dos manipuladores de lógica de negócios, você pode escrever um assembly de código gerenciado durante o processo de sincronização de mesclagem. O assembly inclui lógica comercial que pode responder a uma série de condições durante a sincronização: alterações de dados, conflitos e erros. Para obter mais informações, consulte [executar lógica de negócios durante a sincronização direta](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
## Consulte também  
 [Detectar e resolver conflitos de replicação de mesclagem](../../relational-databases/replication/merge/detect-and-resolve-merge-replication-conflicts.md)  
  
  