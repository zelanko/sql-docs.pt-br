---
title: Gravar o status do trabalho no log de aplicativos do Windows | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- status information [SQL Server], jobs
- SQL Server Agent jobs, status
- writing job status to log
- jobs [SQL Server Agent], status
- logs [SQL Server], jobs
ms.assetid: 3b813702-8f61-40ec-bf3b-ce9deb7e68be
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ec615911233227c15f43e55125adfd6166cb51e8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72783366"
---
# <a name="write-the-job-status-to-the-windows-application-log"></a>Write the Job Status to the Windows Application Log
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Este tópico descreve como configurar o Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para gravar o status do trabalho no log de eventos de aplicativos [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]do [!INCLUDE[tsql](../../includes/tsql-md.md)]Windows usando o, o ou o SQL Server Management Objects.  
  
 As respostas de trabalho asseguram que os administradores de banco de dados saibam quando os trabalhos são concluídos e a frequência com que são executados. São respostas de trabalho típicas:  
  
-   Notificar o operador por meio de email, pager eletrônico ou uma mensagem **net send** . Use uma dessas respostas de trabalho se o operador tiver de executar uma ação de acompanhamento. Por exemplo, se um trabalho de backup for concluído com êxito, o operador deverá ser notificado para remover a fita de backup e armazená-la em local seguro.  
  
-   Gravar uma mensagem de evento no log de aplicativos do Windows. Essa resposta só pode ser utilizada para trabalhos que falharam.  
  
-   Excluir o trabalho automaticamente. Use essa resposta de trabalho se você tiver certeza de que não precisará reexecutar o trabalho.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para gravar o status do trabalho no log de aplicativos do Windows usando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
 Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-write-job-status-to-the-windows-application-log"></a>Para gravar o status do trabalho no log de aplicativos do Windows  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e a expanda.  
  
2.  Expanda **SQL Server Agent**, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho que deseja editar e clique em **Propriedades**.  
  
3.  Selecione a página **Notificações** .  
  
4.  Marque **Gravar no log de eventos de aplicativos do Windows**e siga um destes procedimentos:  
  
    -   Clique em**Quando o trabalho for bem-sucedido**para registrar o status do trabalho quando ele for concluído com êxito.  
  
    -   Clique em**Quando o trabalho falhar**para registrar o status do trabalho quando ele não for concluído com êxito.  
  
    -   Clique em**Quando o trabalho for concluído** para registrar o status do trabalho independentemente do status de conclusão.  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Usando SQL Server Management Objects  

### <a name="to-write-job-status-to-the-windows-application-log"></a>Para gravar o status do trabalho no log de aplicativos do Windows
  
 Chame a propriedade `EventLogLevel` da classe `Job` usando uma linguagem de programação que você escolher, como o Visual Basic, Visual C# ou PowerShell.  
  
 O código de exemplo a seguir define o trabalho para gerar uma entrada no log de eventos do sistema deve ser gerada quando a execução do trabalho for concluída.  
  
```powershell
$srv = new-object Microsoft.SqlServer.Management.Smo.Server("(local)")  
$jb = new-object Microsoft.SqlServer.Management.Smo.Agent.Job($srv.JobServer, "Test Job")  
$jb.EventLogLevel = [Microsoft.SqlServer.Management.Smo.Agent.CompletionAction]::Always  
```  
