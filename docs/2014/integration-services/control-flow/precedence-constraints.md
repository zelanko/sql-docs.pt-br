---
title: Restrições de precedência | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- tasks [Integration Services], precedence constraints
- control flow [Integration Services], precedence constraints
- precedence constraints [Integration Services]
- constraints [Integration Services]
- sequence execution options [Integration Services]
- containers [Integration Services], precedence constraints
ms.assetid: c5ce5435-fd89-4156-a11f-68470a69aa9f
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 42b73f3657b668e63f7f02025e7902e19074a7eb
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84918397"
---
# <a name="precedence-constraints"></a>Restrições de precedência
  As restrições de precedência vinculam executáveis, contêineres e tarefas em pacotes em um fluxo de controle e especificam condições que determinam a execução de executáveis. Um executável pode ser um contêiner Loop For, Loop Foreach ou Sequência; uma tarefa; ou um manipulador de eventos. Os manipuladores de eventos também usam restrições de precedência para vincular os seus executáveis a um fluxo de controle.

 Uma restrição de precedência vincula dois executáveis: o de precedência e o restrito. O executável de precedência é executado antes do executável restrito e o resultado da execução do executável de precedência poderá determinar se o executável restrito será executado. O diagrama a seguir mostra dois executáveis vinculados por uma restrição de precedência.

 ![Executáveis conectados por uma restrição de precedência](../media/ssis-pcsimple.gif "Executáveis conectados por uma restrição de precedência")

 Em um fluxo de controle linear, ou seja, aquele sem-ramificação, as restrições de precedência orientam sozinhas a sequência na qual a tarefa é executada. Se um fluxo de controle se ramifica, o mecanismo de tempo de execução [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] determina a ordem de execução dentre as tarefas e contêineres que vêm logo após a ramificação. O mecanismo de tempo de execução também determina a ordem de execução entre fluxos de trabalho não conectados em um fluxo de controle.

 A arquitetura de contêiner aninhado do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] habilita todos os contêineres, com exceção do contêiner host da tarefa que encapsula somente uma única tarefa, a incluírem outros contêineres, cada um com seu próprio fluxo de controle. Os contêineres Loop For, Loop Foreach e Sequência podem incluir várias tarefas e outros contêineres que, por sua vez, podem incluir várias tarefas e contêineres. Por exemplo, um pacote com uma tarefa Script e um contêiner Sequência tem uma restrição de precedência que vincula a tarefa Script e o contêiner Sequência. O contêiner Sequência inclui três tarefas Script e suas restrições de precedência vinculam as três tarefas Script em um fluxo de controle. O diagrama a seguir mostra as restrições de precedência em um pacote com dois níveis de aninhamento.

 ![Restrições de precedência em um pacote](../media/mw-dts-12.gif "Restrições de precedência em um pacote")

 Como o pacote está no topo da hierarquia de contêineres do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , vários pacotes não podem ser vinculados por restrições de precedência; entretanto, é possível adicionar uma tarefa Executar Pacote a um pacote e, indiretamente, vincular outro pacote ao fluxo de controle.

 É possível configurar restrições de precedência adotando um dos seguinte procedimentos:

-   Especifique uma operação de avaliação. A restrição de precedência usa um valor de restrição, uma expressão, ambos ou para determinar se o executável restrito será executado.

-   Se a restrição de precedência usar um resultado de execução, você poderá especificar o resultado de execução para ser sucesso, falha ou conclusão.

-   Se a restrição de precedência usar um resultado de avaliação, você poderá fornecer uma expressão que avalie a um booleano.

-   Especifique se a restrição de precedência é avaliada isoladamente ou junto com outras restrições aplicáveis ao executável restrito.

## <a name="evaluation-operations"></a>Operações de avaliação
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] fornece as operações de avaliação a seguir:

-   Uma restrição que usa somente o resultado da execução do executável de precedência para determinar se o executável restrito será executado. O resultado da execução do executável de precedência pode ser conclusão, sucesso ou falha. Essa é a operação padrão.

-   Uma expressão que é avaliada para determinar se o executável restrito será executado. Se a expressão avaliar como true, o executável restrito será executado.

-   Uma expressão e uma restrição que combinam os requisitos dos resultados da execução do executável de precedência e os resultados de retorno da avaliação da expressão.

-   Uma expressão ou restrição que usa os resultados da execução do executável de precedência ou os resultados de retorno da avaliação da expressão.

 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] O Designer usa cores para identificar o tipo de restrição de precedência. A restrição Bem-sucedida é verde, a restrição Falha é vermelha, e a restrição Conclusão é azul. Para exibir rótulos de texto no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer que mostrem o tipo de restrição, você deve configurar os recursos de acessibilidade do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer.

 A expressão deve ser uma expressão válida do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] e pode incluir funções, operadores e, variáveis do sistema e personalizadas. Para obter informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../expressions/integration-services-ssis-expressions.md) e [Manipuladores de Eventos do Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md).

## <a name="execution-results"></a>Resultados da execução
 A restrição de precedência pode usar os resultados de execução a seguir sozinhos ou em combinação com uma expressão.

-   A conclusão requer que somente o executável de precedência seja concluído, sem considerar o resultado, para que o executável restrito seja executado.

-   O sucesso requer que o executável de precedência seja concluído com êxito para que o executável restrito seja executado.

-   A falha requer que o executável de precedência falhe para que o executável restrito seja executado.

> [!NOTE]
>  Somente as restrições de precedência que forem membros da mesma coleção `Precedence Constraint` poderão ser agrupadas em uma condição AND lógica. Por exemplo, você não pode combinar restrições de precedência de dois contêineres Loop Foreach.

## <a name="configuration-of-the-precedence-constraint"></a>Configuração da restrição de precedência
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.

 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, consulte [Editor de Restrição de Precedência](../precedence-constraint-editor.md).

 Para obter informações sobre como definir essas propriedades programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint>.

## <a name="related-tasks"></a>Related Tasks
 Para obter detalhes sobre como definir essas propriedades no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, clique em um dos tópicos a seguir:

-   [Definir as propriedades de uma restrição de precedência](../set-the-properties-of-a-precedence-constraint.md)

-   [Definir o valor de uma restrição de precedência por meio do menu de atalho](../set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)

-   [Como conectar tarefas e contêineres por meio de uma restrição de precedência padrão](../connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)

     Este tópico fornece informações sobre como definir o comportamento padrão de restrições de precedência e como conectar executáveis usando as restrições de precedência padrão, consulte.

## <a name="related-content"></a>Conteúdo relacionado
 Artigo técnico, [Exemplos de expressões SSIS](https://go.microsoft.com/fwlink/?LinkId=220761), em social.technet.microsoft.com

## <a name="see-also"></a>Consulte Também
 [Adicionar expressões a restrições de](../add-expressions-to-precedence-constraints.md) precedência [várias restrições de precedência](../multiple-precedence-constraints.md)


