---
description: Contêiner Loop For
title: Contêiner do Loop For | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.forloopcontainerdetails.f1
- sql13.dts.designer.forloopcontainer.f1
helpviewer_keywords:
- repeating control flow
- containers [Integration Services], For Loop
- For Loop containers
ms.assetid: 44cf7355-992b-4bbf-a28c-bfb012de06f6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2a8c0bb1cb003605ec863b41e2194bad4e3cf3e6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88393562"
---
# <a name="for-loop-container"></a>Contêiner Loop For

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  O contêiner Loop For define um fluxo de controle repetitivo em um pacote. A implementação de loop é semelhante à estrutura de loop **For** em linguagens de programação. Em cada repetição do loop, o contêiner Loop For avalia uma expressão e repete seu fluxo de trabalho até a expressão ser avaliada como **False**.  
  
 O contêiner Loop For usa os seguintes elementos para definir o loop:  
  
-   Uma expressão de inicialização opcional que atribui valores aos contadores de loop.  
  
-   Uma expressão de avaliação que contém a expressão usada para testar se o loop deve parar ou continuar.  
  
-   Uma expressão de iteração opcional que incrementa ou diminui o contador de loop.  
  
 O diagrama a seguir mostra um contêiner Loop For com uma tarefa Enviar Email. Se a expressão de inicialização é `@Counter = 0`, a expressão de avaliação é `@Counter < 4`e a expressão de iteração é `@Counter = @Counter + 1`, o loop é repetido quatro vezes e envia quatro mensagens de email.  
  
 ![Um contêiner Loop For repete uma tarefa quatro vezes](../../integration-services/control-flow/media/ssis-forloop.gif "Um contêiner Loop For repete uma tarefa quatro vezes")  
  
 As expressões devem ser expressões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] válidas.  
  
 Para criar as expressões de inicialização e de atribuição, você pode usar o operador de atribuição (=). Não há suporte para esse operador pela gramática de expressão do Integration Services e só pode ser usado pelos tipos de expressão de inicialização e de atribuição no contêiner Loop For. Qualquer expressão que usa o operador de atribuição deve ter a sintaxe `@Var = <expression>`, em que **Var** é uma variável de tempo de execução e \<expression> é uma expressão que segue as regras da sintaxe de expressão do [!INCLUDE[ssIS](../../includes/ssis-md.md)]. A expressão pode incluir as variáveis, literais e quaisquer operadores e funções que a gramática de expressão SSIS ofereça suporte. A expressão deve avaliar um tipo de dados que pode ser convertido em tipo de dados da variável.  
  
 Um contêiner Loop For pode ter só uma expressão de avaliação. Isso significa que o contêiner Loop For executa todos os seus elementos de fluxo de controle o mesmo número de vezes. Como o contêiner Loop For pode incluir outros contêineres Loop For, você pode construir loops aninhados e implementar loop complexo em pacotes.  
  
 Você pode definir uma propriedade de transação no contêiner Loop For para estabelecer uma transação para um subconjunto do fluxo de controle de pacote. Desse modo, é possível gerenciar as transações em um nível mais granular. Por exemplo, se um contêiner Loop For repetir um fluxo de controle que atualiza dados em uma tabela várias vezes, você poderá configurar o Loop For e seu fluxo de controle para usar uma transação para garantir que, se todos os dados não forem atualizados com êxito, nenhum dado seja atualizado. Para obter mais informações, consulte [Transações do Integration Services](../../integration-services/integration-services-transactions.md).  
  
## <a name="add-iteration-to-a-control-flow-with-the-for-loop-container"></a>Adicionar iteração a um fluxo de controle com o contêiner do Loop For
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui o contêiner Loop For, um elemento de fluxo de controle que torna simples a inclusão de um looping que repete condicionalmente um fluxo de controle em um pacote. Para obter mais informações, consulte [Contêiner Loop For](../../integration-services/control-flow/for-loop-container.md).  
  
 O contêiner Loop For avalia uma condição em cada iteração do loop e para quando a condição for avaliada como falsa. O contêiner Loop For inclui expressões para inicializar o loop, especificar a condição da avaliação que para a execução da repetição do fluxo de controle e designar um valor para uma expressão que atualize o valor contra o qual a condição da avaliação é comparada. Você deve fornecer uma condição de avaliação, mas expressões de inicialização e tarefa são opcionais.  
  
 O contêiner Loop For não fornece nenhuma funcionalidade, ele só fornece a estrutura na qual você cria o fluxo de controle repetível. Para fornecer funcionalidade de contêiner, você deve incluir no mínimo uma tarefa no contêiner Loop For. Para obter mais informações, consulte [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md).  
  
 O contêiner Loop For pode incluir um fluxo de controle com várias tarefas, além de outros contêineres. Adicionar tarefas e contêineres ao contêiner Loop For é semelhante a adicioná-las a um pacote, exceto que você arrasta as tarefas e contêineres para o contêiner Loop Forem e não para o pacote. Se o contêiner Loop For incluir mais de uma tarefa ou contêiner, você poderá conectá-los usando as restrições de precedência, assim como faria em um pacote. Para obter informações, consulte [Restrições de precedência](../../integration-services/control-flow/precedence-constraints.md).  
  
