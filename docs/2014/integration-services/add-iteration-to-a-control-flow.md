---
title: Adicionar iteração a um fluxo de controle | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- repeating workflows
- adding iterations
- control flow [Integration Services], iterations
- expressions [Integration Services], control flow
- iterations [Integration Services]
- For Loop containers
ms.assetid: eb3a7494-88ae-4165-9d0f-58715eb1734a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 039f1dff39f5bc89dbe360d49ad0d4174d665074
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439633"
---
# <a name="add-iteration-to-a-control-flow"></a>Adicionar iteração a um fluxo de controle
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] inclui o contêiner Loop For, um elemento de fluxo de controle que torna simples a inclusão de um looping que repete condicionalmente um fluxo de controle em um pacote. Para obter mais informações, consulte [Contêiner Loop For](control-flow/for-loop-container.md).  
  
 O contêiner Loop For avalia uma condição em cada iteração do loop e para quando a condição for avaliada como falsa. O contêiner Loop For inclui expressões para inicializar o loop, especificar a condição da avaliação que para a execução da repetição do fluxo de controle e designar um valor para uma expressão que atualize o valor contra o qual a condição da avaliação é comparada. Você deve fornecer uma condição de avaliação, mas expressões de inicialização e tarefa são opcionais.  
  
 O contêiner Loop For não fornece nenhuma funcionalidade, ele só fornece a estrutura na qual você cria o fluxo de controle repetível. Para fornecer funcionalidade de contêiner, você deve incluir no mínimo uma tarefa no contêiner Loop For. Para obter mais informações, consulte [Tarefas do Integration Services](control-flow/integration-services-tasks.md).  
  
 O contêiner Loop For pode incluir um fluxo de controle com várias tarefas, além de outros contêineres. Adicionar tarefas e contêineres ao contêiner Loop For é semelhante a adicioná-las a um pacote, exceto que você arrasta as tarefas e contêineres para o contêiner Loop Forem e não para o pacote. Se o contêiner Loop For incluir mais de uma tarefa ou contêiner, você poderá conectá-los usando as restrições de precedência, assim como faria em um pacote. Para obter informações, consulte [Restrições de precedência](control-flow/precedence-constraints.md).  
  
## <a name="using-expressions-in-for-loop-configuration"></a>Usando expressões na configuração de Loop For  
 Quando você configura o contêiner Loop For especificando uma condição de avaliação, valor de inicialização ou atribuição de valor, pode usar expressões ou literais.  
  
 As expressões podem incluir variáveis. A vantagem de usar variáveis é que elas podem ser atualizadas no tempo de execução, tornando os pacotes mais flexíveis e fáceis de gerenciar. O comprimento máximo de uma expressão é de 4000 caracteres.  
  
 Quando você especifica uma variável em uma expressão, deve introduzir o nome da variável com o sinal de arroba (@). Por exemplo, para uma variável chamada `Counter` , insira @Counter na expressão que o contêiner loop for usa. Se você incluir a propriedade namespace na variável, deverá incluir a variável e namespace entre colchetes. Por exemplo, para uma `Counter` variável no `MyNamespace` namespace, digite [ @MyNamespace::Counter ].  
  
 As variáveis que o contêiner Loop For usa devem ser definidas no escopo do contêiner Loop For ou no escopo de qualquer contêiner que seja o maior na hierarquia de contêiner do pacote. Por exemplo, um contêiner Loop For pode usar variáveis definidas em seu escopo e também variáveis definidas no escopo do pacote. Para obter mais informações, consulte [Variáveis do Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md) e [Usar variáveis em pacotes](../../2014/integration-services/use-variables-in-packages.md).  
  
 A gramática de expressão do [!INCLUDE[ssIS](../includes/ssis-md.md)] fornece um conjunto completo de operadores e funções para implementar as complexas expressões usadas para avaliação, inicialização ou atribuição. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md).  
  
### <a name="to-implement-a-for-loop-container-in-a-control-flow"></a>Para implementar um contêiner Loop For em um fluxo de controle  
  
1.  Adicione o contêiner Loop For ao pacote. Para obter mais informações, consulte [Adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
2.  Adicione tarefas e contêineres ao contêiner Loop For. Para obter mais informações, consulte [Adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
3.  Conecte tarefas e contêineres ao contêiner Loop For usando restrições de precedência. Para obter mais informações, consulte [Como conectar tarefas e contêineres utilizando uma restrição de precedência padrão](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md).  
  
4.  Configure o contêiner Loop For. Para obter mais informações, consulte [Configurar um contêiner Loop For](../../2014/integration-services/configure-a-for-loop-container.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [Agrupar ou desagrupar componentes](group-or-ungroup-components.md)   
 [Conectar tarefas e contêineres usando uma restrição de precedência padrão](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)   
 [Adicionar Enumeração a um fluxo de controle](../../2014/integration-services/add-enumeration-to-a-control-flow.md)   
 [Fluxo de controle](control-flow/control-flow.md)  
  
  
