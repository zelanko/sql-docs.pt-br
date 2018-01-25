---
title: Desabilitar o backup gerenciado do SQL Server no Microsoft Azure | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3e02187f-363f-4e69-a82f-583953592544
caps.latest.revision: "8"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f9dfdda2643529d7a6c632b255065fe3606d3055
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="disable-sql-server-managed-backup-to-microsoft-azure"></a>Desabilitar o backup gerenciado do SQL Server no Microsoft Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tópico descreve como desabilitar ou pausar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] nos níveis de instância e do banco de dados.  
  
##  <a name="DatabaseDisable"></a> Desabilitar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para um banco de dados  
 Você pode desabilitar as configurações do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] usando o procedimento armazenado do sistema, [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md). O *@enable_backup* é usada para habilitar e desabilitar configurações do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para um banco de dados específico, em que 1 habilita e 0 desabilita os parâmetros de configuração.  
  
#### <a name="to-disable-includesssmartbackupincludesss-smartbackup-mdmd-for-a-specific-database"></a>Para desabilitar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para um banco de dados específico:  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
```  
EXEC msdb.managed_backup.sp_backup_config_basic  
                @database_name = 'TestDB'   
                ,@enable_backup = 0;  
GO  
  
```  
  
##  <a name="DatabaseAllDisable"></a> Desabilitar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para todos os bancos de dados na instância  
 O procedimento a seguir deverá ser usado quando você quiser desabilitar parâmetros de configuração do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] de todos os bancos de dados que atualmente têm o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] habilitado na instância.  Os parâmetros de configuração, como a URL de armazenamento, retenção e a Credencial do SQL permanecerão nos metadados e poderão ser usados se o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] for habilitado para o banco de dados posteriormente. Se você quiser apenas pausar os serviços do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] temporariamente, use a opção mestra explicada nas seções posteriores deste tópico.  
  
#### <a name="to-disable-includesssmartbackupincludesss-smartbackup-mdmd-for-all-the-databases"></a>Para desabilitar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para todos os bancos de dados:  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo a seguir identifica se o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está configurado no nível da instância e em todos os bancos de dados do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] habilitados na instância e executa o procedimento armazenado **sp_backup_config_basic** de sistema para desabilitar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
```  
-- Create a working table to store the database names  
Declare @DBNames TABLE  
  
       (  
             RowID int IDENTITY PRIMARY KEY  
             ,DBName varchar(500)  
  
       )  
-- Define the variables  
DECLARE @rowid int  
DECLARE @dbname varchar(500)  
DECLARE @SQL varchar(2000)  
-- Get the database names from the system function  
  
INSERT INTO @DBNames (DBName)  
  
SELECT db_name  
       FROM   
  
       msdb.managed_backup.fn_backup_db_config (NULL)  
       WHERE is_managed_backup_enabled = 1  
  
       --Select DBName from @DBNames  
  
       select @rowid = min(RowID)  
       FROM @DBNames  
  
       WHILE @rowID IS NOT NULL  
       Begin  
  
             Set @dbname = (Select DBName From @DBNames Where RowID = @rowid)  
             Begin  
             Set @SQL = 'EXEC msdb.managed_backup.sp_backup_config_basic    
                @database_name= '''+'' + @dbname+ ''+''',   
                @enable_backup=0'  
  
            EXECUTE (@SQL)  
  
             END  
             Select @rowid = min(RowID)  
             From @DBNames Where RowID > @rowid  
  
       END  
```  
  
 Para examinar os parâmetros de configuração de todos os bancos de dados da instância, use a seguinte consulta:  
  
```  
Use msdb;  
GO  
SELECT * FROM managed_backup.fn_backup_db_config (NULL);  
GO  
  
```  
  
##  <a name="InstanceDisable"></a> Habilitar as configurações padrão do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para a instância  
 As configurações padrão no nível da instância se aplicam a todos os novos bancos de dados criados nessa instância.  Se não precisar mais das configurações padrão ou estas não forem mais exigidas, você poderá desabilitar essa configuração usando o procedimento armazenado do sistema **managed_backup.sp_backup_config_basic** com o parâmetro *@database_name* definido como NULL. A desabilitação não remove os outros parâmetros de configuração como a URL de armazenamento, a configuração de retenção ou o nome da Credencial do SQL. Essas configurações serão usadas se o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] estiver habilitado para a instância mais tarde.  
  
#### <a name="to-disable-includesssmartbackupincludesss-smartbackup-mdmd-default-configuration-settings"></a>Para desabilitar os parâmetros de configuração padrão do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] :  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    EXEC msdb.managed_backup.sp_backup_config_basic  
                    @database_name = 'TestDB'   
                    ,@enable_backup = 0;  
    GO  
  
    ```  
  
##  <a name="InstancePause"></a> Pause o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] no nível da instância  
 Pode haver momentos em que você precise pausar temporariamente os serviços do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] por um curto período de tempo.  O procedimento armazenado do sistema **managed_backup.sp_backup_master_switch** permite que você desabilite o serviço do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] no nível da instância.  O mesmo procedimento armazenado é usado para retomar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. O parâmetro @state é usado para definir se o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] deve ser desativado ou ativado.  
  
#### <a name="to-pause-includesssmartbackupincludesss-smartbackup-mdmd-services-using-transact-sql"></a>Para pausar os serviços do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] usando o Transact-SQL:  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
```  
Use msdb;  
GO  
EXEC managed_backup.sp_backup_master_switch @new_state=0;  
Go  
  
```  
  
#### <a name="to-resume-includesssmartbackupincludesss-smartbackup-mdmd-using-transact-sql"></a>Para retomar o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] usando Transact-SQL  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
```  
Use msdb;  
Go  
EXEC managed_backup. sp_backup_master_switch @new_state=1;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Habilitar o backup gerenciado do SQL Server no Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)  
  
  
