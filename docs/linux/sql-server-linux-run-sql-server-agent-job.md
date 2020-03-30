---
title: Criar e executar trabalhos para o SQL Server em Linux
description: Este tutorial mostra como executar o trabalho do SQL Server Agent no Linux.
author: VanMSFT
ms.author: vanto
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1d93d95e-9c89-4274-9b3f-fa2608ec2792
ms.openlocfilehash: 5abd2db590a89350f45497d7f94b81940a0ec5bc
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68065149"
---
# <a name="create-and-run-sql-server-agent-jobs-on-linux"></a>Criar e executar trabalhos do SQL Server Agent no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Trabalhos do SQL Server são usados para executar regularmente a mesma sequência de comandos em seu banco de dados do SQL Server. Este tutorial apresenta um exemplo de como criar um trabalho do SQL Server Agent no Linux usando tanto o Transact-SQL quanto o SSMS (SQL Server Management Studio).

> [!div class="checklist"]
> * Instalar o SQL Server Agent no Linux
> * Criar um novo trabalho para executar backups diários de banco de dados
> * Agendar e executar o trabalho
> * Executar as mesmas etapas no SSMS (opcional)

Para problemas conhecidos com o SQL Server Agent no Linux, confira as [Notas sobre a versão](sql-server-linux-release-notes.md).

## <a name="prerequisites"></a>Prerequisites

Os pré-requisitos a seguir são necessários para concluir esse tutorial:

* Computador Linux com os seguintes pré-requisitos:
  * SQL Server ([RHEL](quickstart-install-connect-red-hat.md), [SLES](quickstart-install-connect-suse.md) ou [Ubuntu](quickstart-install-connect-ubuntu.md)) com ferramentas de linha de comando.

Os seguintes pré-requisitos são opcionais:

* Computador com Windows com SSMS:
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) para etapas opcionais do SSMS.

## <a name="enable-sql-server-agent"></a>Habilitar o SQL Server Agent

Para usar o SQL Server Agent no Linux, primeiro você deve habilitar o SQL Server Agent em um computador que já tenha o SQL Server instalado.

1. Para habilitar o SQL Server Agent, siga as etapas abaixo.
  ```bash
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
  ```

1. Reinicie SQL Server com o seguinte comando:
  ```bash
  sudo systemctl restart mssql-server
  ```

> [!NOTE]
> Do SQL Server 2017 CU4 em diante, o SQL Server Agent está incluído no pacote **mssql-server** e está desabilitado por padrão. Para configurar o agente antes da CU4, acesse [Instalar o SQL Server Agent no Linux](sql-server-linux-setup-sql-agent.md).

## <a name="create-a-sample-database"></a>Criar banco de dados de exemplo

Use as etapas a seguir para criar um banco de dados de exemplo chamado **SampleDB**. Esse banco de dados é usado para o trabalho de backup diário.

1. Em seu computador Linux, abra uma sessão de terminal Bash.

1. Use o **sqlcmd** para executar um comando **CREATE DATABASE** do Transact-SQL.

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -Q 'CREATE DATABASE SampleDB'
   ```

1. Verifique se o banco de dados é criado listando os bancos de dados no servidor.

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -Q 'SELECT Name FROM sys.Databases'
   ```

## <a name="create-a-job-with-transact-sql"></a>Criar um trabalho com o Transact-SQL

As etapas a seguir criam um trabalho de SQL Server Agent no Linux com comandos Transact-SQL. O trabalho executa um backup diário do banco de dados de exemplo, **SampleDB**.

> [!TIP]
> Você pode usar qualquer cliente T-SQL para executar esses comandos. Por exemplo, no Linux, você pode usar o [sqlcmd](sql-server-linux-setup-tools.md) ou o [Visual Studio Code](sql-server-linux-develop-use-vscode.md). Em um Windows Server remoto, você também pode executar consultas no SSMS (SQL Server Management Studio) ou usar a interface do usuário para gerenciamento de trabalho, que é descrita na próxima seção.

1. Use [sp_add_job](../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md) para criar um trabalho chamado `Daily SampleDB Backup`.

   ```sql
   -- Adds a new job executed by the SQLServerAgent service
   -- called 'Daily SampleDB Backup'
   USE msdb ;
   GO
   EXEC dbo.sp_add_job
      @job_name = N'Daily SampleDB Backup' ;
   GO
   ```

