---
title: Definir uma resposta a um alerta
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, alerts
- alerts [SQL Server], responding to
- responding to alerts
ms.assetid: c86ca6eb-c59f-46e9-bc32-d474e7c3b170
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8dd80ad63be8446371328e154b7d18d1f8faa7de
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75256016"
---
# <a name="define-the-response-to-an-alert"></a>Definir uma resposta a um alerta

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como definir o modo de resposta do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a alertas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>Limitações e restrições  
  
-   As opções Pager e **net send** serão removidas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esses recursos em novo trabalho de desenvolvimento e planeje modificar os aplicativos que os usam atualmente.  
  
-   Observe que o SQL Server Agent deve ser configurado para usar o Database Mail a fim de enviar notificações por pager ou email a operadores. Para obter mais informações, consulte [Atribuir alertas a um operador](assign-alerts-to-an-operator.md).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] gerencia trabalhos de forma fácil e com representação gráfica. Além disso, ele é recomendado para criar e gerenciar a infraestrutura de trabalhos.  
  
### <a name="security"></a><a name="Security"></a>Segurança  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permissões  
Somente membros da função de servidor fixa **sysadmin** podem definir a resposta a um alerta.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-define-the-response-to-an-alert"></a>Para definir uma resposta a um alerta  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor que contém o alerta sobre o qual você quer definir uma resposta.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique no sinal de adição para expandir a pasta **Alertas** .  
  
4.  Clique com o botão direito do mouse no alerta no qual você deseja definir uma resposta e selecione **Propriedades**.  
  
5.  Na caixa de diálogo _alert\_name_**propriedades do alerta**, em **Selecionar uma página**, selecione **Resposta**.  
  
6.  Marque a caixa de seleção **Executar trabalho** e, na lista abaixo da caixa de seleção **Executar trabalho** , selecione um trabalho para executar quando o alerta ocorrer. Você pode criar um trabalho novo clicando em **Novo Trabalho** Você pode exibir mais informações sobre o trabalho clicando em **Exibir Trabalho**. Para obter mais informações sobre as opções disponíveis nas caixas de diálogo **Novo Trabalho** e **Propriedades do trabalho**_job\_name_, consulte [Criar um trabalho](../../ssms/agent/create-a-job.md) e [Exibir um trabalho](../../ssms/agent/view-a-job.md).  
  
7.  Marque a caixa de seleção **Notificar Operadores** se você quiser notificar os operadores quando o alerta for ativado. Na **Lista de operadores**, selecione um ou mais dos métodos a seguir para notificar o operador ou operadores: **Email**, **Pager**ou **Net Send**. Você pode criar um operador novo clicando em **Novo Operador** Você pode visualizar mais informações sobre um operador clicando em **Exibir Operador**. Para obter mais informações sobre as opções disponíveis nas caixas de diálogo **Novo Operador** e **Exibir Propriedades do Operador** , consulte [Create an Operator](../../ssms/agent/create-an-operator.md) e [View Information About an Operator](../../ssms/agent/view-information-about-an-operator.md).  
  
8.  Quando terminar, clique em **OK**.  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Usando Transact-SQL  
  
#### <a name="to-define-the-response-to-an-alert"></a>Para definir uma resposta a um alerta  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- adds an e-mail notification for Test Alert.  
    -- assumes that Test Alert already exists and that
    -- François Ajenstat is a valid operator name   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_notification  
     @alert_name = N'Test Alert',  
     @operator_name = N'François Ajenstat',  
     @notification_method = 1 ;  
    GO  
    ```  
  
Para obter mais informações, consulte [sp_add_notification (Transact-SQL)](https://msdn.microsoft.com/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd).