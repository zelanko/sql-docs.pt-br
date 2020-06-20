---
title: Contêiner da Sequência | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sequencecontainer.f1
helpviewer_keywords:
- Sequence container
- grouping control flows
- containers [Integration Services], Sequence
- subset control flow [Integration Services]
ms.assetid: 7731f91e-b8b3-4d96-a0d9-73f568547cb3
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c380921202b1037c3bd066f4aef0610703a75a91
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84918196"
---
# <a name="sequence-container"></a>Contêiner de sequência
  O contêiner da sequência define um fluxo de controle que é um subconjunto do fluxo de controle do pacote. Os contêineres da sequência agrupam o pacote em vários fluxos de controle separados, cada um contendo uma ou mais tarefas e contêineres, que são executados dentro do fluxo de controle de pacote geral.  
  
 O contêiner Sequência pode incluir múltiplas tarefas além de outros contêineres. Adicionar tarefas e contêineres a um contêiner de Sequência é semelhante a adicioná-los a um pacote, exceto que você arrasta as tarefas e contêineres para o contêiner de Sequência e não para o contêiner de pacote. Se o contêiner Sequência incluir mais de uma tarefa ou contêiner, você pode conectá-los usando restrições de precedência, exatamente como faria em um pacote. Para obter informações, consulte [Restrições de precedência](precedence-constraints.md).  
  
 São muitos os benefícios para utilizar um contêiner da sequência:  
  
-   Desabilitar grupos de tarefas para focalizar a depuração de pacote em um subconjunto do fluxo de controle de pacote.  
  
-   Gerenciar as propriedades de várias tarefas em um local definindo-se as propriedades em um contêiner da sequência em vez de em tarefas individuais.  
  
     Por exemplo, você pode definir a propriedade `Disable` do contêiner da sequência como `True` para desabilitar todas as tarefas e contêineres no contêiner da sequência.  
  
-   Fornecer o escopo para variáveis que um grupo de tarefas relacionadas e contêineres usa.  
  
-   Agrupar muitas tarefas para que você possa gerenciá-las mais facilmente com o recolhimento e a expansão do contêiner de sequência.  
  
     Você também pode criar grupos que expandem e recolhem usando a caixa **Grupo** . Entretanto, a caixa **Grupo** é um recurso de tempo de design que não tem propriedades ou comportamento de tempo de execução. Para obter mais informações, consulte [Agrupar ou desagrupar componentes](../group-or-ungroup-components.md)  
  
-   Definir um atributo de transação no contêiner de sequência para definir uma transação para um subconjunto do fluxo de controle do pacote. Desse modo, é possível gerenciar as transações em um nível mais granular.  
  
     Por exemplo, se um contêiner da sequência incluir duas tarefas relacionadas, uma que exclui dados de uma tabela e outra que insere, você poderá configurar uma transação para assegurar que a ação de exclusão seja revertida se a ação de inserção falhar. Para obter mais informações, consulte [Transações do Integration Services](../integration-services-transactions.md).  
  
## <a name="configuration-of-the-sequence-container"></a>Configuração do contêiner da sequência  
 O contêiner da sequência não tem nenhuma interface do usuário personalizada e você somente poderá configurá-lo na janela **Propriedades** do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre como definir essas propriedades programaticamente, consulte a documentação da classe **T:Microsoft.SqlServer.Dts.Runtime.Sequence** no Guia do Desenvolvedor.  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter informações sobre como definir as propriedades do componente no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], consulte [Definir as propriedades de um componente de fluxo de dados](../set-the-properties-of-a-task-or-container.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle](add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [Como conectar tarefas e contêineres por meio de uma restrição de precedência padrão](../connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)   
 [Contêineres do Integration Services](integration-services-containers.md)  
  
  
