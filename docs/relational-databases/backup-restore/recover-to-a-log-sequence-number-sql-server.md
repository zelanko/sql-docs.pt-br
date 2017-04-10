---
title: "Recuperar para um n&#250;mero de sequ&#234;ncia de log (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "números de sequência de log [SQL Server]"
  - "opção STOPBEFOREMARK [instrução RESTORE]"
  - "opção STOPATMARK [instrução RESTORE]"
  - "recuperação pontual [SQL Server]"
  - "restaurando banco de dados [SQL Server], pontual"
  - "recuperação [SQL Server], bancos de dados"
  - "restaurando [SQL Server], pontual"
  - "LSNs"
  - "recuperação do banco de dados [SQL Server]"
  - "restaurações de banco de dados [SQL Server], pontuais"
ms.assetid: f7b3de5b-198d-448d-8c71-1cdd9239676c
caps.latest.revision: 38
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 37
---
# Recuperar para um n&#250;mero de sequ&#234;ncia de log (SQL Server)
  Este tópico é relevante apenas para bancos de dados que estejam usando modelos de recuperação completa ou bulk-logged.  
  
 Você pode usar um LSN (número de sequência de log) para definir o ponto de recuperação para uma operação de restauração. No entanto, esse é um recurso especializado destinado a fornecedores de ferramentas e provavelmente não é de uso geral.  
  
##  <a name="LSNs"></a> Visão geral de números de sequência de log  
 Os LSNs são usados internamente durante uma sequência RESTORE para localizar o point-in-time para o qual os dados foram restaurados. Quando um backup é restaurado, os dados são restaurados ao LSN que corresponde ao point-in-time em que o backup foi realizado. O backup diferencial e o backup de log avançam o banco de dados restaurado para uma hora posterior que corresponde a um LSN mais alto.  
  
 Cada registro do log de transações é identificado de forma exclusiva por um LSN (número da sequência de log). Os LSNs são ordenados de tal modo que se LSN2 for maior do que LSN1, a alteração descrita pelo registro de log mencionado por LSN2 ocorreu depois da alteração descrita pelo registro de log LSN.  
  
 O LSN de um registro de log no qual ocorreu um evento significativo pode ser útil para construir sequências de restauração corretas. Como são ordenadas, as LSNs podem ser comparadas quanto à igualdade e desigualdade (isto é **\<**, **>**, **=**, **\<=**, **>=**). Essas comparações são úteis ao construir sequências de restauração.  
  
> [!NOTE]  
>  Os LSNs são valores do tipo de dados **numérico**(25,0). Operações aritméticas (por exemplo, adição ou subtração) não são significativas e não devem ser usadas com LSNs.  
  
 [&#91;Início&#93;](#Top)  
  
## Exibindo LSNs usados por Backup e Restauração  
 O LSN de um registro de log no qual um determinado evento de backup e restauração ocorrido pode ser exibido usando um ou mais do seguinte:  
  
-   [backupset](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
-   [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md)  
  
-   [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md); [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
-   [RESTORE HEADERONLY](../Topic/RESTORE%20HEADERONLY%20\(Transact-SQL\).md)  
  
-   [RESTORE FILELISTONLY](../Topic/RESTORE%20FILELISTONLY%20\(Transact-SQL\).md)  
  
> [!NOTE]  
>  Os LSNs também aparecem em alguns textos de mensagem.  
  
## Sintaxe de Transact-SQL para restaurar para um LSN  
 Usando uma instrução [RESTORE](../Topic/RESTORE%20\(Transact-SQL\).md) é possível parar no LSN ou imediatamente antes, da seguinte maneira:  
  
-   Use a cláusula WITH STOPATMARK **='**lsn:*<lsn_number>***'**, em que lsn:*\<lsnNumber>* é uma cadeia de caracteres que especifica que o registro de log que contém o LSN especificado é o ponto de recuperação.  
  
     O STOPATMARK efetua roll forward para o LSN e inclui o registro de log no roll forward.  
  
-   Use a cláusula WITH STOPBEFOREMARK **='**lsn:*<lsn_number>***'**, em que lsn:*\<lsnNumber>* é uma sequência que determina que o registro de log imediatamente anterior ao registro de log que contém o número do LSN especificado é o ponto de recuperação.  
  
     O STOPATMARK efetua roll forward para o LSN e exclui o registro de log do roll forward.  
  
 Normalmente, uma transação específica é selecionada para ser incluída ou excluída. Embora não seja exigido, na prática, o registro de log especificado é um registro da confirmação de transação.  
  
## Exemplos  
 O exemplo a seguir assume que o banco de dados `AdventureWorks` foi alterado para usar o modelo de recuperação completa.  
  
```  
RESTORE LOG AdventureWorks FROM DISK = 'c:\adventureworks_log.bak'   
WITH STOPATMARK = 'lsn:15000000040000037'  
GO  
```  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [Restaurar um backup de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [Restaurar um banco de dados até o ponto de falha no modelo de recuperação completa &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore database to point of failure - full recovery.md)  
  
-   [Restaurar um banco de dados para uma transação marcada &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [Restaurar um banco de dados do SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
## Consulte também  
 [Aplicar backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)  
  
  