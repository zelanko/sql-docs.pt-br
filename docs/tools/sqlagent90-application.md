---
title: Aplicativo SQLAGENT90 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: sqlagent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- starting SQL Server Agent
- sqlagent90 application
- SQL Server Agent, starting
- command prompt utilities [SQL Server], sqlagent90
ms.assetid: e8b80e8d-d0c9-4500-a868-0ce08233da08
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bbc6f3a3b463b27108f7e5601078416ea3267973
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33076783"
---
# <a name="sqlagent90-application"></a>aplicativo sqlagent90
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O aplicativo **sqlagent90** inicia o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent no prompt de comando. Normalmente, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent deve ser executado no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ou usando métodos SQL-SMO em um aplicativo. Execute o **sqlagent90** no prompt de comando apenas quando estiver diagnosticando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent ou quando for direcionado a ele por seu provedor de suporte.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlagent90  
-c [-v] [-i instance_name]  
```  
  
## <a name="arguments"></a>Argumentos  
 **-c**  
 Indica que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent está sendo executado pelo prompt de comando e é independente do Gerenciador de Controle de Serviços do Microsoft Windows. Quando **-c** é usado, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent não pode ser controlado no aplicativo de Serviços nas Ferramentas Administrativas nem no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager. Esse argumento é obrigatório.  
  
 **-v**  
 Indica que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent é executado em modo detalhado e grava informações de diagnóstico na janela do prompt de comando. As informações de diagnóstico são iguais às informações gravadas no log de erros do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent.  
  
 **-i** *instance_name*  
 Indica que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent se conecta com a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nomeada especificada por *instance_name*.  
  
## <a name="remarks"></a>Remarks  
 Depois de exibir uma mensagem de direitos autorais, o **sqlagent90** exibe a saída na janela de prompt de comando somente quando a opção **-v** é especificada. Para interromper o **sqlagent90**, pressione CTRL+C no prompt de comando. Não feche a janela do prompt de comando antes de interromper o **sqlagent90**.  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas de administração automatizadas &#40;SQL Server Agent&#41;](http://msdn.microsoft.com/library/541ee5ac-2c9f-4b74-b4f0-13b7bd5920b0)  
  
  
