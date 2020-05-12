---
title: Restauração de backups armazenados no Microsoft Azure | Microsoft Docs
description: Compreenda os aspectos da restauração de um banco de dados do SQL Server usando um backup armazenado no Armazenamento de Blobs do Azure.
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 6ae358b2-6f6f-46e0-a7c8-f9ac6ce79a0e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b608af9a25b6a4fe14078043276e0689990e6246
ms.sourcegitcommit: 37a3e2c022c578fc3a54ebee66d9957ff7476922
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922259"
---
# <a name="restoring-from-backups-stored-in-microsoft-azure"></a>Restaurando de backups armazenados no Microsoft Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve o que você precisa considerar ao restaurar um banco de dados usando um backup armazenado no serviço de Armazenamento de Blobs do Azure. Isso se aplica aos backups criados através do Backup do SQL Server para URL ou pelo [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
 É recomendável analisar este tópico se você tiver backups armazenados no serviço de Armazenamento de Blobs do Azure que pretende restaurar e, em seguida, analisar os tópicos que descrevem as etapas de restauração de um banco de dados, que são as mesmas para backups locais e do Azure.  
  
## <a name="overview"></a>Visão geral  
 As ferramentas e os métodos que são usados para restaurar um banco de dados de um backup local se aplicam à restauração de um banco de dados de um backup na nuvem.  As seções a seguir descrevem essas considerações e todas as diferenças que você precisa saber ao usar os backups armazenados no serviço de Armazenamento de Blobs do Azure.  
  
### <a name="using-transact-sql"></a>Usando o Transact-SQL  
  
-   Como o SQL Server precisa se conectar a uma fonte externa para recuperar os arquivos de backup, a Credenciais do SQL é usada para autenticação para a conta de armazenamento. Em virtude disso, a instrução RESTORE requer a opção WITH CREDENTIAL. Para obter mais informações, consulte [Backup e restauração do SQL Server com o serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
-   Se você estiver usando o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para gerenciar seus backups para a nuvem, poderá examinar todos os backups disponíveis no armazenamento usando a função de sistema **smart_admin.fn_available_backups** . Essa função de sistema retorna todos os backups disponíveis para um banco de dados em uma tabela. Como os resultados são retornados em uma tabela, você pode filtrá-los ou classificá-los. Para obter mais informações, veja [managed_backup.fn_available_backups &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql.md).  
  
### <a name="using-sql-server-management-studio"></a>Como usar o SQL Server Management Studio.  
  
-   A tarefa de restauração é usada restaurar um banco de dados usando o SQL Server Management Studio. A página da mídia de backup agora inclui a opção **URL** para mostrar os arquivos de backup armazenados no serviço de Armazenamento de Blobs do Azure. Você também deve fornecer a Credencial do SQL usada para autenticação para a conta de armazenamento. A grade **Conjuntos de backup a serem restaurados** é preenchida com os backups disponíveis no Armazenamento de Blobs do Azure. Para obter mais informações, confira [Restaurar por meio do Armazenamento do Microsoft Azure usando o SQL Server Management Studio](../../relational-databases/backup-restore/sql-server-backup-to-url.md#RestoreSSMS).  
  
### <a name="optimizing-restores"></a>Otimizando restaurações  
 Para reduzir o tempo de gravação da restauração, adicione o direito de usuário **Executar tarefas de manutenção de volume** à conta de usuário do SQL Server. Para obter mais informações, consulte [Inicialização de arquivos de bancos de dados](https://go.microsoft.com/fwlink/?LinkId=271622). Se a restauração ainda estiver lenta com a inicialização instantânea de arquivo ativada, examine o tamanho do arquivo de log na instância onde foi feito o backup do banco de dados. Se o log é muito grande em tamanho (vários GBs), espera-se que a restauração seja lenta. Durante a restauração, o arquivo de log deve ser zerado, o que leva uma quantidade significativa de tempo.  
  
 Para reduzir o tempo de restauração, recomendamos o uso de backups compactados.  Para os tamanhos de backup superiores a 25 GB, use o [utilitário AzCopy](https://docs.microsoft.com/archive/blogs/windowsazurestorage/azcopy-uploadingdownloading-files-for-windows-azure-blobs) para baixar à unidade local e execute a restauração. Para outras práticas recomendadas de backup e recomendações, consulte [SQL Server Backup to URL Best Practices and Troubleshooting](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md).  
  
 Você também pode ativar o sinalizador de rastreamento 3051 ao fazer a restauração para gerar um log detalhado. Este arquivo de log é colocado no diretório de log e nomeado usando o formato: BackupToUrl-\<instancename>-\<dbname>-action-\<PID>.log. O arquivo de log inclui informações sobre cada viagem de ida e volta para o Armazenamento do Microsoft Azure, inclusive o controle de tempo, que pode ser útil para diagnosticar o problema.  
  
### <a name="topics-on-performing-restore-operations"></a>Tópicos sobre a execução de operações de restauração  
  
-   [Restaurações completas de banco de dados &#40;Modelo de recuperação simples#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [Restaurações completas de banco de dados &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)  
  
-   [Restaurações de arquivos &#40;Modelo de recuperação simples&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)  
  
-   [Restaurações de arquivo &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)  
  
-   [Restaurações por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
