---
title: "Backups de instant&#226;neo de arquivo para arquivos de banco de dados no Azure | Microsoft Docs"
ms.custom: 
  - "IAAS"
  - "SQL2016_New_Updated"
ms.date: "05/23/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 17a81fcd-8dbd-458d-a9c7-2b5209062f45
caps.latest.revision: 34
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 33
---
# Backups de instant&#226;neo de arquivo para arquivos de banco de dados no Azure
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O backup de instantâneo de arquivo usa os instantâneos do Azure para fornecer backups quase imediatos e restaurações mais rápidas para os arquivos de banco de dados armazenados usando o serviço de Armazenamento de Blobs do Azure. Esse recurso permite que você simplifique as políticas de backup e restauração. Para uma demonstração ao vivo, confira [Demonstração da recuperação pontual](https://channel9.msdn.com/Blogs/Windows-Azure/File-Snapshot-Backups-Demo). Para saber mais sobre como armazenar arquivos de banco de dados usando o serviço de armazenamento de Blog do Azure, consulte [Arquivos de dados do SQL Server no Microsoft Azure](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md).  
  
 ![snapshot backup architectural diagram](../../relational-databases/backup-restore/media/snapshotbackups.PNG "snapshot backup architectural diagram")  
  
 **Download**  
  
-   Para baixar o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], acesse o **[Centro de Avaliação](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)**.  
  
-   Tem uma conta do Azure?  Em seguida, acesse **[aqui](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016ctp3evaluationwindowsserver2012r2/?wt.mc_id=sqL16_vm)** para criar uma Máquina Virtual com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] já instalado.  
  
## Como usar instantâneos do Azure para fazer backup de arquivos de banco de dados armazenados no Azure  
  
### O que é um backup de instantâneo de arquivo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Um backup de instantâneo de arquivo é composto por um conjunto de instantâneos do Azure dos blobs que contêm os arquivos de banco de dados, mais um arquivo de backup que contém ponteiros para esses instantâneos de arquivo. Cada instantâneo de arquivo é armazenado no contêiner com o blob de base. Você pode especificar que o próprio arquivo de backup seja gravado em URL, disco ou fita. Recomendamos o backup em URL. Para obter mais informações sobre como fazer backup, consulte [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md) e sobre como fazer backup em uma URL, consulte [Backup do SQL Server para URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md).  
  
 ![architecture of snapshot feature](../../relational-databases/backup-restore/media/snapshotbackups-flat.png "architecture of snapshot feature")  
  
 A exclusão do blob de base invalidará o conjunto de backup, e não é possível descartar um blob que contenha instantâneos de arquivo (a menos que você escolha expressamente excluir um blob com todos os seus instantâneos de arquivo). Além disso, descartar um banco de dados ou um arquivo de dados não exclui o blob de base ou qualquer um de seus instantâneos de arquivo. Além disso, excluir o arquivo de backup não exclui qualquer instantâneo de arquivo no conjunto de backup. Para excluir um conjunto de backup de instantâneo de arquivo, use o procedimento armazenado do sistema **sys.sp_delete_backup**.  
  
 **Backup completo do banco de dados:** a execução de um backup completo do banco de dados usando o backup de instantâneo de arquivo cria um instantâneo do Azure para cada arquivo de log e de dados que compõe o banco de dados, estabelece a cadeia de backup de log de transações e grava o local dos instantâneos de arquivo no arquivo de backup.  
  
 **Backup de log de transações:** a execução de um backup de log de transações usando o backup de instantâneo de arquivo cria um instantâneo de arquivo para cada arquivo de banco de dados (não apenas do log de transações), registra as informações de local do instantâneo de arquivo no arquivo de backup e trunca o arquivo de log de transações.  
  
> [!IMPORTANT]  
>  Após o backup inicial completo, obrigatório para estabelecer a cadeia de backup de log de transações (que pode ser um backup de instantâneo de arquivo), basta executar os backups de log de transações, pois cada conjunto de backups de instantâneo de arquivo do log de transações contém instantâneos de arquivo de todos os arquivos de banco de dados, e pode ser usado para executar uma restauração de banco de dados ou uma restauração de log. Após o backup inicial completo do banco de dados, não é necessário realizar outros backups completos ou diferenciais, pois o serviço de Armazenamento de Blobs do Azure lida com as diferenças entre cada instantâneo de arquivo e o estado atual do blob de base de cada arquivo de banco de dados.  
  
