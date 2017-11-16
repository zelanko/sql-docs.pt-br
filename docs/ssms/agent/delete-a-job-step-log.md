---
title: Excluir um log de etapa de trabalho | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- job steps [SQL Server Agent]
- deleting job step logs
- logs [SQL Server], jobs
- removing job step logs
ms.assetid: ee20c6cd-0258-4550-bdb0-71e86a0fb330
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 399ded1a034d3664def419322c91d3b84e8d62e2
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="delete-a-job-step-log"></a>Delete a Job Step Log
Este tópico descreve como excluir um log de etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
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
  
Para obter mais informações, veja [sp_delete_jobsteplog (Transact-SQL)](http://msdn.microsoft.com/en-us/e9ef4c99-abde-4038-b6a3-a25dcbaf0958).  
  
## <a name="SMO"></a>Usando o SQL Server Management Objects  
Use os métodos **DeleteJobStepLogs** da classe **Job** usando uma linguagem de programação à sua escolha, como Visual Basic, Visual C# ou PowerShell. Para obter mais informações, consulte[SMO (SQL Server Management Objects)](http://msdn.microsoft.com/library/ms162169.aspx).  
  
```  
-- Uses PowerShell to delete all job step log files that have ID values larger than 5.  
$srv = new-object Microsoft.SqlServer.Management.Smo.Server("(local)")  
$jb = $srv.JobServer.Jobs["Test Job"]  
$jb.DeleteJobStepLogs(5)  
```  
  
