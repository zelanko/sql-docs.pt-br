---
title: MSSQL_ENG003165 | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: MSSQL_ENG003165 error
ms.assetid: 707d33dd-644e-4cc9-ac51-dddd49031530
caps.latest.revision: "15"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fa8ceca22073f9540506d978fb56dd92c53b3613
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="mssqleng003165"></a>MSSQL_ENG003165
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|3165|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|O banco de dados '%ls' foi restaurado; entretanto, houve um erro durante a restauração/remoção da replicação. O banco de dados foi deixado offline. Consulte o tópico MSSQL_ENG003165 dos Manuais Online do SQL Server.|  
  
## <a name="explanation"></a>Explicação  
 O erro será gerado se ocorrer um problema durante a restauração de um backup de um banco de dados replicado:  
  
-   Se o backup estiver sendo restaurado para o mesmo banco de dados e servidor nos quais foi obtido, o erro indica que não foi possível restaurar as configurações de replicação corretamente.  
  
-   Se o backup estiver sendo restaurado para um banco de dados ou servidor diferente, o erro indica que não foi possível remover as configurações de replicação corretamente (por padrão, as configurações de replicação são removidas se o banco de dados ou servidor for diferente).  
  
 É provável que o erro seja resultado de uma não correspondência entre o estado de um banco de dados restaurado e um ou mais bancos de dados do sistema com metadados de replicação: banco de dados **msdb**, **mestre**ou de distribuição.  
  
## <a name="user-action"></a>Ação do usuário  
 Para resolver o problema:  
  
1.  Execute ALTER DATABASE para que o banco de dados fique online; por exemplo: `ALTER DATABASE AdventureWorks SET ONLINE`. Para obter mais informações, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md). Se desejar preservar as configurações de replicação, vá para a etapa 2. Caso contrário, vá para a etapa 3.  
  
2.  Execute [sp_restoredbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-restoredbreplication-transact-sql.md). Se esse procedimento armazenado for executado com êxito, a restauração será concluída. Se não for executado com êxito, vá para a etapa 3.  
  
3.  Execute [sp_removedbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) para remover todas as configurações de replicação.  
  
     Se necessário, reconfigure a replicação. Se a topologia de replicação tiver sido inserida no script conforme recomendado, você deverá usar scripts para reconfigurar a topologia.  
  
## <a name="see-also"></a>Consulte Também  
 [Backup e Restauração de bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Fazer backup e restaurar bancos de dados replicados](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
