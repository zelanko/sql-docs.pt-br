---
title: Preparar um banco de dados secundário para um grupo de disponibilidade
description: Uma descrição de como preparar manualmente um banco de dados secundário para ingressá-lo em um Grupo de Disponibilidade AlwaysOn.
ms.custom: seodec18
ms.date: 07/25/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.preparedbs.f1
- sql13.swb.availabilitygroup.configsecondarydbs.f1
helpviewer_keywords:
- secondary databases [SQL Server], in availability group
- secondary databases [SQL Server]
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], databases
ms.assetid: 9f2feb3c-ea9b-4992-8202-2aeed4f9a6dd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: aaf5b4f4c8e93d3f36ddbd4768ebf2e453112fae
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726360"
---
# <a name="prepare-a-secondary-database-for-an-always-on-availability-group"></a>Preparar um banco de dados secundário manualmente para um Grupo de Disponibilidade AlwaysOn
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
Este tópico descreve como preparar um banco de dados para um grupo de disponibilidade AlwaysOn no [!INCLUDE[ssnoversion](../../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou o PowerShell. A preparação de um banco de dados exige duas etapas: 

1. Restaurar um backup de banco de dados recente do banco de dados primário e os backups de log posteriores em cada instância de servidor que hospeda a réplica secundária, usando RESTORE WITH NORECOVERY
2. Ingressar o banco de dados restaurado no grupo de disponibilidade.  
  
> [!TIP]  
>  Se você tiver uma configuração de envio de logs existente, talvez consiga converter o banco de dados primário de envio de logs junto com um ou mais de seus bancos de dados secundários em uma réplica primária do grupo de disponibilidade e em uma ou mais réplicas secundárias. Para obter mais informações, consulte [Pré-requisitos para a migração do envio de logs para Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-migrating-log-shipping-to-always-on-availability-groups.md).  

##  <a name="prerequisites-and-restrictions"></a><a name="Prerequisites"></a> Pré-requisitos e restrições  
  
-   Verifique se o sistema onde você planeja colocar o banco de dados possui um disco com espaço suficiente para os bancos de dados secundários.  
  
-   O nome do banco de dados secundário deve ser igual ao nome do banco de dados primário.  
  
-   Use RESTORE WITH NORECOVERY para cada operação de restauração.  
  
-   Se o banco de dados secundário precisar residir em um caminho de arquivo diferente (inclusive a letra da unidade) do banco de dados primário, o comando de restauração também deve usar a opção WITH MOVE para cada um dos arquivos de banco de dados para especificar o caminho do banco de dados secundário.  
  
-   Se restaurar o grupo de arquivos de banco de dados pelo grupo de arquivos, restaure todo o banco de dados.  
  
-   Depois de restaurar o banco de dados, você deve restaurar (WITH NORECOVERY) cada backup de log criado desde o último backup de dados restaurado.  
  
##  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Em instâncias autônomas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], é recomendável que, se possível, o caminho do arquivo (incluindo a letra da unidade) de um determinado banco de dados secundário seja idêntico ao caminho do banco de dados primário correspondente. Isso ocorre porque, se você mover os arquivos de banco de dados ao criar um banco de dados secundário, uma operação de adição de arquivo posterior poderá apresentar falha no banco de dados secundário e fazer com que o banco de dados secundário seja suspenso.  
  
-   Antes de preparar seus bancos de dados secundários, é altamente recomendável suspender os backups de log agendados nos bancos de dados no grupo de disponibilidade até que a inicialização das réplicas secundárias seja concluída.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
 Quando é feito backup de um banco de dados, a [propriedade TRUSTWORTHY do banco de dados](../../../relational-databases/security/trustworthy-database-property.md) é definida como OFF. Portanto, em um banco de dados recém-restaurado, TRUSTWORTHY sempre será OFF.  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 As permissões BACKUP DATABASE e BACKUP LOG usam como padrão os membros da função de servidor fixa **sysadmin** e as funções de banco de dados fixas **db_owner** e **db_backupoperator** . Para obter mais informações, veja [BACKUP &#40;Transact-SQL&#41;](../../../t-sql/statements/backup-transact-sql.md).  
  
 Quando o banco de dados que está sendo restaurado não existir na instância do servidor, a instrução RESTORE exigirá as permissões CREATE DATABASE. Para obter mais informações, veja [RESTORE &#40;Transact-SQL&#41;](../../../t-sql/statements/restore-statements-transact-sql.md).  
  
##  <a name="use-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usar o SQL Server Management Studio  
  
> [!NOTE]  
>  Se os caminhos de arquivos de backup e restauração forem idênticos entre a instância de servidor que hospeda a réplica primária e todas as instâncias que hospedam uma réplica secundária, você deverá conseguir criar bancos de dados secundários com o [Assistente de Novo Grupo de Disponibilidade](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md), o [Assistente para Adicionar Réplica a um Grupo de Disponibilidade](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md) ou o [Assistente para Adicionar Banco de Dados a um Grupo de Disponibilidade](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md).  
  
 **Para preparar um banco de dados secundário**  
  
1.  A menos que você já tenha um backup recente do banco de dados primário, crie um novo backup completo ou diferencial do banco de dados. Como prática recomendada, coloque esse backup e qualquer backup de log subsequente no compartilhamento de rede recomendado.  
  
2.  Crie pelo menos um novo backup de log do banco de dados primário.

   >[!NOTE]
   >Um backup de log de transações poderá não ser necessário se um backup de log de transações não tiver sido capturado anteriormente no banco de dados na réplica primária. A Microsoft recomenda fazer um backup de log de transações sempre que um novo banco de dados é ingressado no grupo de disponibilidade. 
  
3.  Na instância do servidor que hospeda a réplica secundária, restaure o backup completo do banco de dados primário (e opcionalmente um backup diferencial) seguido por quaisquer backups de log subsequentes.  
  
     Na página **Opções de RESTORE DATABASE**, selecione **Deixar o banco de dados não operacional e não reverter as transações não confirmadas. Os logs de transações adicionais podem ser restaurados. (RESTAURAR COM NORECOVERY)** .  
  
     Se os caminhos de arquivo dos bancos de dados primário e secundário forem diferentes, por exemplo, se o banco de dados primário estiver na unidade 'F:', mas a instância do servidor que hospeda a réplica secundária não tiver uma unidade F:, inclua a opção MOVE na cláusula WITH.  
  
4.  Para concluir a configuração do banco de dados secundário, você precisa unir o banco de dados secundário ao grupo de disponibilidade. Para obter mais informações, veja [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md).  
  
> [!NOTE]  
>  Para obter informações sobre como executar estas operações de backup e restauração, veja [Tarefas de backup e restauração relacionadas](#RelatedTasks), mais adiante nesta seção.  
  
###  <a name="related-backup-and-restore-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas a backup e restauração  
 **Para criar um backup de banco de dados**  
  
-   [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Criar um backup diferencial de banco de dados &#40;SQL Server&#41;](../../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
 **Para criar um backup do log**  
  
-   [Fazer backup de um log de transações &#40;SQL Server&#41;](../../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
 **Para restaurar backups**  
  
-   [Restore a Database Backup Using SSMS](../../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [Restaurar um backup de banco de dados diferencial &#40;SQL Server&#41;](../../../relational-databases/backup-restore/restore-a-differential-database-backup-sql-server.md)  
  
-   [Restaurar um backup de log de transações &#40;SQL Server&#41;](../../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [Restaurar um banco de dados em um novo local &#40;SQL Server&#41;](../../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para preparar um banco de dados secundário**  
  
> [!NOTE]  
>  Para obter um exemplo desse procedimento, veja [Exemplo (Transact-SQL)](#ExampleTsql), acima neste tópico.  
  
1.  A menos que você tenha um backup completo recente do banco de dados primário, conecte-se à instância do servidor que hospeda a réplica primária e crie um backup completo do banco de dados. Como prática recomendada, coloque esse backup e qualquer backup de log subsequente no compartilhamento de rede recomendado.  
  
2.  Na instância do servidor que hospeda a réplica secundária, restaure o backup completo do banco de dados primário (e opcionalmente um backup diferencial) seguido por todos os backups de log subsequentes. Use WITH NORECOVERY para cada operação de restauração.  
  
     Se os caminhos de arquivo dos bancos de dados primário e secundário forem diferentes, por exemplo, se o banco de dados primário estiver na unidade 'F:', mas a instância do servidor que hospeda a réplica secundária não tiver uma unidade F:, inclua a opção MOVE na cláusula WITH.  
  
3.  Se quaisquer backups de log tiverem sido executados no banco de dados primário desde o backup de log necessário, será necessário copiá-los na instância do servidor que hospeda a réplica secundária e aplicar cada um desses backups de log ao banco de dados secundário, começando com o mais recente e sempre usando RESTORE WITH NORECOVERY.  
  
    > [!NOTE]  
    >  Um backup de log não existirá se o banco de dados primário tiver acabado de ser criado, e nenhum backup de log tiver sido executado ainda, ou se o modelo de recuperação tiver acabado de ser alterado de simples para completo.  
  
4.  Para concluir a configuração do banco de dados secundário, você precisa unir o banco de dados secundário ao grupo de disponibilidade. Para obter mais informações, veja [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md).  
  
> [!NOTE]  
>  Para obter informações sobre como executar estas operações de backup e restauração, veja [Tarefas de backup e restauração relacionadas](#RelatedTasks), mais adiante neste tópico.  
  
###  <a name="transact-sql-example"></a><a name="ExampleTsql"></a> Exemplo de Transact-SQL  
 O exemplo a seguir prepara um banco de dados secundário. Esse exemplo usa o banco de dados de exemplo do [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] que, por padrão, usa o modelo de recuperação simples.  
  
1.  Para usar o banco de dados [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] , modifique-o para usar o modelo de recuperação completa:  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE MyDB1   
    SET RECOVERY FULL;  
    GO  
    ```  
  
2.  Depois de modificar o modelo de recuperação do banco de dados de SIMPLE para FULL, crie um backup completo, que pode ser usado para criar o banco de dados secundário. Como o modelo de recuperação acabou de ser alterado, a opção WITH FORMAT estará especificada para criar um novo conjunto de mídias. Isso é útil para separar os backups sob o modelo de recuperação completa de qualquer backup anterior feito sob o modelo de recuperação simples. Para a finalidade deste exemplo, o arquivo de backup (C:\\[!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)].bak) será criado na mesma unidade que o banco de dados.  
  
    > [!NOTE]  
    >  Em um banco de dados de produção, você deve sempre fazer backup em um dispositivo separado.  
  
     Na instância do servidor que hospeda a réplica primária (`INSTANCE01`), crie um backup completo do banco de dados primário da seguinte maneira:  
  
    ```  
    BACKUP DATABASE MyDB1   
        TO DISK = 'C:\MyDB1.bak'   
        WITH FORMAT  
    GO  
    ```  
  
3.  Copie o backup completo na instância do servidor que hospeda a réplica secundária.  
  
4.  Restaure o backup completo usando RESTORE WITH NORECOVERY na instância do servidor que hospeda a réplica secundária. O comando de restauração depende de se os caminhos dos bancos de dados primário e secundário são idênticos.  
  
    -   **Se os caminhos forem idênticos:**  
  
         No computador que hospeda a réplica secundária, restaure o backup completo da seguinte maneira:  
  
        ```  
        RESTORE DATABASE MyDB1   
            FROM DISK = 'C:\MyDB1.bak'   
            WITH NORECOVERY  
        GO  
        ```  
  
    -   **Se os caminhos forem diferentes:**  
  
         Se o caminho do banco de dados secundário for diferente do caminho do banco de dados primário (por exemplo, se as letras das unidades forem diferentes), a criação do banco de dados secundário exigirá que a operação de restauração inclua uma cláusula MOVE.  
  
        > [!IMPORTANT]  
        >  Se os nomes dos caminhos dos bancos de dados primário e secundário forem diferentes, não será possível adicionar um arquivo. Isso acontece porque, ao receber o log para a operação de adição de arquivo, a instância do servidor da réplica secundária tenta colocar o novo arquivo no mesmo caminho usado pelo banco de dados primário.  
  
         Por exemplo, o comando a seguir restaura um backup de um banco de dados primário que reside no diretório de dados da instância padrão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], C:\Arquivos de Programas\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA. A operação de restauração do banco de dados deve mover o banco de dados para o diretório de dados de uma instância remota do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] denominada (*Always On1*), que hospeda a réplica secundária em outro nó de cluster. Lá, os arquivos de dados e de log são restaurados para o diretório *C:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.Always On1\MSSQL\DATA* . O operação de restauração usa WITH NORECOVERY, para deixar o banco de dados secundário no banco de dados de restauração.  
  
        ```  
        RESTORE DATABASE MyDB1  
          FROM DISK='C:\MyDB1.bak'  
         WITH NORECOVERY,   
            MOVE 'MyDB1_Data' TO   
             'C:\Program Files\Microsoft SQL Server\MSSQL13.Always On1\MSSQL\DATA\MyDB1_Data.mdf',   
            MOVE 'MyDB1_Log' TO  
             'C:\Program Files\Microsoft SQL Server\MSSQL13.Always On1\MSSQL\DATA\MyDB1_Data.ldf';  
        GO  
        ```  
  
5.  Depois que você restaura o backup completo, será necessário criar um backup de log no banco de dados primário. Por exemplo, a seguinte instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] faz backup do log em um arquivo de backup chamado *E:\MyDB1_log.trn*:  
  
    ```  
    BACKUP LOG MyDB1   
      TO DISK = 'E:\MyDB1_log.trn'   
    GO  
    ```  
  
6.  Para poder unir o banco de dados com a réplica secundária, é necessário aplicar o backup de log exigido (e qualquer backup de log subsequente).  
  
     Por exemplo, a seguinte instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] restaura o primeiro log de *C:\MyDB1.trn*:  
  
    ```  
    RESTORE LOG MyDB1   
      FROM DISK = 'E:\MyDB1_log.trn'   
        WITH FILE=1, NORECOVERY  
    GO  
    ```  
  
7.  Se qualquer backup de log adicional ocorrer antes da junção do banco de dados com a réplica secundária, você também deverá restaurar todos esses backups de log, em sequência, na instância do servidor que hospeda a réplica secundária usando RESTORE WITH NORECOVERY.  
  
     Por exemplo, a seguinte instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] restaura dois logs adicionais de *E:\MyDB1_log.trn*:  
  
    ```  
    RESTORE LOG MyDB1   
      FROM DISK = 'E:\MyDB1_log.trn'   
        WITH FILE=2, NORECOVERY  
    GO  
    RESTORE LOG MyDB1   
      FROM DISK = 'E:\MyDB1_log.trn'   
        WITH FILE=3, NORECOVERY  
    GO  
    ```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para preparar um banco de dados secundário**  
  
1.  Se você precisar criar um backup recente do banco de dados primário, altere o diretório (**cd**) para a instância de servidor que hospeda a réplica primária.  
  
2.  Use o cmdlet **Backup-SqlDatabase** para criar cada um dos backups.  
  
3.  Altere o diretório (**cd**) para a instância de servidor que hospeda a réplica secundária.  
  
4.  Para restaurar os backups do banco de dados e do log de cada banco de dados primário, use o cmdlet **restore-SqlDatabase** , especificando o parâmetro de restauração **NoRecovery** . Se os caminhos dos arquivos forem diferentes nos computadores que hospedam a réplica primária e a réplica secundária de destino, use também o parâmetro de restauração **RelocateFile** .  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet **Get-Help** no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
5.  Para concluir a configuração do banco de dados secundário, você precisa uni-lo ao grupo de disponibilidade. Para obter mais informações, veja [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md)  
  
###  <a name="sample-backup-and-restore-script-and-command"></a><a name="ExamplePSscript"></a> Script e comando de backup e restauração de exemplo  
 Os comandos PowerShell a seguir fazem backup de um backup de banco de dados completo e do log de transações em um compartilhamento de rede e restaura esses backups a partir desse compartilhamento. Este exemplo supõe que o caminho do arquivo para o qual o banco de dados é restaurado é igual ao caminho do arquivo no qual foi feito o backup do banco de dados.  
  
```  
# Create database backup  
Backup-SqlDatabase -Database "MyDB1" -BackupFile "\\share\backups\MyDB1.bak" -ServerInstance "SourceMachine\Instance"  
# Create log backup  
Backup-SqlDatabase -Database "MyDB1" -BackupAction "Log" -BackupFile "\\share\backups\MyDB1.trn" -ServerInstance "SourceMachine\Instance"  
# Restore database backup   
Restore-SqlDatabase -Database "MyDB1" -BackupFile "\\share\backups\MyDB1.bak" -NoRecovery -ServerInstance "DestinationMachine\Instance"  
# Restore log backup   
Restore-SqlDatabase -Database "MyDB1" -BackupFile "\\share\backups\MyDB1.trn" -RestoreAction "Log" -NoRecovery -ServerInstance "DestinationMachine\Instance"  
  
```  
  
##  <a name="next-steps"></a><a name="FollowUp"></a> Próximas etapas  
 Para concluir a configuração do banco de dados secundário, una o banco de dados recém-restaurado ao grupo de disponibilidade. Para obter mais informações, consulte [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md).  
  
## <a name="see-also"></a>Confira também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../../t-sql/statements/backup-transact-sql.md)   
 [Argumentos de RESTORE &#40;Transact-SQL&#41;](../../../t-sql/statements/restore-statements-arguments-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../../t-sql/statements/restore-statements-transact-sql.md)   
 [Solução de problemas de uma operação de adição de arquivos com falha &#40;Grupos de disponibilidade de AlwaysOn&#41;](../../../database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
