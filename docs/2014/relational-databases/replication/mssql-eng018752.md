---
title: MSSQL_ENG018752 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG018752 error
ms.assetid: 405b2655-acb4-4e15-bcc6-b8f86bb22b37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0558ded6ed10284df39270ddeca9d92434daf40e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63057466"
---
# <a name="mssql_eng018752"></a>MSSQL_ENG018752
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|18752|  
|Origem do Evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Somente um Agente de Leitor de Log ou um procedimento relacionado ao log (sp_repldone, sp_replcmds e sp_replshowcmds) pode se conectar ao banco de dados de cada vez. Se você tiver executado um procedimento relacionado ao log, descarte a conexão através da qual o procedimento foi executado ou execute sp_replflush por essa conexão antes de iniciar o Agente de Leitor de Log ou de executar outro procedimento relacionado ao log.|  
  
## <a name="explanation"></a>Explicação  
 Mais de uma conexão atual está tentando executar um dos seguintes: **sp_repldone**, **sp_replcmds**ou **sp_replshowcmds**. Os procedimentos armazenados [sp_repldone &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-repldone-transact-sql) e [sp_replcmds &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replcmds-transact-sql) são usados pelo Agente de Leitor de Log para localizar e atualizar informações sobre as transações replicadas em um banco de dados publicado. O procedimento armazenado [sp_replshowcmds &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql) é usado para solucionar alguns tipos de problemas com a replicação transacional.  
  
 Esse erro é gerado nas seguintes circunstâncias:  
  
-   Se o Log Reader Agent de um banco de dados publicado estiver sendo executado e um segundo Log Reader Agent tentar ser executado no mesmo banco de dados, o erro será gerado para o segundo agente e será exibido no histórico do agente.  
  
     Em uma situação na qual há vários agentes, é possível que mais de um agente seja resultado de um processo órfão.  
  
-   Se o Agente de Leitor de Log de um banco de dados publicado for iniciado e um usuário executar **sp_repldone**, **sp_replcmds**ou **sp_replshowcmds** no mesmo banco de dados, o erro será gerado no aplicativo em que o procedimento armazenado foi executado (como **sqlcmd**).  
  
-   Se nenhum Log Reader Agent estiver sendo executado para um banco de dados publicado, um usuário executar **sp_repldone**, **sp_replcmds**ou **sp_replshowcmds** e a conexão na qual o procedimento foi executado não for encerrada, o erro será gerado quando o Log Reader Agent tentar se conectar ao banco de dados.  
  
## <a name="user-action"></a>Ação do usuário  
 As etapas a seguir podem ajudar a solucionar o problema. Se qualquer etapa permitir que o Log Reader Agent seja iniciado sem erros, não será necessário concluir as etapas restantes.  
  
-   Verifique o histórico do Log Reader Agent em relação a qualquer outro erro que poderia estar contribuindo com esse erro. Para obter informações sobre como exibir o status do agente e os detalhes do erro no Replication Monitor, consulte [Exibir informações e executar tarefas usando o Replication Monitor](monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
-   Verifique o resultado de [sp_who &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-who-transact-sql) para obter os SPIDs (números de identificação do processo específico) conectados ao banco de dados publicado. Feche qualquer conexão que poderia haver executado **sp_repldone**, **sp_replcmds**ou **sp_replshowcmds**.  
  
-   Reinicie o Agente de Leitor de Log. Para obter mais informações, consulte [Iniciar e interromper um agente de replicação &#40;SQL Server Management Studio&#41;](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
-   Reinicie o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent (offline ou online em um cluster) no Distribuidor. Se houver a possibilidade de um trabalho agendado ter executado **sp_repldone**, **sp_replcmds**ou **sp_replshowcmds** de qualquer outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , também será necessário reiniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para essas instâncias. Para obter mais informações, consulte [Iniciar, parar ou pausar o serviço SQL Server Agent](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md).  
  
-   Execute [sp_replflush &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replflush-transact-sql) no Publicador do banco de dados de publicação e reinicie o Agente de Leitor de Log.  
  
-   Se o erro continuar ocorrendo, aumente o log do agente e especifique um arquivo de saída para o log. Dependendo do contexto do erro, isso poderá fornecer as etapas que levaram ao erro e/ou as mensagens de erros adicionais.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](errors-and-events-reference-replication.md)   
 [Agente do Leitor de Log de Replicação](agents/replication-log-reader-agent.md)  
  
  
