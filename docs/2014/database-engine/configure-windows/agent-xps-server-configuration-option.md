---
title: Opção de configuração de servidor Agent XPs | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Agent XPs option
- extended stored procedures [SQL Server], SQL Server Agent
ms.assetid: 2e1c6c64-5ce7-4357-98c7-ac7763a9f9de
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4598678cc4dea0a11c37545487ce09529dbb4584
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935917"
---
# <a name="agent-xps-server-configuration-option"></a>Opção Agent XPs de configuração do servidor
  Use a opção **Agent XPs** para habilitar os procedimentos armazenados estendidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent neste servidor. Quando esta opção não está habilitada, o nó [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não fica disponível no Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
 Quando a ferramenta [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] é usada para iniciar o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, esses procedimentos armazenados estendidos são habilitados automaticamente. Para obter mais informações, consulte [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
> [!NOTE]  
>  O Pesquisador de Objetos do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] não exibe o conteúdo do nó [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agent, a menos que os procedimentos armazenados estendidos estejam habilitados, independentemente do estado do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 Os valores possíveis são:  
  
-   **0**, indicando que os procedimentos armazenados estendidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não estão disponíveis (o padrão).  
  
-   **1**, indicando que os procedimentos armazenados estendidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent estão disponíveis.  
  
 A configuração entra em vigor imediatamente, sem que o servidor seja parado e reiniciado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir habilita os procedimentos armazenados estendidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Agent XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas de administração automatizadas &#40;SQL Server Agent&#41;](../../ssms/agent/sql-server-agent.md)   
 [Start, Stop, or Pause the SQL Server Agent Service](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
  
