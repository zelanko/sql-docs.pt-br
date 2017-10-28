---
title: Criar um alerta de eventos WMI | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- WMI event alerts [SQL Server Management Studio]
ms.assetid: b8c46db6-408b-484e-98f0-a8af3e7ec763
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 97694f2029532a172f0b0f895dfc95ebc5a8a729
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="create-a-wmi-event-alert"></a>Criar um alerta de eventos WMI
Este tópico descreve como criar um alerta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent a ser emitido mediante a ocorrência de um evento específico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] monitorado pelo Provedor WMI para Eventos de Servidor no [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] ou [!INCLUDE[tsql](../../includes/tsql_md.md)].  
  
Para obter informações sobre como usar o provedor WMI para monitorar eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , consulte [Provedor WMI para classes e propriedades de eventos de servidor](http://msdn.microsoft.com/en-us/80767fe0-32ac-406a-81a0-8212cd6ce7e4). Para obter informações sobre as permissões necessárias para receber notificações de alertas de eventos WMI, consulte [Selecionar uma conta para o serviço do SQL Server Agent](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md). Para obter mais informações sobre WQL, consulte [Usando o WQL com o Provedor WMI para eventos de servidor](http://msdn.microsoft.com/en-us/58b67426-1e66-4445-8e2c-03182e94c4be).  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Limitações e restrições](#Restrictions)  
  
    [Segurança](#Security)  
  
-   **Para criar um alerta de eventos WMI, usando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Restrictions"></a>Limitações e restrições  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] fornece um modo gráfico e fácil para gerenciar o sistema de alertas inteiro e é recomendado para configurar uma infraestrutura de alerta.  
  
-   Eventos gerados com **xp_logevent** ocorrem no banco de dados mestre. Portanto, **xp_logevent** não dispara um alerta a menos que o **@database_name** para o alerta seja **'mestre'** ou NULL.  
  
-   Só têm suporte os namespaces WMI em computadores que executam o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
### <a name="Security"></a>Segurança  
  
#### <a name="Permissions"></a>Permissões  
Por padrão, somente membros da função de servidor fixa **sysadmin** podem executar **sp_add_alert**.  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-wmi-event-alert"></a>Para criar um alerta de eventos WMI  
  
1.  No **Pesquisador de Objetos** , clique no sinal de adição para expandir o servidor em que você deseja criar um alerta de eventos WMI.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique com o botão direito do mouse em **Alertas** e selecione **Novo Alerta**.  
  
4.  Na caixa de diálogo **Novo Alerta** , na caixa **Nome** , digite um nome para esse alerta.  
  
5.  Marque a caixa de seleção **Habilitar** para permitir a execução do alerta. Por padrão, **Habilitar** encontra-se selecionado.  
  
6.  Na lista **Tipo** , selecione **Alerta de eventos WMI**.  
  
7.  Em **Definição de alerta do evento WMI**, na caixa **Namespace** , especifique o namespace WMI da instrução WQL que identifica o evento WMI que vai disparar o alerta.  
  
8.  Na caixa **Consulta** , especifique a instrução WQL que identifica o evento ao qual o alerta responde.  
  
9. Clique em **OK**.  
  
## <a name="TsqlProcedure"></a>Usando Transact-SQL  
  
#### <a name="to-create-a-wmi-event-alert"></a>Para criar um alerta de eventos WMI  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- creates a WMI event alert that retrieves all event properties for any ALTER_TABLE event that occurs on table AdventureWorks2012.Sales.SalesOrderDetail  
    -- This example assumes that the message 54001 already exists.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_alert  
        @name = N'Test Alert 2',  
        @message_id = 54001  
        @notification_message = N'Error 54001 has occurred on the Sales.SalesOrderDetail table on the AdventureWorks2012 database.',  
        @wmi_namespace = '\\.\root\Microsoft\SqlServer\ServerEvents\,  
        @wmi_query = N'SELECT * FROM ALTER_TABLE   
    WHERE DatabaseName = 'AdventureWorks2012' AND SchemaName = 'Sales'   
        AND ObjectType='Table' AND ObjectName = 'SalesOrderDetail'';  
    GO  
    ```  
  
Para obter mais informações, veja [sp_add_alert (Transact-SQL)](http://msdn.microsoft.com/en-us/d9b41853-e22d-4813-a79f-57efb4511f09).  
  

