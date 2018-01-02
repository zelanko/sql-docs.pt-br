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
ms.openlocfilehash: d0b8dbc635523b33a480ad887b73d9f395d71c8d
ms.sourcegitcommit: ffa4ce9bd71ecf363604966c20cbd2710d029831
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/12/2017
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

### <a name="prerequisites"></a>Pré-requisitos

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

> [!IMPORTANT]
> Use os scripts JSON no exemplo a seguir com a atividade de procedimento armazenado da versão 1 do Azure Data Factory.

Para agendar um pacote com a atividade de procedimento armazenado do Azure Data Factory SQL Server, faça o seguinte:

1.  Crie um data factory.

2.  Crie um serviço vinculado do Banco de Dados SQL que hospede um SSISDB.

3.  Crie um conjunto de dados de saída que conduza o agendamento.

4.  Crie um pipeline do data factory que use a atividade de procedimento armazenado do SQL Server para executar o pacote SSIS.

Esta seção fornece uma visão geral dessas etapas. Um tutorial completo de data factory está além do escopo deste artigo. Para obter mais informações, consulte [Atividade de procedimento armazenado do SQL Server](https://docs.microsoft.com/azure/data-factory/data-factory-stored-proc-activity).

Se uma execução agendada falhar e a atividade de Procedimento armazenado do ADF fornece uma ID de execução para a execução com falha, verifique o relatório de execução para essa ID no SSMS no catálogo do SSIS.

### <a name="created-a-linked-service-for-the-sql-database-that-hosts-ssisdb"></a>Um serviço vinculado do Banco de Dados SQL que hospeda um SSISDB foi criado
O serviço vinculado permite que o data factory se conecte ao SSISDB.

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "description": "",
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Data Source = tcp: YourSQLDBServer.database.windows.net, 1433; Initial Catalog = SSISDB; User ID = YourUsername; Password = YourPassword; Integrated Security = False; Encrypt = True; Connect Timeout = 30"
        }
    }
}
```

### <a name="create-an-output-dataset"></a>Criar um conjunto de dados de saída
O conjunto de dados de saída contém as informações de agendamento.

```json
{
    "name": "sprocsampleout",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
### <a name="create-a-data-factory-pipeline"></a>Criar um pipeline do data factory
O pipeline usa a atividade de procedimento armazenado do SQL Server para executar o pacote SSIS.

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [{
            "name": "SprocActivitySample",
            "type": "SqlServerStoredProcedure",
            "typeProperties": {
                "storedProcedureName": "sp_executesql",
                "storedProcedureParameters": {
                    "stmt": "Transact-SQL script to create and start SSIS package execution using SSISDB catalog stored procedures"
                }
            },
            "outputs": [{
                "name": "sprocsampleout"
            }],
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            }
        }],
        "start": "2017-10-01T00:00:00Z",
        "end": "2017-10-01T05:00:00Z",
        "isPaused": false
    }
}
```

Você não precisa criar um novo procedimento armazenado para encapsular os comandos Transact-SQL necessários para criar e iniciar a execução de pacote SSIS. Você pode fornecer todo o script como o valor do parâmetro `stmt` na amostra de JSON anterior. Aqui está um exemplo de script:

```sql
-- T-SQL script to create and start SSIS package execution using SSISDB catalog stored procedures
DECLARE @return_value INT,@exe_id BIGINT,@err_msg NVARCHAR(150)

-- Create the exectuion
EXEC @return_value=[SSISDB].[catalog].[create_execution] @folder_name=N'folderName', @project_name=N'projectName', @package_name=N'packageName', @use32bitruntime=0, @runinscaleout=1,@useanyworker=1, @execution_id=@exe_id OUTPUT

-- To synchronize SSIS package execution, set the SYNCHRONIZED execution parameter
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @exe_id, @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1

-- Start the execution                                                         
EXEC [SSISDB].[catalog].[start_execution] @execution_id=@exe_id,@retry_count=0
                                          
-- Raise an error for unsuccessful package execution
-- Execution status values include the following:
-- created (1)
-- running (2)
-- canceled (3)
-- failed (4)
-- pending (5)
-- ended unexpectedly (6)
-- succeeded (7)
-- stopping (8)
-- completed (9) 
IF(SELECT [status]
   FROM [SSISDB].[catalog].[executions]
   WHERE execution_id=@exe_id)<>7
BEGIN
    SET @err_msg=N'Your package execution did not succeed for execution ID: ' + CAST(@exe_id AS NVARCHAR(20))
    RAISERROR(@err_msg,15,1)
END
GO
```

Para fornecer o script SQL mostrado acima como o valor do parâmetro `stmt`, normalmente, você precisa incluir todo o script em uma única linha, como mostrado no exemplo a seguir. (O [JSON padrão](https://json.org/) não oferece suporte a caracteres de controle, incluindo o caractere de controle de nova linha `\n` usado em outras linguagens para separar linhas em uma cadeia de caracteres de várias linhas.)

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_executesql",
                    "storedProcedureParameters": {
                        "stmt": "DECLARE @return_value INT, @exe_id BIGINT, @err_msg NVARCHAR(150)    EXEC @return_value=[SSISDB].[catalog].[create_execution] @folder_name=N'test', @project_name=N'TestProject', @package_name=N'STestPackage.dtsx', @use32bitruntime=0, @runinscaleout=1, @useanyworker=1, @execution_id=@exe_id OUTPUT    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @exe_id, @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1    EXEC [SSISDB].[catalog].[start_execution] @execution_id=@exe_id, @retry_count=0    IF(SELECT [status] FROM [SSISDB].[catalog].[executions] WHERE execution_id=@exe_id)<>7 BEGIN SET @err_msg=N'Your package execution did not succeed for execution ID: ' + CAST(@exe_id AS NVARCHAR(20)) RAISERROR(@err_msg,15,1) END"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Minute",
                    "interval": 15
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2017-12-06T12:00:00Z",
        "end": "2017-12-06T12:30:00Z",
        "isPaused": false,
        "hubName": "test_hub",
        "pipelineMode": "Scheduled"
    }
}
```

Para obter mais informações sobre o código nesse script, consulte [Implantar e executar pacotes SSIS usando procedimentos armazenados](../packages/deploy-integration-services-ssis-projects-and-packages.md#deploy-and-execute-ssis-packages-using-stored-procedures).

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre o SQL Server Agent, consulte [Trabalhos do SQL Server Agent para pacotes](../packages/sql-server-agent-jobs-for-packages.md).

Para obter mais informações sobre trabalhos elásticos no Banco de Dados SQL, consulte [Gerenciando bancos de dados de nuvem expandidos](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview).