1. Chame [sp_add_jobstep](../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md) para criar uma etapa de trabalho que cria um backup do banco de dados `SampleDB`.

   ```sql
   -- Adds a step (operation) to the job
   EXEC sp_add_jobstep
      @job_name = N'Daily SampleDB Backup',
      @step_name = N'Backup database',
      @subsystem = N'TSQL',
      @command = N'BACKUP DATABASE SampleDB TO DISK = \
         N''/var/opt/mssql/data/SampleDB.bak'' WITH NOFORMAT, NOINIT, \
         NAME = ''SampleDB-full'', SKIP, NOREWIND, NOUNLOAD, STATS = 10',
      @retry_attempts = 5,
      @retry_interval = 5 ;
   GO
   ```

1. Em seguida, crie um agendamento diário para seu trabalho com [sp_add_schedule](../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md).

   ```sql
   -- Creates a schedule called 'Daily'
   EXEC dbo.sp_add_schedule
      @schedule_name = N'Daily SampleDB',
      @freq_type = 4,
      @freq_interval = 1,
      @active_start_time = 233000 ;
   USE msdb ;
   GO
   ```

1. Anexe a agenda de trabalho ao trabalho com [sp_attach_schedule](../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md).

   ```sql
   -- Sets the 'Daily' schedule to the 'Daily SampleDB Backup' Job
   EXEC sp_attach_schedule
      @job_name = N'Daily SampleDB Backup',
      @schedule_name = N'Daily SampleDB';
   GO
   ```

1. Use [sp_add_jobserver](../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md) para atribuir o trabalho a um servidor de destino. Neste exemplo, o destino é o servidor local.

   ```sql
   EXEC dbo.sp_add_jobserver
      @job_name = N'Daily SampleDB Backup',
      @server_name = N'(LOCAL)';
   GO
   ```
1. Inicie o trabalho com [sp_start_job](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md).

   ```sql
   EXEC dbo.sp_start_job N' Daily SampleDB Backup' ;
   GO
   ```

## <a name="create-a-job-with-ssms"></a>Criar um trabalho com o SSMS

Você também pode criar e gerenciar trabalhos remotamente usando o SSMS (SQL Server Management Studio) no Windows.

1. Inicie o SSMS no Windows e conecte-se à sua instância do SQL Server do Linux. Para obter mais informações, confira [Gerenciar SQL Server em Linux com o SSMS](sql-server-linux-manage-ssms.md).

1. Verifique se você criou um banco de dados de exemplo chamado **SampleDB**.

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-0.png" alt="Create a SampleDB database" style="width: 550px;"/>

1. Verifique se o SQL Agent foi [instalado](sql-server-linux-setup-sql-agent.md) e configurado corretamente. Procure o sinal de adição ao lado do SQL Server Agent no Pesquisador de Objetos. Se o SQL Server Agent não estiver habilitado, tente reiniciar o serviço **mssql-server** no Linux.

   ![Verifique se o SQL Server Agent foi instalado](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-1.png)

1. Criar um novo trabalho.

   ![Criar um novo trabalho](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-2.png)

1. Dê um nome ao seu trabalho e crie sua etapa de trabalho.

   ![Criar uma etapa de trabalho](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-3.png)

1. Especifique que subsistema você deseja usar e o que a etapa de trabalho deve fazer.

   ![Subsistema de trabalho](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-4.png)

   ![Ação da etapa de trabalho](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-5.png)

1. Crie uma nova agenda de trabalho.

   ![Agenda do trabalho](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-6.png)

   ![Agenda do trabalho](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-8.png)

1. Inicie seu trabalho.

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-9.png" alt="Start the SQL Server Agent job" style="width: 550px;"/>

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a:

> [!div class="checklist"]
> * Instalar o SQL Server Agent no Linux
> * Usar o Transact-SQL e os procedimentos armazenados do sistema para criar trabalhos
> * Criar um trabalho que executa backups diários de banco de dados
> * Usar a interface do usuário do SSMS para criar e gerenciar trabalhos

Em seguida, explore outros recursos para criar e gerenciar trabalhos:

> [!div class="nextstepaction"]
>[Documentação do SQL Server Agent](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent)
