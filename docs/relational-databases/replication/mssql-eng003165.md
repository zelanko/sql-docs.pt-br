---
title: "MSSQL_ENG003165 | Microsoft Docs"
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
  - "erro MSSQL_ENG003165"
ms.assetid: 707d33dd-644e-4cc9-ac51-dddd49031530
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# MSSQL_ENG003165
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|3165|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|O banco de dados '%ls' foi restaurado; entretanto, houve um erro durante a restauração/remoção da replicação. O banco de dados foi deixado offline. Consulte o tópico MSSQL_ENG003165 dos Manuais Online do SQL Server.|  
  
## Explicação  
 O erro será gerado se ocorrer um problema durante a restauração de um backup de um banco de dados replicado:  
  
-   Se o backup estiver sendo restaurado para o mesmo banco de dados e servidor nos quais foi obtido, o erro indica que não foi possível restaurar as configurações de replicação corretamente.  
  
-   Se o backup estiver sendo restaurado para um banco de dados ou servidor diferente, o erro indica que não foi possível remover as configurações de replicação corretamente (por padrão, as configurações de replicação são removidas se o banco de dados ou servidor for diferente).  
  
 O erro provavelmente é o resultado de uma incompatibilidade entre o estado do banco de dados restaurado e um ou mais bancos de dados sistema que contêm metadados de replicação: **msdb**, **mestre**, ou o banco de dados de distribuição.  
  
## Ação do usuário  
 Para resolver o problema:  
  
1.  Execute ALTER DATABASE para que o banco de dados fique online; por exemplo: `ALTER DATABASE AdventureWorks SET ONLINE`. Para obter mais informações, consulte [ALTER DATABASE & #40. O Transact-SQL e 41;](../../t-sql/statements/alter-database-transact-sql.md). Se desejar preservar as configurações de replicação, vá para a etapa 2. Caso contrário, vá para a etapa 3.  
  
2.  Executar [sp_restoredbreplication & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-restoredbreplication-transact-sql.md). Se esse procedimento armazenado for executado com êxito, a restauração será concluída. Se não for executado com êxito, vá para a etapa 3.  
  
3.  Executar [sp_removedbreplication & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) Para remover todas as configurações de replicação.  
  
     Se necessário, reconfigure a replicação. Se a topologia de replicação tiver sido inserida no script conforme recomendado, você deverá usar scripts para reconfigurar a topologia.  
  
## Consulte também  
 [Fazer backup e restaurar bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Fazer backup e restaurar bancos de dados replicados](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  