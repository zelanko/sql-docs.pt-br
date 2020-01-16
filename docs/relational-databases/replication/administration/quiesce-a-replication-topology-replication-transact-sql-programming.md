---
title: Desativar uma topologia de replicação (SP de replicação)
description: Saiba como usar procedimentos armazenados de replicação para desativar uma topologia de replicação do SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- administering replication, quiescing
- quiesce [SQL Server replication]
- transactional replication, backup and restore
ms.assetid: 7626d575-9994-47be-b772-5b6f1b7ef7ca
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 0ad5d9595419c5d991dd1e33d15e1e7a4d1a8721
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321997"
---
# <a name="quiesce-a-replication-topology-replication-transact-sql-programming"></a>Confirmar uma topologia de replicação (Programação Transact-SQL de replicação)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  *Confirmar* um sistema inclui interromper as atividades em tabelas publicadas em todos os nós, e assegurar que todos eles tenham recebido todas as alterações de todos os demais nós. Esse tópico explica como confirmar a topologia de replicação, necessária para um número de tarefas administrativas, e como garantir que um nó tenha recebido todas as alterações dos demais nós.  
  
### <a name="to-quiesce-a-transactional-replication-topology-with-read-only-subscriptions"></a>Para confirmar uma topologia de replicação transacional com assinaturas somente leitura  
  
1.  Interrompa a atividade em todas as tabelas publicadas no Publicador.  
  
2.  No Publicador do banco de dados de publicação, execute [sp_posttracertoken &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql.md).  
  
3.  No Publicador do banco de dados de publicação, execute [sp_helptracertokenhistory](../../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md).  
  
4.  Certifique-se de que cada Assinante tenha recebido o token de rastreamento.  

### <a name="to-quiesce-a-transactional-replication-topology-with-updatable-subscriptions"></a>Para confirmar uma topologia de replicação transacional com assinaturas atualizáveis  
  
1.  Interrompa a atividade em todas as tabelas publicadas no Publicador e em todos os Assinantes.  
  
2.  Se os Assinantes usarem assinaturas de atualização em fila:  
  
    1.  Se o Agente de Leitor de Fila não estiver executando em modo contínuo, execute o agente. Para obter mais informações sobre os agentes em execução, consulte [Conceitos dos executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) ou [Iniciar e parar um agente de replicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
    2.  Para verificar se a fila está vazia, execute [sp_replqueuemonitor](../../../relational-databases/system-stored-procedures/sp-replqueuemonitor-transact-sql.md) em cada Assinante.  
  
3.  No Publicador do banco de dados de publicação, execute [sp_posttracertoken](../../../relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql.md).  
  
4.  No Publicador do banco de dados de publicação, execute [sp_helptracertokenhistory](../../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md).  
  
5.  Certifique-se de que cada Assinante tenha recebido o token de rastreamento.  
  
### <a name="to-quiesce-a-peer-to-peer-transactional-replication-topology"></a>Para confirmar uma topologia de replicação transacional ponto a ponto  
  
1.  Interrompa a atividade em todas as tabelas publicadas em todos os nós.  
  
2.  Execute [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) em cada banco de dados de publicação na topologia.  
  
3.  Se o Agente de Leitor de Log ou o Agente de Distribuição não estiver executando em modo contínuo, execute o agente. O Agente de Leitor de Log deve ser iniciado antes do Agente de Distribuição. Para obter mais informações sobre os agentes em execução, consulte [Conceitos dos executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) ou [Iniciar e parar um agente de replicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
4.  Execute [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md) em cada banco de dados de publicação na topologia. Certifique-se de que o conjunto de resultados contenha as respostas de cada um dos demais nós.  
  
### <a name="to-ensure-a-peer-to-peer-node-has-received-all-prior-changes"></a>Para ter certeza de que um nó ponto a ponto recebeu todas as alterações anteriores  
  
1.  Execute [sp_requestpeerresponse](../../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) no banco de dados de publicação, no nó que você está verificando.  
  
2.  Se o Agente de Leitor de Log ou o Agente de Distribuição não estiver executando em modo contínuo, execute o agente. O Agente de Leitor de Log deve ser iniciado antes do Agente de Distribuição. Para obter mais informações sobre os agentes em execução, consulte [Conceitos dos executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) ou [Iniciar e parar um agente de replicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
3.  Execute [sp_helppeerresponses](../../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md) no banco de dados de publicação, no nó que você está verificando. Certifique-se de que o conjunto de resultados contenha as respostas de cada um dos demais nós.  
  
### <a name="to-quiesce-a-merge-replication-topology"></a>Para confirmar uma topologia de replicação de mesclagem  
  
1.  Interrompa a atividade em todas as tabelas publicadas no Publicador e em todos os Assinantes.  
  
2.  Execute o Agente de Mesclagem para cada assinatura duas vezes: sincronize todas as assinaturas uma vez e, em seguida, sincronize cada assinatura uma segunda vez: Isso garantirá que todos as alterações sejam replicadas em todos os nós. Para obter mais informações sobre os agentes em execução, consulte [Conceitos dos executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) ou [Iniciar e parar um agente de replicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
    > [!NOTE]  
    >  Em caso de conflitos durante a sincronização, é possível que as alterações exigidas pela resolução do conflito não sejam propagadas a todos os nós, após a execução do Agente de Mesclagem duas vezes.  
  
## <a name="see-also"></a>Consulte Também  
 [Administrar uma topologia ponto a ponto &#40;programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Medir a latência e validar conexões para replicação transacional](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
