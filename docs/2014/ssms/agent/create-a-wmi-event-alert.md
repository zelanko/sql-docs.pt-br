---
title: Criar um alerta de eventos WMI | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- WMI event alerts [SQL Server Management Studio]
ms.assetid: b8c46db6-408b-484e-98f0-a8af3e7ec763
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5fb396587fa3f3a29f499ccef35e1c555f5121f5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019479"
---
# <a name="create-a-wmi-event-alert"></a>Criar um alerta de eventos WMI
  Este tópico descreve como criar um alerta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a ser emitido mediante a ocorrência de um evento específico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] monitorado pelo Provedor WMI para Eventos de Servidor no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Para obter informações sobre como usar o provedor WMI para monitorar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eventos, consulte [provedor WMI para conceitos de eventos de servidor](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md). Para obter informações sobre as permissões necessárias para receber notificações de alertas de eventos WMI, consulte [Selecionar uma conta para o serviço do SQL Server Agent](select-an-account-for-the-sql-server-agent-service.md). Para obter mais informações sobre WQL, consulte [Usando o WQL com o Provedor WMI para eventos de servidor](../../relational-databases/wmi-provider-server-events/using-wql-with-the-wmi-provider-for-server-events.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para criar um alerta de eventos WMI, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornece um modo gráfico e fácil para gerenciar o sistema de alertas inteiro e é recomendado para configurar uma infraestrutura de alerta.  
  
-   Eventos gerados com **xp_logevent** ocorrem no banco de dados mestre. Portanto, **xp_logevent** não dispara um alerta a menos que o **@database_name** para o alerta seja **'mestre'** ou NULL.  
  
-   Só têm suporte os namespaces WMI em computadores que executam o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Por padrão, somente membros da função de servidor fixa **sysadmin** podem executar **sp_add_alert**.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
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
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-wmi-event-alert"></a>Para criar um alerta de eventos WMI  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
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
        @notification_message = N'Error 54001 has occurred on the Sales.SalesOrderDetail table on the AdventureWorks2012 database. Please see the following information…',  
        @wmi_namespace = '\\.\root\Microsoft\SqlServer\ServerEvents\,  
        @wmi_query = N'SELECT * FROM ALTER_TABLE   
    WHERE DatabaseName = 'AdventureWorks2012' AND SchemaName = 'Sales'   
        AND ObjectType='Table' AND ObjectName = 'SalesOrderDetail'';  
    GO  
    ```  
  
 Para obter mais informações, consulte [sp_add_alert &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql).  
  
  
