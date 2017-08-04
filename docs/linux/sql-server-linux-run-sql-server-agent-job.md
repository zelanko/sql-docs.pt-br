---
title: Criar e executar trabalhos do SQL Server no Linux | Microsoft Docs
description: Este tutorial mostra como executar o trabalho do SQL Server Agent no Linux.
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 1d93d95e-9c89-4274-9b3f-fa2608ec2792
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3ffb76838940f42d7a696e1c17f227517d89012d
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---

# <a name="create-and-run-sql-server-agent-jobs-on-linux"></a>Criar e executar trabalhos do SQL Server Agent no Linux
Trabalhos do SQL Server são usados para executar regularmente a mesma sequência de comandos no banco de dados do SQL Server. Este tópico fornece exemplos de como criar trabalhos do SQL Server Agent no Linux usando o Transact-SQL e SQL Server Management Studio (SSMS).

Para problemas conhecidos com o SQL Server Agent nesta versão, consulte o [notas de versão](sql-server-linux-release-notes.md).

## <a name="prerequisites"></a>Pré-requisitos 
Para criar e executar trabalhos, primeiro você deve instalar o serviço SQL Server Agent. Para obter instruções de instalação, consulte o [tópico de instalação do SQL Server Agent](sql-server-linux-setup-sql-agent.md).

## <a name="create-a-job-with-transact-sql"></a>Criar um trabalho com o Transact-SQL

As seguintes etapas fornecem um exemplo de como criar um trabalho do SQL Server Agent no Linux com comandos Transact-SQL. Esses trabalho neste exemplo é executado um backup diário em um banco de dados de exemplo `SampleDB`. 


> [!TIP]
> Você pode usar qualquer cliente de T-SQL para executar esses comandos. Por exemplo, no Linux você pode usar [sqlcmd](sql-server-linux-setup-tools.md) ou [código do Visual Studio](sql-server-linux-develop-use-vscode.md). De um servidor remoto do Windows, você também pode executar consultas no SQL Server Management Studio (SSMS) ou usar a interface do usuário para o gerenciamento de trabalho, que é descrito na próxima seção.

1. **Criar o trabalho**. O exemplo a seguir usa [sp_add_job](https://msdn.microsoft.com/library/ms182079.aspx) para criar um trabalho denominado `Daily AdventureWorks Backup`.

    ```tsql
     -- Adds a new job executed by the SQLServerAgent service 
     -- called 'Daily SampleDB Backup'  
     CREATE DATABASE SampleDB
     USE msdb ;  
     GO  
     EXEC dbo.sp_add_job  
         @job_name = N'Daily SampleDB Backup' ;  
     GO

    ```

2. **Adicionar uma ou mais etapas de trabalho**. Script Transact-SQL a seguir usa [sp_add_jobstep](https://msdn.microsoft.com/library/ms187358.aspx) para criar uma etapa de trabalho que cria um backup do `AdventureWlorks2014` banco de dados.

    ```tsql
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

3. **Criar uma agenda de trabalho**. Este exemplo usa [sp_add_schedule](https://msdn.microsoft.com/library/ms366342.aspx) para criar uma agenda diária para o trabalho.

    ```tsql
    -- Creates a schedule called 'Daily'  
    EXEC dbo.sp_add_schedule  
     @schedule_name = N'Daily SampleDB',  
     @freq_type = 4,  
     @freq_interval = 1,
     @active_start_time = 233000 ;  
   USE msdb ;  
   GO
    ```

4. **Anexar a agenda de trabalho para o trabalho**. Use [sp_attach_schedule](https://msdn.microsoft.com/library/ms186766.aspx) para anexar a agenda de trabalho para o trabalho.

    ```tsql
    -- Sets the 'Daily' schedule to the 'Daily AdventureWorks Backup' Job  
    EXEC sp_attach_schedule  
     @job_name = N'Daily SampleDB Backup',  
     @schedule_name = N'Daily SampleDB';  
    GO
    ```

5. **Atribuir o trabalho a um servidor de destino**. Atribuir o trabalho a um servidor de destino com [sp_add_jobserver](https://msdn.microsoft.com/library/ms178625.aspx). Neste exemplo, o servidor local é o destino.

    ```tsql
    EXEC dbo.sp_add_jobserver  
     @job_name = N'Daily SampleDB Backup',  
     @server_name = N'(LOCAL)';  
    GO
    ```
6. **Iniciar o trabalho**. 

    ```tsql
    EXEC dbo.sp_start_job N' Daily SampleDB Backup' ;
    GO
    ```
## <a name="create-a-job-with-ssms"></a>Criar um trabalho com o SSMS

Você também pode criar e gerenciar trabalhos remotamente usando o SQL Server Management Studio (SSMS) no Windows.

1. **Inicie o SSMS no Windows e conecte-se à instância do SQL Server do Linux.** Para obter mais informações, consulte [gerenciar o SQL Server no Linux com o SSMS](sql-server-linux-develop-use-ssms.md).

1. **Criar um novo banco de dados denominado SampleDB**.

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-0.png" alt="Create a SampleDB database" style="width: 550px;"/>

2. **Verifique se o SQL Agent foi instalado e configurado corretamente.** Procure o sinal de adição ao lado do SQL Server Agent no Pesquisador de objetos. Se o SQL Server Agent não estiver instalado, consulte [instalar o SQL Server Agent no Linux](sql-server-linux-setup-sql-agent.md).

    ![Verifique se o que SQL Server Agent foi instalado](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-1.png)


3. **Crie um novo trabalho.**

    ![Criar um novo trabalho](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-2.png)


4. **Dê um nome de seu trabalho e criar a etapa de trabalho.**

    ![Criar uma etapa de trabalho](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-3.png)


5. **Especifique o subsistema que você deseja usar e o que fazer a etapa de trabalho.**

    ![Subsistema de trabalho](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-4.png)

    ![Ação de etapa de trabalho](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-5.png)

6. **Crie uma nova agenda de trabalho.**

    ![Agenda do trabalho](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-6.png)
  
    ![Agenda do trabalho](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-8.png)

7. **Inicie o trabalho.**

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-9.png" alt="Start the SQL Server Agent job" style="width: 550px;"/>

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como criar e gerenciar trabalhos do SQL Server Agent, consulte [do SQL Server Agent](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent).

