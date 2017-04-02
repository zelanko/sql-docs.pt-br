---
title: "Adicionar ou excluir uma tarefa ou um cont&#234;iner em um fluxo de controle | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "contêineres [Integration Services], adicionando"
  - "adicionando tarefas"
  - "adicionando contêineres"
  - "tarefas [Integration Services], adicionando"
ms.assetid: 653084c6-87a3-45d5-b458-914ecf24d56a
caps.latest.revision: 46
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 45
---
# Adicionar ou excluir uma tarefa ou um cont&#234;iner em um fluxo de controle
  Quando você está trabalhando no designer de fluxo de controle, a Caixa de Ferramentas do [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer lista as tarefas que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece para criar o fluxo de controle em um pacote. Para obter mais informações a Barra de Ferramentas, consulte [Caixa de Ferramentas do SSIS](../../integration-services/ssis-toolbox.md).  
  
 Um pacote pode incluir várias instâncias da mesma tarefa. Cada instância de uma tarefa é identificada exclusivamente no pacote e você pode configurar cada instância de forma diferente.  
  
 Se você excluir a tarefa, as restrições de precedência que conectam a tarefa às outras tarefas e contêineres no fluxo de controle também serão excluídas.  
  
 Os procedimentos a seguir descrevem como adicionar ou excluir uma tarefa ou um contêiner no fluxo de controle de um pacote.  
  
### Para adicionar uma tarefa ou um contêiner a um fluxo de controle  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** .  
  
4.  Para abrir a **Caixa de Ferramentas**, clique em **Caixa de Ferramentas** no menu **Exibir**.  
  
5.  Expanda **Itens do Fluxo de Controle** e **Tarefas de Manutenção**.  
  
6.  Arraste as tarefas e os contêineres da **Caixa de Ferramentas** para a superfície de design da guia **Fluxo de Controle**.  
  
7.  Conecte uma tarefa ou um contêiner dentro do pacote do fluxo de controle arrastando seu conector até outro componente no fluxo de controle.  
  
8.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
### Para excluir uma tarefa ou um contêiner de um fluxo de controle  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo. Siga um destes procedimentos:  
  
    -   Clique na guia **Fluxo de Controle**, clique com o botão direito do mouse na tarefa ou no contêiner a ser removido e clique em **Excluir**.  
  
    -   Abra o **Explorador de Pacotes**. Na pasta **Executáveis**, clique com o botão direito do mouse na tarefa ou no contêiner a ser removido e clique em **Excluir**.  
  
3.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## Consulte também  
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Contêineres do Integration Services](../../integration-services/control-flow/integration-services-containers.md)   
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)  
  
  