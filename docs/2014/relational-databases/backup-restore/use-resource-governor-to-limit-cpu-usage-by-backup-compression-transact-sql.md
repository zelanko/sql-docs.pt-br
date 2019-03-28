---
title: Usar o Administrador de Recursos para limitar o uso de CPU por meio de compactação de backup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backup compression [SQL Server], Resource Governor
- backup compression [SQL Server], CPU usage
- compression [SQL Server], backup compression
- backups [SQL Server], compression
- Resource Governor, backup compression
ms.assetid: 01796551-578d-4425-9b9e-d87210f7ba72
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5fcd3d72ef3e716cd640d35505b82df459eb37b7
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58531448"
---
# <a name="use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql"></a>Usar o Administrador de Recursos para limitar o uso de CPU por meio de compactação de backup (Transact-SQL)
  Por padrão, a compactação de backup aumenta consideravelmente o uso de CPU, e o consumo adicional da CPU por parte do processo de compactação pode afetar negativamente as operações simultâneas. Portanto, convém criar um backup compactado de baixa prioridade em uma sessão cujo uso de CPU seja limitado pelo[Administrador de Recursos](../resource-governor/resource-governor.md) quando houver contenção de CPU. Este tópico apresenta um cenário que classifica as sessões de um usuário específico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapeando-as para um grupo de carga de trabalho do Administrador de Recursos que limita o uso de CPU em casos como esse.  
  
> [!IMPORTANT]  
>  Em um determinado cenário do Administrador de Recursos, a classificação de sessão pode ser baseada em um nome de usuário, em um nome de aplicativo ou em qualquer outro item que possa diferenciar uma conexão. Para obter mais informações, consulte [Resource Governor Classifier Function](../resource-governor/resource-governor-classifier-function.md) e [Resource Governor Workload Group](../resource-governor/resource-governor-workload-group.md).  
  
##  <a name="Top"></a> Este tópico contém o seguinte conjunto de cenários que são apresentados em sequência:  
  
