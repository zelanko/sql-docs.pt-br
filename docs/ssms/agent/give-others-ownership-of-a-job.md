---
title: Conceder a propriedade de um trabalho a outras pessoas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], owners
- owners [SQL Server], jobs
- SQL Server Agent jobs, owners
ms.assetid: 2ded5e9c-4251-4fb1-a047-99f13d150b61
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d795f709f37772c22cfcffb2b9f0d98c77a7501e
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38980028"
---
# <a name="give-others-ownership-of-a-job"></a>Give Others Ownership of a Job
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como reatribuir a propriedade de trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent a outro usuário.  
  
-   **Antes de começar:**  [Limitações e restrições](#Restrictions), [Segurança](#Security)  
  
-   **Para conceder a propriedade de um trabalho a outros usando:**  
  
    [SQL Server Management Studio](#SSMSProc2)  
  
    [Transact-SQL](#TsqlProc2)  
  
    [SQL Server Management Objects](#SMOProc2)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Restrictions"></a>Limitações e restrições  
Para criar um trabalho, o usuário deve ser membro de uma das funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent ou da função de servidor fixa **sysadmin** . Um trabalho só pode ser editado por seu proprietário ou por membros da função **sysadmin** . Para obter mais informações sobre as funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
Você precisa ser um administrador do sistema para alterar o proprietário de um trabalho.  
  
Atribuir um trabalho a outro logon não garante que o novo proprietário tenha permissões adequadas para executar o trabalho com êxito.  
  
### <a name="Security"></a>Segurança  
Por questão de segurança, apenas o proprietário do trabalho ou um membro da função **sysadmin** pode alterar a definição do trabalho. Somente os membros da função de servidor fixa **sysadmin** podem atribuir a propriedade do trabalho a outros usuários, bem como executar qualquer trabalho, independentemente de seu proprietário.  
  
> [!NOTE]  
> Se você transmitir a propriedade a um usuário que não seja membro da função de servidor fixa **sysadmin** e o trabalho estiver executando etapas que exijam contas proxy (por exemplo, execução de pacotes [!INCLUDE[ssIS](../../includes/ssis_md.md)] ), verifique se o usuário tem acesso à conta proxy necessária, ou o trabalho falhará.  
  
#### <a name="Permissions"></a>Permissões  
Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMSProc2"></a>Usando o SQL Server Management Studio  
**Para conceder a propriedade de um trabalho a outros**  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e a expanda.  
  
2.  Expanda **SQL Server Agent**, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho e então clique em **Propriedades**.  
  
3.  Na lista **Proprietário** , selecione um logon. Você precisa ser um administrador do sistema para alterar o proprietário de um trabalho.  
  
    Atribuir um trabalho a outro logon não garante que o novo proprietário tenha permissões adequadas para executar o trabalho com êxito.  
  
## <a name="TsqlProc2"></a>Usando Transact-SQL  
**Para conceder a propriedade de um trabalho a outros**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do Mecanismo de Banco de Dados e expanda-a.  
  
2.  Na barra de ferramentas, clique em **Nova Consulta**.  
  
3.  Na janela de consulta, insira a instrução a seguir que usa o procedimento armazenado do sistema [sp_manage_jobs_by_login (Transact-SQL)](http://msdn.microsoft.com/832ec15a-6e92-4eb5-8c4a-af4dba79fbaa) . O exemplo a seguir reatribui todos os trabalhos de `danw` para `françoisa`.  
  
    ```  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_manage_jobs_by_login  
        @action = N'REASSIGN',  
        @current_owner_login_name = N'danw',  
        @new_owner_login_name = N'françoisa' ;  
    GO  
    ```  
  
## <a name="SMOProc2"></a>Usando o SQL Server Management Objects  
**Para conceder a propriedade de um trabalho a outros**  
  
1.  Chame a classe **Job** com uma linguagem de programação à sua escolha, como Visual Basic, Visual C# ou PowerShell. Para obter um código de exemplo, consulte [Agendamento de tarefas administrativas automáticas no SQL Server Agent](http://msdn.microsoft.com/900242ad-d6a2-48e9-8a1b-f0eea4413c16).  
  
## <a name="see-also"></a>Consulte Também  
[Implementar trabalhos](../../ssms/agent/implement-jobs.md)  
[Criar trabalhos](../../ssms/agent/create-jobs.md)  
  
