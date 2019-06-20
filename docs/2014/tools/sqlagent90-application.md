---
title: Aplicativo SQLAGENT90 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- starting SQL Server Agent
- sqlagent90 application
- SQL Server Agent, starting
- command prompt utilities [SQL Server], sqlagent90
ms.assetid: e8b80e8d-d0c9-4500-a868-0ce08233da08
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cf72b26a7b5649b8d48a3d1da6dd6eab8d6c264a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63035351"
---
# <a name="sqlagent90-application"></a>aplicativo sqlagent90
  O aplicativo **sqlagent90** inicia o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent no prompt de comando. Normalmente, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent deve ser executado no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ou usando métodos SQL-SMO em um aplicativo. Execute o **sqlagent90** no prompt de comando apenas quando estiver diagnosticando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent ou quando for direcionado a ele por seu provedor de suporte.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlagent90  
-c [-v] [-iinstance_name]  
```  
  
## <a name="arguments"></a>Argumentos  
 **-c**  
 Indica que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent está sendo executado pelo prompt de comando e é independente do Gerenciador de Controle de Serviços do Microsoft Windows. Quando **-c** é usado, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent não pode ser controlado no aplicativo de Serviços nas Ferramentas Administrativas nem no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager. Esse argumento é obrigatório.  
  
 **-v**  
 Indica que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent é executado em modo detalhado e grava informações de diagnóstico na janela do prompt de comando. As informações de diagnóstico são iguais às informações gravadas no log de erros do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent.  
  
 **-i** *instance_name*  
 Indica que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent se conecta com a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nomeada especificada por *instance_name*.  
  
## <a name="remarks"></a>Comentários  
 Depois de exibir uma mensagem de direitos autorais, o **sqlagent90** exibe a saída na janela de prompt de comando somente quando a opção **-v** é especificada. Para interromper o **sqlagent90**, pressione CTRL+C no prompt de comando. Não feche a janela do prompt de comando antes de interromper o **sqlagent90**.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas de administração automatizadas &#40;SQL Server Agent&#41;](../ssms/agent/automated-administration-tasks-sql-server-agent.md)  
  
  
