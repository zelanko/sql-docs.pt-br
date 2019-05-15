---
title: Excluir um log de etapa de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job steps [SQL Server Agent]
- deleting job step logs
- logs [SQL Server], jobs
- removing job step logs
ms.assetid: ee20c6cd-0258-4550-bdb0-71e86a0fb330
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e5e15c07338afe9274a747f9e4b19db0d4ff76cd
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65096768"
---
# <a name="delete-a-job-step-log"></a>Delete a Job Step Log
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como excluir um log de etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
-   **Antes de começar:**  
  
    [Limitações e restrições](#Restrictions)  
  
    [Segurança](#Security)  
  
-   **Para excluir um log de etapas de trabalho do SQL Server Agent usando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Restrictions"></a>Limitações e restrições  
Quando etapas de trabalho são excluídas seu log de saída é excluído automaticamente.  
  
### <a name="Security"></a>Segurança  
  
#### <a name="Permissions"></a>Permissões  
A menos que seja membro da função de servidor fixa **sysadmin** , você poderá modificar somente trabalhos de sua propriedade.  
  
## <a name="SSMS"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-delete-a-sql-server-agent-job-step-log"></a>Para excluir um log de etapas de trabalho do SQL Server Agent  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e a expanda.  
  
2.  Expanda o **SQL Server Agent**, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho que deseja modificar e clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do Trabalho** , exclua a etapa de trabalho selecionada.  
  
## <a name="TSQL"></a>Usando Transact-SQL  
  
#### <a name="to-delete-a-sql-server-agent-job-step-log"></a>Para excluir um log de etapas de trabalho do SQL Server Agent  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- removes the job step log for step 2 in the job Weekly Sales Data Backup  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_delete_jobsteplog  
        @job_name = N'Weekly Sales Data Backup',  
        @step_id = 2;  
    GO  
    ```  
  
Para obter mais informações, veja [sp_delete_jobsteplog (Transact-SQL)](https://msdn.microsoft.com/e9ef4c99-abde-4038-b6a3-a25dcbaf0958).  
  
## <a name="SMO"></a>Usando o SQL Server Management Objects  
Use os métodos **DeleteJobStepLogs** da classe **Job** usando uma linguagem de programação à sua escolha, como Visual Basic, Visual C# ou PowerShell. Para obter mais informações, consulte[SMO (SQL Server Management Objects)](https://msdn.microsoft.com/library/ms162169.aspx).  
  
```  
-- Uses PowerShell to delete all job step log files that have ID values larger than 5.  
$srv = new-object Microsoft.SqlServer.Management.Smo.Server("(local)")  
$jb = $srv.JobServer.Jobs["Test Job"]  
$jb.DeleteJobStepLogs(5)  
```  
  
