---
title: "Li&#231;&#227;o 9: Gerenciar conjuntos de backup e backups de instant&#226;neo de arquivo | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 766a0846-db15-4346-b814-4049039bcbfc
caps.latest.revision: 10
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 10
---
# Li&#231;&#227;o 9: Gerenciar conjuntos de backup e backups de instant&#226;neo de arquivo
Nesta lição, você aprenderá a excluir um conjunto de backup usando o procedimento armazenado do sistema [sp_delete_backup &#40;Transact-SQL&#41;](../Topic/sp_delete_backup%20(Transact-SQL).md). Esse procedimento armazenado do sistema exclui o arquivo de backup e o arquivo de instantâneo em cada arquivo de banco de dados associado a esse conjunto de backup.  
  
> [!NOTE]  
> Se você tentar excluir um conjunto de backup excluindo apenas o arquivo de backup do contêiner de blobs do Azure, você só excluirá o arquivo de backup – os instantâneos de arquivo associados permanecerão. Se você se deparar com este cenário, use a função do sistema [sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md) para identificar a URL dos instantâneos de arquivo órfão e use o procedimento armazenado do sistema [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../Topic/sp_delete_backup_file_snapshot%20(Transact-SQL).md) para excluir cada instantâneo de arquivo órfão. Para obter mais informações, consulte [Backups de instantâneo de arquivo para arquivos de banco de dados no Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
Para excluir um conjunto de backup de instantâneo de arquivo, siga estas etapas:  
  
1.  Conecte-se ao SQL Server Management Studio.  
  
2.  Abra uma janela de nova consulta e conecte-se à instância do Azure SQL Server 2016 do mecanismo de banco de dados na máquina virtual do Azure (ou a qualquer instância do SQL Server 2016 com permissões de leitura e gravação nesse contêiner).  
  
3.  Copie e cole o script Transact-SQL a seguir na janela de consulta. Selecione o backup de log que você deseja excluir, juntamente com seus instantâneos de arquivo associados. Modifique a URL de forma adequada para o nome de sua conta de armazenamento e o contêiner especificado na Lição 1, forneça o nome do arquivo de backup de log e execute este script.  
  
    ```  
  
    sys.sp_delete_backup 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/tutorial-9164-20150726012420.bak';  
  
    ```  
  
4.  No Pesquisador de Objetos, conecte-se ao armazenamento do Azure.  
  
5.  Expanda Contêineres, expanda o contêiner criado na Lição 1 e verifique se o arquivo de backup utilizado na etapa 3 não é mais exibido neste contêiner (atualize o nó, conforme necessário).  
  
    ![Azure container showing the deletion of the log backup blob](../relational-databases/media/c0070b08-4667-4db5-aaff-987a404ec934.JPG "Azure container showing the deletion of the log backup blob")  
  
6.  Copie, cole e execute o script Transact-SQL a seguir na janela de consulta para verificar se os dois instantâneos de arquivo foram excluídos.  
  
    ```  
  
    -- verify that two file snapshots have been removed  
    SELECT * from sys.fn_db_backup_file_snapshots ('AdventureWorks2014');  
  
    ```  
  
    ![Results pane showing 2 file snapshots deleted](../relational-databases/media/f3891361-dfb6-4f4d-a090-ebfeb977981e.JPG "Results pane showing 2 file snapshots deleted")  
  
**Fim do tutorial**  
  
## Consulte também  
[Backups de instantâneo de arquivo para arquivos de banco de dados no Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
[sp_delete_backup &#40;Transact-SQL&#41;](../Topic/sp_delete_backup%20(Transact-SQL).md)  
[sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)  
[sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../Topic/sp_delete_backup_file_snapshot%20(Transact-SQL).md)  
  
  
  
