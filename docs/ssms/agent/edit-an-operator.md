---
title: Editar um operador
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- modifying operators
- jobs [SQL Server Agent], operators
- operators (users) [Database Engine], modifying with Management Studio
ms.assetid: b2ba2168-ca0b-4b59-9007-4e1e4c30679e
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1b69797d3a308d6fe34fa96751143cbaa480f3ea
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75242405"
---
# <a name="edit-an-operator"></a>Editar um operador
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como editar a disponibilidade de operadores para o recebimento de notificações e seus endereços de email, pager e net send no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Restrictions"></a>Limitações e restrições  
  
-   As opções Pager e **net send** serão removidas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esses recursos em novo trabalho de desenvolvimento e planeje modificar os aplicativos que os usam atualmente.  
  
-   Observe que o SQL Server Agent deve ser configurado para usar o Database Mail a fim de enviar notificações por pager ou email a operadores. Para obter mais informações, consulte [Atribuir alertas a um operador](assign-alerts-to-an-operator.md).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] gerencia trabalhos de forma fácil e com representação gráfica. Além disso, ele é recomendado para criar e gerenciar a infraestrutura de trabalhos.  
  
### <a name="Security"></a>Segurança  
  
#### <a name="Permissions"></a>Permissões  
Somente membros da função de servidor fixa **sysadmin** podem editar operadores.  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-edit-an-operator"></a>Para editar um operador  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor que contém o operador que você deseja editar.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique no sinal de adição para expandir a pasta **Operadores** .  
  
4.  Clique com o botão direito do mouse no operador que você deseja editar e selecione **Propriedades**.  
  
    Para obter mais informações sobre as opções disponíveis contidas na caixa de diálogo _operator\_name_**Propriedades**, consulte:  
  
    -   [Propriedades do operador – Novo operador &#40;página Geral&#41;](../../ssms/agent/operator-properties-new-operator-general-page.md)  
  
    -   [Propriedades do operador – Novo operador &#40;página Notificações&#41;](../../ssms/agent/operator-properties-new-operator-notifications-page.md)  
  
    -   [Propriedades do operador &#40;página Histórico&#41;](../../ssms/agent/operator-properties-history-page.md)  
  
5.  Quando terminar, clique em **OK**.  
  
## <a name="TsqlProcedure"></a>Usando Transact-SQL  
  
#### <a name="to-edit-an-operator"></a>Para editar um operador  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- updates the operator status to enabled, and sets the days   
    -- (from Monday through Friday, from 8 A.M. through 5 P.M.)
    --  when the operator can be paged.   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_operator   
        @name = N'François Ajenstat',  
        @enabled = 1,  
        @email_address = N'françoisa',  
        @pager_address = N'5551290AW@pager.Adventure-Works.com',  
        @weekday_pager_start_time = 080000,  
        @weekday_pager_end_time = 170000,  
        @pager_days = 64 ;  
    GO  
    ```  
  
Para obter mais informações, consulte [sp_update_operator (Transact-SQL)](https://msdn.microsoft.com/231750a6-4828-4d03-afe6-b91d38c42ed3).  
  
