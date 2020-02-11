---
title: Definir as propriedades de uma restrição de precedência | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Precedence Constraint Editor dialog box
- precedence constraints [Integration Services], properties
ms.assetid: d990f600-5c09-4cd5-8528-0a58d79dc9f2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bc83e1b636aa03e37717ac62de1a44e9c6f1cfd2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66055738"
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
  
6.  Na lista `Value` suspensa, selecione o resultado da execução do executável de precedência.  
  
7.  Se a operação de avaliação usar uma expressão, na `Expression` caixa, digite uma expressão e clique em **testar** para avaliar a expressão.  
  
    > [!NOTE]  
    >  Nomes de variáveis diferenciam maiúsculas e minúsculas.  
  
8.  Se várias tarefas ou contêineres estiverem conectados ao executável restrito, selecione **lógico e** para especificar que os resultados da execução de todos os executáveis anteriores devem ser avaliados como `true`. Selecione **lógico ou** para especificar que apenas um resultado de execução deve ser `true`avaliado como.  
  
9. Clique em **OK** para fechar o **Editor de Restrição de Precedência**.  
  
10. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
### <a name="to-set-the-properties-of-a-precedence-constraint-by-using-the-properties-window"></a>Para definir as propriedades de uma restrição de precedência utilizando a janela Propriedades  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote a ser modificado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **fluxo de controle** . Na superfície de design da guia **fluxo de controle** , clique com o botão direito do mouse na restrição de precedência e clique em **Propriedades**. Na janela Propriedades, modifique os valores de propriedade.  
  
4.  Na janela **Propriedades** , defina as seguintes propriedades de leitura/gravação de restrições de precedência:  
  
    |Propriedade de leitura/gravação|Ação de configuração|  
    |--------------------------|--------------------------|  
    |DESCRIÇÃO|Forneça uma descrição.|  
    |EvalOp|Selecione uma operação de avaliação. Se a `Expression`operação, **ExpressionAndConstant**ou **ExpressionOrConstant** for selecionada, você poderá especificar uma expressão.|  
    |Expression|Se a operação de avaliação incluir uma expressão, forneça uma expressão. A expressão deve ser avaliada como um booliano. Para obter mais informações sobre a linguagem de expressão, consulte [Expressões do Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md).|  
    |LogicalAnd|Defina `LogicalAnd` para especificar se a restrição de precedência é avaliada em conjunto com outras restrições de precedência, quando vários executáveis precedem e estão vinculados ao executável restrito|  
    |Nome|Atualize o nome da restrição de precedência.|  
    |ShowAnnotation|Especifique o tipo de anotação a ser usada. Selecione **Nunca** para desabilitar anotações, **AsNeeded** para habilitar a anotação sob demanda, **ConstraintName** para efetuar anotações automáticas usando o valor da propriedade Name, **ConstraintDescription** para efetuar anotações automaticamente usando o valor da propriedade Description e **ConstraintOptions** para efetuar anotações automáticas usando os valores das propriedades Value e Expression.|  
    |Valor|Se a operação de avaliação especificada na propriedade EvalOP incluir uma restrição, selecione o resultado de execução do executável de restrição.|  
  
5.  Feche a janela Propriedades.  
  
6.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte Também  
 [Restrições de precedência](control-flow/precedence-constraints.md)   
 [Como conectar tarefas e contêineres por meio de uma restrição de precedência padrão](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)   
 [Definir o valor de uma restrição de precedência usando o menu de atalho](../../2014/integration-services/set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)   
 [Usar uma expressão em uma restrição de precedência](../../2014/integration-services/use-an-expression-in-a-precedence-constraint.md)  
  
  
