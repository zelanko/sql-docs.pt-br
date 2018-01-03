---
title: Criar uma etapa de trabalho CmdExec | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: CmdExec jobs
ms.assetid: b48da5b4-6fe7-4eb7-bade-dc7d697c6d5c
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 547a4e0e0361079baf818765c95b2abbf2e5ad70
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="create-a-cmdexec-job-step"></a>Create a CmdExec Job Step
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tópico descreve como criar e definir uma etapa de trabalho do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] que usa um programa executável ou comando do sistema operacional usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)] ou SQL Server Management Objects.  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Segurança](#Security)  
  
-   **Para criar uma etapa de trabalho CmdExec, usando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Security"></a>Segurança  
Por padrão, só membros da função de servidor fixa **sysadmin** podem criar etapas de trabalho CmdExec. Essas etapas de trabalho são executadas no contexto da conta de serviço do SQL Server Agent, a menos que o usuário de **sysadmin** crie uma conta proxy. Usuários que não sejam membros da função **sysadmin** poderão criar etapas de trabalho CmdExec se tiverem acesso à conta proxy de CmdExec.  
  
#### <a name="Permissions"></a>Permissões  
Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-cmdexec-job-step"></a>Para criar uma etapa de trabalho CmdExec  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e a expanda.  
  
2.  Expanda **SQL Server Agent**, crie um novo trabalho ou clique com o botão direito do mouse em um trabalho existente e clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do Trabalho** , clique na página **Etapas** e, em seguida, em **Nova**.  
  
4.  Na caixa de diálogo **Nova Etapa de Trabalho** , digite o **Nome da etapa**de trabalho.  
  
5.  Na lista **Tipo** , escolha **Sistema operacional (CmdExec)**.  
  
6.  Na lista **Executar como** , selecione a conta proxy com as credenciais que o trabalho usará. Por padrão, etapas de trabalho CmdExec são executadas no contexto da conta do serviço do SQL Server Agent .  
  
7.  Na caixa **Código de saída do processo de um comando bem sucedido** , insira um valor de 0 a 999999.  
  
8.  Na caixa **Comando** , digite o comando de sistema operacional ou programa executável. Consulte "Usando Transact T-SQL para obter um exemplo.  
  
9. Clique na página **Avançado** para definir opções para a etapa de trabalho, como a ação a tomar em caso de êxito ou falha da etapa, quantas vezes o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent deve tentar executar a etapa e o arquivo onde o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent pode gravar a saída da etapa. Só membros da função de servidor fixa **sysadmin** podem gravar a saída de etapas de trabalho em um arquivo do sistema operacional.  
  
## <a name="TSQL"></a>Usando Transact-SQL  
  
#### <a name="to-create-a-cmdexec-job-step"></a>Para criar uma etapa de trabalho CmdExec  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- creates a job step that that uses CmdExec  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'CMDEXEC',  
        @command = C:\clickme_scripts\SQL11\PostBOLReorg GetHsX.exe',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
Para obter mais informações, consulte [sp_add_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/97900032-523d-49d6-9865-2734fba1c755)  
  
## <a name="SMO"></a>Usando o SQL Server Management Objects  
**Para criar uma etapa de trabalho CmdExec**  
  
Use a classe **JobStep** com uma linguagem de programação à sua escolha, como Visual Basic, Visual C# ou PowerShell.  
  
