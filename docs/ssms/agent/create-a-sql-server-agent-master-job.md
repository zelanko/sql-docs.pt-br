---
title: Criar um trabalho mestre do SQL Server Agent | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], master jobs
- jobs [SQL Server Agent], creating
- master SQL Server Agent job [SQL Server]
ms.assetid: c12ab23f-d7ee-43a5-8cd2-0a9121292bcd
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 97df1479aee6e7b1a057fa08e6bb52569c3ab431
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="create-a-sql-server-agent-master-job"></a>Criar um trabalho mestre do SQL Server Agent
Este tópico descreve como criar um trabalho mestre do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] ou [!INCLUDE[tsql](../../includes/tsql_md.md)].  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Limitações e restrições](#Restrictions)  
  
    [Segurança](#Security)  
  
-   **Para criar um trabalho mestre do SQL Server Agent, usando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Restrictions"></a>Limitações e restrições  
Alterações em trabalhos mestres do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent devem ser propagadas para todos os servidores de destino envolvidos. Como os servidores de destino inicialmente não baixam um trabalho até que os destinos estejam especificados, a [!INCLUDE[msCoName](../../includes/msconame_md.md)] recomenda que você conclua todas as etapas de trabalho e as agendas de um trabalho em particular antes de especificar servidores de destino. Caso contrário, você deve solicitar manualmente que os servidores de destino baixem o trabalho modificado novamente, executando o procedimento armazenado **sp_post_msx_operation** ou modificando o trabalho usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]. Para obter mais informações, consulte [sp_post_msx_operation (Transact-SQL)](http://msdn.microsoft.com/en-us/085deef8-2709-4da9-bb97-9ab32effdacf) ou [Modificar um trabalho](../../ssms/agent/modify-a-job.md).  
  
### <a name="Security"></a>Segurança  
  
#### <a name="Permissions"></a>Permissões  
Trabalhos distribuídos que possuem etapas associadas a um proxy são executados no contexto da conta proxy no servidor de destino. Certifique-se de que as seguintes condições sejam atendidas, ou as etapas de trabalho associadas a um proxy não serão baixadas do servidor mestre para o destino:  
  
-   A subchave do Registro **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<&#42;instance_name&#42;>\SQL Server Agent\AllowDownloadedJobsToMatchProxyName** (REG_DWORD) é definida como 1 (verdadeiro). Por padrão, essa subchave encontra-se definida como 0 (falso).  
  
-   Existe uma conta proxy no servidor de destino com o mesmo nome da conta proxy do servidor mestre sob a qual a etapa de trabalho é executada.  
  
Se as etapas de trabalho que usam contas proxy falharem ao serem baixadas do servidor mestre para o servidor de destino, verifique a coluna **error_message** da tabela **sysdownloadlist** no banco de dados **msdb** quanto às seguintes mensagens de erro:  
  
-   "A etapa do trabalho requer uma conta proxy. Entretanto, a verificação de proxy está desabilitada no servidor de destino." Para resolver este erro, defina a subchave **AllowDownloadedJobsToMatchProxyName** do Registro como 1.  
  
-   "Proxy não localizado." Para resolver este erro, certifique-se de que existe uma conta proxy no servidor de destino com o mesmo nome da conta proxy do servidor mestre sob a qual a etapa de trabalho é executada.  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-master-sql-server-agent-job"></a>Para criar um trabalho mestre do SQL Server Agent  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor no qual você deseja criar o trabalho do SQL Server Agent.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique com o botão direito do mouse na pasta **Trabalhos** e selecione **Novo Trabalho...**.  
  
4.  Na caixa de diálogo **Novo Trabalho** , na página **Geral** , modifique as propriedades gerais do trabalho. Para obter mais informações sobre as opções disponíveis nessa página, consulte [Propriedades do trabalho – Novo trabalho &#40;página Geral&#41;](../../ssms/agent/job-properties-new-job-general-page.md)  
  
5.  Na página **Etapas** , organize as etapas de trabalho. Para obter mais informações sobre as opções disponíveis nessa página, consulte [Propriedades do trabalho – Novo trabalho &#40;página Etapas&#41;](../../ssms/agent/job-properties-new-job-steps-page.md)  
  
6.  Na página **Agendas** , organize agendas para o trabalho. Para obter mais informações sobre as opções disponíveis nessa página, consulte [Propriedades do trabalho – Novo trabalho &#40;página Agendamentos&#41;](../../ssms/agent/job-properties-new-job-schedules-page.md)  
  
7.  Na página **Alertas** , organize os alertas para o trabalho. Para obter mais informações sobre as opções disponíveis nessa página, consulte [Propriedades do trabalho – Novo trabalho &#40;página Alertas&#41;](../../ssms/agent/job-properties-new-job-alerts-page.md)  
  
8.  Na página **Notificações** , defina ações para que o [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent seja executado quando o trabalho terminar. Para obter mais informações sobre as opções disponíveis nessa página, consulte [Propriedades do trabalho – Novo trabalho &#40;página Notificações&#41;](../../ssms/agent/job-properties-new-job-notifications-page.md).  
  
9. Na página **Destinos** , gerencie os servidores de destino para o trabalho. Para obter mais informações sobre as opções disponíveis nessa página, consulte [Propriedades do trabalho – Novo trabalho &#40;página Destinos&#41;](../../ssms/agent/job-properties-new-job-targets-page.md).  
  
10. Quando terminar, clique em **OK**.  
  
## <a name="TsqlProcedure"></a>Usando Transact-SQL  
  
#### <a name="to-create-a-master-sql-server-agent-job"></a>Para criar um trabalho mestre do SQL Server Agent  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE msdb ;  
    GO  
    -- Adds a new job executed by the SQLServerAgent service called 'Weekly Sales Data Backup'  
    EXEC dbo.sp_add_job  
        @job_name = N'Weekly Sales Data Backup' ;  
    GO  
    -- Adds a step (operation) to the 'Weekly Sales Data Backup' job.  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    -- Creates a schedule called RunOnce  
    EXEC dbo.sp_add_schedule  
        @schedule_name = N'RunOnce',  
        @freq_type = 1,  
        @active_start_time = 233000 ;  
    USE msdb ;  
    GO  
    -- Sets the 'RunOnce' schedule to the "Weekly Sales Data Backup' Job  
    EXEC sp_attach_schedule  
       @job_name = N'Weekly Sales Data Backup',  
       @schedule_name = N'RunOnce';  
    GO  
    -- assigns the multiserver job Weekly Sales Backups to the server SEATTLE2  
    -- assumes that SEATTLE2 is registered as a target server for the current instance.  
    EXEC dbo.sp_add_jobserver  
        @job_name = N'Weekly Sales Data Backups',  
        @server_name = N'SEATTLE2' ;  
    GO  
    ```  
  
Para obter mais informações, consulte:  
  
-   [sp_add_job (Transact-SQL)](http://msdn.microsoft.com/en-us/6ca8fe2c-7b1c-4b59-b4c7-e3b7485df274)  
  
-   [sp_add_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/97900032-523d-49d6-9865-2734fba1c755)  
  
-   [sp_add_schedule (Transact-SQL)](http://msdn.microsoft.com/en-us/9060aae3-3ddd-40a5-83bb-3ea7ab1ffbd7)  
  
-   [sp_attach_schedule (Transact-SQL)](http://msdn.microsoft.com/en-us/80c80eaf-cf23-4ed8-b8dd-65fe59830dd1)  
  
-   [sp_add_jobserver (Transact-SQL)](http://msdn.microsoft.com/en-us/485252cc-0081-490a-9bd1-cbbd68eea286)  
  

