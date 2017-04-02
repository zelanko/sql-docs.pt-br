---
title: "MSSQL_REPL020011 | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "erro MSSQL_REPL020011"
ms.assetid: f72072d7-bbb6-48ad-ac88-afa74aeb4d58
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# MSSQL_REPL020011
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|20011|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|O processo não pôde executar '%1' em '%2'.|  
  
## Explicação  
 Esse erro pode ser gerado em várias circunstâncias durante a replicação transacional, processamento, como quando o Log Reader Agent executa **sp_replcmds** (o processo não pôde executar 'sp_replcmds' em \< ServerName>) ou **sp_repldone** (o processo não pôde executar 'sp_repldone' em \< ServerName>).  
  
## Ação do usuário  
 Se esse erro é gerado em um banco de dados que você acabou de restaurar de um backup, certifique-se de ter seguido as etapas descritas na documentação do backup e restauração, incluindo a execução de **sp_replrestart** se apropriado. Para obter mais informações, consulte [Strategies for Backing Up and Restoring Snapshot and Transactional Replication](../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md).  
  
 Esse erro é um erro de processamento interno e, se for gerado em circunstâncias diferentes de uma restauração, geralmente indica que a replicação deve ser removida e reconfigurada. Se você não puder remover a replicação, entre em contato com o atendimento ao cliente para assistência técnica.  
  
## Consulte também  
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [sp_replcmds & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)  
  
  