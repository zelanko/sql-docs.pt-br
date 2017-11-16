---
title: Criar uma etapa de trabalho do Analysis Services | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: job steps [Analysis Services]
ms.assetid: 03d4bb86-514b-4a55-97b9-c2c0fa08b428
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bcfaded951e2f4b574747f74167487e2538d8658
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="create-an-analysis-services-job-step"></a>Create an Analysis Services Job Step
Este tópico descreve como criar e definir etapas de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] que executem comandos e consultas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Analysis Services usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], o [!INCLUDE[tsql](../../includes/tsql_md.md)] ou o SQL Server Management Objects.  
  
-   **Antes de começar:**  
  
    [Limitações e restrições](#Restrictions)  
  
    [Segurança](#Security)  
  
-   **Para criar etapas de trabalho do SQL Server usando comandos e/ou consultas do Analysis Services com:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Restrictions"></a>Limitações e restrições  
  
-   Se a etapa de trabalho usar um comando do Analysis Services, a instrução de comando deverá ser o método **Execute** do XML for Analysis Services. A instrução não pode conter um envelope do protocolo SOAP completo nem o método **Discover** do XML for Analysis. Embora o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] ofereça suporte a envelopes SOAP completos e ao método **Discover** , as etapas de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent não oferecem. Para obter mais informações sobre o XML for Analysis Services, consulte [Visão geral do XMLA (XML for Analysis)](http://msdn.microsoft.com/library/ms187190.aspx).  
  
-   Se a etapa de trabalho usar uma consulta do Analysis Services, a instrução de consulta deverá ser uma consulta MDX. Para obter mais informações sobre o MDX, consulte [Conceitos básicos da instrução MDX](http://msdn.microsoft.com/en-us/a560383b-bb58-472e-95f5-65d03d8ea08b).  
  
### <a name="Security"></a>Segurança  
  
#### <a name="Permissions"></a>Permissões  
  
-   Para executar uma etapa de trabalho que use o subsistema Analysis Services, o usuário deve ser um membro da função de servidor fixa **sysadmin** ou ter acesso a uma conta proxy válida definida para usar esse subsistema. Além disso, a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent ou o proxy deve ser um administrador do Analysis Services e uma conta de domínio do Windows válida.  
  
-   Apenas membros da função de servidor fixa **sysadmin** podem gravar em arquivo a saída de uma etapa de trabalho. Se a etapa de trabalho for executada por usuários membros da função de banco de dados **SQLAgentUserRole** no banco de dados **msdb** , a saída poderá ser gravada apenas em uma tabela. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent grava a saída da etapa de trabalho na tabela **sysjobstepslog** do banco de dados **msdb** .  
  
-   Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-create-an-analysis-services-command-job-step"></a>Para criar uma etapa de trabalho de comando do Analysis Services  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e a expanda.  
  
2.  Expanda **SQL Server Agent**, crie um novo trabalho ou clique com o botão direito do mouse em um trabalho existente e clique em **Propriedades**. Para obter mais informações sobre como criar um trabalho, consulte [Criar trabalhos](../../ssms/agent/create-jobs.md).  
  
3.  Na caixa de diálogo **Propriedades do Trabalho** , clique na página **Etapas** e, em seguida, em **Nova**.  
  
4.  Na caixa de diálogo **Nova Etapa de Trabalho** , digite um trabalho **Step name**(Nome da etapa).  
  
5.  Na lista **Tipo** , clique em **Comando do SQL Server Analysis Services**.  
  
6.  Na lista **Executar como** , selecione um proxy que tenha sido definido para usar o subsistema Comando do Analysis Services. Um usuário membro da função de servidor fixa **sysadmin** também pode selecionar **Conta de Serviço do SQL Agent** para executar essa etapa de trabalho.  
  
7.  Selecione o **Servidor** onde a etapa de trabalho será executada ou digite o nome do servidor.  
  
8.  Na caixa **Comando** , digite a instrução a executar ou clique em **Abrir** para selecionar uma instrução.  
  
9. Clique na página **Avançado** para definir opções para essa etapa de trabalho, como a ação que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent deve tomar em caso de êxito ou falha da etapa, quantas vezes a etapa deve ser tentada e onde deve ser gravada sua saída.  
  
#### <a name="to-create-an-analysis-services-query-job-step"></a>Para criar uma etapa de trabalho de consulta do Analysis Services  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e a expanda.  
  
2.  Expanda **SQL Server Agent**, crie um novo trabalho ou clique com o botão direito do mouse em um trabalho existente e clique em **Propriedades**. Para obter mais informações sobre como criar um trabalho, consulte [Criar trabalhos](../../ssms/agent/create-jobs.md).  
  
3.  Na caixa de diálogo **Propriedades do Trabalho** , clique na página **Etapas** e, em seguida, em **Nova**.  
  
4.  Na caixa de diálogo **Nova Etapa de Trabalho** , digite o **Nome da etapa**de trabalho.  
  
5.  Na lista **Tipo** , clique em **Consulta do SQL Server Analysis Services**.  
  
6.  Na lista **Executar como** , selecione um proxy que tenha sido definido para usar o subsistema Consulta do Analysis Services. Um usuário membro da função de servidor fixa **sysadmin** também pode selecionar **Conta de Serviço do SQL Agent** para executar essa etapa de trabalho.  
  
7.  Selecione o **Servidor** e o **Banco de Dados** onde a etapa de trabalho será executada ou digite o nome do servidor ou do banco de dados.  
  
8.  Na caixa **Comando** , digite a instrução a executar ou clique em **Abrir** para selecionar uma instrução.  
  
9. Clique na página **Avançado** para definir opções para essa etapa de trabalho, como a ação que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent deve tomar em caso de êxito ou falha da etapa, quantas vezes a etapa deve ser tentada e onde deve ser gravada sua saída.  
  
## <a name="TSQL"></a>Usando Transact-SQL  
  
#### <a name="to-create-an-analysis-services-command-job-step"></a>Para criar uma etapa de trabalho de comando do Analysis Services  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- Creates a job step that uses XMLA to create a relational data source that
    -- references the AdventureWorks2012 Microsoft SQL Server database.  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name =
            N'Create a relational data source that references the AdventureWorks2012 Microsoft SQL Server database',  
        @subsystem = N'ANALYSISCOMMAND',  
        @command =
            N' <Create xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
        <ParentObject>  
            <DatabaseID>AdventureWorks2012</DatabaseID>  
        </ParentObject>  
        <ObjectDefinition>  
            <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                xsi:type="RelationalDataSource">  
                <ID>AdventureWorks2012</ID>  
                <Name>Adventure Works 2012</Name>  
                <ConnectionString>Data Source=localhost;Initial Catalog=AdventureWorks2012;Integrated Security=True</ConnectionString>  
                <ImpersonationInfo>  
                    <ImpersonationMode>ImpersonateServiceAccount</ImpersonationMode>  
                </ImpersonationInfo>  
                <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
                <Timeout>PT0S</Timeout>  
            </DataSource>  
        </ObjectDefinition>  
    </Create>', ;  
    GO  
    ```  
  
Para obter mais informações, consulte [sp_add_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/97900032-523d-49d6-9865-2734fba1c755).  
  
#### <a name="to-create-an-analysis-services-query-job-step"></a>Para criar uma etapa de trabalho de consulta do Analysis Services  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- Creates a job step that uses MDX to return data  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Returns the Internet sales amount by state',  
        @subsystem = N'ANALYSISQUERY',  
        @command = N' SELECT  
       [Measures].[Internet Sales Amount] ON COLUMNS,  
       [Customer].[State-Province].Members ON ROWS  
    FROM [AdventureWorks2012]',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
Para obter mais informações, consulte [sp_add_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/97900032-523d-49d6-9865-2734fba1c755).  
  
## <a name="SMO"></a>Usando o SQL Server Management Objects  
**Para criar uma etapa de trabalho de script PowerShell**  
  
Use a classe **JobStep** com uma linguagem de programação à sua escolha, como XMLA ou MDX. Para obter mais informações, veja [SMO (SQL Server Management Objects)](http://msdn.microsoft.com/library/ms162169.aspx).  
  
