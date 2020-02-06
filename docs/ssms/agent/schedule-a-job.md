---
title: Schedule a Job
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- scheduling jobs [SQL Server]
- SQL Server Agent jobs, scheduling
- jobs [SQL Server Agent], scheduling
ms.assetid: f626390a-a3df-4970-b7a7-a0529e4a109c
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2368c8c4d68e0a7da701526e3ec2012ec7342dbd
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75245856"
---
# <a name="schedule-a-job"></a>Schedule a Job
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como agendar um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
-   **Antes de começar:** ,  
  
    [Segurança](#Security)  
  
-   **Para agendar um trabalho usando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Security"></a>Segurança  
Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-create-and-attach-a-schedule-to-a-job"></a>Para criar e anexar uma agenda a um trabalho  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e a expanda.  
  
2.  Expanda **SQL Server Agent**, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho que deseja agendar e clique em **Propriedades**.  
  
3.  Selecione a página **Agendas** e clique em **Nova**.  
  
4.  Na caixa **Nome** , digite um nome para a nova agenda.  
  
5.  Desmarque a caixa de seleção **Habilitado** se não quiser que a agenda entre em vigor imediatamente após a sua criação.  
  
6.  Para **Tipo de Agenda**, siga um destes procedimentos:  
  
    -   Clique em **Iniciar automaticamente quando o SQL Server Agent for iniciado** para iniciar o trabalho quando o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent for iniciado.  
  
    -   Clique em **Iniciar quando as CPUs estiverem ociosas** para iniciar o trabalho quando as CPUs atingirem uma condição de ociosidade.  
  
    -   Clique em **Recorrente** se desejar que a agenda seja executada seguidamente. Para definir a agenda recorrente, complete os grupos **Frequência**, **Frequência Diária**e **Duração** na caixa de diálogo.  
  
    -   Clique em **Uma vez** se quiser que a agenda seja executada apenas uma vez. Para definir uma agenda executada apenas **Uma vez** , complete o grupo **Ocorrência única** na caixa de diálogo.  
  
#### <a name="to-attach-a-schedule-to-a-job"></a>Para anexar uma agenda a um trabalho  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e a expanda.  
  
2.  Expanda **SQL Server Agent**, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho que deseja agendar e clique em **Propriedades**.  
  
3.  Selecione a página **Agendas** e clique em **Escolher**.  
  
4.  Selecione a agenda que você quer anexar e clique em **OK**.  
  
5.  Na caixa de diálogo **Propriedades do Trabalho** , clique duas vezes na agenda anexada.  
  
6.  Verifique se a **Data de Início** está definida corretamente. Se não estiver, estabeleça a data desejada para o início da agenda e clique em **OK**.  
  
7.  Na caixa de diálogo **Propriedades do Trabalho** , clique em **OK**.  
  
## <a name="TSQL"></a>Usando Transact-SQL  
  
#### <a name="to-schedule-a-job"></a>Para agendar um trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE msdb ;  
    GO  
    -- creates a schedule named NightlyJobs.   
    -- Jobs that use this schedule execute every day when the time on the server is 01:00.   
    EXEC sp_add_schedule  
        @schedule_name = N'NightlyJobs' ,  
        @freq_type = 4,  
        @freq_interval = 1,  
        @active_start_time = 010000 ;  
    GO  
    -- attaches the schedule to the job BackupDatabase  
    EXEC sp_attach_schedule  
       @job_name = N'BackupDatabase',  
       @schedule_name = N'NightlyJobs' ;  
    GO  
    ```  
  
Para obter mais informações, consulte [sp_add_schedule (Transact-SQL)](https://msdn.microsoft.com/9060aae3-3ddd-40a5-83bb-3ea7ab1ffbd7) e [sp_attach_schedule (Transact-SQL)](https://msdn.microsoft.com/80c80eaf-cf23-4ed8-b8dd-65fe59830dd1).  
  
## <a name="SMO"></a>Usando o SQL Server Management Objects  
Use a classe **JobSchedule** usando uma linguagem de programação que você escolher, como Visual Basic, Visual C# ou PowerShell. Para obter mais informações, consulte[SMO (SQL Server Management Objects)](https://msdn.microsoft.com/library/ms162169.aspx).  
  