1.  [Configurando um logon e um usuário para operações de baixa prioridade](#setup_login_and_user)  
  
2.  [Configurando o Administrador de Recursos para limitar o uso de CPU](#configure_RG)  
  
3.  [Verificando a classificação da sessão atual (Transact-SQL)](#verifying)  
  
4.  [Compactando backups usando uma sessão com CPU limitada](#creating_compressed_backup)  
  
##  <a name="setup_login_and_user"></a> Configurando um logon e um usuário para operações de baixa prioridade  
 O cenário deste tópico requer um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e um usuário de baixa prioridade. O nome do usuário será usado para classificar sessões que executam no logon e roteá-las as para um grupo de carga de trabalho do Administrador de Recursos que limita o uso de CPU.  
  
 O seguinte procedimento descreve as etapas para configuração de um logon e um usuário para essa finalidade, seguido por um exemplo do [!INCLUDE[tsql](../../includes/tsql-md.md)], "Exemplo A: Configurando um logon e um usuário (Transact-SQL)".  
  
### <a name="to-set-up-a-login-and-database-user-for-classifying-sessions"></a>Para configurar um logon e um usuário de banco de dados para classificar sessões  
  
1.  Crie um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para criar backups compactados de baixa prioridade.  
  
     **Para criar um logon**  
  
    -   [Criar um logon](../security/authentication-access/create-a-login.md)  
  
    -   [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)  
  
2.  Opcionalmente, conceda VIEW SERVER STATE a esse logon.  
  
    -   [Permissões de objeto do sistema GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-system-object-permissions-transact-sql)  
  
     Para obter mais informações, consulte [Permissões de principal do banco de dados GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-database-principal-permissions-transact-sql).  
  
3.  Crie um usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para esse logon.  
  
     **Para criar um usuário**  
  
    -   [Criar um usuário de banco de dados](../security/authentication-access/create-a-database-user.md)  
  
    -   [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)  
  
4.  Para habilitar sessões desse logon e usuário para fazer backup de um determinado banco de dados, adicione o usuário à função de banco de dados db_backupoperator desse banco de dados. Faça isso para cada banco de dados do qual o usuário fará backup. Opcionalmente, adicione o usuário a outras funções fixas do banco de dados.  
  
     **Para adicionar um usuário a uma função de banco de dados fixa**  
  
    -   [sp_addrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql)  
  
     Para obter mais informações, consulte [Permissões de principal do banco de dados GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-database-principal-permissions-transact-sql).  
  
### <a name="example-a-setting-up-a-login-and-user-transact-sql"></a>Exemplo A: Configurando um logon e um usuário (Transact-SQL)  
 O exemplo a seguir é relevante apenas se você optar por criar um novo logon e usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para backups de baixa prioridade. Alternativamente, você pode usar um logon e um usuário existentes, se forem apropriados.  
  
> [!IMPORTANT]  
>  O exemplo a seguir usa um logon e um nome de usuário de exemplo, *domain_name*`\MAX_CPU`. Substitua-os pelos nomes de logon e de usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que serão usados ao criar backups compactados de baixa prioridade.  
  
 Esse exemplo cria um logon para a conta do Windows *domain_name*`\MAX_CPU` e, em seguida, concede a permissão VIEW SERVER STATE ao logon. Essa permissão permite verificar a classificação do Administrador de Recursos de sessões do logon. Em seguida, o exemplo cria um usuário para *domain_name*`\MAX_CPU` e o adiciona à função de banco de dados fixa db_backupoperator do banco de dados de exemplo do [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . Esse nome de usuário será usado pela função de classificação do Administrador de Recursos.  
  
```sql  
-- Create a SQL Server login for low-priority operations  
USE master;  
CREATE LOGIN [domain_name\MAX_CPU] FROM WINDOWS;  
GRANT VIEW SERVER STATE TO [domain_name\MAX_CPU];  
GO  
-- Create a SQL Server user in AdventureWorks2012 for this login  
USE AdventureWorks2012;  
CREATE USER [domain_name\MAX_CPU] FOR LOGIN [domain_name\MAX_CPU];  
EXEC sp_addrolemember 'db_backupoperator', 'domain_name\MAX_CPU';  
GO  
  
```  
  
 [&#91;Início&#93;](#Top)  
  
##  <a name="configure_RG"></a> Configurando o Administrador de Recursos para limitar o uso de CPU  
  
> [!NOTE]  
>  Verifique se o Administrador de Recursos está habilitado. Para obter mais informações, consulte [Habilitar Administrador de Recursos](../resource-governor/enable-resource-governor.md).  
  
 Neste cenário do Administrador de Recursos, a configuração inclui as seguintes etapas básicas:  
  
1.  Criar e configurar um pool de recursos do Administrador de Recursos que limite a largura de banda média máxima da CPU que será fornecida a solicitações no pool de recursos quando houver contenção de CPU.  
  
2.  Criar e configurar um grupo de carga de trabalho do Administrador de Recursos que use esse pool.  
  
3.  Criar uma *função de classificação*, que seja uma UDF (função definida pelo usuário) cujos valores de retorno sejam usados pelo Administrador de Recursos para classificar sessões para que sejam roteadas para o grupo de carga de trabalho adequado.  
  
4.  Registrar a função de classificação com o Administrador de Recursos.  
  
5.  Aplicar as alterações à configuração na memória do Administrador de Recursos.  
  
> [!NOTE]  
>  Para obter informações sobre pools de recursos do Administrador de Recursos, grupos de carga de trabalho e classificação, consulte [Administrador de Recursos](../resource-governor/resource-governor.md).  
  
 As instruções do [!INCLUDE[tsql](../../includes/tsql-md.md)] para essas etapas são descritas no procedimento, "Para configurar o Administrador de Recursos para limitar o uso de CPU", que é seguido por um exemplo do procedimento do [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
 **Para configurar o Administrador de Recursos (SQL Server Management Studio)**  
  
-   [Configurar o administrador de recursos usando um modelo](../resource-governor/configure-resource-governor-using-a-template.md)  
  
-   [Criar um pool de recursos](../resource-governor/create-a-resource-pool.md)  
  
-   [Criar um grupo de carga de trabalho](../resource-governor/create-a-workload-group.md)  
  
### <a name="to-configure-resource-governor-for-limiting-cpu-usage-transact-sql"></a>Para configurar o Administrador de Recursos para limitar o uso de CPU (Transact-SQL)  
  
1.  Emita uma instrução [CREATE RESOURCE POOL](/sql/t-sql/statements/create-resource-pool-transact-sql) para criar um pool de recursos. O exemplo deste procedimento usa a seguinte sintaxe:  
  
     *CREATE RESOURCE POOL pool_name* WITH ( MAX_CPU_PERCENT = *value* );  
  
     *Value* é um inteiro de 1 a 100 que indica a porcentagem da largura de banda média máxima da CPU. O valor adequado depende do ambiente. Para fins de ilustração, o exemplo deste tópico usa 20 por cento (MAX_CPU_PERCENT = 20).  
  
2.  Emita uma instrução [CREATE WORKLOAD GROUP](/sql/t-sql/statements/create-workload-group-transact-sql) para criar um grupo de carga de trabalho para operações de baixa prioridade cujo uso de CPU deve ser administrado. O exemplo deste procedimento usa a seguinte sintaxe:  
  
     CREATE WORKLOAD GROUP *group_name* USING *pool_name*;  
  
3.  Emita uma instrução [CREATE FUNCTION](/sql/t-sql/statements/create-function-transact-sql) para criar uma função de classificação que mapeie o grupo de carga de trabalho criado na etapa anterior para o usuário do logon de baixa prioridade. O exemplo deste procedimento usa a seguinte sintaxe:  
  
     CREATE FUNCTION [*schema_name*.]*function_name*() RETURNS sysname  
  
     WITH SCHEMABINDING  
  
     AS  
  
     BEGIN  
  
     DECLARE @workload_group_name AS *sysname*  
  
     IF (SUSER_NAME() = '*user_of_low_priority_login*')  
  
     SET @workload_group_name = '*workload_group_name*'  
  
     RETURN @workload_group_name  
  
     END  
  
     Para obter informações sobre os componentes dessa instrução CREATE FUNCTION, consulte:  
  
    -   [DECLARE @local_variable &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql)  
  
    -   [SUSER_SNAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/suser-sname-transact-sql)  
  
        > [!IMPORTANT]  
        >  SUSER_NAME é apenas uma das várias funções do sistema que podem ser usadas em uma função de classificação. Para obter mais informações, consulte [Criar e testar uma função de classificação definida pelo usuário](../resource-governor/create-and-test-a-classifier-user-defined-function.md).  
  
    -   [SET @local_variable &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/set-local-variable-transact-sql).  
  
4.  Emita uma instrução [ALTER RESOURCE GOVERNOR](/sql/t-sql/statements/alter-resource-governor-transact-sql) para registrar a função de classificação com o Administrador de Recursos. O exemplo deste procedimento usa a seguinte sintaxe:  
  
     ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION = *schema_name*.*function_name*);  
  
5.  Emita uma segunda instrução ALTER RESOURCE GOVERNADOR para aplicar as alterações à configuração na memória do Administrador de Recursos, da seguinte maneira:  
  
    ```  
    ALTER RESOURCE GOVERNOR RECONFIGURE;  
    ```  
  
### <a name="example-b-configuring-resource-governor-transact-sql"></a>Exemplo B: Configurando o Resource Governor (Transact-SQL)  
 O exemplo a seguir executa as seguintes etapas em uma única transação:  
  
1.  Cria o pool de recursos `pMAX_CPU_PERCENT_20` .  
  
2.  Cria o grupo de carga de trabalho `gMAX_CPU_PERCENT_20` .  
  
3.  Cria a função de classificação `rgclassifier_MAX_CPU()` que usa o nome de usuário criado no exemplo anterior.  
  
4.  Registra a função de classificação no Administrador de Recursos.  
  
 Após confirmar a transação, o exemplo aplica as alterações da configuração nas instruções ALTER WORKLOAD GROUP ou ATER RESOURCE POOL.  
  
> [!IMPORTANT]  
>  O seguinte exemplo usa o nome de usuário de exemplo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criado no "Exemplo A: Configurando um logon e um usuário (Transact-SQL)", *domain_name*`\MAX_CPU`. Substitua-os pelo nome do usuário do logon que será usado para criar backups compactados de baixa prioridade.  
  
```sql  
-- Configure Resource Governor.  
BEGIN TRAN  
USE master;  
-- Create a resource pool that sets the MAX_CPU_PERCENT to 20%.   
CREATE RESOURCE POOL pMAX_CPU_PERCENT_20  
   WITH  
      (MAX_CPU_PERCENT = 20);  
GO  
-- Create a workload group to use this pool.   
CREATE WORKLOAD GROUP gMAX_CPU_PERCENT_20  
USING pMAX_CPU_PERCENT_20;  
GO  
-- Create a classification function.  
-- Note that any request that does not get classified goes into   
-- the 'Default' group.  
CREATE FUNCTION dbo.rgclassifier_MAX_CPU() RETURNS sysname   
WITH SCHEMABINDING  
AS  
BEGIN  
    DECLARE @workload_group_name AS sysname  
      IF (SUSER_NAME() = 'domain_name\MAX_CPU')  
          SET @workload_group_name = 'gMAX_CPU_PERCENT_20'  
    RETURN @workload_group_name  
END;  
GO  
  
-- Register the classifier function with Resource Governor.  
ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION= dbo.rgclassifier_MAX_CPU);  
COMMIT TRAN;  
GO  
-- Start Resource Governor  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
  
```  
  
 [&#91;Início&#93;](#Top)  
  
##  <a name="verifying"></a> Verificando a classificação da sessão atual (Transact-SQL)  
 Opcionalmente, faça logon como o usuário especificado na função de classificação e verifique a classificação da sessão emitindo a seguinte instrução [SELECT](/sql/t-sql/queries/select-transact-sql) no Pesquisador de Objetos:  
  
```sql  
USE master;  
SELECT sess.session_id, sess.login_name, sess.group_id, grps.name   
FROM sys.dm_exec_sessions AS sess   
JOIN sys.dm_resource_governor_workload_groups AS grps   
    ON sess.group_id = grps.group_id  
WHERE session_id > 50;  
GO  
```  
  
 No painel de resultados, a coluna **name** deve listar uma ou mais sessões para o nome do grupo de cargas de trabalho especificado na função de classificação.  
  
> [!NOTE]  
>  Para obter informações sobre as exibições de gerenciamento dinâmico chamado por essa instrução SELECT, consulte [sys.dm_exec_sessions &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql) e [sys.dm_resource_governor_workload_groups &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql).  
  
 [&#91;Início&#93;](#Top)  
  
##  <a name="creating_compressed_backup"></a> Compactando backups usando uma sessão com CPU limitada  
 Para criar um backup compactado em uma sessão com uma CPU máxima limitada, faça logon como o usuário especificado na função de classificação. No comando de backup, especifique WITH COMPRESSION ([!INCLUDE[tsql](../../includes/tsql-md.md)]) ou selecione **Compactar backup** ([!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]). Para criar um backup de banco de dados compactado, consulte [Criar um backup completo de banco de dados &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md).  
  
### <a name="example-c-creating-a-compressed-backup-transact-sql"></a>Exemplo C: Criando um backup compactado (Transact-SQL)  
 O exemplo de [BACKUP](/sql/t-sql/statements/backup-transact-sql) a seguir cria um backup completo compactado do banco de dados [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] em um arquivo de backup recém-formatado, `Z:\SQLServerBackups\AdvWorksData.bak`.  
  
```sql  
--Run backup statement in the gBackup session.  
BACKUP DATABASE AdventureWorks2012 TO DISK='Z:\SQLServerBackups\AdvWorksData.bak'   
WITH   
   FORMAT,   
   MEDIADESCRIPTION='AdventureWorks2012 Compressed Data Backups'  
   DESCRIPTION='First database backup on AdventureWorks2012 Compressed Data Backups media set'  
   COMPRESSION;  
GO  
```  
  
 [&#91;Início&#93;](#Top)  
  
## <a name="see-also"></a>Consulte também  
 [Criar e testar uma função de classificação definida pelo usuário](../resource-governor/create-and-test-a-classifier-user-defined-function.md)   
 [Administrador de Recursos](../resource-governor/resource-governor.md)  
  
  
