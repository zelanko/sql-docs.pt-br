---
title: Criar um alerta usando um número de erro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server], creating
- SQL Server Agent, alerts
- alerts [SQL Server], error numbers
ms.assetid: 03dd7fac-5073-4f86-babd-37e45a86023c
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 453c8e5a2361e93580b7cdd737f03d357946df89
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65090147"
---
# <a name="create-an-alert-using-an-error-number"></a>Criar um alerta usando um número de erro
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como criar um alerta do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que ocou ou oe no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e que será emitido ao ocou ou oer um erro de número específico usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Limitações e restrições](#Restrictions)  
  
    [Segurança](#Security)  
  
-   **Para criar um alerta usando um número de erro com:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Restrictions"></a>Limitações e restrições  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornece um modo gráfico e fácil para gerenciar o sistema de alertas inteiro e é recomendado para configurar uma infraestrutura de alerta.  
  
-   Eventos gerados com **xp_logevent** ocorrem no banco de dados mestre. Portanto, **xp_logevent** não dispara um alerta a menos que o **@database_name** para o alerta seja **'mestre'** ou NULL.  
  
### <a name="Security"></a>Segurança  
  
#### <a name="Permissions"></a>Permissões  
Por padrão, somente membros da função de servidor fixa **sysadmin** podem executar **sp_add_alert**.  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-create-an-alert-using-an-error-number"></a>Para criar um alerta usando um número de erro  
  
1.  No **Pesquisador de Objetos** , clique no sinal de adição para expandir o servidor no qual você deseja criar um alerta usando um número de erro.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique com o botão direito do mouse em **Alertas** e selecione **Novo Alerta**.  
  
4.  Na caixa de diálogo **Novo Alerta** , na caixa **Nome** , digite um nome para esse alerta.  
  
5.  Marque a caixa de seleção **Habilitar** para permitir a execução do alerta. Por padrão, **Habilitar** encontra-se selecionado.  
  
6.  Na lista **Tipo** , selecione **Alerta de evento do SQL Server**.  
  
7.  Em **Definição de alerta de evento**, na lista **Nome do banco de dados** , selecione um banco de dados para restringir o alerta a um banco de dados específico.  
  
8.  Em **Os alertas serão gerados com base em**, clique em **Número de erro**e digite um número de erro válido para o alerta. Opcionalmente, clique em **Severidade** e selecione a severidade específica que irá gerar o alerta.  
  
9. Marque a caixa correspondente à caixa de seleção **Gerar alertas quando a mensagem contiver** para restringir o alerta a uma sequência de caracteres específica e digite uma palavra-chave ou uma cadeia de caracteres para o **Texto da mensagem**. O número máximo de caracteres é 100.  
  
10. Clique em **OK**.  
  
## <a name="TsqlProcedure"></a>Usando Transact-SQL  
  
#### <a name="to-create-an-alert-using-an-error-number"></a>Para criar um alerta usando um número de erro  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- adds an alert (Test Alert) that runs the Back up
    -- the AdventureWorks2012 Database job when fired   
    -- assumes that the message 55001 and the Back up
    -- the AdventureWorks2012 Database job already exist.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_alert  
        @name = N'Test Alert',  
        @message_id = 55001,   
       @severity = 0,   
       @notification_message = N'Error 55001 has occurred. The DB will be backed up...',   
       @job_name = N'Back up the AdventureWorks2012 Database' ;  
    GO  
    ```  
  
Para obter mais informações, veja [sp_add_alert (Transact-SQL)](https://msdn.microsoft.com/d9b41853-e22d-4813-a79f-57efb4511f09).  
  
