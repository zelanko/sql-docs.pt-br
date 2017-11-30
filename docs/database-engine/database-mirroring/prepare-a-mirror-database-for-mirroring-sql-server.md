---
title: Preparar um banco de dados espelho para espelhamento (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 11/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database mirroring [SQL Server], preparing for mirroring
- logins [SQL Server], database mirroring
- mirror database [SQL Server]
ms.assetid: 8676f9d8-c451-419b-b934-786997d46c2b
caps.latest.revision: "43"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c8a533d76c1dc37a1a067c9971ec4cc4fa771790
ms.sourcegitcommit: 284a64817d5641b5245bc70ddebef2dc51d2e558
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2017
---
# <a name="prepare-a-mirror-database-for-mirroring-sql-server"></a>Preparar um banco de dados espelho para espelhamento (SQL Server)
  Antes de uma sessão de espelhamento do banco de dados poder iniciar, o proprietário do banco de dados ou administrador de sistema devem ter certeza de que o banco de dados espelho foi criado e está pronto para espelhar. A criação de um novo banco de dados espelho requer minimamente um backup cheio do banco de dados principal e um backup de log subsequente e a restauração de ambos sobre a instância do servidor espelho, usando WITH NORECOVERY.  
  
 Este tópico descreve como preparar um banco de dados espelho no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   **Antes de começar:**  
  
     [Requisitos](#Requirements)  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   [Para preparar um banco de dados espelho existente para reiniciar o espelhamento](#PrepareToRestartMirroring)  
  
-   [Para preparar um novo banco de dados espelho](#CombinedProcedure)  
  
-   **Acompanhamento:**  [depois de preparar um banco de dados espelho](#FollowUp)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Requirements"></a> Requisitos  
  
-   As instâncias de servidor principal e espelho devem ser executadas na mesma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Embora o servidor espelho possa ter uma versão posterior do SQL Server, essa configuração é recomendável somente durante um processo de atualização cuidadosamente planejado. Nessa configuração, você corre o risco de um failover automático, no qual a movimentação de dados é suspensa automaticamente porque os dados não podem migrar para uma versão anterior do SQL Server. Para obter mais informações, veja [Atualizando instâncias espelhadas](../../database-engine/database-mirroring/upgrading-mirrored-instances.md).  
  
-   As instâncias de servidor principal e espelho devem ser executadas na mesma edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter informações sobre o suporte para o espelhamento de banco de dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], consulte [Edições e recursos com suporte do SQL Server 2017](~/sql-server/editions-and-components-of-sql-server-2017.md).  
  
-   O banco de dados deve usar o modelo de recuperação completa.  
  
     Para obter mais informações, veja [Exibir ou alterar o modelo de recuperação de um banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md) ou [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) e [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
-   O nome do banco de dados espelho deve ser igual ao nome do banco de dados principal.  
  
-   O banco de dados espelho deve estar no estado de RESTORING para espelhar o trabalho. Ao preparar um banco de dados espelho, é necessário usar RESTORE WITH NORECOVERY para todas as operações de restauração. Minimamente, você precisará restaurar o backup completo WITH NORECOVERY do banco de dados principal, seguido por todos os backups de log subsequentes.  
  
-   O sistema onde você planeja criar o banco de dados espelho deve ter uma unidade de disco com espaço suficiente para conter o banco de dados espelho.  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Não é possível espelhar os bancos de dados do sistema **mestre**, **msdb**, **temp**ou **modelo** .  
  
-   Não é possível espelhar um banco de dados que pertence a um [grupo de disponibilidade AlwaysOn](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md).  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Use um backup de banco de dados completo muito recente ou diferencial recente do banco de dados principal.  
  
-   Se um trabalho de backup de log estiver agendado para ser executado com muita frequência no banco de dados principal, talvez você precise desabilitar o trabalho de backup até o início do espelhamento.  
  
-   Se possível, o caminho (inclusive a letra da unidade) do banco de dados espelho deve ser idêntico ao caminho do banco de dados principal.  
  
     Se os caminhos dos arquivos precisarem ser diferentes, por exemplo, se o banco de dados principal estiver na unidade 'F:', mas o sistema espelho não tiver uma unidade F:, será necessário incluir a opção MOVE na instrução RESTORE.  
  
    > [!IMPORTANT]  
    >  Ao adicionar um arquivo durante uma sessão de espelhamento sem afetá-la, é necessário que o caminho do arquivo exista nos dois servidores. Portanto, se você mover os arquivos de banco de dados quando estiver criando o banco de dados espelho, uma operação adicionar arquivo posterior pode não funcionar no banco de dados espelho e causar a suspensão do espelhamento. Para obter informações sobre como lidar com uma falha na operação de criar arquivo, veja [Solução de problemas de configuração de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md).  
  
-   Se o banco de dados principal tiver catálogos de texto completo, é recomendável conferir [Espelhamento de banco de dados e catálogos de texto completo &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-full-text-catalogs-sql-server.md).  
  
-   Em um banco de dados de produção, sempre faça backup em um dispositivo separado.  
  
###  <a name="Security"></a> Segurança  
 TRUSTWORTHY é definido como OFF em um backup de banco de dados. Portanto, em um novo banco de dados espelho, TRUSTWORTHY será sempre OFF. Se o banco de dados tiver que ser confiável depois de um failover, serão necessárias etapas de instalação adicionais. Para obter mais informações, veja [Configurar um banco de dados espelho para usar a propriedade confiável &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md).  
  
 Para obter informações sobre como habilitar a decodificação automática da chave mestre de um banco de dados espelho, veja [Configurar um banco de dados espelho criptografado](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md).  
  
####  <a name="Permissions"></a> Permissões  
 Proprietário de banco de dados ou administrador do sistema.  
  
##  <a name="PrepareToRestartMirroring"></a> Para preparar um banco de dados espelho existente para reiniciar o espelhamento  
 Se o espelhamento foi removido e o banco de dados espelho ainda está no estado de RECOVERING, você pode reinicializar o espelhamento.  
  
1.  Faça pelo menos um backup de log no banco de dados principal. Para obter mais informações, veja [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md).  
  
2.  No banco de dados espelho, use RESTORE WITH NORECOVERY para restaurar todos os backups de logs efetuados no banco de dados principal desde que o espelhamento foi removido. Para obter mais informações, veja [Restaurar um backup de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md).  
  
##  <a name="CombinedProcedure"></a> Para preparar um novo banco de dados espelho  
 **Para preparar um banco de dados espelho**  
  
> [!NOTE]  
>  Para obter um exemplo [!INCLUDE[tsql](../../includes/tsql-md.md)] desse procedimento, veja [Exemplo (Transact-SQL)](#TsqlExample), mais adiante nesta seção.  
  
1.  Conecte-se à instância de servidor principal.  
  
2.  Crie um backup de banco de dados completo ou diferencial do banco de dados principal.  
  
    -   [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
    -   [Criar um backup de banco de dados diferencial &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md).  
  
3.  Geralmente, você precisa efetuar pelo menos um backup de log no banco de dados principal. Porém, um backup de log pode ser desnecessário, caso o banco de dados tenha acabado de ser criado e nenhum backup realizado ou se o modelo de recuperação foi alterado de SIMPLE para FULL.  
  
    -   [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
4.  A menos que os backups estejam em uma unidade de rede que esteja acessível de ambos os sistemas, copie o banco de dados e os backups de log para o sistema que hospedará a instância de servidor espelho.  
  
5.  Conecte-se à instância de servidor espelho.  
  
6.  Usando RESTORE WITH NORECOVERY, crie o banco de dados espelho restaurando o backup completo do banco de dados e, opcionalmente, o backup de banco de dados diferencial mais recente, na instância do servidor espelho.  
  
    > [!NOTE]  
    >  Se restaurar o grupo de arquivos de banco de dados pelo grupo de arquivos, restaure todo o banco de dados.  
  
    -   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
    -   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md) e [Argumentos de RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
7.  Usando RESTORE WITH NORECOVERY, aplique quaisquer backups de log pendentes ou backups ao banco de dados espelho.  
  
    -   [Restaurar um backup de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 Antes de poder iniciar uma sessão de espelhamento de banco de dados, é preciso criar o banco de dados espelho. Isso deve ser feito antes de iniciar a sessão de espelhamento.  
  
 Esse exemplo usa o banco de dados de exemplo do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] que, por padrão, usa o modelo de recuperação simples.  
  
1.  Para usar espelhamento de banco de dados com o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] , modifique-o para usar o modelo de recuperação completa:  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE AdventureWorks   
    SET RECOVERY FULL;  
    GO  
    ```  
  
2.  Depois de modificar o modelo de recuperação do banco de dados de SIMPLE para FULL, crie um backup completo, que pode ser usado para criar o banco de dados do espelho. Como o modelo de recuperação acabou de ser alterado, a opção WITH FORMAT estará especificada para criar um novo conjunto de mídias. Isso é útil para separar os backups sob o modelo de recuperação completa de qualquer backup anterior feito sob o modelo de recuperação simples. Com a finalidade deste exemplo, o arquivo de backup (`C:\AdventureWorks.bak`) será criado na mesma unidade como o banco de dados.  
  
    > [!NOTE]  
    >  Em um banco de dados de produção, você deve sempre fazer backup em um dispositivo separado.  
  
     Na instância de servidor principal (em `PARTNERHOST1`), crie um backup completo do banco de dados principal conforme segue:  
  
    ```  
    BACKUP DATABASE AdventureWorks   
        TO DISK = 'C:\AdventureWorks.bak'   
        WITH FORMAT  
    GO  
    ```  
  
3.  Copiar o backup completo para servidor espelho.  
  
4.  Usando RESTORE WITH NORECOVERY, restaure o backup completo na instância do servidor espelho. O comando para restaurar depende que os caminhos dos bancos de dados principal e espelho sejam idênticos.  
  
    -   **Se os caminhos forem idênticos:**  
  
         Na instância de servidor espelho (em `PARTNERHOST5`), restaure o backup completo conforme a seguir:  
  
        ```  
        RESTORE DATABASE AdventureWorks   
            FROM DISK = 'C:\AdventureWorks.bak'   
            WITH NORECOVERY  
        GO  
        ```  
  
    -   **Se os caminhos forem diferentes:**  
  
         Se o caminho do banco de dados espelho for diferente do caminho do banco de dados principal (por exemplo, as letras da unidade são diferentes), crie o banco de dados espelho requer que a operação de restauração inclua uma cláusula MOVE.  
  
        > [!IMPORTANT]  
        >  Se os nomes do caminho dos bancos de dados espelho e principal forem diferentes, não será possível adicionar um arquivo. Isso acontece porque, ao receber o log para a operação do arquivo adicionado, a instância do servidor espelho tenta colocar o novo arquivo no local usado pelo banco de dados principal.  
  
         Por exemplo, o seguinte comando restaura um backup de um banco de dados principal que está em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL.*n*\MSSQL\Data\ para um local diferente, D:\Arquivos de Programas\Microsoft SQL Server\MSSQL.*n*\MSSQL\Dat`a\`, em que o banco de dados espelho reside.  
  
        ```  
        RESTORE DATABASE AdventureWorks  
           FROM DISK='C:\AdventureWorks.bak'  
           WITH NORECOVERY,   
              MOVE 'AdventureWorks_Data' TO   
                 'D:\Program Files\Microsoft SQL Server\MSSQL.n\MSSQL\Data\AdventureWorks_Data.mdf',   
              MOVE 'AdventureWorks_Log' TO  
                 'D:\Program Files\Microsoft SQL Server\MSSQL.n\MSSQL\Data\AdventureWorks_Log.ldf';  
        GO  
        ```  
  
5.  Depois de criar o backup completo, deve-se criar um backup de log no banco de dados principal. Por exemplo, a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] faz o backup de log ao mesmo arquivo usado pelo backup completo anterior:  
  
    ```  
    BACKUP LOG AdventureWorks   
        TO DISK = 'C:\AdventureWorks.bak'   
    GO  
    ```  
  
6.  Antes de poder iniciar o espelhamento, é necessário aplicar o backup de log exigido (e qualquer backup de log subsequente).  
  
     Por exemplo, a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] restaura o primeiro log do `C:\AdventureWorks.bak`:  
  
    ```  
    RESTORE LOG AdventureWorks   
        FROM DISK = 'C:\AdventureWorks.bak'   
        WITH FILE=1, NORECOVERY  
    GO  
    ```  
  
7.  Se qualquer backup de log adicional ocorrer antes de começar o espelhamento, deve-se também restaurar todos os backups de log, em sequência, ao servidor espelho usando WITH NORECOVERY.  
  
     Por exemplo, a instrução seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] restaura dois logs adicionais de `C:\AdventureWorks.bak`:  
  
    ```  
    RESTORE LOG AdventureWorks   
        FROM DISK = 'C:\AdventureWorks.bak'   
        WITH FILE=2, NORECOVERY  
    GO  
    RESTORE LOG AdventureWorks   
        FROM DISK = 'C:\AdventureWorks.bak'   
        WITH FILE=3, NORECOVERY  
    GO  
    ```  
  
 Para obter um exemplo completo de configuração de espelhamento de banco de dados, exibição da configuração de segurança, preparo do banco de dados espelho, configuração de parceiros e adição de uma testemunha, veja [Configurando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md).  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de preparar um banco de dados espelho  
  
1.  Se algum backup de log adicional tiver sido realizado desde sua operação RESTORE LOG mais recente, você deverá aplicar manualmente todos os backups de log adicionais, usando RESTORE WITH NORECOVERY.  
  
2.  Inicie a sessão de espelhamento. Para obter mais informações, veja [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md) ou o [Estabelecer uma sessão de espelhamento de banco de dados com a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-establish-session-windows-authentication.md).  
  
3.  Se você desabilitou o trabalho de backup no banco de dados principal, reabilite o trabalho.  
  
4.  Se o banco de dados precisar estar confiável após um failover, serão necessárias etapas adicionais de instalação após o início do espelhamento. Para obter mais informações, veja [Configurar um banco de dados espelho para usar a propriedade confiável &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Restaurar um backup de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados com a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-establish-session-windows-authentication.md)  
  
-   [Configurar um banco de dados espelho criptografado](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)  
  
-   [Configurar um banco de dados espelho para usar a propriedade confiável &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md)  
  
## <a name="see-also"></a>Consulte também  
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Segurança de transporte para espelhamento de banco de dados e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [Configurando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)   
 [Fazer backup e restaurar índices e catálogos de texto completo](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)   
 [Espelhamento de banco de dados e catálogos de texto completo &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-full-text-catalogs-sql-server.md)   
 [Espelhamento e replicação de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Argumentos de RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)  
  
  

