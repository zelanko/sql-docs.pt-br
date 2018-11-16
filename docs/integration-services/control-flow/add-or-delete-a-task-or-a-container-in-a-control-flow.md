---
title: Adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], adding
- adding tasks
- adding containers
- tasks [Integration Services], adding
ms.assetid: 653084c6-87a3-45d5-b458-914ecf24d56a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7524bd375dcf2c2d34395a0e87c1b3fe7d08ba63
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2018
ms.locfileid: "51640053"
---
# <a name="add-or-delete-a-task-or-a-container-in-a-control-flow"></a>Adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle
  Quando você está trabalhando no designer de fluxo de controle, a Caixa de Ferramentas do [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer lista as tarefas que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece para criar o fluxo de controle em um pacote. Para obter mais informações a Barra de Ferramentas, consulte [Caixa de Ferramentas do SSIS](../../integration-services/ssis-toolbox.md).  
  
 Um pacote pode incluir várias instâncias da mesma tarefa. Cada instância de uma tarefa é identificada exclusivamente no pacote e você pode configurar cada instância de forma diferente.  
  
 Se você excluir a tarefa, as restrições de precedência que conectam a tarefa às outras tarefas e contêineres no fluxo de controle também serão excluídas.  
  
 Os procedimentos a seguir descrevem como adicionar ou excluir uma tarefa ou um contêiner no fluxo de controle de um pacote.  
  
## <a name="add-a-task-or-a-container-to-a-control-flow"></a>Adicionar uma tarefa ou um contêiner a um fluxo de controle  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** .  
  
4.  Para abrir a **Caixa de Ferramentas**, clique em **Caixa de Ferramentas** no menu **Exibir** .  
  
5.  Expanda **Itens do Fluxo de Controle** e **Tarefas de Manutenção**.  
  
6.  Arraste as tarefas e os contêineres da **Caixa de Ferramentas** para a superfície de design da guia **Fluxo de Controle** .  
  
7.  Conecte uma tarefa ou um contêiner dentro do pacote do fluxo de controle arrastando seu conector até outro componente no fluxo de controle.  
  
8.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="delete-a-task-or-a-container-from-a-control-flow"></a>Excluir uma tarefa ou um contêiner de um fluxo de controle  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo. Siga um destes procedimentos:  
  
    -   Clique na guia **Fluxo de Controle** , clique com o botão direito do mouse na tarefa ou no contêiner a ser removido e clique em **Excluir**.  
  
    -   Abra o **Explorador de Pacotes**. Na pasta **Executáveis** , clique com o botão direito do mouse na tarefa ou no contêiner a ser removido e clique em **Excluir**.  
  
3.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  

## <a name="set-the-properties-of-a-task-or-container"></a>Definir as propriedades de uma tarefa ou contêiner
Você pode definir a maioria das propriedades de tarefas e contêineres usando a janela **Propriedades** . As exceções são as propriedades de coleções de tarefas e as propriedades que são muito complexas para se definir usando a janela **Propriedades** . Por exemplo, você não pode configurar o enumerador que o contêiner Loop Foreach usa na janela **Propriedades** . Você deve usar um editor de tarefa ou de contêiner para definir essas propriedades complexas. A maioria dos editores de tarefas e contêineres possui vários nós, e cada nó contém propriedades relacionadas. O nome do nó indica o assunto das propriedades contidas no nó.  
  
 Os procedimentos a seguir descrevem como definir as propriedades de uma tarefa ou de um contêiner usando as janelas **Propriedades** ou o editor de tarefas ou de contêineres correspondente.  
  
### <a name="set-the-properties-of-a-task-or-container-with-the-properties-window"></a>Definir as propriedades de uma tarefa ou contêiner usando a janela Propriedades  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** .  
  
4.  Na superfície de design da guia **Fluxo de Controle** , clique com o botão direito do mouse na tarefa ou no contêiner e clique em **Propriedades**.  
  
5.  Na janela **Propriedades** , atualize o valor da propriedade.  
  
    > [!NOTE]  
    >  A maioria das propriedades pode ser definida digitando um valor diretamente na caixa de texto ou selecionando um valor de uma lista. Porém, algumas propriedades são mais complexas e têm um editor de propriedade personalizado. Para definir a propriedade, clique na caixa de texto e clique no botão de criação **(...)** para abrir o editor personalizado.  
  
6.  Como alternativa, crie expressões de propriedade para atualizar as propriedades da tarefa ou do contêiner dinamicamente. Para obter mais informações, consulte [Adicionar ou alterar uma expressão de propriedade](../../integration-services/expressions/add-or-change-a-property-expression.md).  
  
7.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
### <a name="set-the-properties-of-a-task-or-container-with-the-task-or-container-editor"></a>Definir as propriedades de uma tarefa ou de um contêiner com o editor de tarefas ou de contêineres  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** .  
  
4.  Na superfície de design da guia **Fluxo de Controle** , clique com o botão direito do mouse na tarefa ou no contêiner e clique em **Editar** para abrir o editor correspondente.  
  
     Para obter informações sobre como configurar um contêiner Loop For, consulte [Para configurar um contêiner Loop For](https://msdn.microsoft.com/library/b9cd7ea7-b198-4a35-8b16-6acf09611ca5).  
  
     Para obter informações sobre como configurar um contêiner Loop Foreach, consulte [Para configurar um contêiner Loop Foreach](https://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25).  
  
    > [!NOTE]  
    >  O contêiner Sequência não tem um editor personalizado.  
  
5.  Se o editor de tarefas ou de contêineres tiver vários nós, clique no nó que contém a propriedade a ser definida.  
  
6.  Você também pode clicar em **Expressões** e, na página **Expressões** , criar expressões de propriedade para atualizar as propriedades da tarefa ou do contêiner dinamicamente. Para obter mais informações, consulte [Adicionar ou alterar uma expressão de propriedade](../../integration-services/expressions/add-or-change-a-property-expression.md).  
  
7.  Atualize o valor de propriedade.  
  
8.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Contêineres do Integration Services](../../integration-services/control-flow/integration-services-containers.md)   
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)  
  
  
