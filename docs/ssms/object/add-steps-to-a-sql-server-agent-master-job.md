---
title: Adicionar etapas a um trabalho mestre do SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9cc1e8ab-7ddc-427b-859e-203aa7e24642
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ce3801d0377b65b14395a1c502cf63fc0e132d69
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33044823"
---
# <a name="add-steps-to-a-sql-server-agent-master-job"></a>Add Steps to a SQL Server Agent Master Job
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Este tópico descreve como adicionar etapas a um trabalho mestre do SQL Server Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] ou [!INCLUDE[tsql](../../includes/tsql_md.md)].  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Limitações e restrições](#Restrictions)  
  
    [Segurança](#Security)  
  
-   **Para adicionar etapas a um trabalho mestre do SQL Server Agent, usando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Restrictions"></a>Limitações e restrições  
Um trabalho mestre do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent não pode ser destino em ambos os servidores, local e remoto.  
  
### <a name="Security"></a>Segurança  
  
#### <a name="Permissions"></a>Permissões  
A menos que seja membro da função de servidor fixa **sysadmin** , você poderá modificar somente trabalhos de sua propriedade. Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-add-steps-to-a-sql-server-agent-master-job"></a>Para adicionar etapas a um trabalho mestre do SQL Server Agent  
  
1.  No **Pesquisador de Objetos** , clique no sinal de adição para expandir o servidor que contém o trabalho ao qual você deseja adicionar etapas.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique no sinal de adição para expandir a pasta **Trabalhos** .  
  
4.  Clique com o botão direito do mouse no trabalho ao qual você deseja adicionar etapas e selecione **Propriedades**.  
  
5.  Na caixa de diálogo **Propriedades do Trabalho –***job_name*, em **Selecione uma página**, selecione **Etapas**. Para obter mais informações sobre as opções disponíveis nessa página, consulte [Propriedades do trabalho – Novo trabalho &#40;página Etapas&#41;](../../ssms/agent/job-properties-new-job-steps-page.md).  
  
6.  Quando terminar, clique em **OK**.  
  
## <a name="TsqlProcedure"></a>Usando Transact-SQL  
  
#### <a name="to-add-steps-to-a-sql-server-agent-master-job"></a>Para adicionar etapas a um trabalho mestre do SQL Server Agent  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- creates a job step that changes database access to read-only for the Sales database.   
    -- specifies 5 retry attempts, with each retry to occur after a 5 minute wait.   
    -- assumes that the Weekly Sales Data Backup job already exists  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
Para obter mais informações, consulte [sp_add_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/97900032-523d-49d6-9865-2734fba1c755).  
  
