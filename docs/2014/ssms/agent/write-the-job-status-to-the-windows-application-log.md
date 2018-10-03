---
title: Gravar o status do trabalho no log de aplicativos do Windows | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
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
ms.openlocfilehash: ec23171d809252bc7ebb669db1da020dd1a9862f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48223026"
---
# <a name="write-the-job-status-to-the-windows-application-log"></a>Gravar o status do trabalho no log de aplicativos do Windows
  Este tópico descreve como configurar o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para gravar status de trabalho no log de eventos de aplicativos Windows usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]ou o SQL Server Management Objects.  
  
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
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
 Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-write-job-status-to-the-windows-application-log"></a>Para gravar o status do trabalho no log de aplicativos do Windows  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e a expanda.  
  
2.  Expanda **SQL Server Agent**, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho que deseja editar e clique em **Propriedades**.  
  
3.  Selecione a página **Notificações** .  
  
4.  Marque **Gravar no log de eventos de aplicativos do Windows**e siga um destes procedimentos:  
  
    -   Clique em**Quando o trabalho for bem-sucedido**para registrar o status do trabalho quando ele for concluído com êxito.  
  
    -   Clique em**Quando o trabalho falhar**para registrar o status do trabalho quando ele não for concluído com êxito.  
  
    -   Clique em**Quando o trabalho for concluído** para registrar o status do trabalho independentemente do status de conclusão.  
  
##  <a name="SMO"></a> Usando o SQL Server Management Objects  
 **Para gravar o status do trabalho no log de aplicativos do Windows**  
  
 Chame a propriedade `EventLogLevel` da classe `Job` usando uma linguagem de programação que você escolher, como o Visual Basic, Visual C# ou PowerShell.  
  
 O código de exemplo a seguir define o trabalho para gerar uma entrada no log de eventos do sistema deve ser gerada quando a execução do trabalho for concluída.  
  
 **PowerShell**  
  
```  
$srv = new-object Microsoft.SqlServer.Management.Smo.Server("(local)")  
$jb = new-object Microsoft.SqlServer.Management.Smo.Agent.Job($srv.JobServer, "Test Job")  
$jb.EventLogLevel = [Microsoft.SqlServer.Management.Smo.Agent.CompletionAction]::Always  
```  
  
  
