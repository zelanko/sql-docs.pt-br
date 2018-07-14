---
title: Definir as propriedades de uma restrição de precedência | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Precedence Constraint Editor dialog box
- precedence constraints [Integration Services], properties
ms.assetid: d990f600-5c09-4cd5-8528-0a58d79dc9f2
caps.latest.revision: 47
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 38e20290eb9499191307c7afb146e9242603c3ed
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37271342"
---
# <a name="set-the-properties-of-a-precedence-constraint"></a>Definir as propriedades de uma restrição de precedência
  Para definir propriedades em restrições de precedência, você pode usar uma destas ferramentas:  
  
-   Você pode usar a caixa de diálogo **Editor de Restrição de Precedência** .  
  
-   Você pode usar a janela Propriedades. A janela Propriedades lista as propriedades para configurar restrições de precedência que não estão disponíveis na caixa de diálogo **Editor de Restrição de Precedência** . Na janela Propriedades, você pode fornecer uma descrição e um nome da restrição de precedência e configurar a anotação para exibir a restrição de precedência na superfície de design.  
  
 Os procedimentos a seguir descrevem como definir propriedades em restrições de precedência usando cada dessas ferramentas.  
  
### <a name="to-set-the-properties-of-a-precedence-constraint-by-using-the-precedence-constraint-editor"></a>Para definir as propriedades de uma restrição de precedência utilizando o Editor de Restrição de Precedência  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** .  
  
4.  Clique duas vezes na restrição de precedência.  
  
     O **Editor de Restrição de Precedência** será aberto.  
  
5.  Na lista suspensa **Operação de avaliação** , selecione uma operação de avaliação.  
  
6.  No `Value` lista suspensa, selecione o resultado da execução do executável de precedência.  
  
7.  Se a operação de avaliação usar uma expressão, nos `Expression` caixa, digite uma expressão e clique em **teste** para avaliar a expressão.  
  
    > [!NOTE]  
    >  Nomes de variáveis diferenciam maiúsculas e minúsculas.  
  
8.  Se várias tarefas ou contêineres são conectados ao executável restrito, selecione **e lógica** para especificar que os resultados da execução de todos os executáveis precedentes devem avaliar a `true`. Selecione **OR lógico** para especificar que apenas um resultado de execução deve ser avaliadas como `true`.  
  
9. Clique em **OK** para fechar o **Editor de Restrição de Precedência**.  
  
10. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
### <a name="to-set-the-properties-of-a-precedence-constraint-by-using-the-properties-window"></a>Para definir as propriedades de uma restrição de precedência utilizando a janela Propriedades  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote a ser modificado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** . Na superfície de design da guia **Fluxo de Controle** , clique com o botão direito do mouse na restrição de precedência e clique em **Propriedades**. Na janela Propriedades, modifique os valores de propriedade.  
  
4.  Na janela **Propriedades** , defina as seguintes propriedades de leitura/gravação de restrições de precedência:  
  
    |Propriedade de leitura/gravação|Ação de configuração|  
    |--------------------------|--------------------------|  
    |Description|Forneça uma descrição.|  
    |EvalOp|Selecione uma operação de avaliação. Se o `Expression`, **ExpressionAndConstant**, ou **ExpressionOrConstant** operação for selecionada, você pode especificar uma expressão.|  
    |Expression|Se a operação de avaliação incluir uma expressão, forneça uma expressão. A expressão deve ser avaliada como um booliano. Para obter mais informações sobre a linguagem de expressão, consulte [Expressões do Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md).|  
    |LogicalAnd|Definir `LogicalAnd` para especificar se a restrição de precedência é avaliada juntamente com outras restrições de precedência, quando vários executáveis precederem e estiverem vinculados ao executável restrito|  
    |Nome|Atualize o nome da restrição de precedência.|  
    |ShowAnnotation|Especifique o tipo de anotação a ser usada. Selecione **Nunca** para desabilitar anotações, **AsNeeded** para habilitar a anotação sob demanda, **ConstraintName** para efetuar anotações automáticas usando o valor da propriedade Name, **ConstraintDescription** para efetuar anotações automaticamente usando o valor da propriedade Description e **ConstraintOptions** para efetuar anotações automáticas usando os valores das propriedades Value e Expression.|  
    |Valor|Se a operação de avaliação especificada na propriedade EvalOP incluir uma restrição, selecione o resultado de execução do executável de restrição.|  
  
5.  Feche a janela Propriedades.  
  
6.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte também  
 [Restrições de precedência](control-flow/precedence-constraints.md)   
 [Como conectar tarefas e contêineres por meio de uma restrição de precedência padrão](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)   
 [Defina o valor de uma restrição de precedência usando o Menu de atalho](../../2014/integration-services/set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)   
 [Usar uma expressão em uma restrição de precedência](../../2014/integration-services/use-an-expression-in-a-precedence-constraint.md)  
  
  
