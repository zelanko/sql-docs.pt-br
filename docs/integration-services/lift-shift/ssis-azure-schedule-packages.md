---
title: "Agendar a execução de pacotes do SSIS no Azure | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: bc1321dd91a0fcb7ab76b207301c6302bb3a5e64
ms.openlocfilehash: a3ecfce9a6adac332b72033955ba51271ed8197b
ms.contentlocale: pt-br
ms.lasthandoff: 10/06/2017

---
# <a name="schedule-the-execution-of-an-ssis-package-on-azure"></a>Agendar a execução de um pacote do SSIS no Azure
Você pode agendar a execução de pacotes armazenados no banco de dados de catálogo do SSISDB em um servidor de banco de dados SQL, escolhendo uma das seguintes opções de agendamento:
-   [SQL Server Agent](#agent)
-   [Trabalhos Elásticos de banco de dados SQL](#elastic)
-   [A atividade de procedimento armazenado do Azure Data Factory SQL Server](#sproc)

## <a name="agent"></a>Agendar um pacote com o SQL Server Agent

### <a name="prerequisite"></a>Pré-requisito

Antes de usar o SQL Server Agent no local para agendar a execução de pacotes armazenados em um servidor de banco de dados SQL, você precisa adicionar o servidor de banco de dados SQL como um servidor vinculado. Para obter mais informações, consulte [criar servidores vinculados](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md) e [servidores vinculados](../../relational-databases/linked-servers/linked-servers-database-engine.md).

### <a name="create-a-sql-server-agent-job"></a>Criar um trabalho do SQL Server Agent

Para agendar um pacote com o SQL Server Agent no local, crie um trabalho com uma etapa de trabalho que chama o catálogo do SSIS procedimentos armazenados `[catalog].[create_execution]` e `[catalog].[start_execution]`. Para obter mais informações, consulte [trabalhos do SQL Server Agent para pacotes](../packages/sql-server-agent-jobs-for-packages.md).

1.  No SQL Server Management Studio, conecte-se para o banco de dados local do SQL Server no qual você deseja criar o trabalho.

2.  Clique com botão direito no **do SQL Server Agent** nó, selecione **novo**e, em seguida, selecione **trabalho** para abrir o **novo trabalho** caixa de diálogo.

3.  No **novo trabalho** caixa de diálogo, selecione o **etapas** página e, em seguida, selecione **novo** para abrir o **nova etapa de trabalho** caixa de diálogo.

4.  No **nova etapa de trabalho** caixa de diálogo, selecione `SSISDB` como o **banco de dados.**

5.  No campo de comando, digite um script Transact-SQL, semelhante ao mostrado no exemplo a seguir:

    ```sql
    DECLARE @return_value int, @exe_id bigint 

    EXEC @return_value = [YourLinkedServer].[SSISDB].[catalog].[create_execution] 
    @folder_name=N'folderName', @project_name=N'projectName', 
    @package_name=N'packageName', @use32bitruntime=0, 
    @runincluster=1, @useanyworker=1, @execution_id=@exe_id OUTPUT 
 
    EXEC [YourLinkedServer].[SSISDB].[catalog].[start_execution] @execution_id=@exe_id

    GO
    ```

6.  Conclua configuração e agendar o trabalho.

## <a name="elastic"></a>Agendar um pacote com trabalhos Elástico de banco de dados SQL

Para obter mais informações sobre trabalhos Elásticos no banco de dados SQL, consulte [Gerenciando bancos de dados de nuvem expansíveis](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-jobs-overview).

### <a name="prerequisites"></a>Pré-requisitos

Antes de usar trabalhos Elásticos para agendar pacotes do SSIS no banco de dados de catálogo do SSISDB em um servidor de banco de dados SQL, você deve fazer o seguinte:

1.  Instalar e configurar os componentes de trabalhos do banco de dados Elástico. Para obter mais informações, consulte [visão geral da instalação do banco de dados Elástico trabalhos](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-jobs-service-installation).

2. Crie credenciais no escopo do banco de dados que os trabalhos podem usar para enviar comandos para o banco de dados de catálogo do SSIS. Para obter mais informações, consulte [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).

### <a name="create-an-elastic-job"></a>Criar um trabalho Elástico

Crie o trabalho usando um script Transact-SQL, semelhante ao mostrado no exemplo a seguir:

```sql
-- Create Elastic Jobs target group 
EXEC jobs.sp_add_target_group 'TargetGroup' 
? 
-- Add Elastic Jobs target group member 
EXEC jobs.sp_add_target_group_member @target_group_name='TargetGroup', 
    @target_type='SqlDatabase', @server_name='YourSQLDBServer.database.windows.net',
    @database_name='SSISDB' 
? 
-- Add a job to schedule SSIS package execution
EXEC jobs.sp_add_job @job_name='ExecutePackageJob', @description='Description', 
    @schedule_interval_type='Minutes', @schedule_interval_count=60

-- Add a job step to create/start SSIS package execution using SSISDB catalog stored procedures
EXEC jobs.sp_add_jobstep @job_name='ExecutePackageJob', 
    @command=N'DECLARE @exe_id bigint 
        EXEC [SSISDB].[catalog].[create_execution]
            @folder_name=N''folderName'', @project_name=N''projectName'',
            @package_name=N''packageName'', @use32bitruntime=0,
            @runincluster=1, @useanyworker=1, 
            @execution_id=@exe_id OUTPUT         
        EXEC [SSISDB].[catalog].[start_execution] @exe_id, @retry_count=0', 
    @credential_name='YourDBScopedCredentials', 
    @target_group_name='TargetGroup' 

-- Enable the job schedule 
EXEC jobs.sp_update_job @job_name='ExecutePackageJob', @enabled=1, 
    @schedule_interval_type='Minutes', @schedule_interval_count=60 
```

## <a name="sproc"></a>Agendar um pacote com a atividade de procedimento armazenado do Azure Data Factory SQL Server

Para agendar um pacote com a atividade de procedimento armazenado do Azure Data Factory SQL Server, faça o seguinte:
1.  Crie uma fábrica de dados.
2.  Criar um serviço vinculado do banco de dados do SQL que hospeda o SSISDB.
3.  Crie um conjunto de dados de saída que orienta o agendamento.
4.  Crie um pipeline da fábrica de dados que usa a atividade de procedimento armazenado do SQL Server para executar o pacote do SSIS.

Esta seção fornece uma visão geral dessas etapas. Um tutorial completo de fábrica de dados está além do escopo deste artigo. Para obter mais informações, consulte [a atividade de procedimento armazenado do SQL Server](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-stored-proc-activity).

### <a name="created-a-linked-service-for-the-sql-database-that-hosts-ssisdb"></a>Criar um serviço vinculado do banco de dados SQL que hospeda o SSISDB
O serviço vinculado permite que a fábrica de dados se conectar ao SSISDB.

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "description": "",
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Data Source = tcp: YourSQLDBServer.database.windows.net, 1433; Initial Catalog = SSISDB; User ID = YourUsername; Password = YourPassword; Integrated Security = False; Encrypt = True; Connect Timeout = 30 "
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
### <a name="create-a-data-factory-pipeline"></a>Criar um pipeline da fábrica de dados
O pipeline usa a atividade de procedimento armazenado do SQL Server para executar o pacote do SSIS.

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

Você não precisa criar um novo procedimento armazenado para encapsular os comandos Transact-SQL necessários para criar e iniciar a execução de pacote SSIS. Você pode fornecer o script como o valor de `stmt` parâmetro no exemplo anterior de JSON. Aqui está um exemplo de script:

```sql
-- T-SQL script to create and start SSIS package execution using SSISDB catalog stored procedures
DECLARE @return_value INT,@exe_id BIGINT,@err_msg NVARCHAR(150)

EXEC @return_value=[SSISDB].[catalog].[create_execution] @folder_name=N'folderName', @project_name=N'projectName', @package_name=N'packageName', @use32bitruntime=0, @runincluster=1,@useanyworker=1, @execution_id=@exe_id OUTPUT
                                                         
EXEC [SSISDB].[catalog].[start_execution] @execution_id=@exe_id,@retry_count=0
-- To synchronize SSIS package execution, poll package execution status
-- created (1)
-- running (2)
-- canceled (3)
-- failed (4)
-- pending (5)
-- ended unexpectedly (6)
-- succeeded (7)
-- stopping (8)
-- completed (9) 
                                          
WHILE(SELECT [status]
      FROM [SSISDB].[catalog].[executions]
      WHERE execution_id=@exe_id) NOT IN(3,4,6,7,9)
BEGIN
    WAITFOR DELAY '00:00:01';
END

-- Raise an error for unsuccessful package execution
IF(SELECT [status]
   FROM [SSISDB].[catalog].[executions]
   WHERE execution_id=@exe_id)<>7
BEGIN
    SET @err_msg=N'Your package execution did not succeed for execution ID: '+CAST(@exe_id AS NVARCHAR(20))
    RAISERROR(@err_msg,15,1)
END
GO
```

Para obter mais informações sobre o código nesse script, consulte [implantar e executar pacotes SSIS usando procedimentos armazenados](../packages/deploy-integration-services-ssis-projects-and-packages.md#deploy-and-execute-ssis-packages-using-stored-procedures).

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre o SQL Server Agent, consulte [trabalhos do SQL Server Agent para pacotes](../packages/sql-server-agent-jobs-for-packages.md).

Para obter mais informações sobre trabalhos Elásticos no banco de dados SQL, consulte [Gerenciando bancos de dados de nuvem expansíveis](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-jobs-overview).
