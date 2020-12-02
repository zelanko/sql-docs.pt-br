---
title: Recuperar para um número de sequência de log (SQL Server) | Microsoft Docs
description: No SQL Server, você pode usar o número de sequência de log para recuperar para um determinado ponto. Este recurso destina-se a fornecedores de ferramentas.
ms.custom: ''
ms.date: 10/23/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- log sequence numbers [SQL Server]
- STOPBEFOREMARK option [RESTORE statement]
- STOPATMARK option [RESTORE statement]
- point in time recovery [SQL Server]
- restoring databases [SQL Server], point in time
- recovery [SQL Server], databases
- restoring [SQL Server], point in time
- LSNs
- database recovery [SQL Server]
- database restores [SQL Server], point in time
ms.assetid: f7b3de5b-198d-448d-8c71-1cdd9239676c
author: cawrites
ms.author: chadam
ms.openlocfilehash: 685f7f2ec51688045a528a3cd04f89b043600c9d
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96129163"
---
# <a name="recover-to-a-log-sequence-number-sql-server"></a>Recuperar para um número de sequência de log (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico é relevante apenas para bancos de dados que estejam usando modelos de recuperação completa ou bulk-logged.  
  
 Você pode usar um LSN (número de sequência de log) para definir o ponto de recuperação para uma operação de restauração. No entanto, esse é um recurso especializado destinado a fornecedores de ferramentas e provavelmente não é de uso geral.  
  
##  <a name="overview-of-log-sequence-numbers"></a><a name="LSNs"></a> Visão geral de números de sequência de log  
 Os LSNs são usados internamente durante uma sequência RESTORE para localizar o point-in-time para o qual os dados foram restaurados. Quando um backup é restaurado, os dados são restaurados ao LSN que corresponde ao point-in-time em que o backup foi realizado. O backup diferencial e o backup de log avançam o banco de dados restaurado para uma hora posterior que corresponde a um LSN mais alto. Saiba mais sobre LSNs no [Guia de arquitetura e gerenciamento de log de transações do SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch).  
  
> [!NOTE]  
> Os LSNs são valores do tipo de dados **numérico (25,0)** . Operações aritméticas (por exemplo, adição ou subtração) não são significativas e não devem ser usadas com LSNs.  
 
## <a name="viewing-lsns-used-by-backup-and-restore"></a>Exibir LSNs usados por Backup e Restauração  
 O LSN de um registro de log no qual um determinado evento de backup e restauração ocorrido pode ser exibido usando um ou mais do seguinte:  
  
-   [backupset](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
-   [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md)  
  
-   [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md); [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
-   [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
> [!NOTE]  
>  Os LSNs também aparecem em algumas mensagens no log de erros.  
  
## <a name="transact-sql-syntax-for-restoring-to-an-lsn"></a>Sintaxe de Transact-SQL para restaurar para um LSN  
 Usando uma instrução [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) é possível parar no LSN ou imediatamente antes, da seguinte maneira:  
  
-   Use a cláusula WITH STOPATMARK **='** lsn: _<número_de_lsn>_ **'** , em que lsn: *\<lsnNumber>* é uma cadeia de caracteres que especifica que o registro de log que contém o LSN especificado é o ponto de recuperação.  
  
     O STOPATMARK efetua roll forward para o LSN e inclui o registro de log no roll forward.  
  
-   Use a cláusula WITH STOPBEFOREMARK **='** lsn: _<número_de_lsn>_ **'** , em que lsn: *\<lsnNumber>* é uma cadeia de caracteres que especifica que o registro de log imediatamente anterior ao registro de log que contém o número do LSN especificado é o ponto de recuperação.  
  
     O STOPATMARK efetua roll forward para o LSN e exclui o registro de log do roll forward.  
  
 Normalmente, uma transação específica é selecionada para ser incluída ou excluída. Embora não seja exigido, na prática, o registro de log especificado é um registro da confirmação de transação.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir assume que o banco de dados `AdventureWorks` foi alterado para usar o modelo de recuperação completa.  
  
```sql  
RESTORE LOG AdventureWorks FROM DISK = 'c:\adventureworks_log.bak'   
WITH STOPATMARK = 'lsn:15000000040000037'  
GO  
```  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [Restaurar um backup de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [Restaurar um banco de dados até o ponto de falha no modelo de recuperação completa &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)  
  
-   [Restaurar um banco de dados para uma transação marcada &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [Restaurar um banco de dados do SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Aplicar backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)     
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)     
 [Visão geral da restauração e recuperação (SQL Server)](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#TlogAndRecovery)       
 [Guia de arquitetura e gerenciamento de log de transações do SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)      
  
