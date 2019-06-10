---
title: Opção de configuração de servidor Agent XPs | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Agent XPs option
- extended stored procedures [SQL Server], SQL Server Agent
ms.assetid: 2e1c6c64-5ce7-4357-98c7-ac7763a9f9de
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 85af1eb285a8739fb6c9e092609909be660223bb
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66786799"
---
# <a name="agent-xps-server-configuration-option"></a>Opção Agent XPs de configuração do servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Use a opção **Agent XPs** para habilitar os procedimentos armazenados estendidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent neste servidor. Quando esta opção não está habilitada, o nó [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não fica disponível no Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
 Quando a ferramenta [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] é usada para iniciar o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, esses procedimentos armazenados estendidos são habilitados automaticamente. Para obter mais informações, consulte [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
> [!NOTE]  
>  O Pesquisador de Objetos do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] não exibe o conteúdo do nó [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agent, a menos que os procedimentos armazenados estendidos estejam habilitados, independentemente do estado do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 Os valores possíveis são:  
  
-   **0**, indicando que os procedimentos armazenados estendidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não estão disponíveis (o padrão).  
  
-   **1**, indicando que os procedimentos armazenados estendidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent estão disponíveis.  
  
 A configuração entra em vigor imediatamente, sem que o servidor seja parado e reiniciado.  
  
## <a name="example"></a>Exemplo
 O exemplo a seguir habilita os procedimentos armazenados estendidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  

1. No Microsoft SQL Server Management Studio, conecte-se ao Mecanismo de Banco de Dados.

2.  Na barra Padrão, clique em **Nova Consulta**.

3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. 
  
```sql 
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
 [Tarefas de administração automatizadas &#40;SQL Server Agent&#41;](https://msdn.microsoft.com/library/541ee5ac-2c9f-4b74-b4f0-13b7bd5920b0)   
 [Iniciar, parar ou pausar o serviço do SQL Server Agent](https://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)  
  
  
