---
title: "Confirmar uma topologia de replica&#231;&#227;o (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "Administrando a replicação, fechando para novas sessões"
  - "confirmação [replicação do SQL Server]"
  - "replicação transacional, backup e restauração"
ms.assetid: 7626d575-9994-47be-b772-5b6f1b7ef7ca
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Confirmar uma topologia de replica&#231;&#227;o (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o)
  *Confirmar* um sistema envolve parar as atividades em tabelas publicadas em todos os nós e garantir que cada nó tenha recebido todas as alterações de todos os outros nós. Esse tópico explica como confirmar a topologia de replicação, necessária para um número de tarefas administrativas, e como garantir que um nó tenha recebido todas as alterações dos demais nós.  
  
### Para confirmar uma topologia de replicação transacional com assinaturas somente leitura  
  
1.  Interrompa a atividade em todas as tabelas publicadas no Publicador.  
  
2.  No publicador do banco de dados de publicação, execute [sp_posttracertoken & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql.md).  
  
3.  No publicador do banco de dados de publicação, execute [sp_helptracertokenhistory](../../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md).  
  
4.  Certifique-se de que cada Assinante tenha recebido o token de rastreamento.  
  
### Para confirmar uma topologia de replicação transacional com assinaturas atualizáveis  
  
1.  Interrompa a atividade em todas as tabelas publicadas no Publicador e em todos os Assinantes.  
  
2.  Se os Assinantes usarem assinaturas de atualização em fila:  
  
    1.  Se o Agente de Leitor de Fila não estiver executando em modo contínuo, execute o agente. Para obter mais informações sobre agentes, consulte [conceitos dos executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) ou [Iniciar e parar um agente de replicação e 40; SQL Server Management Studio e 41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
    2.  Para verificar se a fila está vazia, execute [sp_replqueuemonitor](../../../relational-databases/system-stored-procedures/sp-replqueuemonitor-transact-sql.md) em cada assinante.  
  
3.  No publicador do banco de dados de publicação, execute [sp_posttracertoken](../../../relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql.md).  
  
4.  No publicador do banco de dados de publicação, execute [sp_helptracertokenhistory](../../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md).  
  
5.  Certifique-se de que cada Assinante tenha recebido o token de rastreamento.  
  
### Para confirmar uma topologia de replicação transacional ponto a ponto  
  
1.  Interrompa a atividade em todas as tabelas publicadas em todos os nós.  
  
2.  Executar [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) em cada banco de dados de publicação na topologia.  
  
3.  Se o Agente de Leitor de Log ou o Agente de Distribuição não estiver executando em modo contínuo, execute o agente. O Agente de Leitor de Log deve ser iniciado antes do Agente de Distribuição. Para obter mais informações sobre agentes, consulte [conceitos dos executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) ou [Iniciar e parar um agente de replicação e 40; SQL Server Management Studio e 41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
4.  Executar [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md) em cada banco de dados de publicação na topologia. Certifique-se de que o conjunto de resultados contenha as respostas de cada um dos demais nós.  
  
### Para ter certeza de que um nó ponto a ponto recebeu todas as alterações anteriores  
  
1.  Executar [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) no banco de dados de publicação no nó que você está verificando.  
  
2.  Se o Agente de Leitor de Log ou o Agente de Distribuição não estiver executando em modo contínuo, execute o agente. O Agente de Leitor de Log deve ser iniciado antes do Agente de Distribuição. Para obter mais informações sobre agentes, consulte [conceitos dos executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) ou [Iniciar e parar um agente de replicação e 40; SQL Server Management Studio e 41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
3.  Executar [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md) no banco de dados de publicação no nó que você está verificando. Certifique-se de que o conjunto de resultados contenha as respostas de cada um dos demais nós.  
  
### Para confirmar uma topologia de replicação de mesclagem  
  
1.  Interrompa a atividade em todas as tabelas publicadas no Publicador e em todos os Assinantes.  
  
2.  Execute o Agente de Mesclagem para cada assinatura duas vezes: sincronize todas as assinaturas uma vez e, em seguida, sincronize cada assinatura uma segunda vez: Isso garantirá que todos as alterações sejam replicadas em todos os nós. Para obter mais informações sobre agentes, consulte [conceitos dos executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) ou [Iniciar e parar um agente de replicação e 40; SQL Server Management Studio e 41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
    > [!NOTE]  
    >  Em caso de conflitos durante a sincronização, é possível que as alterações exigidas pela resolução do conflito não sejam propagadas a todos os nós, após a execução do Agente de Mesclagem duas vezes.  
  
## Consulte também  
 [Administrar uma topologia ponto a ponto e 40; Programação Transact-SQL de replicação e 41;](../../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Measure Latency and Validate Connections for Transactional Replication](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  