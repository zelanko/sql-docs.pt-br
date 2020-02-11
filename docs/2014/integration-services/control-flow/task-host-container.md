---
title: Contêiner do Host da Tarefa | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.taskhostcontainer.f1
helpviewer_keywords:
- containers [Integration Services], Task Host
- Task Host container
ms.assetid: 7394a2c2-1b07-427d-b94a-9792e7783d35
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9d5c965f4012244a3ccc2eb80470205e8d55e887
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62830053"
---
# <a name="task-host-container"></a>Contêiner Host da Tarefa
  O contêiner do host da tarefa encapsula uma única tarefa. No Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , o host da tarefa não é configurado separadamente, ele é configurado quando você define as propriedades da tarefa que ele encapsula. Para obter mais informações sobre as tarefas que os contêineres do host da tarefa encapsulam, consulte [Tarefas do Integration Services](integration-services-tasks.md).  
  
 Esse contêiner estende o uso de variáveis e manipuladores de eventos no nível de tarefa. Para obter informações, consulte [Manipuladores de Eventos do Integration Services &#40;SSIS&#41;](../integration-services-ssis-event-handlers.md) e [Variáveis do Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md).  
  
## <a name="configuration-of-the-task-host"></a>Configuração do host da tarefa  
 Você pode definir as propriedades na janela **Propriedades** do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou programaticamente.  
  
 Para obter informações sobre como definir essas propriedades no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], consulte [Definir as propriedades de uma tarefa ou de um contêiner](../set-the-properties-of-a-task-or-container.md).  
  
 Para obter informações sobre como definir essas propriedades programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>.  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Contêineres do Integration Services](integration-services-containers.md)  
  
  
