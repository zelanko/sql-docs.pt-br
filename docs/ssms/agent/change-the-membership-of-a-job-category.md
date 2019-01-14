---
title: Alterar a associação de uma categoria de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- members [SQL Server], job categories
ms.assetid: 6a18f7f0-eb50-485f-a9c7-df31ae0f994e
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: cbb3f5d659a859e58deb7410e6890b5b39ac2895
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54131126"
---
# <a name="change-the-membership-of-a-job-category"></a>Change the Membership of a Job Category
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como alterar a associação da categoria de trabalho no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou o SQL Server Management Objects.  
  
As categorias de trabalho ajudam a organizar os trabalhos de modo a facilitar sua filtragem e agrupamento. Você pode criar suas próprias categorias de trabalho. Você também pode alterar a associação de trabalhos do Microsoft SQL Server Agent em categorias de trabalho.  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Segurança](#Security)  
  
-   **Para alterar a associação de uma categoria de trabalho usando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Security"></a>Segurança  
Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-change-the-membership-of-a-job-category"></a>Para alterar a associação de uma categoria de trabalho  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor no qual você deseja editar uma categoria de trabalho.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique com o botão direito do mouse na pasta **Trabalhos** e selecione **Gerenciar Categorias de Trabalho**.  
  
4.  Na caixa de diálogo **Gerenciar Categorias de Trabalho**_server_name_ , selecione a categoria de trabalho que você deseja editar e clique em **Exibir Trabalhos**.  
  
5.  Marque a caixa de seleção **Mostrar todos os trabalhos** .  
  
6.  Para adicionar um trabalho à categoria, na grade principal, marque a caixa de seleção na coluna **Selecionar** correspondente ao trabalho. Para remover um trabalho da categoria, desmarque a caixa. Quando terminar, clique em **OK**.  
  
7.  Feche a caixa de diálogo **Gerenciar Categorias de Trabalho**_server_name_ .  
  
## <a name="TSQL"></a>Usando Transact-SQL  
  
#### <a name="to-change-the-membership-of-a-job-category"></a>Para alterar a associação de uma categoria de trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- adding a new job category to the "NightlyBackups" job  
    USE msdb ;  
    GO  
    EXEC dbo.sp_update_job  
        @job_name = N'NightlyBackups',  
        @category_name = N'[Uncategorized (Local)]';  
    GO  
    ```  
  
Para obter mais informações, veja [sp_update_job (Transact-SQL)](https://msdn.microsoft.com/cbdfea38-9e42-47f3-8fc8-5978b82e2623).  
  
## <a name="SMO"></a>Usando o SQL Server Management Objects  
**Para alterar a associação de uma categoria de trabalho**  
  
Use a classe **JobCategory** com uma linguagem de programação à sua escolha, como Visual Basic, Visual C# ou PowerShell.  
  
