---
title: "Lição 9: Gerenciar conjuntos de backup e backups de instantâneo de arquivo | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 766a0846-db15-4346-b814-4049039bcbfc
caps.latest.revision: 10
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9747a3c7730db5d3fe1eda6145ece133c7b6d523
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-9-manage-backup-sets-and-file-snapshot-backups"></a>Lição 9: Gerenciar conjuntos de backup e backups de instantâneo de arquivo
Nesta lição, você aprenderá a excluir um conjunto de backup usando o procedimento armazenado do sistema [sp_delete_backup &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md) . Esse procedimento armazenado do sistema exclui o arquivo de backup e o arquivo de instantâneo em cada arquivo de banco de dados associado a esse conjunto de backup.  
  
> [!NOTE]  
> Se você tentar excluir um conjunto de backup excluindo apenas o arquivo de backup do contêiner de blobs do Azure, você só excluirá o arquivo de backup – os instantâneos de arquivo associados permanecerão. Se você se deparar com este cenário, use a função do sistema [sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md) para identificar a URL dos instantâneos de arquivo órfão e use o procedimento armazenado do sistema [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) para excluir cada instantâneo de arquivo órfão. Para obter mais informações, consulte  [Backups de instantâneo de arquivo para arquivos de banco de dados no Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
Para excluir um conjunto de backup de instantâneo de arquivo, siga estas etapas:  
  
1.  Conecte-se ao SQL Server Management Studio.  
  
2.  Abra uma janela de nova consulta e conecte-se à instância do Azure SQL Server 2016 do mecanismo de banco de dados na máquina virtual do Azure (ou a qualquer instância do SQL Server 2016 com permissões de leitura e gravação nesse contêiner).  
  
3.  Copie e cole o script Transact-SQL a seguir na janela de consulta. Selecione o backup de log que você deseja excluir, juntamente com seus instantâneos de arquivo associados. Modifique a URL de forma adequada para o nome de sua conta de armazenamento e o contêiner especificado na Lição 1, forneça o nome do arquivo de backup de log e execute este script.  
  
    ```  
  
    sys.sp_delete_backup 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/tutorial-9164-20150726012420.bak';  
  
    ```  
  
4.  No Pesquisador de Objetos, conecte-se ao armazenamento do Azure.  
  
5.  Expanda Contêineres, expanda o contêiner criado na Lição 1 e verifique se o arquivo de backup utilizado na etapa 3 não é mais exibido neste contêiner (atualize o nó, conforme necessário).  
  
    ![Contêiner do Azure mostrando a exclusão do blob de backup de log](../relational-databases/media/c0070b08-4667-4db5-aaff-987a404ec934.JPG "Contêiner do Azure mostrando a exclusão do blob de backup de log")  
  
6.  Copie, cole e execute o script Transact-SQL a seguir na janela de consulta para verificar se os dois instantâneos de arquivo foram excluídos.  
  
    ```  
  
    -- verify that two file snapshots have been removed  
    SELECT * from sys.fn_db_backup_file_snapshots ('AdventureWorks2014');  
  
    ```  
  
    ![Painel Resultados mostrando dois instantâneos de arquivo excluídos](../relational-databases/media/f3891361-dfb6-4f4d-a090-ebfeb977981e.JPG "Painel Resultados mostrando dois instantâneos de arquivo excluídos")  
  
**Fim do tutorial**  
  
## <a name="see-also"></a>Consulte também  
[Backups de instantâneo de arquivo para arquivos de banco de dados no Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
[sp_delete_backup &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
[sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)  
[sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)  
  
  
  


