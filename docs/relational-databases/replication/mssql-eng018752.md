---
title: MSSQL_ENG018752 | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG018752 error
ms.assetid: 405b2655-acb4-4e15-bcc6-b8f86bb22b37
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 929c5e1c6205ab46b89ce4818183bb5ba9084fbe
ms.lasthandoff: 04/11/2017

---
# <a name="mssqleng018752"></a>MSSQL_ENG018752
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|18752|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Somente um Agente de Leitor de Log ou um procedimento relacionado ao log (sp_repldone, sp_replcmds e sp_replshowcmds) pode se conectar ao banco de dados de cada vez. Se você tiver executado um procedimento relacionado ao log, descarte a conexão através da qual o procedimento foi executado ou execute sp_replflush por essa conexão antes de iniciar o Agente de Leitor de Log ou de executar outro procedimento relacionado ao log.|  
  
## <a name="explanation"></a>Explicação  
 Mais de uma conexão atual está tentando executar um dos seguintes: **sp_repldone**, **sp_replcmds**ou **sp_replshowcmds**. Os procedimentos armazenados [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md) e [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) são usados pelo Agente de Leitor de Log para localizar e atualizar informações sobre as transações replicadas em um banco de dados publicado. O procedimento armazenado [sp_replshowcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md) é usado para solucionar alguns tipos de problemas com a replicação transacional.  
  
 Esse erro é gerado nas seguintes circunstâncias:  
  
-   Se o Log Reader Agent de um banco de dados publicado estiver sendo executado e um segundo Log Reader Agent tentar ser executado no mesmo banco de dados, o erro será gerado para o segundo agente e será exibido no histórico do agente.  
  
     Em uma situação na qual há vários agentes, é possível que mais de um agente seja resultado de um processo órfão.  
  
-   Se o Agente de Leitor de Log de um banco de dados publicado for iniciado e um usuário executar **sp_repldone**, **sp_replcmds**ou **sp_replshowcmds** no mesmo banco de dados, o erro será gerado no aplicativo em que o procedimento armazenado foi executado (como **sqlcmd**).  
  
-   Se nenhum Log Reader Agent estiver sendo executado para um banco de dados publicado, um usuário executar **sp_repldone**, **sp_replcmds**ou **sp_replshowcmds** e a conexão na qual o procedimento foi executado não for encerrada, o erro será gerado quando o Log Reader Agent tentar se conectar ao banco de dados.  
  
## <a name="user-action"></a>Ação do usuário  
 As etapas a seguir podem ajudar a solucionar o problema. Se qualquer etapa permitir que o Log Reader Agent seja iniciado sem erros, não será necessário concluir as etapas restantes.  
  
-   Verifique o histórico do Log Reader Agent em relação a qualquer outro erro que poderia estar contribuindo com esse erro. Para obter informações sobre como exibir o status do agente e detalhes de erro no Replication Monitor, consulte [Exibir informações e executar tarefas para os agentes associados a uma publicação &#40;Replication Monitor&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
-   Verifique o resultado de [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) para obter os SPIDs (números de identificação do processo específico) conectados ao banco de dados publicado. Feche qualquer conexão que poderia haver executado **sp_repldone**, **sp_replcmds**ou **sp_replshowcmds**.  
  
-   Reinicie o Agente de Leitor de Log. Para obter mais informações, consulte [Iniciar e interromper um agente de replicação &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
-   Reinicie o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent (offline ou online em um cluster) no Distribuidor. Se houver a possibilidade de um trabalho agendado ter executado **sp_repldone**, **sp_replcmds**ou **sp_replshowcmds** de qualquer outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , também será necessário reiniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para essas instâncias. Para obter mais informações, consulte [Iniciar, parar ou pausar o serviço SQL Server Agent](http://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c).  
  
-   Execute [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md) no Publicador do banco de dados de publicação e reinicie o Agente de Leitor de Log.  
  
-   Se o erro continuar ocorrendo, aumente o log do agente e especifique um arquivo de saída para o log. Dependendo do contexto do erro, isso poderá fornecer as etapas que levaram ao erro e/ou as mensagens de erros adicionais.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Agente do Leitor de Log de Replicação](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
  
