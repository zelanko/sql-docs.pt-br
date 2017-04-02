---
title: "MSSQL_ENG020554 | Microsoft Docs"
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
  - "erro MSSQL_ENG020554"
ms.assetid: ef1a1b88-b2ab-43e8-99cd-163a973262d6
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# MSSQL_ENG020554
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|20554|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|O agente de replicação não registrou uma mensagem de progresso em %ld minutos. Isso pode indicar inoperância do agente ou alta atividade do sistema. Verifique se os registros estão sendo replicados no destino e se as conexões com o Assinante, o Publicador e o Distribuidor ainda estão ativas.|  
  
## Explicação  
 O **verificação de agentes de replicação** trabalho é executado em um intervalo especificado (10 minutos por padrão) para verificar o status de cada agente de replicação. Se um agente não tiver registrado nenhuma mensagem de progresso desde a última vez que o trabalho de verificação de agente foi executado, poderá ocorrer o erro MSSQL_ENG020554. É esperado que, pelo menos, o agente registre mensagens de histórico, mesmo se nenhuma outra atividade de replicação esteja acontecendo. Embora o agente de replicação não esteja respondendo conforme esperado, não necessariamente foi interrompido ou falhou (se ocorrer falha no agente, o erro MSSQL_ENG020536 será exibido).  
  
 Os seguintes problemas podem causar o erro MSSQL_ENG020554:  
  
-   O agente está ocupado.  
  
     Se o agente estiver muito ocupado para responder quando sondado pelo trabalho de verificação do agente, o trabalho de verificação do agente não poderá reportar se o agente de replicação está ou não em funcionamento. Há várias motivos pelos quais o agente de replicação pode estar ocupado: talvez existam muitos dados sendo replicados ou existam problemas no design ou na configuração do aplicativo, o que resultam em processos com execução de longa duração.  
  
-   O agente não pode efetuar logon em um dos computadores na topologia.  
  
     Todos os agentes têm um parâmetro **- LoginTimeOut** (definido como 15 segundos por padrão), que determina quanto tempo um agente tenta fazer logon um nó de replicação, como o Merge Agent efetuar login no Editor. Se o **- LoginTimeOut** valor é definido como maior que o intervalo no qual o trabalho de verificação do agente de replicação é executado, um problema de logon pode ser a causa do erro: erro MSSQL_ENG020554 é gerado antes do agente é capaz de gerar um erro mais específico.  
  
## Ação do usuário  
 A ação necessária depende da causa do erro:  
  
-   Para todos os casos nos quais esse erro é gerado:  
  
     Verifique os detalhes de erro no Replication Monitor e, depois, reinicie o agente, se ele tiver sido interrompido. Os detalhes de erro podem fornecer informações adicionais sobre o motivo do agente não estar sendo executado corretamente. Se o agente estiver em execução, não interrompa nem reinicie o agente, já que isso pode agravar o problema. Para obter informações sobre como exibir o status do agente e os detalhes de erro no Replication Monitor, consulte os seguintes tópicos:  
  
    -   Para o Snapshot Agent, Log Reader Agent e Queue Reader Agent, consulte [Exibir informações e executar tarefas para os agentes associados com uma publicação e 40; Monitor de replicação e 41;](../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md).  
  
    -   Para o Distribution Agent e o agente de mesclagem, consulte [Exibir informações e executar tarefas para os agentes associados a uma assinatura & #40. Monitor de replicação e 41;](../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
-   Se o erro ocorrer frequentemente porque o agente está ocupado:  
  
     Talvez seja necessário recriar o seu aplicativo de forma que o processamento do agente leve menos tempo.  
  
     É possível aumentar o intervalo em que o status do agente é verificado usando a caixa de diálogo **Propriedades do Trabalho** . Para obter informações sobre como acessar essa caixa de diálogo de trabalhos de replicação, consulte [Exibir informações e executar tarefas para um publicador e 40; Monitor de replicação e 41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md).  
  
-   Se um agente não puder efetuar logon em um dos computadores na topologia:  
  
     É recomendável que o **- LoginTimeOut** valor seja definido como menor que o intervalo no qual o trabalho de verificação do agente de replicação é executado. Em alguns casos, o valor para **- LoginTimeOut** é definido como maior devido a problemas de rede que causam logons de tempo limite. Se o **- LoginTimeOut** for definido como menor, replicação poderá reportar erros mais específicos, permitindo que você solucione problemas de logon que pode ser causados por permissões, problemas de rede ou outros problemas. Os parâmetros de agente podem ser especificados em perfis de agente e na linha de comando. Para obter mais informações, consulte:  
  
    -   [Trabalhar com perfis do agente de replicação](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [Exibir e modificar parâmetros de Prompt de comando do agente de replicação e 40; SQL Server Management Studio e 41;](../../relational-databases/replication/agents/view and modify replication agent command prompt parameters.md)  
  
    -   [Conceitos de executáveis do agente de replicação](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## Consulte também  
 [Administração do agente de replicação](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Agente de Distribuição de Replicação](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Replication Agente de Leitor de Log](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Replication Queue Reader Agent](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  