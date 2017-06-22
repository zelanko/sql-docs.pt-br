---
title: "Configurar opções avançadas de backup gerenciado do SQL Server para o Microsoft Azure | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ffd28159-8de8-4d40-87da-1586bfef3315
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6c41a2a22b034f36ebe96508e978096b0ed29524
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure"></a>Configurar opções avançadas de backup gerenciado do SQL Server para o Microsoft Azure
  O tutorial a seguir descreve como definir opções avançadas para o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Esses procedimentos só serão necessários se você precisar dos recursos que oferecem. Caso contrário, você pode habilitar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] e depender do comportamento padrão.  
  
 Em cada cenário, o backup é especificado usando o parâmetro `database_name` . Quando `database_name` é NULL ou *, as alterações afetam as configurações padrão no nível da instância. Configurações de nível de instância também afetam os novos bancos de dados criados após a alteração.  
  
 Depois de especificar essas configurações, será possível habilitar o backup gerenciado para o banco de dados ou a instância usando o procedimento armazenado do sistema [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md). Para obter mais informações, veja [Habilitar o backup gerenciado do SQL Server no Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md).  
  
> [!WARNING]  
>  Você sempre deve configurar as opções avançadas e as opções de agendamento personalizado antes de habilitar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] com [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md). Caso contrário, é possível que operações de backup não desejadas ocorram durante a janela de tempo entre a habilitação do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] e a definição dessas configurações.  
  
## <a name="configure-encryption"></a>Configurar a criptografia  
 As etapas a seguir descrevem como especificar as configurações de criptografia usando o procedimento armazenado [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md).  
  
1.  **Determinar o algoritmo de criptografia:** primeiro determine o nome do algoritmo de criptografia a ser usado. Selecione um dos seguintes algoritmos.  
  
    -   AES_128  
  
    -   AES_192  
  
    -   AES_256  
  
    -   TRIPLE_DES_3KEY  
  
    -   NO_ENCRYPTION  
  
2.  **Criar uma chave mestra de banco de dados:** Escolha uma senha por criptografar a cópia da chave mestra que será armazenada no banco de dados.  
  
    ```  
    -- Creates a database master key.  
    -- The key is encrypted using the password "<master key password>"  
    USE Master;  
    GO  
       CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
    ```  
  
3.  **Criar um certificado de backup ou uma chave assimétrica:** você pode usar um certificado ou uma chave assimétrica com a criptografia. O exemplo a seguir cria um certificado de backup a ser usado na criptografia.  
  
    ```tsql  
    USE Master;  
    GO  
       CREATE CERTIFICATE MyTestDBBackupEncryptCert  
          WITH SUBJECT = 'MyTestDBBackupEncryptCert';  
    GO  
    ```  
  
4.  **Definir criptografia de backup gerenciado:** chame o procedimento armazenado **managed_backup.sp_backup_config_advanced** com os valores correspondentes. Por exemplo, o exemplo a seguir configura o banco de dados `MyDB` para criptografia usando um certificado denominado `MyTestDBBackupEncryptCert` e o algoritmo de criptografia `AES_128` .  
  
    ```  
    USE msdb;  
    GO  
       EXEC managed_backup.sp_backup_config_advanced  
          @database_name = 'MyDB'                
          ,@encryption_algorithm ='AES_128'  
          ,@encryptor_type = 'CERTIFICATE'  
          ,@encryptor_name = 'MyTestDBBackupEncryptCert';  
    GO  
    ```  
  
    > [!WARNING]  
    >  Se `@database_name` for NULL no exemplo anterior, as configurações se aplicarão à instância do SQL Server.  
  
## <a name="configure-a-custom-backup-schedule"></a>Configurar um agendamento de backup personalizado  
 As etapas a seguir descrevem como definir um agendamento personalizado com o procedimento armazenado [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md).  
  
1.  **Determinar a frequência de backups completos:** determine a frequência de backups completos do banco de dados. Você pode escolher entre backups completos “Diariamente” e “Semanalmente”.  
  
2.  **Determinar a frequência de backups do log:** determine a frequência de um backup de log. Esse valor é em minutos ou horas.  
  
3.  **Determinar o dia da semana para os backups semanais:** se o backup for semanal, escolha um dia da semana para o backup completo.  
  
4.  **Determinar a hora de início do bakup:** usando a notação de 24 horas, escolha um horário para iniciar o backup.  
  
5.  **Determinar o período de tempo do backup:** especifica a quantidade de tempo que um backup tem para ser concluído.  
  
6.  **Definir o agendamento de backup personalizada:** o procedimento armazenado a seguir define um agendamento personalizada para o banco de dados `MyDB` . Backups completos são realizados semanalmente em `Monday` às `17:30`. Backups de log são executados a cada `5` minutos. Os backups têm duas horas para serem concluídos.  
  
    ```  
    USE msdb;  
    GO  
    EXEC managed_backup.sp_backup_config_schedule   
         @database_name =  'MyDB'  
        ,@scheduling_option = 'Custom'  
        ,@full_backup_freq_type = 'Weekly'  
        ,@days_of_week = 'Monday'  
        ,@backup_begin_time =  '17:30'  
        ,@backup_duration = '02:00'  
        ,@log_backup_freq = '00:05'  
    GO  
  
    ```  
  
## <a name="next-steps"></a>Próximas etapas  
 Depois de configurar opções avançadas e agendas personalizadas, é necessário habilitar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] no banco de dados de destino ou instância do SQL Server. Para obter mais informações, veja [Habilitar o backup gerenciado do SQL Server no Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md).  
  
## <a name="see-also"></a>Consulte também  
 [Backup gerenciado do SQL Server no Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
