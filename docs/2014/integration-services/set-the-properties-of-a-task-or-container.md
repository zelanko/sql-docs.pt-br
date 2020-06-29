---
title: Definir as propriedades de uma tarefa ou contêiner | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- tasks [Integration Services], properties
ms.assetid: 52d47ca4-fb8c-493d-8b2b-48bb269f859b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 278ce3d1a7f1fafeb3c378559e5ec88da62895c8
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85421463"
---
# <a name="set-the-properties-of-a-task-or-container"></a>Definir as propriedades de uma tarefa ou de um contêiner
  Você pode definir a maioria das propriedades de tarefas e contêineres usando a janela **Propriedades** . As exceções são as propriedades de coleções de tarefas e as propriedades que são muito complexas para se definir usando a janela **Propriedades** . Por exemplo, você não pode configurar o enumerador que o contêiner Loop Foreach usa na janela **Propriedades** . Você deve usar um editor de tarefa ou de contêiner para definir essas propriedades complexas. A maioria dos editores de tarefas e contêineres possui vários nós, e cada nó contém propriedades relacionadas. O nome do nó indica o assunto das propriedades contidas no nó.  
  
 Os procedimentos a seguir descrevem como definir as propriedades de uma tarefa ou de um contêiner usando as janelas **Propriedades** ou o editor de tarefas ou de contêineres correspondente.  
  
### <a name="to-set-the-properties-of-a-task-or-container-by-using-the-properties-window"></a>Para definir as propriedades de uma tarefa ou de um contêiner usando a janela Propriedades  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** .  
  
4.  Na superfície de design da guia **Fluxo de Controle** , clique com o botão direito do mouse na tarefa ou no contêiner e clique em **Propriedades**.  
  
5.  Na janela **Propriedades** , atualize o valor da propriedade.  
  
    > [!NOTE]  
    >  A maioria das propriedades pode ser definida digitando um valor diretamente na caixa de texto ou selecionando um valor de uma lista. Porém, algumas propriedades são mais complexas e têm um editor de propriedade personalizado. Para definir a propriedade, clique na caixa de texto e clique no botão de criação **(…)** para abrir o editor personalizado.  
  
6.  Como alternativa, crie expressões de propriedade para atualizar as propriedades da tarefa ou do contêiner dinamicamente. Para obter mais informações, consulte [Adicionar ou alterar uma expressão de propriedade](expressions/add-or-change-a-property-expression.md).  
  
7.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
### <a name="to-set-the-properties-of-a-task-or-container-by-using-a-task-or-container-editor"></a>Para definir as propriedades de uma tarefa ou de um contêiner usando um editor de tarefas ou de contêineres  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** .  
  
4.  Na superfície de design da guia **Fluxo de Controle** , clique com o botão direito do mouse na tarefa ou no contêiner e clique em **Editar** para abrir o editor correspondente.  
  
     Para obter informações sobre como configurar um contêiner Loop For, consulte [Para configurar um contêiner Loop For](control-flow/for-loop-container.md).  
  
     Para obter informações sobre como configurar o contêiner Loop Foreach, consulte [configurar um contêiner Loop Foreach](control-flow/foreach-loop-container.md).  
  
    > [!NOTE]  
    >  O contêiner Sequência não tem um editor personalizado.  
  
5.  Se o editor de tarefas ou de contêineres tiver vários nós, clique no nó que contém a propriedade a ser definida.  
  
6.  Você também pode clicar em **Expressões** e, na página **Expressões** , criar expressões de propriedade para atualizar as propriedades da tarefa ou do contêiner dinamicamente. Para obter mais informações, consulte [Adicionar ou alterar uma expressão de propriedade](expressions/add-or-change-a-property-expression.md).  
  
7.  Atualize o valor de propriedade.  
  
8.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas de Integration Services](control-flow/integration-services-tasks.md)   
 [Contêineres do Integration Services](control-flow/integration-services-containers.md)  
  
  
