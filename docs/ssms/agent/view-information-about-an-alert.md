---
title: Exibir informações sobre um alerta
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, alerts
- viewing alerts
- alerts [SQL Server], viewing
- displaying alerts
- status information [SQL Server], alerts
ms.assetid: a0e3a8c4-e3c2-42a5-b2f8-aa06061d3fa6
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 52c53a90befe99862cbac6b5b76810be0a79924a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75257812"
---
# <a name="view-information-about-an-alert"></a>Exibir informações sobre um alerta

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como exibir informações sobre alertas do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Security"></a>Segurança  
  
#### <a name="Permissions"></a>Permissões  
Por padrão, os membros da função de servidor fixa **sysadmin** podem exibir as informações sobre um alerta. Deve ser concedida a outros usuários a função de banco de dados fixa **SQLAgentOperatorRole** no banco de dados **msdb** .  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-view-information-about-an-alert"></a>Para exibir informações sobre um alerta  
  
1.  No **Pesquisador de Objetos** , clique no sinal de adição para expandir o servidor no qual você deseja exibir informações sobre um alerta.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique no sinal de adição para expandir a pasta **Alertas** .  
  
4.  Clique com o botão direito do mouse no alerta que tem as informações que você deseja exibir e selecione **Propriedades**.  
  
    Para obter mais informações sobre as opções disponíveis contidas na caixa de diálogo _alert\_name_**propriedades do alerta** consulte:  
  
    -   [Propriedades do alerta – Novo alerta &#40;página Geral&#41;](../../ssms/agent/alert-properties-new-alert-general-page.md)  
  
    -   [Propriedades do alerta – Novo alerta &#40;página Resposta&#41;](../../ssms/agent/alert-properties-new-alert-response-page.md)  
  
    -   [Propriedades do alerta – Novo alerta &#40;página Opções&#41;](../../ssms/agent/alert-properties-new-alert-options-page.md)  
  
    -   [Propriedades do alerta &#40;página Histórico&#41;](../../ssms/agent/alert-properties-history-page.md)  
  
5.  Quando terminar, clique em **OK**.  
  
## <a name="TsqlProcedure"></a>Usando Transact-SQL  
  
#### <a name="to-view-information-about-an-alert"></a>Para exibir informações sobre um alerta  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- reports information about the Demo: Sev. 25 Errors alert  
    -- This example assumes that the 'Demo: Sev. 25 Errors' alert exists.  
    USE msdb ;  
    GO  
  
    EXEC sp_help_alert @alert_name = 'Demo: Sev. 25 Errors'  
    GO  
    ```  
  
Para obter mais informações, veja [sp_help_alert (Transact-SQL)](https://msdn.microsoft.com/850cef4e-6348-4439-8e79-fd1bca712091).  
  
