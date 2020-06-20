---
title: Notificar um operador sobre o status do trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- status information [SQL Server], jobs
- jobs [SQL Server Agent], notification options
- SQL Server Agent jobs, status
- jobs [SQL Server Agent], status
- SQL Server Agent jobs, notification options
- notifications [SQL Server], job status
ms.assetid: e7399505-27ac-48d9-a637-73bf92b9df49
author: stevestein
ms.author: sstein
ms.openlocfilehash: a202327ad63cf7ef8f51d3572b257816ee6d9419
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064456"
---
# <a name="notify-an-operator-of-job-status"></a>Notify an Operator of Job Status
  Este tópico descreve como definir as opções de notificação no usando [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , [!INCLUDE[tsql](../../includes/tsql-md.md)] ou SQL Server Management Objects, para que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent possa enviar notificações para operadores sobre trabalhos.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para notificar um operador sobre o status do trabalho usando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
 Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-notify-an-operator-of-job-status"></a>Para notificar um operador sobre o status do trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e a expanda.  
  
2.  Expanda **SQL Server Agent**, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho que deseja editar e selecione **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do Trabalho** , selecione a página **Notificações** .  
  
4.  Se desejar notificar um operador via email, marque **Email**, escolha um operador na lista e selecione uma destas opções:  
  
    -   **Quando o trabalho for bem-sucedido** , para notificar o operador quando o trabalho for concluído com êxito.  
  
    -   **Quando ocorrer falha no trabalho** para notificar o operador quando o trabalho não for concluído com êxito.  
  
    -   **Quando o trabalho for concluído** , para notificar o operador independentemente do status de conclusão.  
  
5.  Se desejar notificar um operador via pager, marque **Pager**, escolha um operador na lista e selecione uma destas opções:  
  
    -   **Quando o trabalho for bem-sucedido** , para notificar o operador quando o trabalho for concluído com êxito.  
  
    -   **Quando ocorrer falha no trabalho** para notificar o operador quando o trabalho não for concluído com êxito.  
  
    -   **Quando o trabalho for concluído** , para notificar o operador independentemente do status de conclusão.  
  
6.  Se desejar notificar um operador via net send, marque **Net send**, escolha um operador na lista e selecione uma destas opções:  
  
    -   **Quando o trabalho for bem-sucedido** , para notificar o operador quando o trabalho for concluído com êxito.  
  
    -   **Quando ocorrer falha no trabalho** para notificar o operador quando o trabalho não for concluído com êxito.  
  
    -   **Quando o trabalho for concluído** , para notificar o operador independentemente do status de conclusão.  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> Usando o Transact-SQL  
  
#### <a name="to-notify-an-operator-of-job-status"></a>Para notificar um operador sobre o status do trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```sql
    -- adds an e-mail notification for the specified alert (Test Alert).  
    -- This example assumes that Test Alert already exists and that Fran??ois Ajenstat is a valid operator name.  
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_notification   
    @alert_name = N'Test Alert',   
    @operator_name = N'Fran??ois Ajenstat',   
    @notification_method = 1 ;  
    GO  
    ```  
  
 Para obter mais informações, consulte [sp_add_notification &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-add-notification-transact-sql).  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Usando SQL Server Management Objects  
 **Para notificar um operador sobre o status do trabalho**  
  
 Use a classe `Job` usando uma linguagem de programação da sua escolha, como o Visual Basic, o Visual C# ou o PowerShell. Para obter mais informações, veja [SMO (SQL Server Management Objects)](https://msdn.microsoft.com/library/ms162169.aspx).  
