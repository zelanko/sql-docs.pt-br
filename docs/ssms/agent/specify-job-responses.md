---
title: Especificar respostas de trabalho | Microsoft Docs
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
- jobs [SQL Server Agent], responses
- SQL Server Agent jobs, responses
- actions [SQL Server Agent jobs]
- responding to jobs
ms.assetid: 050242e1-9b79-4ade-91a9-580707b9d2d9
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 493fe4698081d7d748e0cb4a16993dc697baf799
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="specify-job-responses"></a>Especificar respostas de trabalho
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] As respostas de trabalho especificam ações que o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent deve efetuar após a conclusão de um trabalho. As respostas de trabalho asseguram que os administradores de banco de dados saibam quando os trabalhos são concluídos e a frequência com que são executados. São respostas de trabalho típicas:  
  
-   Notificar o operador por meio de email, pager eletrônico ou uma mensagem **net send** .  
  
    Use uma dessas respostas de trabalho se o operador tiver de executar uma ação de acompanhamento. Por exemplo, se um trabalho de backup for concluído com êxito, o operador deverá ser notificado para remover a fita de backup e armazená-la em local seguro.  
  
-   Gravar uma mensagem de evento no log de aplicativos do Windows.  
  
    Essa resposta só pode ser utilizada para trabalhos que falharam.  
  
-   Excluir o trabalho automaticamente.  
  
    Use essa resposta de trabalho se você tiver certeza de que não precisará reexecutar o trabalho.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Descrição**|**Tópico**|  
|Descreve como notificar um operador sobre o status do trabalho.|[Notify an Operator of Job Status](../../ssms/agent/notify-an-operator-of-job-status.md)|  
|Descreve como gravar o status do trabalho no log de aplicativos do Windows.|[Write the Job Status to the Windows Application Log](../../ssms/agent/write-the-job-status-to-the-windows-application-log.md)|  
  
## <a name="see-also"></a>Consulte Também  
[Monitorar e responder a eventos](../../ssms/agent/monitor-and-respond-to-events.md)  
  
