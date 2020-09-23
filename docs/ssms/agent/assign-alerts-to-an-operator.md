---
description: Assign Alerts to an Operator
title: Assign Alerts to an Operator
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- assigning alerts to operator
- SQL Server Agent, alerts
- alerts [SQL Server], assigning to operator
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: aa818155-6fa2-4565-a09f-5c7e31c89754
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 605496e5d5993e791b347bc343649d738703f029
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88320082"
---
# <a name="assign-alerts-to-an-operator"></a>Assign Alerts to an Operator

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada de SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira detalhes nas [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Este tópico descreve como atribuir alertas do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a operadores, para que estes recebam notificações sobre trabalhos no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>Limitações e Restrições  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornece um modo fácil e gráfico para gerenciar o sistema de alertas inteiro. Usar o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] é o modo recomendado de configuração de sua infraestrutura de alerta.  
  
-   Para enviar uma notificação em resposta a um alerta, primeiro você deve configurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para enviar email. Para obter mais informações, consulte [Configurar o SQL Server Agent Mail para usar o Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md).  
  
-   Se ocorrer uma falha ao enviar uma mensagem de email ou uma notificação de pager, a falha será relatada no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
### <a name="security"></a><a name="Security"></a>Segurança  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permissões  
Somente membros da função de servidor fixa **sysadmin** podem atribuir alertas a operadores.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-assign-alerts-to-an-operator"></a>Para atribuir alertas a um operador  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor que contém o operador ao qual você deseja atribuir um alerta.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique no sinal de adição para expandir a pasta **Operadores** .  
  
4.  Clique com o botão direito do mouse no operador ao qual você deseja atribuir um alerta e selecione **Propriedades**e a página **Notificações** .  
  
5.  Na caixa de diálogo _operator\_name_**Propriedades**, em **Selecionar uma página**, selecione **Notificações**.  
  
6.  Em **Exibir notificações enviadas a esse usuário por**, selecione **Alertas** , para visualizar uma lista dos alertas enviados ao operador, ou **Trabalhos** , para visualizar uma lista dos trabalhos que enviam notificações ao operador. Marque uma ou mais das seguintes caixas de seleção para definir o método de cada notificação, conforme a necessidade: **Email**, **Pager**ou **Net send**.  
  
7.  Quando terminar, clique em **OK**.  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Usando Transact-SQL  
  
#### <a name="to-assign-alerts-to-an-operator"></a>Para atribuir alertas a um operador  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- adds an e-mail notification for the specified alert (Test Alert)  
    -- This example assumes that Test Alert already exists
    -- and that François Ajenstat is a valid operator name.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_notification  
     @alert_name = N'Test Alert',  
     @operator_name = N'François Ajenstat',  
     @notification_method = 1 ;  
    GO  
    ```  
  
Para obter mais informações, consulte [sp_add_notification (Transact-SQL)](https://msdn.microsoft.com/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd).  
  
