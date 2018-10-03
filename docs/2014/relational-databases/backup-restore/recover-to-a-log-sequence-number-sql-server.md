---
title: Recuperar para um número de sequência de log (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e88773137297430763f5ddd47cf7b95030f53d87
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48050375"
---
# <a name="recover-to-a-log-sequence-number-sql-server"></a>Recuperar para um número de sequência de log (SQL Server)
  Este tópico é relevante apenas para bancos de dados que estejam usando modelos de recuperação completa ou bulk-logged.  
  
 Você pode usar um LSN (número de sequência de log) para definir o ponto de recuperação para uma operação de restauração. No entanto, esse é um recurso especializado destinado a fornecedores de ferramentas e provavelmente não é de uso geral.  
  
##  <a name="LSNs"></a> Visão geral de números de sequência de log  
 Os LSNs são usados internamente durante uma sequência RESTORE para localizar o point-in-time para o qual os dados foram restaurados. Quando um backup é restaurado, os dados são restaurados ao LSN que corresponde ao point-in-time em que o backup foi realizado. O backup diferencial e o backup de log avançam o banco de dados restaurado para uma hora posterior que corresponde a um LSN mais alto.  
  
 Cada registro do log de transações é identificado de forma exclusiva por um LSN (número da sequência de log). Os LSNs são ordenados de tal modo que se LSN2 for maior do que LSN1, a alteração descrita pelo registro de log mencionado por LSN2 ocorreu depois da alteração descrita pelo registro de log LSN.  
  
 O LSN de um registro de log no qual ocorreu um evento significativo pode ser útil para construir sequências de restauração corretas. Como são ordenadas, as LSNs podem ser comparadas quanto à igualdade e desigualdade (isto é **\<**, **>**, **=**, **\<=**, **>=**). Essas comparações são úteis ao construir sequências de restauração.  
  
> [!NOTE]  
>  Os LSNs são valores de tipo de dados `numeric`(25,0). Operações aritméticas (por exemplo, adição ou subtração) não são significativas e não devem ser usadas com LSNs.  
  

  
## <a name="viewing-lsns-used-by-backup-and-restore"></a>Exibindo LSNs usados por Backup e Restauração  
 O LSN de um registro de log no qual um determinado evento de backup e restauração ocorrido pode ser exibido usando um ou mais do seguinte:  
  
-   [backupset](/sql/relational-databases/system-tables/backupset-transact-sql)  
  
-   [backupfile](/sql/relational-databases/system-tables/backupfile-transact-sql)  
  
-   [sys.database_files](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql); [sys.master_files](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
-   [RESTORE HEADERONLY](/sql/t-sql/statements/restore-statements-headeronly-transact-sql)  
  
-   [RESTORE FILELISTONLY](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql)  
  
> [!NOTE]  
>  Os LSNs também aparecem em alguns textos de mensagem.  
  
## <a name="transact-sql-syntax-for-restoring-to-an-lsn"></a>Sintaxe de Transact-SQL para restaurar para um LSN  
 Usando uma instrução [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) é possível parar no LSN ou imediatamente antes, da seguinte maneira:  
  
-   Use a cláusula WITH STOPATMARK **='** lsn:*<lsn_number>***'**, em que lsn:*\<lsnNumber>* é uma cadeia de caracteres que especifica que o registro de log que contém o LSN especificado é o ponto de recuperação.  
  
     O STOPATMARK efetua roll forward para o LSN e inclui o registro de log no roll forward.  
  
-   Use a cláusula WITH STOPBEFOREMARK **='** lsn:*<lsn_number>***'**, em que lsn:*\<lsnNumber>* é uma cadeia de caracteres que especifica que o registro de log imediatamente anterior ao registro de log que contém o número do LSN especificado é o ponto de recuperação.  
  
     O STOPATMARK efetua roll forward para o LSN e exclui o registro de log do roll forward.  
  
 Normalmente, uma transação específica é selecionada para ser incluída ou excluída. Embora não seja exigido, na prática, o registro de log especificado é um registro da confirmação de transação.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir assume que o banco de dados `AdventureWorks` foi alterado para usar o modelo de recuperação completa.  
  
```  
RESTORE LOG AdventureWorks FROM DISK = 'c:\adventureworks_log.bak'   
WITH STOPATMARK = 'lsn:15000000040000037'  
GO  
```  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Restaurar um Backup de banco de dados &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [Fazer backup de um log de transações &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [Restaurar um backup de log de transações &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)  
  
-   [Restaurar um banco de dados até o ponto de falha no modelo de recuperação completa &#40;Transact-SQL&#41;](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [Restaurar um banco de dados para uma transação marcada &#40;SQL Server Management Studio&#41;](restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [Restaurar um banco de dados do SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
## <a name="see-also"></a>Consulte também  
 [Aplicar backups de log de transações &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [O log de transações &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
