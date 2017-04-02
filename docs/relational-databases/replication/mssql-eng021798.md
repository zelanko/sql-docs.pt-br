---
title: "MSSQL_ENG021798 | Microsoft Docs"
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
  - "erro MSSQL_ENG021798"
ms.assetid: 596f5092-75ab-4a19-8582-588687c7b089
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# MSSQL_ENG021798
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|21798|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|O trabalho do agente '%s' deve ser adicionado por meio de '%s' antes de continuar. Consulte a documentação de '%s'.|  
  
## Explicação  
 Para criar uma publicação, você deve ser um membro do **sysadmin** a função de servidor fixa no Editor ou um membro do **db_owner** função de banco de dados fixa no banco de dados de publicação. Se você for um membro do **db_owner** função, esse erro é gerada se:  
  
-   Você executar scripts do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. O modelo de segurança foi alterado no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]e esses scripts devem ser atualizados.  
  
-   O procedimento armazenado **sp_addpublication** é executado antes da execução [sp_addlogreader_agent & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md). Isso se aplica a todas as publicações transacionais.  
  
-   O procedimento armazenado **sp_addpublication** é executado antes da execução [sp_addqreader_agent & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md). Isso se aplica a publicações transacionais habilitadas para assinaturas de atualização enfileiradas (um valor de TRUE para o **@allow_queued_tran** parâmetro do **sp_addpublication**).  
  
 Os procedimentos armazenados **sp_addlogreader_agent** e **sp_addqreader_agent** criam um trabalho do agente e permitem que você especifique o [!INCLUDE[msCoName](../../includes/msconame-md.md)] da conta do Windows na qual o agente é executado. Para os usuários a **sysadmin** função, trabalhos de agente são criados implicitamente se **sp_addlogreader_agent** e **sp_addqreader_agent** não são executadas; agentes são executados no contexto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de serviço do Agent no distribuidor. Embora **sp_addlogreader_agent** e **sp_addqreader_agent** não são necessários para os usuários a **sysadmin** função, é uma prática recomendada de segurança para especificar uma conta separada para os agentes. Para obter mais informações, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## Ação do usuário  
 Certifique-se de executar os procedimentos na ordem correta. Para obter mais informações, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md). Se você tiver scripts de replicação de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], atualize esses scripts para incluir os procedimentos e os parâmetros armazenados exigidos por [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. Para obter mais informações, consulte [Atualizar Scripts de replicação e 40; Programação Transact-SQL de replicação e 41;](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md).  
  
## Consulte também  
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  