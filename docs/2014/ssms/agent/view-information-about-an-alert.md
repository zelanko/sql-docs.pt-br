---
title: Exibir informações sobre um alerta | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, alerts
- viewing alerts
- alerts [SQL Server], viewing
- displaying alerts
- status information [SQL Server], alerts
ms.assetid: a0e3a8c4-e3c2-42a5-b2f8-aa06061d3fa6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c5567abc0893bd183c2468f82278a014e2005113
ms.sourcegitcommit: 78e32562f9c1fbf2e50d3be645941d4aa457e31f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2019
ms.locfileid: "54100227"
---
# <a name="view-information-about-an-alert"></a>Exibir informações sobre um alerta
  Este tópico descreve como exibir infoumações sobre alertas do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para exibir informações sobre um alerta, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem exibir as informações sobre um alerta. Deve ser concedida a outros usuários a função de banco de dados fixa **SQLAgentOperatorRole** no banco de dados **msdb** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-information-about-an-alert"></a>Para exibir informações sobre um alerta  
  
1.  No **Pesquisador de Objetos** , clique no sinal de adição para expandir o servidor no qual você deseja exibir informações sobre um alerta.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique no sinal de adição para expandir a pasta **Alertas** .  
  
4.  Clique com o botão direito do mouse no alerta que tem as informações que você deseja exibir e selecione **Propriedades**.  
  
     Para obter mais informações sobre as opções disponíveis contidas na caixa de diálogo _alert_name_**propriedades do alerta** , consulte:  
  
    -   [Propriedades do novo alerta de alerta &#40;página geral&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
    -   [Propriedades do novo alerta de alerta &#40;página de resposta&#41;](alert-properties-new-alert-response-page.md)  
  
    -   [Propriedades do alerta: Novo alerta &#40;página de opções&#41;](alert-properties-new-alert-options-page.md)  
  
    -   [Propriedades do alerta &#40;página Histórico&#41;](alert-properties-history-page.md)  
  
5.  Quando terminar, clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-view-information-about-an-alert"></a>Para exibir informações sobre um alerta  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
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
  
 Para obter mais informações, consulte [sp_help_alert &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-alert-transact-sql).  
  
  
