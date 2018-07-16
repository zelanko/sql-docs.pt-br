---
title: Adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle | Microsoft Docs
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
- containers [Integration Services], adding
- adding tasks
- adding containers
- tasks [Integration Services], adding
ms.assetid: 653084c6-87a3-45d5-b458-914ecf24d56a
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1546a8bf4d0da741d63cb8bd8d4b2f849cf921d2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37256932"
---
# <a name="add-or-delete-a-task-or-a-container-in-a-control-flow"></a>Adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle
  Quando você está trabalhando no designer de fluxo de controle, a Caixa de Ferramentas do [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer lista as tarefas que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece para criar o fluxo de controle em um pacote. Para obter mais informações a Barra de Ferramentas, consulte [Caixa de Ferramentas do SSIS](../ssis-toolbox.md).  
  
 Um pacote pode incluir várias instâncias da mesma tarefa. Cada instância de uma tarefa é identificada exclusivamente no pacote e você pode configurar cada instância de forma diferente.  
  
 Se você excluir a tarefa, as restrições de precedência que conectam a tarefa às outras tarefas e contêineres no fluxo de controle também serão excluídas.  
  
 Os procedimentos a seguir descrevem como adicionar ou excluir uma tarefa ou um contêiner no fluxo de controle de um pacote.  
  
### <a name="to-add-a-task-or-a-container-to-a-control-flow"></a>Para adicionar uma tarefa ou um contêiner a um fluxo de controle  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** .  
  
4.  Para abrir a **Caixa de Ferramentas**, clique em **Caixa de Ferramentas** no menu **Exibir** .  
  
5.  Expanda **Itens do Fluxo de Controle** e **Tarefas de Manutenção**.  
  
6.  Arraste as tarefas e os contêineres da **Caixa de Ferramentas** para a superfície de design da guia **Fluxo de Controle** .  
  
7.  Conecte uma tarefa ou um contêiner dentro do pacote do fluxo de controle arrastando seu conector até outro componente no fluxo de controle.  
  
8.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
### <a name="to-delete-a-task-or-a-container-from-a-control-flow"></a>Para excluir uma tarefa ou um contêiner de um fluxo de controle  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo. Siga um destes procedimentos:  
  
    -   Clique na guia **Fluxo de Controle** , clique com o botão direito do mouse na tarefa ou no contêiner a ser removido e clique em **Excluir**.  
  
    -   Abra o **Explorador de Pacotes**. Na pasta **Executáveis** , clique com o botão direito do mouse na tarefa ou no contêiner a ser removido e clique em **Excluir**.  
  
3.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas do Integration Services](integration-services-tasks.md)   
 [Contêineres do Integration Services](integration-services-containers.md)   
 [Fluxo de Controle](control-flow.md)  
  
  
