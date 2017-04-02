---
title: "MSSQL_ENG014150 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "erro MSSQL_ENG014150"
ms.assetid: c3dd3109-abf3-4b38-a4e9-ef48d0235656
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 11
---
# MSSQL_ENG014150
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|14150|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Replicação-%s: agente %s bem-sucedida. %s|  
  
## Explicação  
 Essa mensagem indica que um agente de replicação concluiu a execução com êxito. A replicação usa os seguintes agentes:  
  
-   O Snapshot Agent. Esse agente é usado por todas as publicações.  
  
-   O Log Reader Agent. Esse agente é usado por todas as publicações transacionais.  
  
-   O Queue Reader Agent. Esse agente é usado pelas publicações transacionais habilitadas para atualização de assinaturas em fila.  
  
-   O Distribution Agent. Esse agente sincroniza as assinaturas para publicações transacionais e de instantâneo.  
  
-   O Merge Agent. Esse agente sincroniza as assinaturas para publicações de mesclagem.  
  
-   Trabalhos de manutenção de replicação.  
  
## Ação do usuário  
 O Log Reader Agent, o Queue Reader Agent e o Distribution Agent são, em geral, executados continuamente, diferente de outros agentes, que são, em geral, executados sob demanda ou de forma programada. Se você não esperar que um agente tenha concluído a sua execução, verifique o estado do agente. Para obter mais informações, consulte [monitorar agentes de replicação](../../relational-databases/replication/monitor/monitor-replication-agents.md).  
  
## Consulte também  
 [Administração do agente de replicação](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Agente de Distribuição de Replicação](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Replication Agente de Leitor de Log](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Replication Queue Reader Agent](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  