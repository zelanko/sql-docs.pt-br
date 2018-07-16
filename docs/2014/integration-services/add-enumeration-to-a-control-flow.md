---
title: Adicionar enumeração a um fluxo de controle | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- adding enumerations
- Foreach Loop containers
- control flow [Integration Services], enumerations
- repeating workflows
- enumerations [Integration Services]
ms.assetid: f212b5fb-3cc4-422e-9b7c-89eb769a812a
caps.latest.revision: 38
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 039b9a1cd94b3baa207c5d738dc8ed2455bb9d74
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37223717"
---
# <a name="add-enumeration-to-a-control-flow"></a>Adicionar enumeração a um fluxo de controle
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] inclui o contêiner do Loop Foreach, um elemento de fluxo de controle que torna simples a inclusão de um constructo de loop que enumera arquivos e objetos no fluxo de controle de um pacote. Para obter mais informações, consulte [Foreach Loop Container](control-flow/foreach-loop-container.md).  
  
 O contêiner Loop Foreach não fornece nenhuma funcionalidade, ele só fornece a estrutura na qual você cria o fluxo de controle repetível, especifica o tipo do enumerados e configura o enumerador. Para fornecer funcionalidade de contêiner, você deve incluir no mínimo uma tarefa no contêiner Loop Foreach. Para obter mais informações, consulte [Tarefas do Integration Services](control-flow/integration-services-tasks.md).  
  
 O contêiner Loop Foreach pode incluir um fluxo de controle com várias tarefas e outros contêineres. Adicionar tarefas e contêineres ao contêiner Loop Foreach é semelhante a adicioná-las a um pacote, exceto que você arrasta as tarefas e contêineres para o contêiner Loop Foreach e não para o pacote. Se o contêiner Loop Foreach incluir mais de uma tarefa ou contêiner, você poderá conectá-los usando as restrições de precedência, assim como faria em um pacote. Para obter mais informações, consulte [Precedence Constraints](control-flow/precedence-constraints.md).  
  
### <a name="to-implement-a-foreach-loop-container-in-a-control-flow"></a>Para implementar um contêiner Loop Foreach em um fluxo de controle  
  
1.  Adicione o contêiner Loop Foreach ao pacote. Para obter mais informações, consulte [adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  para obter informações sobre a ferramenta de configuração e recursos adicionais.  
  
2.  Adicione tarefas e contêineres ao contêiner Loop Foreach. Para obter mais informações, consulte [adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  para obter informações sobre a ferramenta de configuração e recursos adicionais.  
  
3.  Conecte tarefas e contêineres no contêiner Loop Foreach usando restrições de precedência. Para obter mais informações, consulte [Como conectar tarefas e contêineres utilizando uma restrição de precedência padrão](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md).  
  
4.  Configure o contêiner Loop Foreach. Para obter mais informações, consulte [Configurar um Contêiner do Loop Foreach](../../2014/integration-services/configure-a-foreach-loop-container.md).  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [Agrupar ou desagrupar componentes](group-or-ungroup-components.md)   
 [Restrições de precedência](control-flow/precedence-constraints.md)   
 [Adicionar iteração a um fluxo de controle](add-iteration-to-a-control-flow.md)   
 [Fluxo de Controle](control-flow/control-flow.md)  
  
  
