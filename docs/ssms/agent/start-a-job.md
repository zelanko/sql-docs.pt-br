---
title: Iniciar um trabalho | Microsoft Docs
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
helpviewer_keywords:
- jobs [SQL Server Agent], starting
- SQL Server Agent jobs, starting
- starting jobs
ms.assetid: cec9f7f7-d0a7-4239-9dc5-a69c011ebaa0
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 98f1b223349d098220a6a91fe51f1d71f62a5e7d
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="start-a-job"></a>Start a Job
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tópico descreve como começar a executar um trabalho do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], o [!INCLUDE[tsql](../../includes/tsql_md.md)] ou o SQL Server Management Objects.  
  
Um trabalho é uma série especificada de ações que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent executa. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent podem ser executados em um servidor local ou em vários servidores remotos.  
  
-   **Antes de começar:**  
  
    [Segurança](#Security)  
  
-   **Para iniciar um trabalho, usando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Security"></a>Segurança  
Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-start-a-job"></a>Para iniciar um trabalho  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e a expanda.  
  
2.  Expanda **SQL Server Agent** e expanda **Trabalhos**. Segundo o modo pelo qual você queira que o trabalho seja iniciado, siga um destes procedimentos:  
  
    -   Se estiver trabalhando em um único servidor, em um servidor de destino ou executando um trabalho de servidor local em um servidor mestre, clique com o botão direito do mouse no trabalho que deseja iniciar e, em seguida, clique em **Iniciar Trabalho**.  
  
    -   Se desejar iniciar vários trabalhos, clique com o botão direito do mouse em **Monitor de Atividade do Trabalho**e clique em **Exibir Atividade do Trabalho**. No Monitor de Atividade do Trabalho, você pode selecionar vários trabalhos, clicar com o botão direito do mouse na seleção e clicar em **Iniciar Trabalhos**.  
  
    -   Se estiver trabalhando em um servidor mestre e quiser que todos os servidores de destino executem o trabalho simultaneamente, clique com o botão direito do mouse no trabalho que deseja iniciar, clique em **Iniciar Trabalho**e, em seguida, clique em **Iniciar em todos os servidores de destino**.  
  
    -   Se estiver trabalhando em um servidor mestre e quiser especificar servidores de destino para o trabalho, clique com o botão direito do mouse no trabalho que deseja iniciar, clique em **Iniciar Trabalho**e, em seguida, clique em **Iniciar em servidores de destino específicos**. Na caixa de diálogo **Instruções Pós-Download** , marque a caixa de seleção **Estes servidores de destino** e selecione cada servidor de destino em que o trabalho deve ser executado.  
  
## <a name="TSQL"></a>Usando Transact-SQL  
  
#### <a name="to-start-a-job"></a>Para iniciar um trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- starts a job named Weekly Sales Data Backup.    
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_start_job N'Weekly Sales Data Backup' ;  
    GO  
    ```  
  
Para obter mais informações, consulte [sp_start_job (Transact-SQL)](http://msdn.microsoft.com/en-us/8a91df6a-eb84-4512-9a17-4a6e32a9538a).  
  
## <a name="SMO"></a>Usando o SQL Server Management Objects  
**Para iniciar um trabalho**  
  
Chame o método **Start** da classe **Job** usando uma linguagem de programação à sua escolha, como Visual Basic, Visual C# ou PowerShell. Para obter mais informações, veja [SMO (SQL Server Management Objects)](http://msdn.microsoft.com/library/ms162169.aspx).  
  
