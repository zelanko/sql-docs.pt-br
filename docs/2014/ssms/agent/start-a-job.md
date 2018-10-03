---
title: Iniciar um trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], starting
- SQL Server Agent jobs, starting
- starting jobs
ms.assetid: cec9f7f7-d0a7-4239-9dc5-a69c011ebaa0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c056b9a0c70329e350edccebabe63992853b3ee1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48154125"
---
# <a name="start-a-job"></a>Start a Job
  Este tópico descreve como começar a executar um trabalho do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] ou SQL Server Management Objects.  
  
 Um trabalho é uma série especificada de ações que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent executa. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent podem ser executados em um servidor local ou em vários servidores remotos.  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para iniciar um trabalho, usando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
 Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-start-a-job"></a>Para iniciar um trabalho  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e a expanda.  
  
2.  Expanda **SQL Server Agent** e expanda **Trabalhos**. Segundo o modo pelo qual você queira que o trabalho seja iniciado, siga um destes procedimentos:  
  
    -   Se estiver trabalhando em um único servidor, em um servidor de destino ou executando um trabalho de servidor local em um servidor mestre, clique com o botão direito do mouse no trabalho que deseja iniciar e, em seguida, clique em **Iniciar Trabalho**.  
  
    -   Se desejar iniciar vários trabalhos, clique com o botão direito do mouse em **Monitor de Atividade do Trabalho**e clique em **Exibir Atividade do Trabalho**. No Monitor de Atividade do Trabalho, você pode selecionar vários trabalhos, clicar com o botão direito do mouse na seleção e clicar em **Iniciar Trabalhos**.  
  
    -   Se estiver trabalhando em um servidor mestre e quiser que todos os servidores de destino executem o trabalho simultaneamente, clique com o botão direito do mouse no trabalho que deseja iniciar, clique em **Iniciar Trabalho**e, em seguida, clique em **Iniciar em todos os servidores de destino**.  
  
    -   Se estiver trabalhando em um servidor mestre e quiser especificar servidores de destino para o trabalho, clique com o botão direito do mouse no trabalho que deseja iniciar, clique em **Iniciar Trabalho**e, em seguida, clique em **Iniciar em servidores de destino específicos**. Na caixa de diálogo **Instruções Pós-Download** , marque a caixa de seleção **Estes servidores de destino** e selecione cada servidor de destino em que o trabalho deve ser executado.  
  
##  <a name="TSQL"></a> Usando o Transact-SQL  
  
#### <a name="to-start-a-job"></a>Para iniciar um trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- starts a job named Weekly Sales Data Backup.    
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_start_job N'Weekly Sales Data Backup' ;  
    GO  
    ```  
  
 Para obter mais informações, consulte [sp_start_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-start-job-transact-sql).  
  
##  <a name="SMO"></a> Usando o SQL Server Management Objects  
 **Para iniciar um trabalho**  
  
 Chame o método `Start` da classe `Job` usando uma linguagem de programação da sua escolha, como o Visual Basic, o Visual C# ou o PowerShell. Para obter mais informações, veja [SMO (SQL Server Management Objects)](http://msdn.microsoft.com/library/ms162169.aspx).  
  
  
