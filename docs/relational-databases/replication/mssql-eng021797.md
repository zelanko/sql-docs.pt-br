---
title: "MSSQL_ENG021797 | Microsoft Docs"
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
  - "erro MSSQL_ENG021797"
ms.assetid: 54d83a1e-43fd-449c-a2b2-fdda2609a534
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG021797
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|21797|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|'%s' deve ser um logon válido do Windows na forma: 'MACHINE\Login' ou 'DOMAIN\Login'. Consulte a documentação de '%s'.|  
  
## Explicação  
 Esse erro é gerado por procedimentos armazenados de replicação se o valor especificado para o **@job_login** parâmetro é nulo ou não é válido. Esse erro pode ocorrer se um membro do **db_owner** função fixa de banco de dados executa scripts de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O modelo de segurança foi alterado no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]e esses scripts devem ser atualizados.  
  
-   [sp_addlogreader_agent & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
-   [sp_addqreader_agent & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)  
  
-   [sp_addpublication_snapshot & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)  
  
-   [sp_addpushsubscription_agent & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)  
  
-   [sp_addpullsubscription_agent & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)  
  
-   [sp_addmergepushsubscription_agent & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)  
  
-   [sp_addmergepullsubscription_agent & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)  
  
 Esses procedimentos armazenados podem ser executados por um membro do **sysadmin** a função de servidor fixa no servidor apropriado ou um membro do **db_owner** função de banco de dados fixa no banco de dados apropriado. Os procedimentos armazenados criam um trabalho de agente e permitem que o usuário especifique a conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows em que o agente é executado. Para os usuários a **sysadmin** função, trabalhos de agente são criados implicitamente mesmo se uma conta do Windows não for especificada (se uma conta for especificada, ela deve ser válida); agentes são executados no contexto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de serviço de agente no servidor apropriado. Apesar da conta não ser exigida, é uma prática recomendada de segurança especificar uma conta separada para os agentes. Para obter mais informações, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## Ação do usuário  
 Certifique-se de especificar uma conta válida do Windows para o **@job_login** parâmetro de cada procedimento. Se tiver scripts de replicação de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], atualize esses scripts para incluir os procedimento e os parâmetros armazenados exigidos pelo [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obter mais informações, consulte [Atualizar Scripts de replicação e 40; Programação Transact-SQL de replicação e 41;](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md).  
  
## Consulte também  
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  