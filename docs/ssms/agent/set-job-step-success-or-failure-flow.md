---
title: Definir o fluxo de êxito ou falha das etapas do trabalho | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, action flow logic
- successful jobs [SQL Server]
- failed jobs [SQL Server]
- jobs [SQL Server Agent], action flow logic
ms.assetid: 23041ccf-8a07-41d3-85b9-c449a54b7e1e
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0d04cbff4d55a9c34968de3a0eb4e2b3487e86bf
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67685084"
---
# <a name="set-job-step-success-or-failure-flow"></a>Set Job Step Success or Failure Flow
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Ao criar trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, você pode especificar a ação a ser tomada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em caso de falha durante a execução do trabalho. Determine a ação a ser tomada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em caso de êxito ou falha de cada etapa de trabalho. Use o procedimento a seguir para configurar a lógica do fluxo de ações da etapa de trabalho, usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
-   **Antes de começar:**  
  
    [Segurança](#Security)  
  
-   **Para definir o fluxo de êxito ou falha das etapas do trabalho usando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="before-you-begin"></a>Antes de começar  
  
### <a name="Security"></a>Segurança  
Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usando o SQL Server Management Studio  
  
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
  
## <a name="TSQL"></a>Usando Transact-SQL  
  
#### <a name="to-set-job-step-success-or-failure-flow"></a>Para definir o fluxo da etapa de trabalho segundo o êxito ou falha  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
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
  
Para obter mais informações, consulte [sp_add_jobstep (Transact-SQL)](https://msdn.microsoft.com/97900032-523d-49d6-9865-2734fba1c755).  
  
## <a name="SMO"></a>Usando o SQL Server Management Objects  
**Para definir o fluxo da etapa de trabalho segundo o êxito ou falha**  
  
Use a classe **JobStep** com uma linguagem de programação à sua escolha, como Visual Basic, Visual C# ou PowerShell. Para obter mais informações, veja [SMO (SQL Server Management Objects)](https://msdn.microsoft.com/library/ms162169.aspx).  
  
