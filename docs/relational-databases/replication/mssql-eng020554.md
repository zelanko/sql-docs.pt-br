---
title: MSSQL_ENG020554 | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: MSSQL_ENG020554 error
ms.assetid: ef1a1b88-b2ab-43e8-99cd-163a973262d6
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c3cd330495a1956a925bbd37d2b3e841c773d297
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqleng020554"></a>MSSQL_ENG020554
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|20554|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|O agente de replicação não registrou uma mensagem de progresso em %ld minutos. Isso pode indicar inoperância do agente ou alta atividade do sistema. Verifique se os registros estão sendo replicados no destino e se as conexões com o Assinante, o Publicador e o Distribuidor ainda estão ativas.|  
  
## <a name="explanation"></a>Explicação  
 O trabalho de **verificação dos agentes de replicação** é executado em um intervalo especificado (10 minutos, por padrão) para verificar o status de cada agente de replicação. Se um agente não tiver registrado nenhuma mensagem de progresso desde a última vez que o trabalho de verificação de agente foi executado, poderá ocorrer o erro MSSQL_ENG020554. É esperado que, pelo menos, o agente registre mensagens de histórico, mesmo se nenhuma outra atividade de replicação esteja acontecendo. Embora o agente de replicação não esteja respondendo conforme esperado, não necessariamente foi interrompido ou falhou (se ocorrer falha no agente, o erro MSSQL_ENG020536 será exibido).  
  
 Os seguintes problemas podem causar o erro MSSQL_ENG020554:  
  
-   O agente está ocupado.  
  
     Se o agente estiver muito ocupado para responder quando sondado pelo trabalho de verificação do agente, o trabalho de verificação do agente não poderá reportar se o agente de replicação está ou não em funcionamento. Há várias motivos pelos quais o agente de replicação pode estar ocupado: talvez existam muitos dados sendo replicados ou existam problemas no design ou na configuração do aplicativo, o que resultam em processos com execução de longa duração.  
  
-   O agente não pode efetuar logon em um dos computadores na topologia.  
  
     Todos os agentes têm um parâmetro **-LoginTimeOut** (definido para 15 segundos, por padrão), que controla a duração das tentativas de logon de um agente em um nó de replicação, como o Agente de Mesclagem fazendo logon no Publicador. Se o valor de **-LoginTimeOut** for definido como sendo maior que o intervalo no qual o trabalho de verificação do agente de replicação é executado, um problema de logon poderá ser a causa-raiz do erro: o erro MSSQL_ENG020554 será gerado antes de o agente poder gerar um erro mais específico.  
  
## <a name="user-action"></a>Ação do usuário  
 A ação necessária depende da causa do erro:  
  
-   Para todos os casos nos quais esse erro é gerado:  
  
     Verifique os detalhes de erro no Replication Monitor e, depois, reinicie o agente, se ele tiver sido interrompido. Os detalhes de erro podem fornecer informações adicionais sobre o motivo do agente não estar sendo executado corretamente. Se o agente estiver em execução, não interrompa nem reinicie o agente, já que isso pode agravar o problema. Para obter informações sobre como exibir o status do agente e os detalhes de erro no Replication Monitor, consulte os seguintes tópicos:  
  
    -   Para o Snapshot Agent, o Agente de Leitor de Log e o Queue Reader Agent, consulte [Exibir informações e executar tarefas para os agentes associados a uma publicação &#40;Replication Monitor&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
    -   Para o Agente de Distribuição e o Agente de Mesclagem, consulte [Exibir informações e executar tarefas para os agentes associados a uma assinatura &#40;Replication Monitor&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
-   Se o erro ocorrer frequentemente porque o agente está ocupado:  
  
     Talvez seja necessário recriar o seu aplicativo de forma que o processamento do agente leve menos tempo.  
  
     É possível aumentar o intervalo em que o status do agente é verificado usando a caixa de diálogo **Propriedades do Trabalho** . Para obter informações sobre como acessar essa caixa de diálogo em trabalhos de replicação, consulte [Exibir informações e executar tarefas para um Publicador &#40;Replication Monitor&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md).  
  
-   Se um agente não puder efetuar logon em um dos computadores na topologia:  
  
     Recomendamos que o valor **-LoginTimeOut** seja definido como sendo menor que o intervalo no qual o trabalho de verificação do agente de replicação é executado. Em alguns casos, o valor de **-LoginTimeOut** é definido como sendo maior devido a problemas de rede que fazem com que os logons sejam expirados. Se o valor **-LoginTimeOut** for definido como sendo menor, a replicação poderá reportar erros mais específicos, permitindo que você solucione os problemas de logon que podem ser provocados por permissões, problemas de rede ou outros. Os parâmetros de agente podem ser especificados em perfis de agente e na linha de comando. Para obter mais informações, consulte:  
  
    -   [Trabalhar com perfis do Agente de Replicação](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [Exibir e modificar parâmetros do prompt de comando de agentes de replicação &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## <a name="see-also"></a>Consulte também  
 [Administração do agente de replicação](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Agente de Distribuição de Replicação](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Agente do Leitor de Log de Replicação](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Agente de Mesclagem de Replicação](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Agente de Leitor de Fila de Replicação](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  
