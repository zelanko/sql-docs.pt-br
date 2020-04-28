---
title: Definir o fluxo de êxito ou falha das etapas do trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, action flow logic
- successful jobs [SQL Server]
- failed jobs [SQL Server]
- jobs [SQL Server Agent], action flow logic
ms.assetid: 23041ccf-8a07-41d3-85b9-c449a54b7e1e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7e9412ee0bd2be7b44dff2a06bd674abee0da34a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72798172"
---
# <a name="set-job-step-success-or-failure-flow"></a>Set Job Step Success or Failure Flow
  Ao criar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabalhos do Agent, você pode especificar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ação que deve ser tomada se ocorrer uma falha durante a execução do trabalho. Determine a ação a ser tomada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em caso de êxito ou falha de cada etapa de trabalho. Use o procedimento a seguir para configurar a lógica do fluxo de ações da etapa de trabalho, usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para definir o fluxo de êxito ou falha das etapas do trabalho usando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server Management Objects](#SMO)  
  
## <a name="before-you-begin"></a>Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
 Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-set-job-step-success-or-failure-flow"></a>Para definir o fluxo da etapa de trabalho segundo o êxito ou falha  
  
1.  No **Pesquisador de Objetos**, expanda **SQL Server Agent**e, em seguida, expanda **Trabalhos**.  
  
2.  Clique com o botão direito do mouse no trabalho que deseja editar e clique em **Propriedades**.  
  
3.  Selecione a página **Etapas** , clique em uma etapa e em **Editar**.  
  
4.  Na caixa de diálogo **Propriedades da Etapa de Trabalho** , selecione a página **Avançado** .  
  
5.  Na caixa de diálogo **Ação ao obter êxito**, clique na ação a ser executada se a etapa de trabalho for concluída com êxito.  
  
6.  Na caixa **Tentativas de repetição** , insira o número de vezes, de 0 a 9999, que a etapa de trabalho deve ser repetida antes de ser considerada como falha. Se você inserir um valor maior que 0 na caixa **Tentativas de repetição** , insira na caixa **Intervalo de repetição (minutos)** o número de minutos, de 1 a 9999, que devem decorrer antes de uma nova tentativa da etapa de trabalho.  
  
7.  Na lista **Ação ao falhar** , clique na ação a executar caso a etapa de trabalho falhe.  
  
8.  Se o trabalho for um script [!INCLUDE[tsql](../../includes/tsql-md.md)] , você poderá escolher entre as seguintes opções:  
  
    -   Na caixa **Arquivo de saída** , insira o nome de um arquivo de saída no qual o script deverá ser gravado. Por padrão, o arquivo é substituído sempre que a etapa de trabalho é executada. Se não quiser que o arquivo de saída seja substituído, marque **Anexar saída ao arquivo existente**.  
  
    -   Marque **Registrar na tabela** , se desejar registrar a etapa de trabalho em uma tabela de banco de dados. Por padrão, o conteúdo da tabela é substituído sempre que a etapa de trabalho é executada. Se não quiser que o conteúdo da tabela seja substituído, marque **Anexar saída à entrada existente na tabela**. Após a execução da etapa de trabalho, o conteúdo dessa tabela pode ser visualizado clicando-se em **Exibir**.  
  
    -   Marque **Incluir saída da etapa no histórico** , se desejar que a saída seja incluída no histórico da etapa. A saída será exibida apenas se não houver erros. A saída também pode ser truncada.  
  
9. Se a lista **Executar como usuário** estiver disponível, selecione a conta proxy com as credenciais que o trabalho usará.  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> Usando o Transact-SQL  
  
#### <a name="to-set-job-step-success-or-failure-flow"></a>Para definir o fluxo da etapa de trabalho segundo o êxito ou falha  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```sql
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @on_success_action = 1;  
    GO  
    ```  
  
 Para obter mais informações, consulte [sp_add_jobstep &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql).  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Usando SQL Server Management Objects  

### <a name="to-set-job-step-success-or-failure-flow"></a>Para definir o fluxo da etapa de trabalho segundo o êxito ou falha
  
 Use a classe `JobStep` usando uma linguagem de programação da sua escolha, como o Visual Basic, o Visual C# ou o PowerShell. Para obter mais informações, veja [SMO (SQL Server Management Objects)](https://msdn.microsoft.com/library/ms162169.aspx).  
