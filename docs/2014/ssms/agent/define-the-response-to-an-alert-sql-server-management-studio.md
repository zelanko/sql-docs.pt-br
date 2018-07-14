---
title: Definir a resposta a um alerta (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, alerts
- alerts [SQL Server], responding to
- responding to alerts
ms.assetid: c86ca6eb-c59f-46e9-bc32-d474e7c3b170
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 91eebf84cdcb9750e7a5aef10b88b1c3b0bbc31e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37200696"
---
# <a name="define-the-response-to-an-alert-sql-server-management-studio"></a>Definir a resposta a um alerta (SQL Server Management Studio)
  Este tópico descreve como definir o modo de resposta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a alertas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para definir uma resposta a um alerta, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   As opções Pager e **net send** serão removidas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esses recursos em novo trabalho de desenvolvimento e planeje modificar os aplicativos que os usam atualmente.  
  
-   Observe que o SQL Server Agent deve ser configurado para usar o Database Mail a fim de enviar notificações por pager ou email a operadores. Para obter mais informações, consulte [Atribuir alertas a um operador](http://msdn.microsoft.com/library/ms190038.aspx).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] gerencia trabalhos de forma fácil e com representação gráfica. Além disso, ele é recomendado para criar e gerenciar a infraestrutura de trabalhos.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Somente membros da função de servidor fixa **sysadmin** podem definir a resposta a um alerta.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-define-the-response-to-an-alert"></a>Para definir uma resposta a um alerta  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor que contém o alerta sobre o qual você quer definir uma resposta.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique no sinal de adição para expandir a pasta **Alertas** .  
  
4.  Clique com o botão direito do mouse no alerta no qual você deseja definir uma resposta e selecione **Propriedades**.  
  
5.  Na caixa de diálogo *alert_name***Propriedades do alerta**, em **Selecione uma página**, selecione **Resposta**.  
  
6.  Marque a caixa de seleção **Executar trabalho** e, na lista abaixo da caixa de seleção **Executar trabalho** , selecione um trabalho para executar quando o alerta ocorrer. Você pode criar um trabalho novo clicando em **Novo Trabalho** Você pode exibir mais informações sobre o trabalho clicando em **Exibir Trabalho**. Para obter mais informações sobre as opções disponíveis nas caixas de diálogo **Novo Trabalho** e **Propriedades de Trabalho***job_name*, consulte [Criar um Trabalho](create-a-job.md) e [Exibir um Trabalho](view-a-job.md).  
  
7.  Marque a caixa de seleção **Notificar Operadores** se você quiser notificar os operadores quando o alerta for ativado. Na **Lista de operadores**, selecione um ou mais dos métodos a seguir para notificar o operador ou operadores: **Email**, **Pager**ou **Net Send**. Você pode criar um operador novo clicando em **Novo Operador** Você pode visualizar mais informações sobre um operador clicando em **Exibir Operador**. Para obter mais informações sobre as opções disponíveis nas caixas de diálogo **Novo Operador** e **Exibir Propriedades do Operador** , consulte [Create an Operator](create-an-operator.md) e [View Information About an Operator](view-information-about-an-operator.md).  
  
8.  Quando terminar, clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-define-the-response-to-an-alert"></a>Para definir uma resposta a um alerta  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- adds an e-mail notification for Test Alert.  
    -- assumes that Test Alert already exists and that François Ajenstat is a valid operator name   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_notification  
     @alert_name = N'Test Alert',  
     @operator_name = N'François Ajenstat',  
     @notification_method = 1 ;  
    GO  
    ```  
  
 Para obter mais informações, consulte [sp_add_notification &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-notification-transact-sql).  
  
  
