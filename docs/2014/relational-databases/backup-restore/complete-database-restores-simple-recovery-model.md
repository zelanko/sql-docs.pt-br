---
title: Restaurações completas de banco de dados (modelo de recuperação simples) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- complete database restores
- database restores [SQL Server], complete database
- restoring databases [SQL Server], complete database
- simple recovery model [SQL Server]
- restoring [SQL Server], database
ms.assetid: 49828927-1727-4d1d-9ef5-3de43f68c026
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e64bf4d4642d8091cd0892283a996e7dccc56e26
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62877113"
---
# <a name="complete-database-restores-simple-recovery-model"></a>Restaurações completas de banco de dados (modelo de recuperação simples)
  Em uma restauração completa de banco de dados, a meta é restaurar todo o banco de dados. O banco de dados inteiro fica offline durante a restauração. Antes que qualquer parte do banco de dados possa ficar online, todos os dados são recuperados a um ponto consistente, no qual todas as partes do banco de dados estejam no mesmo momento determinado e não exista nenhuma transação não confirmada.  
  
 No modelo de recuperação simples, o banco de dados não poderá ser restaurado para um momento determinado específico durante um backup específico.  
  
> [!IMPORTANT]  
>  Não é recomendável anexar ou restaurar bancos de dados de origem desconhecida ou não confiável. Esses bancos de dados podem conter códigos mal-intencionados que podem executar códigos [!INCLUDE[tsql](../../../includes/tsql-md.md)] inesperados ou causar erros que modifiquem o esquema ou a estrutura física do banco de dados. Antes de usar um banco de dados de origem desconhecida ou não confiável, execute [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) no banco de dados, em um servidor que não seja de produção. Além disso, examine o código, como procedimentos armazenados ou outro código definido pelo usuário, no banco de dados.  
  

  
> [!NOTE]  
>  Para obter informações sobre suporte para backups de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja a seção “Suporte de compatibilidade” de [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).  
  
##  <a name="overview-of-database-restore-under-the-simple-recovery-model"></a><a name="Overview"></a> Visão geral da restauração de banco de dados no modelo de recuperação simples  
 Uma restauração de banco de dados completa no modelo de recuperação simples envolve uma ou duas instruções [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) , dependendo se você deseja restaurar um backup de banco de dados diferencial. Se você estiver usando somente um backup de banco de dados completo, simplesmente restaure o backup mais recente, conforme mostrado na ilustração abaixo.  
  
 ![Restaurando apenas um backup de banco de dados completo](../../database-engine/media/bnrr-rmsimple1-fulldbbu.gif "Restaurando apenas um backup de banco de dados completo")  
  
 Se você também estiver usando um backup de banco de dados diferencial, restaure o backup de banco de dados completo mais recente sem recuperar o banco de dados, e em seguida restaure o backup de banco de dados diferencial mais recente e recupere o banco de dados. A ilustração a seguir mostra este processo.  
  
 ![Restaurando backups de banco de dados diferenciais e completos](../../database-engine/media/bnrr-rmsimple2-diffdbbu.gif "Restaurando backups de banco de dados diferenciais e completos")  
  
> [!NOTE]  
>  Se você pretende restaurar um backup de banco de dados em uma instância de servidor diferente, consulte [Copiar bancos de dados com Backup e Restauração](../databases/copy-databases-with-backup-and-restore.md).  
  
###  <a name="basic-transact-sql-restore-syntax"></a><a name="TsqlSyntax"></a> Sintaxe básica de RESTORE do Transact-SQL  
 A sintaxe básica [!INCLUDE[tsql](../../../includes/tsql-md.md)][RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) para restaurar um backup de banco de dados completo é:  
  
 RESTORE DATABASE *database_name* FROM *backup_device* [ WITH NORECOVERY ]  
  
> [!NOTE]  
>  Use WITH NORECOVERY se você também planeja restaurar um backup de banco de dados diferencial.  
  
 A sintaxe básica [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) para restaurar um backup de banco de dados é:  
  
 RESTORE DATABASE *database_name* FROM *backup_device* WITH RECOVERY  
  
###  <a name="example-transact-sql"></a><a name="Example"></a>Exemplo (Transact-SQL)  
 O exemplo a seguir mostra inicialmente como usar a instrução [BACKUP](/sql/t-sql/statements/backup-transact-sql) para criar um backup de banco de dados completo e um backup de banco de dados diferencial do banco de dados do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . O exemplo restaura em seguida estes backups em sequência. O banco de dados é restaurado a seu estado a partir do momento em que o backup de banco de dados diferencial é concluído.  
  
 O exemplo mostra as opções críticas em uma sequência de restauração referentes a um cenário de restauração de banco de dados completa. Uma *sequência de restauração* consiste em uma ou mais operações de restauração que movem dados por uma ou mais etapas da restauração. Sintaxe e detalhes que não sejam relevantes para esse propósito são omitidos. Quando você recupera um banco de dados, nós recomendamos especificar explicitamente a opção RECOVERY para que haja melhor clareza, mesmo que este seja o padrão.  
  
> [!NOTE]  
>  O exemplo inicia com uma instrução [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) que define o modelo de recuperação como `SIMPLE`.  
  
```  
USE master;  
--Make sure the database is using the simple recovery model.  
ALTER DATABASE AdventureWorks2012 SET RECOVERY SIMPLE;  
GO  
-- Back up the full AdventureWorks2012 database.  
BACKUP DATABASE AdventureWorks2012   
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'   
  WITH FORMAT;  
GO  
--Create a differential database backup.  
BACKUP DATABASE AdventureWorks2012   
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'  
   WITH DIFFERENTIAL;  
GO  
--Restore the full database backup (from backup set 1).  
RESTORE DATABASE AdventureWorks2012   
FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'   
   WITH FILE=1, NORECOVERY;  
--Restore the differential backup (from backup set 2).  
RESTORE DATABASE AdventureWorks2012   
FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'   
   WITH FILE=2, RECOVERY;  
GO  
```  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para restaurar um backup de banco de dados completo**  
  
-   [Restaurar um backup de banco de dados no modelo de recuperação simples &#40;Transact-SQL&#41;](restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [Restaurar um backup de banco de dados &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [Restaurar um banco de dados em um novo local &#40;SQL Server&#41;](restore-a-database-to-a-new-location-sql-server.md)  
  
 **Para restaurar um backup de banco de dados diferencial**  
  
-   [Restaurar um backup de banco de dados diferencial &#40;SQL Server&#41;](restore-a-differential-database-backup-sql-server.md)  
  
 **Para restaurar um backup usando o SQL Server Management Objects (SMO)**  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A>  
  

  
## <a name="see-also"></a>Consulte Também  
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [&#41;&#40;Transact-SQL de sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [Backups completos de banco de dados &#40;SQL Server&#41;](full-database-backups-sql-server.md)   
 [Backups diferenciais &#40;SQL Server&#41;](differential-backups-sql-server.md)   
 [Visão geral do backup &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Visão geral de restauração e recuperação &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)  
  
  
