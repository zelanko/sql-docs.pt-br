---
title: "MSSQL_ENG018752 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "erro MSSQL_ENG018752"
ms.assetid: 405b2655-acb4-4e15-bcc6-b8f86bb22b37
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# MSSQL_ENG018752
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|18752|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Somente um Agente de Leitor de Log ou um procedimento relacionado ao log (sp_repldone, sp_replcmds e sp_replshowcmds) pode se conectar ao banco de dados de cada vez. Se você tiver executado um procedimento relacionado ao log, descarte a conexão através da qual o procedimento foi executado ou execute sp_replflush por essa conexão antes de iniciar o Agente de Leitor de Log ou de executar outro procedimento relacionado ao log.|  
  
## Explicação  
 Mais de uma conexão atual está tentando executar qualquer um dos seguintes: **sp_repldone**, **sp_replcmds**, ou **sp_replshowcmds**. Os procedimentos armazenados [sp_repldone & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md) e [sp_replcmds & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) procedimentos armazenados são usados pelo Log Reader Agent para localizar e atualizar informações sobre transações replicadas em um banco de dados publicado. O procedimento armazenado [sp_replshowcmds & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md) é usada para solucionar determinados tipos de problemas com replicação transacional.  
  
 Esse erro é gerado nas seguintes circunstâncias:  
  
-   Se o Log Reader Agent de um banco de dados publicado estiver sendo executado e um segundo Log Reader Agent tentar ser executado no mesmo banco de dados, o erro será gerado para o segundo agente e será exibido no histórico do agente.  
  
     Em uma situação na qual há vários agentes, é possível que mais de um agente seja resultado de um processo órfão.  
  
-   Se o Log Reader Agent para um banco de dados publicado for iniciado e um usuário executa **sp_repldone**, **sp_replcmds**, ou **sp_replshowcmds** no mesmo banco de dados, o erro é gerado no aplicativo em que o procedimento armazenado foi executado (como **sqlcmd**).  
  
-   Se nenhum Log Reader Agent está em execução para um banco de dados publicado e um usuário executa **sp_repldone**, **sp_replcmds**, ou **sp_replshowcmds** e não for encerrada a conexão através da qual o procedimento foi executado, o erro é gerada quando o Log Reader Agent tenta se conectar ao banco de dados.  
  
## Ação do usuário  
 As etapas a seguir podem ajudar a solucionar o problema. Se qualquer etapa permitir que o Log Reader Agent seja iniciado sem erros, não será necessário concluir as etapas restantes.  
  
-   Verifique o histórico do Log Reader Agent em relação a qualquer outro erro que poderia estar contribuindo com esse erro. Para obter informações sobre como exibir detalhes de status e de erro do agente no Replication Monitor, consulte [Exibir informações e executar tarefas para os agentes associados com uma publicação e 40; Monitor de replicação e 41;](../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md).  
  
-   Verifique a saída de [sp_who & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) para números de identificação de processo específico (SPIDs) que estão conectados ao banco de dados publicado. Feche todas as conexões que podem executar **sp_repldone**, **sp_replcmds**, ou **sp_replshowcmds**.  
  
-   Reinicie o Agente de Leitor de Log. Para obter mais informações, consulte [Iniciar e parar um agente de replicação e 40; SQL Server Management Studio e 41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
-   Reinicie o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent (offline ou online em um cluster) no Distribuidor. Se há possibilidade de um trabalho agendado ter executado **sp_repldone**, **sp_replcmds**, ou **sp_replshowcmds** de qualquer outro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância, reinicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para essas instâncias. Para obter mais informações, consulte [Iniciar, parar ou pausar o serviço SQL Server Agent](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md).  
  
-   Executar [sp_replflush & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md) no publicador de banco de dados de publicação e reinicie o Log Reader Agent.  
  
-   Se o erro continuar ocorrendo, aumente o log do agente e especifique um arquivo de saída para o log. Dependendo do contexto do erro, isso poderá fornecer as etapas que levaram ao erro e/ou as mensagens de erros adicionais.  
  
## Consulte também  
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Replication Agente de Leitor de Log](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
  