> [!NOTE]  
>  Para obter um tutorial sobre como usar o SQL Server 2016 com o serviço de Armazenamento de Blobs do Microsoft Azure, confira [Tutorial: usando o serviço de Armazenamento de Blobs do Microsoft Azure com bancos de dados do SQL Server 2016](https://msdn.microsoft.com/library/dn466438.aspx)  
  
### Restaurar usando backups de instantâneo de arquivo  
 Como cada conjunto de backups de instantâneo de arquivo contém um instantâneo de arquivo de cada arquivo de banco de dados, e um processo de restauração exige no máximo dois conjuntos adjacentes de backup de instantâneo de arquivo. Isso é verdadeiro independentemente de o conjunto de backup ser de um backup de banco de dados completo ou de um backup de log. Isso é muito diferente do processo de restauração que usa arquivos de backup de streaming tradicional para executar o processo de restauração. Com o backup de streaming tradicional, o processo de restauração exige o uso de uma cadeia inteira de conjuntos de backup: o backup completo, um backup diferencial e um ou mais backups de log de transações. A parte de recuperação do processo de restauração permanece a mesma, independentemente de a restauração usar um backup de instantâneo de arquivo ou um conjunto de backup de streaming.  
  
 **Para o horário de um conjunto de backup:** para executar uma operação RESTORE DATABASE para restaurar um banco de dados para o horário de um conjunto de backup de instantâneo de arquivo específico, somente o conjunto de backup específico é necessário, além dos próprios blobs de base. Como você pode usar um conjunto de backup de instantâneo de arquivo do log de transações para executar uma operação RESTORE DATABASE, normalmente você usará um conjunto de backup de log de transações para realizar esse tipo de operação RESTORE DATABASE, e raramente usará um conjunto de backup de banco de dados completo. Veja ao final deste tópico um exemplo que demonstra essa técnica.  
  
 **Para um ponto no tempo entre dois conjuntos de backup de instantâneo de arquivo:** para executar uma operação RESTORE DATABASE a fim de restaurar um banco de dados para um ponto específico no tempo entre dois conjuntos de backup adjacentes de log de transações, você precisará apenas de dois conjuntos de backup de log de transações (um antes e outro após o ponto no tempo no qual você deseja restaurar o banco de dados). Para fazer isso, você deve executar uma operação RESTORE DATABASE WITH NORECOVERY usando o conjunto de backup de instantâneo de arquivo do log de transações do ponto no tempo anterior, e realizar uma operação RESTORE LOG WITH RECOVERY usando o conjunto de backup de instantâneo de arquivo do log de transações do ponto no tempo mais recente, além de usar o argumento STOPAT para especificar o ponto no tempo no qual interromper a recuperação do backup de log de transações. Veja ao final deste tópico um exemplo que demonstra essa técnica. Para uma demonstração ao vivo, confira [Demonstração da recuperação pontual](https://channel9.msdn.com/Blogs/Windows-Azure/File-Snapshot-Backups-Demo).  
  
### Manutenção do conjunto de backup de arquivos  
 **Excluir um conjunto de backup de instantâneo de arquivo:** não é possível substituir um conjunto de backup de instantâneo de arquivo usando o argumento FORMAT. O argumento FORMAT não recebe permissão, a fim de evitar deixar órfãos os instantâneos de arquivos que foram criados com o backup de instantâneo de arquivo original. Para excluir um conjunto de backup de instantâneo de arquivo, use o procedimento armazenado do sistema **sys.sp_delete_backup**. Esse procedimento armazenado exclui o arquivo de backup e os instantâneos de arquivo que compõem o conjunto de backup. O uso de outro método para excluir um conjunto de backup de instantâneo de arquivo pode excluir o arquivo de backup sem excluir os instantâneos de arquivo no conjunto de backup.  
  
 **Exclusão de instantâneos de arquivo de backup órfãos:** talvez você tenha instantâneos de arquivo órfãos se o arquivo de backup tiver sido excluído sem usar o procedimento armazenado do sistema **sys.sp_delete_backup**, ou se um banco de dados, ou arquivo de banco de dados, tiver sido descartado, mas os blobs que contêm o banco de dados ou o arquivo de banco de dados tiverem instantâneos de arquivo de backup associados a eles. Para identificar os instantâneos de arquivo que podem ser órfãos, use a função do sistema **sys.fn_db_backup_file_snapshots** para listar todos os instantâneos de arquivo dos arquivos de banco de dados. Para identificar os instantâneos de arquivo que fazem parte de um conjunto de backup de instantâneo de arquivo específico, use o procedimento armazenado do sistema RESTORE FILELISTONLY. Em seguida, você pode usar o procedimento armazenado do sistema **sys.sp_delete_backup_file_snapshot** para excluir um instantâneo de arquivo de backup individual que ficou órfão. Veja ao final deste tópico exemplos que usam essa função de sistema e esses procedimentos armazenados do sistema. Para obter mais informações, consulte [sp_delete_backup &#40;Transact-SQL&#41;](../Topic/sp_delete_backup%20\(Transact-SQL\).md), [sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md), [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../Topic/sp_delete_backup_file_snapshot%20\(Transact-SQL\).md) e [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../Topic/RESTORE%20FILELISTONLY%20\(Transact-SQL\).md).  
  
### Considerações e limitações  
 **Armazenamento premium:** ao usar o armazenamento premium, as seguintes limitações se aplicam:  
  
-   O próprio arquivo de backup não pode ser armazenado usando o armazenamento premium.  
  
-   A frequência dos backups não pode ser inferior a 10 minutos.  
  
-   O número máximo de instantâneos que você pode armazenar é de 100.  
  
-   RESTORE WITH MOVE é obrigatório.  
  
-   Para obter informações adicionais sobre o armazenamento premium, consulte [Armazenamento Premium: armazenamento de alto desempenho para as cargas de trabalho da máquina virtual do Azure](https://azure.microsoft.com/documentation/articles/storage-premium-storage-preview-portal/)  
  
 **Conta única de armazenamento:** o instantâneo de arquivo e os blobs de destino devem usar a mesma conta de armazenamento.  
  
 **Modelo de recuperação em massa:** ao usar o modo de recuperação bulk-logged e trabalhar com um backup de log de transações que contém transações com registros mínimos, não é possível fazer uma restauração do log (incluindo a recuperação pontual) usando o backup de log de transações. Em vez disso, execute uma restauração de banco de dados para o horário do conjunto de backup de instantâneo de arquivo. Essa limitação é idêntica à limitação com o backup de streaming.  
  
 **Restauração Online:** ao usar os backups de instantâneo de arquivo, não é possível executar uma Restauração online. Para obter mais informações sobre restaurações online, consulte [Restauração online &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md).  
  
 **Cobrança:** ao usar o backup de instantâneo de arquivo do SQL Server, encargos adicionais serão gerados à medida que os dados mudarem. Para saber mais, consulte [Noções básicas sobre como os instantâneos acumulam cobranças](https://msdn.microsoft.com/library/azure/hh768807.aspx).  
  
 **Arquivamento:** se você quiser arquivar um backup de instantâneo de arquivo, poderá arquivar no Armazenamento de Blobs ou no backup de streaming. Para arquivar no Armazenamento de Blobs, copie os instantâneos no conjunto de backup de instantâneo de arquivo em blobs separados. Para arquivar o backup de streaming, restaure o backup de instantâneo de arquivo como um novo banco de dados e execute um backup de streaming normal com compactação e/ou criptografia, e arquive-o durante o tempo desejado, independentemente dos blobs de base.  
  
> [!IMPORTANT]  
>  A manutenção de vários backups de instantâneo de arquivo tem apenas uma pequena sobrecarga de desempenho. No entanto, manter uma quantidade excessiva de backups de instantâneo de arquivo pode afetar o desempenho de E/S no banco de dados. Recomendamos que você mantenha apenas os backups de instantâneo de arquivo necessários para oferecer suporte ao seu objetivo de ponto de recuperação.  
  
## Backup do banco de dados e do log usando um backup de instantâneo de arquivo  
 O exemplo abaixo usa o backup de instantâneo de arquivo para fazer backup do banco de dados de exemplo AdventureWorks2016 em URL.  
  
```  
-- To permit log backups, before the full database backup, modify the database   
-- to use the full recovery model.  
USE master;  
GO  
ALTER DATABASE AdventureWorks2016  
   SET RECOVERY FULL;  
GO  
-- Back up the full AdventureWorks2016 database.  
BACKUP DATABASE AdventureWorks2016   
TO URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mycontainername>/AdventureWorks2016.bak'   
WITH FILE_SNAPSHOT;  
GO  
-- Back up the AdventureWorks2016 log using a time stamp in the backup file name.  
DECLARE @Log_Filename AS VARCHAR (300);  
SET @Log_Filename = 'https://<mystorageaccountname>.blob.core.windows.net/<mycontainername>/AdventureWorks2016_Log_'+   
REPLACE (REPLACE (REPLACE (CONVERT (VARCHAR (40), GETDATE (), 120), '-','_'),':', '_'),' ', '_') + '.trn';  
BACKUP LOG AdventureWorks2016  
 TO URL = @Log_Filename WITH FILE_SNAPSHOT;  
GO  
```  
  
## Restauração de um backup de instantâneo de arquivo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 O exemplo a seguir restaura o banco de dados AdventureWorks2016 usando um conjunto de backup de instantâneo de arquivo do log de transações e mostra uma operação de recuperação. Observe que você pode restaurar um banco de dados de um único conjunto de backup de instantâneo de arquivo do log de transações.  
  
```  
RESTORE DATABASE AdventureWorks2016 FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mycontainername>/AdventureWorks2016_2015_05_18_16_00_00.trn'   
WITH RECOVERY, REPLACE;  
GO  
```  
  
## Restauração de um backup de instantâneo de arquivo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um ponto no tempo  
 O exemplo a seguir restaura o banco de dados AdventureWorks2016 para seu estado em um momento específico usando dois conjuntos de backup de instantâneo de arquivo do log de transações, e mostra uma operação de recuperação.  
  
```  
RESTORE DATABASE AdventureWorks2016 FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mycontainername>/AdventureWorks2016_2015_05_18_16_00_00.trn'   
WITH NORECOVERY,REPLACE;  
GO   
  
RESTORE LOG AdventureWorks2016 FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mycontainername>/AdventureWorks2016_2015_05_18_18_00_00.trn'   
WITH RECOVERY,STOPAT = 'May 18, 2015 5:35 PM';  
GO  
```  
  
## Exclusão de um conjunto de backup de instantâneo de arquivo do banco de dados  
 Para excluir um conjunto de backup de instantâneo de arquivo, use o procedimento armazenado do sistema **sys.sp_delete_backup**. Especifique o nome do banco de dados para que o sistema verifique se o conjunto de backup de instantâneo de arquivo especificado é realmente um backup do banco de dados especificado. Se nenhum nome de banco de dados for especificado, o conjunto de backup especificado com seus instantâneos de arquivo será excluído sem essa validação. Para obter mais informações, consulte [sp_delete_backup &#40;Transact-SQL&#41;](../Topic/sp_delete_backup%20\(Transact-SQL\).md).  
  
> [!WARNING]  
>  A tentativa de excluir um conjunto de backup de instantâneo de arquivo usando outro método, como o Portal de Gerenciamento do Microsoft Azure ou o Visualizador do Armazenamento do Azure no SQL Server Management Studio, não excluirá os instantâneos de arquivos no conjunto de backup. Essas ferramentas excluirão apenas o próprio arquivo de backup que contém os ponteiros para os instantâneos de arquivos no conjunto de backup de instantâneo de arquivo. Para identificar os instantâneos de arquivo de backup que permanecem após a exclusão indevida de um arquivo de backup, use a função do sistema **sys.fn_db_backup_file_snapshots**, e use o procedimento armazenado do sistema **sys.sp_delete_backup_file_snapshot** para excluir um instantâneo de arquivo de backup individual.  
  
 O exemplo a seguir exclui conjunto de backup de instantâneo de arquivo especificado, incluindo o arquivo de backup e os instantâneos de arquivo que compõem o conjunto de backup especificado.  
  
```  
sys.sp_delete_backup 'https://<mystorageaccountname>.blob.core.windows.net/<mycontainername>/AdventureWorks2016.bak', 'adventureworks2016' ;  
GO  
  
```  
  
## Exibição dos instantâneos de arquivo de backup do banco de dados  
 Para exibir instantâneos de arquivo do blob de base para cada arquivo de banco de dados, use a função do sistema **sys.fn_db_backup_file_snapshots**. Essa função do sistema permite que você exiba todos os instantâneos de arquivo de backup de cada blob de base para um banco de dados armazenado usando o serviço de Armazenamento de Blobs do Azure. Um caso de uso principal para essa função é identificar os instantâneos de arquivo de backup de um banco de dados que permanece quando o arquivo de backup de um conjunto de backup de instantâneo de arquivo for excluído usando um mecanismo diferente do procedimento armazenado do sistema **sys.sp_delete_backup**. Para determinar os instantâneos de arquivo de backup que fazem parte dos conjuntos de backup intactos e aqueles que não fazem parte dos conjuntos de backup intactos, use o procedimento armazenado do sistema **RESTORE FILELISTONLY** para listar os instantâneos de arquivos que pertencem a cada arquivo de backup. Para obter mais informações, consulte [sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md) e [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../Topic/RESTORE%20FILELISTONLY%20\(Transact-SQL\).md).  
  
 O exemplo a seguir retorna a lista de todos os instantâneos de arquivo de backup do banco de dados especificado.  
  
```  
--Either specify the database name or set the database context  
USE AdventureWorks2016  
select * from sys.fn_db_backup_file_snapshots (null) ;  
GO  
select * from sys.fn_db_backup_file_snapshots ('AdventureWorks2016') ;  
GO  
  
```  
  
## Excluir um instantâneo de arquivo de backup de banco de dados individual  
 Para excluir um instantâneo de arquivo de backup individual de um blob de base de banco de dados, use o procedimento armazenado do sistema **sys.sp_delete_backup_file_snapshot**. Um caso de uso principal para este procedimento armazenado do sistema é a exclusão dos arquivos de instantâneo de arquivos órfãos que permanecem após a exclusão de um arquivo de backup usando um método diferente do procedimento armazenado do sistema **sys.sp_delete_backup**. Para obter mais informações, consulte [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../Topic/sp_delete_backup_file_snapshot%20\(Transact-SQL\).md).  
  
> [!WARNING]  
>  A exclusão de um instantâneo de arquivo individual que faz parte de um conjunto de backup de instantâneo de arquivo invalidará o conjunto de backup.  
  
 O exemplo a seguir exclui o instantâneo de arquivo de backup especificado. A URL do backup especificado foi obtida usando a função do sistema **sys.fn_db_backup_file_snapshots**.  
  
```  
sys.sp_delete_backup_file_snapshot N'adventureworks2016', N'https://<mystorageaccountname>.blob.core.windows.net/<mycontainername>/AdventureWorks2016Data.mdf?snapshot=2015-05-29T21:31:31.6502195Z';  
GO  
```  
  
## Este artigo foi útil para você? Estamos atentos  
 Quais são as informações que você está procurando? Você as localizou? Estamos atentos aos seus comentários para aprimorar o conteúdo. Envie seus comentários para [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20File-Snapshot%20Backups%20for%20Database%20Files%20in%20Azure%20page)  
  
## Consulte também  
 [Tutorial: Como usar o serviço de Armazenamento de Blobs do Microsoft Azure com os bancos de dados do SQL Server 2016](https://msdn.microsoft.com/library/dn466438.aspx)  
  
  