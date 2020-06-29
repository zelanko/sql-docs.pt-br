---
title: Conectar tarefas e contêineres usando uma restrição de precedência padrão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- tasks [Integration Services], precedence constraints
- precedence constraints [Integration Services], connecting tasks
- default precedence constraints
- containers [Integration Services], precedence constraints
ms.assetid: 8f31f15f-98ff-4c35-b41f-8b8cfd148d75
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4d453b4a24da893515aafd29b0398685a7155d4e
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85434473"
---
# <a name="connect-tasks-and-containers-by-using-a-default-precedence-constraint"></a>Como conectar tarefas e contêineres por meio de uma restrição de precedência padrão
  Restrições de precedência conectam dois executáveis. Um executável pode ser qualquer tarefa ou um contêiner Loop For, Loop Foreach ou Sequência. Este procedimento descreve como definir o comportamento padrão de restrições de precedência e como conectar executáveis usando as restrições de precedência padrão.  
  
## <a name="creating-default-precedence-constraints"></a>Criando restrições de precedência padrão  
 Quando você usa o [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer pela primeira vez, o valor padrão de uma restrição de precedência é `Success`. Siga estas etapas para configurar o [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer para usar um valor padrão diferente para restrições de precedência.  
  
#### <a name="to-set-the-default-value-for-precedence-constraints"></a>Para definir o valor padrão de restrições de precedência  
  
1.  Abra [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  No menu **Ferramentas** , clique em **Opções**.  
  
3.  Na caixa de diálogo **Opções** , expanda **Designers do Business Intelligence** e então expanda **Designers do Integration Services**.  
  
4.  Clique em **Conexão Automática do Fluxo de Controle** e selecione **Conectar uma nova forma à forma selecionada por padrão**.  
  
5.  Na lista suspensa, escolha **Usar uma restrição de Falha para a nova forma** ou **Usar uma restrição de Conclusão para a nova forma**.  
  
6.  Clique em **OK**.  
  
#### <a name="to-create-a-default-precedence-constraint"></a>Para criar uma restrição de precedência padrão  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** .  
  
4.  Na superfície de design da guia **Fluxo de Controle** , clique na tarefa ou no contêiner e arraste seu conector para o executável em que você deseja aplicar a restrição de precedência.  
  
5.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte Também  
 [Restrições de precedência](control-flow/precedence-constraints.md)   
 [Definir o valor de uma restrição de precedência usando o menu de atalho](../../2014/integration-services/set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)   
 [Definir as propriedades de uma restrição de precedência](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)   
 [Usar uma expressão em uma restrição de precedência](../../2014/integration-services/use-an-expression-in-a-precedence-constraint.md)  
  
  
