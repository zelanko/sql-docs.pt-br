---
title: "MSSQL_ENG014151 | Microsoft Docs"
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
  - "erro MSSQL_ENG014151"
ms.assetid: 54b45e70-46b3-4c7a-a5bf-06f6dd028ceb
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# MSSQL_ENG014151
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|14151|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Replicação-%s: falha no agente %s. %s|  
  
## Explicação  
 Este erro ocorre para qualquer falha de agente de replicação. O texto ao término da mensagem depende do contexto da falha.  
  
## Ação do usuário  
 Este erro pode acontecer em várias situações; use as seguintes abordagens, conforme necessário:  
  
-   Reinicie o agente com falha para verificar se será possível executá-lo sem falhas agora. Para obter mais informações, consulte [Iniciar e parar um agente de replicação e 40; SQL Server Management Studio e 41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [conceitos dos executáveis do Replication Agent](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
-   Verifique o histórico de agente e o histórico de trabalho para outros erros que aconteceram quase no mesmo momento. Para obter informações sobre como exibir o status do agente e os detalhes de erro no Replication Monitor, consulte os seguintes tópicos:  
  
    -   Para o Snapshot Agent, Log Reader Agent e Queue Reader Agent, consulte [Exibir informações e executar tarefas para os agentes associados com uma publicação e 40; Monitor de replicação e 41;](../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md).  
  
    -   Para o Distribution Agent e o agente de mesclagem, consulte [Exibir informações e executar tarefas para os agentes associados a uma assinatura & #40. Monitor de replicação e 41;](../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
-   Verifique se a conectividade básica está funcionado entre os computadores acessados pelo agente e, depois, conecte-se a cada computador com um utilitário como [sqlcmd Utility](../../tools/sqlcmd-utility.md). Ao se conectar, use a mesma conta com a qual o agente faz conexões. Para obter mais informações sobre as permissões exigidas para cada conta de agente, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
-   Se o erro ocorrer ao criar ou aplicar um instantâneo, verifique os arquivos no diretório de instantâneos para erros.  
  
-   Se o erro continuar ocorrendo, aumente o log do agente e especifique um arquivo de saída para o log. Dependendo do contexto do erro, isso poderá fornecer as etapas que levaram ao erro e/ou as mensagens de erros adicionais.  
  
## Consulte também  
 [Administração do agente de replicação](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Agente de Distribuição de Replicação](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Replication Agente de Leitor de Log](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Replication Queue Reader Agent](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  