## <a name="add-a-for-loop-container-in-a-control-flow"></a>Adicionar um contêiner do Loop For em um fluxo de controle  
  
1.  Adicione o contêiner Loop For ao pacote. Para obter mais informações, consulte [Adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md).  
  
2.  Adicione tarefas e contêineres ao contêiner Loop For. Para obter mais informações, consulte [Adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md).  
  
3.  Conecte tarefas e contêineres ao contêiner Loop For usando restrições de precedência. Para obter mais informações, consulte [Como conectar tarefas e contêineres utilizando uma restrição de precedência padrão](https://msdn.microsoft.com/library/8f31f15f-98ff-4c35-b41f-8b8cfd148d75).  
  
4.  Configure o contêiner Loop For. Para obter mais informações, consulte [Configurar um contêiner Loop For](https://msdn.microsoft.com/library/b9cd7ea7-b198-4a35-8b16-6acf09611ca5).  

##  <a name="configure-the-for-loop-container"></a>Configurar o contêiner do Loop For
Este procedimento descreve como configurar um contêiner Loop For usando a caixa de diálogo **Editor do Loop For** .  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique duas vezes em contêiner Loop For para abrir o **Editor do Loop For**.  
  
2.  Como alternativa, modifique o nome e a descrição do contêiner Loop For.  
  
3.  Como alternativa, digite uma expressão de inicialização na caixa de texto **InitExpression** .  
  
4.  Como alternativa, digite uma expressão de inicialização na caixa de texto **EvalExpression** .  
  
    > [!NOTE]  
    >  A expressão deve ser avaliada como um booliano. Quando a expressão for avaliada como **false**, o loop vai parar sua execução.  
  
5.  Como alternativa, digite uma expressão de atribuição na caixa de texto **AssignExpression** .  
  
6.  Como alternativa, clique em **Expressões** e, na página **Expressões** , crie expressões de propriedade para as propriedades do contêiner Loop For. Para obter mais informações, consulte [Adicionar ou alterar uma expressão de propriedade](../../integration-services/expressions/add-or-change-a-property-expression.md).  
  
7.  Clique em **OK** para fechar o **Editor do Loop For**.  

## <a name="for-loop-editor-dialog-box"></a>Caixa de diálogo Editor de Loop For
Use a página **Loop For** da caixa de diálogo **Editor do Loop For** para configurar um loop que repita um fluxo de trabalho até que uma condição especificada seja avaliada como falsa.  
  
 Para saber mais sobre o contêiner Loop For e como usá-lo em pacotes, consulte [For Loop Container](../../integration-services/control-flow/for-loop-container.md).  
  
### <a name="options"></a>Opções  
 **InitExpression**  
 Opcionalmente, forneça uma expressão que inicialize valores usados pelo loop.  
  
 **EvalExpression**  
 Forneça uma expressão para avaliar se o loop deve parar ou continuar.  
  
 **AssignExpression**  
 Opcionalmente, forneça uma expressão que altera uma condição cada vez que o loop repete.  
  
 **Nome**  
 Forneça um nome exclusivo para o contêiner do Loop For. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes de objeto devem ser exclusivos em um pacote.  
  
 **Descrição**  
 Forneça uma descrição do contêiner do Loop For.  
 
## <a name="use-expressions-with-the-for-loop-container"></a>Usar expressões com o contêiner do Loop For  
 Quando você configura o contêiner Loop For especificando uma condição de avaliação, valor de inicialização ou atribuição de valor, pode usar expressões ou literais.  
  
 As expressões podem incluir variáveis. A vantagem de usar variáveis é que elas podem ser atualizadas no tempo de execução, tornando os pacotes mais flexíveis e fáceis de gerenciar. O comprimento máximo de uma expressão é de 4000 caracteres.  
  
 Quando você especifica uma variável em uma expressão, deve introduzir o nome da variável com o sinal de arroba (@). Por exemplo, para uma variável nomeada **Counter**, digite @Counter na expressão usada pelo contêiner Loop For. Se você incluir a propriedade namespace na variável, deverá incluir a variável e namespace entre colchetes. Por exemplo, para uma variável **Counter** no namespace **MyNamespace**, digite [@MyNamespace::Counter].  
  
 As variáveis que o contêiner Loop For usa devem ser definidas no escopo do contêiner Loop For ou no escopo de qualquer contêiner que seja o maior na hierarquia de contêiner do pacote. Por exemplo, um contêiner Loop For pode usar variáveis definidas em seu escopo e também variáveis definidas no escopo do pacote. Para obter mais informações, consulte [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) e [Usar variáveis em pacotes](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
 A gramática de expressão do [!INCLUDE[ssIS](../../includes/ssis-md.md)] fornece um conjunto completo de operadores e funções para implementar as complexas expressões usadas para avaliação, inicialização ou atribuição. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
  
## <a name="see-also"></a>Consulte Também  
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)   
 [Expressões do SSIS &#40;Integration Services&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  
