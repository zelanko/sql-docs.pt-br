---
title: Criar uma etapa de trabalho Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL job step
- job steps [Transact-SQL]
- SQL Server Agent jobs, Transact-SQL step
ms.assetid: 69c571a7-debe-4063-9d38-e4b6a1e8e84c
author: stevestein
ms.author: sstein
ms.openlocfilehash: b83ee944d2ca5c10ff1b77f3e6e6da6054b5c99a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85041465"
---
# <a name="create-a-transact-sql-job-step"></a>Create a Transact-SQL Job Step
  Este tópico descreve como criar uma [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] etapa de trabalho do Agent que executa [!INCLUDE[tsql](../../includes/tsql-md.md)] scripts no usando o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , o ou o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] SQL Server Management Objects.  
  
 Esses scripts de etapa de trabalho podem chamar procedimentos armazenados e procedimentos armazenados estendidos. Uma mesma etapa de trabalho [!INCLUDE[tsql](../../includes/tsql-md.md)] pode conter vários lotes e comandos GO inseridos. Para obter mais informações sobre como criar um trabalho, consulte [Criando trabalhos](create-jobs.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para criar uma etapa de trabalho Transact-SQL usando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
 Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-transact-sql-job-step"></a>Para criar uma etapa de trabalho Transact-SQL  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e a expanda.  
  
2.  Expanda **SQL Server Agent**, crie um novo trabalho ou clique com o botão direito do mouse em um trabalho existente e clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do Trabalho** , clique na página **Etapas** e, em seguida, em **Nova**.  
  
4.  Na caixa de diálogo **Nova Etapa de Trabalho** , digite o **Nome da etapa**de trabalho.  
  
5.  Na lista **Tipo** , clique em **Script Transact-SQL (TSQL)**.  
  
6.  Na caixa **Comando** , digite os lotes de comandos [!INCLUDE[tsql](../../includes/tsql-md.md)] ou clique em **Abrir** para selecionar um arquivo [!INCLUDE[tsql](../../includes/tsql-md.md)] a ser usado como comando.  
  
7.  Clique em **Analisar** para verificar a sintaxe.  
  
8.  A mensagem "Êxito da análise" será exibida se a sintaxe estiver correta. Se um erro for encontrado, corrija a sintaxe antes de continuar.  
  
9. Clique na página **Avançado** para definir opções para a etapa de trabalho, tais como: que ação deve ser adotada em caso de êxito ou falha da etapa, quantas vezes o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve tentar executar a etapa e em que arquivo ou tabela o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve gravar a saída da etapa de trabalho. Só membros da função de servidor fixa **sysadmin** podem gravar a saída de etapas de trabalho em um arquivo do sistema operacional. Todos os usuários do SQL Server Agent podem registrar a saída em uma tabela.  
  
10. Se você for membro da função de servidor fixa **sysadmin** e desejar executar a etapa de trabalho como um logon SQL diferente, selecione esse logon na lista **Executar como usuário** .  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-transact-sql-job-step"></a>Para criar uma etapa de trabalho Transact-SQL  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```sql
    -- creates a job step that uses Transact-SQL  
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
  
 Para obter mais informações, consulte [sp_add_jobstep &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql).  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Usando SQL Server Management Objects  
 **Para criar uma etapa de trabalho Transact-SQL**  
  
 Use a classe `JobStep` usando uma linguagem de programação da sua escolha, como o Visual Basic, o Visual C# ou o PowerShell.  
