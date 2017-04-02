---
title: "MSSQL_ENG020557 | Microsoft Docs"
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
  - "erro MSSQL_ENG020557"
ms.assetid: c43c6952-5b60-4347-b881-11a0004dce24
caps.latest.revision: 10
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 10
---
# MSSQL_ENG020557
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|20557|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Desligamento do agente. Para obter mais informações, consulte o histórico de trabalho do SQL Server Agent relacionado ao trabalho '%s'.|  
  
## Explicação  
 Um agente de replicação foi desligado sem gravar um motivo para a tabela de histórico apropriada ou, então, o agente foi desligado no meio de um processo.  
  
## Ação do usuário  
  
-   Reinicie o agente para verificar se agora será possível executá-lo sem falhas. Para obter mais informações, consulte [Iniciar e parar um agente de replicação e 40; SQL Server Management Studio e 41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [conceitos dos executáveis do Replication Agent](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
-   Verifique o histórico de agente e o histórico de trabalho para outros erros que aconteceram quase no mesmo momento. Para obter informações sobre como exibir o status do agente e os detalhes do erro no Replication Monitor, consulte os seguintes tópicos:  
  
    -   Para o Snapshot Agent, Log Reader Agent e Queue Reader Agent, consulte [Exibir informações e executar tarefas para os agentes associados com uma publicação e 40; Monitor de replicação e 41;](../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md).  
  
    -   Para o Distribution Agent e o agente de mesclagem, consulte [Exibir informações e executar tarefas para os agentes associados a uma assinatura & #40. Monitor de replicação e 41;](../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
-   Verifique se a conectividade básica está funcionado entre os computadores acessados pelo agente e, em seguida, conecte-se a cada computador usando um utilitário, como o **sqlcmd** . Ao se conectar, use a mesma conta com a qual o agente faz conexões. Para obter mais informações sobre as permissões necessárias para cada conta de agente, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
-   Se o erro ocorrer ao criar ou aplicar um instantâneo, verifique os arquivos no diretório de instantâneos com relação a erros.  
  
-   Se o erro continuar ocorrendo, aumente o log do agente e especifique um arquivo de saída para o log. Dependendo do contexto do erro, isso poderá fornecer as etapas que levam ao erro e às mensagens de erro adicionais. Para obter mais informações sobre como configurar o log para replicação, consulte o artigo [312292](http://support.microsoft.com/kb/312292)na Base de Dados de Conhecimento Microsoft.  
  
## Consulte também  
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  