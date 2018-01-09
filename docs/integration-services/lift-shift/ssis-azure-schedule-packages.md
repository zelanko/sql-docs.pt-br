---
title: "Agendar execução de pacote SSIS no Azure | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 26160f982982b1a8163662f57cb317e7252ab0e4
ms.sourcegitcommit: 6e016a4ffd28b09456008f40ff88aef3d911c7ba
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="schedule-the-execution-of-an-ssis-package-on-azure"></a>Agendar a execução de um pacote do SSIS no Azure
Você pode agendar a execução de pacotes armazenados no banco de dados de catálogo do SSISDB em um servidor de Banco de Dados SQL do Azure, escolhendo uma das seguintes opções de agendamento:
-   [SQL Server Agent](#agent)
-   [Trabalhos Elásticos de Banco de Dados SQL](#elastic)
-   [A atividade de procedimento armazenado do Azure Data Factory SQL Server](#sproc)

## <a name="agent"></a> Agendar um pacote com o SQL Server Agent

### <a name="prerequisite"></a>Pré-requisito

Antes de usar o SQL Server Agent local para agendar a execução de pacotes armazenados em um servidor de Banco de Dados SQL do Azure, você precisa adicionar o servidor de Banco de Dados SQL como um servidor vinculado. Para obter mais informações, consulte [Criar servidores vinculados](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md) e [Servidores vinculados](../../relational-databases/linked-servers/linked-servers-database-engine.md).

### <a name="create-a-sql-server-agent-job"></a>Criar um trabalho do SQL Server Agent

Para agendar um pacote com o SQL Server Agent local, crie um trabalho com uma etapa de trabalho que chama os procedimentos armazenados do catálogo SSIS `[catalog].[create_execution]` e depois `[catalog].[start_execution]`. Para obter mais informações, consulte [Trabalhos do SQL Server Agent para pacotes](../packages/sql-server-agent-jobs-for-packages.md).

1.  No SQL Server Management Studio, conecte-se ao banco de dados do SQL Server local no qual você deseja criar o trabalho.

2.  Clique com o botão direito do mouse no nó **SQL Server Agent**, selecione **Novo** e, em seguida, selecione **Trabalho** para abrir a caixa de diálogo **Novo Trabalho**.

3.  Na caixa de diálogo **Novo Trabalho**, selecione a página **Etapas** e, em seguida, selecione **Novo** para abrir a caixa de diálogo **Nova Etapa do Trabalho**.

4.  Na caixa de diálogo **Nova Etapa do Trabalho**, selecione `SSISDB` como o **Banco de dados**.

5.  No campo de comando, insira um script Transact-SQL semelhante ao mostrado no exemplo a seguir:

    ```sql
    DECLARE @return_value int, @exe_id bigint 

    EXEC @return_value = [YourLinkedServer].[SSISDB].[catalog].[create_execution] 
    @folder_name=N'folderName', @project_name=N'projectName', 
    @package_name=N'packageName', @use32bitruntime=0, 
    @runinscaleout=1, @useanyworker=1, @execution_id=@exe_id OUTPUT 
 
    EXEC [YourLinkedServer].[SSISDB].[catalog].[start_execution] @execution_id=@exe_id

    GO
    ```

6.  Conclua a configuração e o agendamento do trabalho.

## <a name="elastic"></a> Agendar um pacote com trabalhos elásticos de Banco de Dados SQL

Para obter mais informações sobre trabalhos elásticos no Banco de Dados SQL, consulte [Gerenciando bancos de dados de nuvem expandidos](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview).

### <a name="prerequisites"></a>Prerequisites

Antes que você possa usar trabalhos elásticos para agendar pacotes do SSIS armazenados no banco de dados de catálogo do SSISDB em um servidor de Banco de Dados SQL do Azure, você deverá fazer o seguinte:

1.  Instale e configure os componentes de trabalhos de banco de dados elástico. Para obter mais informações, consulte [Visão geral da instalação de trabalhos de Banco de Dados Elástico](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-service-installation).

2. Crie credenciais no escopo do banco de dados que os trabalhos possam usar para enviar comandos para o banco de dados de catálogo do SSIS. Para obter mais informações, veja [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).

### <a name="create-an-elastic-job"></a>Criar um trabalho elástico

Crie o trabalho usando um script Transact-SQL semelhante ao mostrado no exemplo a seguir:

```sql
-- Create Elastic Jobs target group 
EXEC jobs.sp_add_target_group 'TargetGroup' 

-- Add Elastic Jobs target group member 
EXEC jobs.sp_add_target_group_member @target_group_name='TargetGroup', 
    @target_type='SqlDatabase', @server_name='YourSQLDBServer.database.windows.net',
    @database_name='SSISDB' 

-- Add a job to schedule SSIS package execution
EXEC jobs.sp_add_job @job_name='ExecutePackageJob', @description='Description', 
    @schedule_interval_type='Minutes', @schedule_interval_count=60

-- Add a job step to create/start SSIS package execution using SSISDB catalog stored procedures
EXEC jobs.sp_add_jobstep @job_name='ExecutePackageJob', 
    @command=N'DECLARE @exe_id bigint 
        EXEC [SSISDB].[catalog].[create_execution]
            @folder_name=N''folderName'', @project_name=N''projectName'',
            @package_name=N''packageName'', @use32bitruntime=0,
            @runinscaleout=1, @useanyworker=1, 
            @execution_id=@exe_id OUTPUT         
        EXEC [SSISDB].[catalog].[start_execution] @exe_id, @retry_count=0', 
    @credential_name='YourDBScopedCredentials', 
    @target_group_name='TargetGroup' 

-- Enable the job schedule 
EXEC jobs.sp_update_job @job_name='ExecutePackageJob', @enabled=1, 
    @schedule_interval_type='Minutes', @schedule_interval_count=60 
```

## <a name="sproc"></a> Agende um pacote com a atividade de procedimento armazenado do Azure Data Factory SQL Server

Para obter informações sobre como agendar um pacote do SSIS usando a atividade de Procedimento Armazenado do Azure Data Factory, consulte os seguintes artigos:

-   Para o Data Factory versão 2: [Invocar um pacote do SSIS usando a atividade de procedimento armazenado no Azure Data Factory](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-stored-procedure-activity)

-   Para o Data Factory versão 1: [Invocar um pacote do SSIS usando a atividade de procedimento armazenado no Azure Data Factory](https://docs.microsoft.com/azure/data-factory/v1/how-to-invoke-ssis-package-stored-procedure-activity)

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre o SQL Server Agent, consulte [Trabalhos do SQL Server Agent para pacotes](../packages/sql-server-agent-jobs-for-packages.md).

Para obter mais informações sobre trabalhos elásticos no Banco de Dados SQL, consulte [Gerenciando bancos de dados de nuvem expandidos](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview).
