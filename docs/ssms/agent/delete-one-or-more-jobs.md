---
title: Excluir um ou mais trabalhos | Microsoft Docs
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
- SQL Server Agent jobs, deleting
- dropping jobs
- jobs [SQL Server Agent], deleting
- deleting jobs
- removing jobs
ms.assetid: 67dcdad0-57b2-431c-b77f-4ffc926af93d
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a886339beba637e6a218bbced42212d644347ce8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="delete-one-or-more-jobs"></a>Excluir um ou mais trabalhos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tópico descreve como excluir trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], o [!INCLUDE[tsql](../../includes/tsql_md.md)] ou o SQL Server Management Objects.  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Segurança](#Security)  
  
-   **Para excluir um trabalho usando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Security"></a>Segurança  
A menos que seja membro da função de servidor fixa **sysadmin** , você só poderá excluir trabalhos de sua propriedade.  
  
## <a name="SSMS"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-delete-a-job"></a>Para excluir um trabalho  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e a expanda.  
  
2.  Expanda **SQL Server Agent**, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho que deseja excluir e então clique em **Excluir**.  
  
3.  Na caixa de diálogo **Excluir Objeto** , verifique se o trabalho que você pretende excluir está selecionado.  
  
4.  Clique em **OK**.  
  
#### <a name="to-delete-multiple-jobs"></a>Para excluir vários trabalhos  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e a expanda.  
  
2.  Expanda o **SQL Server Agent**.  
  
3.  Clique com o botão direito do mouse em **Monitor de Atividade do Trabalho**e clique em **Exibir Atividade do Trabalho**.  
  
4.  No Monitor de Atividade do Trabalho, selecione os trabalhos que deseja excluir, clique com o botão direito do mouse em sua seleção e escolha **Excluir trabalhos**.  
  
## <a name="TSQL"></a>Usando Transact-SQL  
  
#### <a name="to-delete-a-job"></a>Para excluir um trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE msdb ;  
    GO  
  
    EXEC sp_delete_job  
        @job_name = N'NightlyBackups' ;  
    GO  
    ```  
  
Para obter mais informações, consulte [sp_delete_job (Transact-SQL)](http://msdn.microsoft.com/en-us/b85db6e4-623c-41f1-9643-07e5ea38db09).  
  
## <a name="SMO"></a>Usando o SQL Server Management Objects  
**Para excluir vários trabalhos**  
  
Use a classe **JobCollection** com uma linguagem de programação à sua escolha, como Visual Basic, Visual C# ou PowerShell. Para obter mais informações, veja [SMO (SQL Server Management Objects)](http://msdn.microsoft.com/library/ms162169.aspx).  
  
