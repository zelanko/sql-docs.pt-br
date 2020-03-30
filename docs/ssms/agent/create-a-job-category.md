---
title: Criar uma categoria de trabalho
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
ms.assetid: e24a6d38-d231-4f64-ab89-2d1ef6f5792c
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2b5721464d63893a917bb0036491eacbb7ca4c8f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75245937"
---
# <a name="create-a-job-category"></a>Criar uma categoria de trabalho
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como criar uma categoria de trabalho no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent fornece categorias de trabalho internas às quais é possível atribuir trabalhos, mas você também pode criar uma categoria e atribuir-lhe trabalhos. As categorias de trabalho ajudam a organizar os trabalhos de modo a facilitar sua filtragem e agrupamento. Por exemplo, você pode organizar todos os seus trabalhos de backup de banco de dados na categoria Manutenção de Banco de Dados. Você também pode criar suas próprias categorias de trabalho.  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>Limitações e restrições  
As categorias multisservidor só existem em um servidor mestre. Há apenas uma categoria de trabalho padrão disponível em um servidor mestre: [**Não Categorizado (Multisservidor)** ]. Quando um trabalho multisservidor é baixado, sua categoria é alterada para **Trabalhos do MSX** no servidor de destino.  
  
### <a name="security"></a><a name="Security"></a>Segurança  
Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-job-category"></a>Para criar uma categoria de trabalho  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor no qual você deseja criar uma categoria de trabalho.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique com o botão direito do mouse na pasta **Trabalhos** e selecione **Gerenciar Categorias de Trabalho**.  
  
4.  Na caixa de diálogo **Gerenciar Categorias de Trabalho**_server_name_ , clique em **Adicionar**.  
  
5.  Na nova caixa de diálogo, na caixa **Nome** , insira um nome para a nova categoria de trabalho.  
  
6.  Marque a caixa de seleção **Mostrar todos os trabalhos** . Selecione um ou mais trabalhos para a nova categorias, marcando as caixas correspondentes a eles.  
  
7.  Clique em **OK**.  
  
8.  Na caixa de diálogo **Gerenciar Categorias de Trabalho**_server_name_ , clique em **Atualizar** para garantir que a nova categoria de trabalho esteja ativa. Se tudo estiver como esperado, feche a caixa de diálogo.  
  
Para obter mais informações sobre essas caixas de diálogo, consulte [Categorias de trabalho – Gerenciar categorias de trabalho](../../ssms/agent/job-categories-manage-job-categories.md) e [Propriedades de categorias de trabalho – Nova categoria de trabalho](../../ssms/agent/job-categories-properties-new-job-category.md).  
  
## <a name="using-transact-sql"></a><a name="TSQL"></a>Usando Transact-SQL  
  
#### <a name="to-create-a-job-category"></a>Para criar uma categoria de trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- creates a local job category named AdminJobs   
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_category  
        @class=N'JOB',  
        @type=N'LOCAL',  
        @name=N'AdminJobs' ;  
    GO  
    ```  
  
Para obter mais informações, consulte [sp_add_category (Transact-SQL)](https://msdn.microsoft.com/6cca32cd-d941-4378-aed6-a7c90cb7520a).  
  
## <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Usando o SQL Server Management Objects  
**Para criar uma categoria de trabalho**  
  
Chame a classe **JobCategory** com uma linguagem de programação à sua escolha, como Visual Basic, Visual C# ou PowerShell. Para obter um código de exemplo, consulte [Agendamento de tarefas administrativas automáticas no SQL Server Agent](../../relational-databases/server-management-objects-smo/tasks/scheduling-automatic-administrative-tasks-in-sql-server-agent.md).  
  
