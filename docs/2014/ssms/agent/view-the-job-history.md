---
title: Exibir o histórico de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], history
- viewing job history
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
- displaying job history
ms.assetid: 3bbd1556-abdb-48a3-b249-546eace76343
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1ba38b6a3c425972ef0b893d302df78e3d835f85
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72783386"
---
# <a name="view-the-job-history"></a>View the Job History
  Este tópico descreve como exibir o log [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de histórico de trabalhos do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Agent no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]usando [!INCLUDE[tsql](../../includes/tsql-md.md)], ou SQL Server Management Objects.  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para exibir o log de histórico do trabalho usando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
 Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-the-job-history-log"></a>Para exibir o log de histórico do trabalho  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e a expanda.  
  
2.  Expanda o **SQL Server Agent**e, em seguida, **Trabalhos**.  
  
3.  Clique com o botão direito do mouse em um trabalho e então em **Exibir Histórico**.  
  
4.  No Visualizador de Arquivos de Log, examine o histórico do trabalho.  
  
5.  Para atualizar o histórico do trabalho, clique em **Atualizar**. Para exibir menos linhas, clique no botão **Filtro** e insira parâmetros de filtro.  
  
##  <a name="TSQL"></a> Usando o Transact-SQL  
  
#### <a name="to-view-the-job-history-log"></a>Para exibir o log de histórico do trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```sql
    -- lists all job information for the NightlyBackups job.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_jobhistory   
        @job_name = N'NightlyBackups' ;  
    GO  
    ```  
  
 Para obter mais informações, consulte [sp_help_jobhistory &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-help-jobhistory-transact-sql).  
  
##  <a name="SMO"></a>Usando SQL Server Management Objects  
 **Para exibir o log de histórico do trabalho**  
  
 Chame o método `EnumHistory` da classe `Job` usando uma linguagem de programação da sua escolha, como o Visual Basic, o Visual C# ou o PowerShell. Para obter mais informações, veja [SMO (SQL Server Management Objects)](https://msdn.microsoft.com/library/ms162169.aspx).  
