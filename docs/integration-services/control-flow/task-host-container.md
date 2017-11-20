---
title: "Contêiner Host da tarefa | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.taskhostcontainer.f1
helpviewer_keywords:
- containers [Integration Services], Task Host
- Task Host container
ms.assetid: 7394a2c2-1b07-427d-b94a-9792e7783d35
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 27fc5684d3ed15dcd8638e0515af57f7164d6e9c
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="task-host-container"></a>Contêiner Host da Tarefa
  O contêiner do host da tarefa encapsula uma única tarefa. No Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , o host da tarefa não é configurado separadamente, ele é configurado quando você define as propriedades da tarefa que ele encapsula. Para obter mais informações sobre as tarefas que os contêineres do host da tarefa encapsulam, consulte [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md).  
  
 Esse contêiner estende o uso de variáveis e manipuladores de eventos no nível de tarefa. Para obter informações, consulte [Manipuladores de Eventos do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-event-handlers.md) e [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## <a name="configuration-of-the-task-host"></a>Configuração do host da tarefa  
 Você pode definir as propriedades na janela **Propriedades** do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou programaticamente.  
  
 Para obter informações sobre como definir essas propriedades no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], consulte [Definir as propriedades de uma tarefa ou de um contêiner](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b).  
  
 Para obter informações sobre como definir essas propriedades programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>.  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
-   [Definir as propriedades de uma tarefa ou de um contêiner](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="see-also"></a>Consulte também  
 [Contêineres do Integration Services](../../integration-services/control-flow/integration-services-containers.md)  
  
  

