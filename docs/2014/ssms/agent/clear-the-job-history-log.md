---
title: Limpar o log do histórico do trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], history
- clearing job history log
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: 34b9398a-c409-4040-8ea1-0deceb18f961
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d6d4943bf3884933cd60e1c0ef51a54771ee00af
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782773"
---
# <a name="clear-the-job-history-log"></a>Clear the Job History Log
  Este tópico descreve como excluir o conteúdo do log do histórico de trabalhos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]ou o SQL Server Management Objects.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para limpar o log do histórico de trabalhos usando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
 Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-clear-the-job-history-log"></a>Para limpar o log de histórico do trabalho  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e a expanda.  
  
2.  Expanda o **SQL Server Agent**e, em seguida, **Trabalhos**.  
  
3.  Clique com o botão direito do mouse em um trabalho e em **Exibir histórico**.  
  
4.  No **Visualizador de Arquivos de Log**, selecione o trabalho cujo histórico você deseja limpar e siga um destes procedimentos:  
  
    -   Clique em **Excluir**e, em seguida, em **Excluir todo o histórico** , na caixa de diálogo **Excluir Histórico** . Você pode excluir todo o histórico de trabalhos ou apenas históricos anteriores a uma data especificada. Se desejar remover todo o histórico de trabalhos, clique em **Excluir todo o histórico**. Se desejar remover apenas logs de histórico de trabalhos mais antigos, clique em **Excluir histórico antes de**e especifique uma data.  
  
    -   Clique em **Status do trabalho** se desejar limpar o log de histórico de um trabalho multisservidor. Clique em **Trabalho**, clique em um nome de trabalho e, em seguida, em **Exibir Histórico do Trabalho Remoto**.  
  
5.  Clique em **Excluir**.  
  
##  <a name="TSQL"></a> Usando Transact-SQL  
  
#### <a name="to-clear-the-job-history-log"></a>Para limpar o log de histórico do trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```sql
    -- example removes the history for a job named NightlyBackups.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_purge_jobhistory  
        @job_name = N'NightlyBackups' ;  
    GO  
    ```  
  
##  <a name="SMO"></a>Usando SQL Server Management Objects  
 **Para limpar o log de histórico do trabalho**  
  
 Use o método `PurgeJobHistory` da classe `JobServer` usando uma linguagem de programação que você escolher, como o Visual Basic, Visual C# ou PowerShell. Para obter mais informações, veja [SMO (SQL Server Management Objects)](https://msdn.microsoft.com/library/ms162169.aspx).  
  
  
