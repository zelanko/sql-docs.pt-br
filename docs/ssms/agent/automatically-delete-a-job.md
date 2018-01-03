---
title: Excluir um trabalho automaticamente | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dropping jobs
- SQL Server Agent jobs, removing
- automatic job removal
- jobs [SQL Server Agent], deleting
- deleting jobs
- removing jobs
ms.assetid: 92dbb6da-5919-4bde-9354-d454e9ea3da0
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3d5f95e01fd94ef41b89c5086cacf8b98bbf720e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="automatically-delete-a-job"></a>Automatically Delete a Job
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tópico descreve como configurar o [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] para excluir trabalhos automaticamente quando eles obtiverem êxito, falharem ou forem concluídos usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] ou o SQL Server Management Objects.  
  
As respostas de trabalho asseguram que os administradores de banco de dados saibam quando os trabalhos são concluídos e a frequência com que são executados. São respostas de trabalho típicas:  
  
-   Notificar o operador por meio de email, pager eletrônico ou uma mensagem **net send** .  
  
    Use uma dessas respostas de trabalho se o operador tiver de executar uma ação de acompanhamento. Por exemplo, se um trabalho de backup for concluído com êxito, o operador deverá ser notificado para remover a fita de backup e armazená-la em local seguro.  
  
-   Gravar uma mensagem de evento no log de aplicativos do Windows.  
  
    Essa resposta só pode ser utilizada para trabalhos que falharam.  
  
-   Excluir o trabalho automaticamente.  
  
    Use essa resposta de trabalho se você tiver certeza de que não precisará reexecutar o trabalho.  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Segurança](#Security)  
  
-   **Para especificar respostas de trabalho, usando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Security"></a>Segurança  
Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-automatically-delete-a-job"></a>Para excluir um trabalho automaticamente  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e a expanda.  
  
2.  Expanda **SQL Server Agent**, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho que deseja editar e clique em **Propriedades**.  
  
3.  Selecione a página **Notificações** .  
  
4.  Marque **Excluir trabalho automaticamente**e siga um destes procedimentos:  
  
    -   Clique em **Quando o trabalho for bem-sucedido** para excluir o status do trabalho quando ele for concluído com êxito.  
  
    -   Clique em **Quando o trabalho falhar** para excluir o trabalho quando ele não puder ser concluído.  
  
    -   Clique em **Quando o trabalho for concluído** para excluir o trabalho independentemente de seu status de conclusão.  
  
## <a name="SMO"></a>Usando o SQL Server Management Objects  
**Para excluir um trabalho automaticamente**  
  
Use a propriedade **DeleteLevel** da classe **Job** com uma linguagem de programação à sua escolha, como Visual Basic, Visual C# ou PowerShell. Para obter mais informações, veja [SMO (SQL Server Management Objects)](http://msdn.microsoft.com/library/ms162169.aspx).  
  
