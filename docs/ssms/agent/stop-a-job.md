---
title: "Parar um trabalho   Microsoft Docs"
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
- jobs [SQL Server Agent], stopping
- SQL Server Agent jobs, stopping
- stopping jobs
ms.assetid: 4249328a-24d8-4284-9d1d-7d04ed90e3d7
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d27aed059ea689f726b6feaf25e22989da0639e7
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="stop-a-job"></a>Stop a Job
Este tópico descreve como interromper um trabalho do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. Um trabalho é uma série especificada de ações que o SQL Server Agent executa.  
  
-   **Antes de começar:**  ,  
  
    [Limitações e restrições](#Restrictions)  
  
    [Segurança](#Security)  
  
-   **Para interromper um trabalho usando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Restrictions"></a>Limitações e restrições  
  
-   Se um trabalho estiver executando no momento uma etapa do tipo **CmdExec** ou **PowerShell**, o processo em execução (por exemplo, MyProgram.exe) será forçado a terminar prematuramente. Isso pode causar comportamento imprevisível, como manter abertos os arquivos em uso pelo processo.  
  
-   Em caso de trabalho multisservidor, uma instrução STOP para o trabalho é postada em todos os servidores de destino do trabalho.  
  
### <a name="Security"></a>Segurança  
Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-stop-a-job"></a>Para interromper um trabalho  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e a expanda.  
  
2.  Expanda **SQL Server Agent**, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho que deseja interromper e clique em **Parar Trabalho**.  
  
3.  Se desejar interromper vários trabalhos, clique com o botão direito do mouse em **Monitor de Atividade do Trabalho**e, depois, clique em **Exibir Atividade do Trabalho**. No Monitor de Atividade do Trabalho, selecione os trabalhos que você deseja interromper, clique com o botão direito do mouse em sua seleção e, depois, clique em **Parar Trabalhos**.  
  
## <a name="TSQL"></a>Usando Transact-SQL  
  
#### <a name="to-stop-a-job"></a>Para interromper um trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- stops a job named Weekly Sales Data Backup  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_stop_job  
        N'Weekly Sales Data Backup' ;  
    GO  
    ```  
  
Para obter mais informações, consulte [sp_stop_job (Transact-SQL)](http://msdn.microsoft.com/en-us/64b4cc75-99a0-421e-b418-94e37595bbb0).  
  
## <a name="SMO"></a>Usando o SQL Server Management Objects  
**Para interromper um trabalho**  
  
Chame o método **Stop** da classe **Job** usando uma linguagem de programação à sua escolha, como Visual Basic, Visual C# ou PowerShell. Para obter mais informações, veja [SMO (SQL Server Management Objects)](http://msdn.microsoft.com/library/ms162169.aspx).  
  

