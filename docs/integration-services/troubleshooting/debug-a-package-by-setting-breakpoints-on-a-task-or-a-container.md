---
title: "Depurar um pacote por meio da defini&#231;&#227;o de pontos de interrup&#231;&#227;o em uma tarefa ou cont&#234;iner | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "contêineres [Integration Services], pontos de interrupção"
  - "pontos de interrupção [Integration Services]"
  - "tarefas [Integration Services], pontos de interrupção"
ms.assetid: e7fa106a-2221-403a-bb74-efc9f12bb450
caps.latest.revision: 35
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 35
---
# Depurar um pacote por meio da defini&#231;&#227;o de pontos de interrup&#231;&#227;o em uma tarefa ou cont&#234;iner
  Este procedimento descreve como definir pontos de interrupção em um pacote, uma tarefa, um contêiner Loop For, um contêiner Loop Foreach ou um contêiner Sequência.  
  
### Para definir pontos de interrupção em um pacote, uma tarefa ou um contêiner  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  Clique duas vezes no pacote em que você deseja definir pontos de interrupção.  
  
3.  No SSIS Designer, siga este procedimento:  
  
    -   Para definir pontos de interrupção no objeto de pacote, clique na guia **Fluxo de Controle**, coloque o cursor em qualquer lugar na tela de fundo da superfície de design e clique com o botão direito do mouse e clique em **Editar Pontos de Interrupção**.  
  
    -   Para definir pontos de interrupção em um fluxo de controle de pacote, clique na guia **Fluxo de Controle**, clique com o botão direito do mouse em uma tarefa, um contêiner Loop For, um contêiner Loop Foreach ou um contêiner Sequência, e clique em **Editar Pontos de Interrupção**.  
  
    -   Para definir pontos de interrupção em um manipulador de eventos, clique na guia **Manipulador de Eventos**, clique com o botão direito do mouse em uma tarefa, um contêiner Loop For, um contêiner Loop Foreach ou um contêiner Sequência e clique em **Editar Pontos de Interrupção**.  
  
4.  Na caixa de diálogo **Definir Pontos de Interrupção \<nome do contêiner>**, selecione os pontos de interrupção para serem habilitados.  
  
5.  Opcionalmente, modifique o tipo de contagem de ocorrências e o número de contagem de ocorrências para cada ponto de interrupção.  
  
6.  Para salvar o pacote, clique em **Salvar Itens Selecionados** no menu **Arquivo**.  
  
## Consulte também  
 [Solucionando problemas de ferramentas para desenvolvimento de pacotes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)   
 [Depurar um script definindo pontos de interrupção em uma tarefa Script e um componente Script](../../integration-services/extending-packages-scripting/debug-a-script-by-setting-breakpoints-in-a-script-task-and-script-component.md)   
 [Codificando e depurando a tarefa Script](../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)   
 [Codificando e depurando o componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  