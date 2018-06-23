---
title: Definir as propriedades de uma variável definida pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- modifying variables
- variables [Integration Services], properties
ms.assetid: f98ddbec-f668-4dba-a768-44ac3ae0536f
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 1d05e9fc6b6c4f1e5e29a4bff9c163305d977202
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119147"
---
# <a name="set-the-properties-of-a-user-defined-variable"></a>Definir as propriedades de uma variável definida pelo usuário
  Para definir as propriedades de uma variável definida pelo usuário no [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], você pode usar um dos seguintes recursos:  
  
-   Janela Variáveis.  
  
-   Janela Propriedades. A janela **Propriedades** lista propriedades para configurar variáveis não disponíveis na janela **Variáveis** : Description, EvaluateAsExpression, Expression, ReadOnly, ValueType e IncludeInDebugDump.  
  
> [!NOTE]  
>  O [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] também fornece um conjunto de variáveis do sistema cujas propriedades não podem ser atualizadas, com a exceção da propriedade RaiseChangedEvent.  
  
 **Definindo as expressões em variáveis**  
  
 Quando você usa a janela **Propriedades** para definir as expressões em uma variável definida pelo usuário:  
  
-   O valor de uma variável pode ser definido pela propriedade Value ou Expression. Por padrão, a propriedade EvaluateAsExpression é definida como `False` e o valor da variável é definido pela propriedade de valor. Para usar uma expressão para definir o valor, você deve primeiro definir EvaluateAsExpression `True`e, em seguida, forneça uma expressão na propriedade de expressão. A propriedade Value é definida automaticamente como o resultado de avaliação da expressão.  
  
-   A propriedade ValueType contém o tipo de dados do valor na propriedade Value. Quando Value é definido por uma expressão, ValueType é atualizado automaticamente para um tipo de dados compatível com o resultado da avaliação da expressão. Por exemplo, se o valor contiver 0 e a propriedade ValueType contém **Int32** e você definir expressão para getDate (), valor contém a data e hora atuais e ValueType é definido como `DateTime`.  
  
-   A janela **Propriedades** para a variável fornece acesso à caixa de diálogo **Construtor de Expressões** . É possível usar essa ferramenta para criar, validar e avaliar expressões. Para obter mais informações, consulte [Construtor de Expressões](expressions/expression-builder.md) e [Expressões do Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md).  
  
 Quando você usa a janela **Variáveis** para definir as expressões em uma variável definida pelo usuário:  
  
-   Para usar uma expressão para definir o valor da variável, primeiro confirmar que o tipo de dados da variável é compatível com o resultado da avaliação da expressão e, em seguida, forneça uma expressão no `Expression` coluna o **variáveis** janela. A propriedade EvaluateAsExpression no **propriedades** janela é definida automaticamente como `True`.  
  
-   Quando você atribui uma expressão a uma variável, um marcador de ícone especial é exibido ao lado da variável. Esse marcador de ícone especial também é exibido ao lado de gerenciadores de conexões e tarefas que têm expressões definidas neles.  
  
-   A janela **Variáveis** para a variável fornece acesso à caixa de diálogo **Construtor de Expressões** . É possível usar essa ferramenta para criar, validar e avaliar expressões. Para obter mais informações, consulte [Construtor de Expressões](expressions/expression-builder.md) e [Expressões do Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md).  
  
 Em ambos os **variáveis** e **propriedades** janela, se você atribuir uma expressão à variável, e `EvaluateAsExpression` é definido como `True`, não é possível alterar o tipo de dados da variável.  
  
 **Definindo as propriedades de nome e Namespace**  
  
 Os valores de `Name` e `Namespace` propriedades devem começar com uma letra de caractere alfabético, conforme definido pelo Unicode Standard 2.0 ou um sublinhado (_). Os caracteres subsequentes podem ser letras ou números conforme definido no padrão Unicode Standard 2.0 ou o sublinhado (\_).  
  
## <a name="using-the-variables-window-to-set-properties"></a>Usando a janela Variáveis para definir propriedades  
  
#### <a name="to-set-the-properties-of-a-variable-by-using-the-variables-window"></a>Para definir as propriedades de uma variável usando a janela Variáveis  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse no pacote para abri-lo.  
  
3.  No menu **SSIS** , clique em **Variáveis**.  
  
     Além disso, você pode exibir a janela **Variáveis** mapeando o comando View.Variables para uma combinação de teclas de sua escolha na página **Teclado** da caixa de diálogo **Opções** .  
  
4.  Opcionalmente, na janela **Variáveis** , clique em **Opções de Grade**e selecione as colunas para serem exibidas na janela **Variáveis** e selecione os filtros para serem aplicados na lista de variáveis.  
  
5.  Selecione a variável na lista e, em seguida, atualizar valores de `Name`, **tipo de dados**, `Value`, `Namespace`, **elevar evento de alteração**, **descrição,** e `Expression` colunas.  
  
6.  Selecione a variável na lista e, em seguida, clique **Mover Variável** para alterar o escopo.  
  
7.  Para salvar o pacote atualizado, no menu **Arquivo** , clique em **Salvar Itens Selecionados**.  
  
## <a name="using-the-properties-window-to-set-properties"></a>Usando a janela Propriedades para definir propriedades  
  
#### <a name="to-set-the-properties-of-a-variable-by-using-the-properties-window"></a>Para definir as propriedades de uma variável usando a janela Propriedades  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse no pacote para abri-lo.  
  
3.  No menu **Exibir** , clique em **Janela Propriedades**.  
  
4.  No Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] , clique na guia **Explorador de Pacotes** e expanda o nó do Pacote.  
  
5.  Para modificar variáveis com escopo no pacote, expanda o nó Variáveis; caso contrário, expanda os Manipuladores de Evento ou os nós Executáveis até que localize o nó Variáveis que contém a variável que deseja modificar.  
  
6.  Clique na variável cujas propriedades você deseja modificar.  
  
7.  Na janela **Propriedades** , atualize as propriedades da variável de leitura/escrita. Algumas propriedades são de leitura/somente leitura para variáveis definidas pelo usuário.  
  
     Para obter mais informações sobre as propriedades, consulte [Integration Services &#40;SSIS&#41; Variables](integration-services-ssis-variables.md).  
  
8.  Para salvar o pacote atualizado, no menu **Arquivo** , clique em **Salvar Itens Selecionados**.  
  
## <a name="see-also"></a>Consulte também  
 [Serviços de integração &#40;SSIS&#41; variáveis](integration-services-ssis-variables.md)   
 [Usar variáveis em pacotes](../../2014/integration-services/use-variables-in-packages.md)   
 [Adicionar, excluir, alterar o escopo de uma variável definida pelo usuário em um pacote](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
  