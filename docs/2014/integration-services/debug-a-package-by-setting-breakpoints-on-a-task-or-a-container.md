---
title: Depurar um pacote definindo pontos de interrupção em uma tarefa ou contêiner | Microsoft Docs
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
- containers [Integration Services], breakpoints
- breakpoints [Integration Services]
- tasks [Integration Services], breakpoints
ms.assetid: e7fa106a-2221-403a-bb74-efc9f12bb450
caps.latest.revision: 33
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b063089105af1de7656387be8cc12639498e7c37
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37308106"
---
# <a name="debug-a-package-by-setting-breakpoints-on-a-task-or-a-container"></a>Depurar um pacote por meio da definição de pontos de interrupção em uma tarefa ou contêiner
  Este procedimento descreve como definir pontos de interrupção em um pacote, uma tarefa, um contêiner Loop For, um contêiner Loop Foreach ou um contêiner Sequência.  
  
### <a name="to-set-breakpoints-in-a-package-a-task-or-a-container"></a>Para definir pontos de interrupção em um pacote, uma tarefa ou um contêiner  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  Clique duas vezes no pacote em que você deseja definir pontos de interrupção.  
  
3.  No SSIS Designer, siga este procedimento:  
  
    -   Para definir pontos de interrupção no objeto de pacote, clique na guia **Fluxo de Controle** , coloque o cursor em qualquer lugar na tela de fundo da superfície de design e clique com o botão direito do mouse e clique em **Editar Pontos de Interrupção**.  
  
    -   Para definir pontos de interrupção em um fluxo de controle de pacote, clique na guia **Fluxo de Controle** , clique com o botão direito do mouse em uma tarefa, um contêiner Loop For, um contêiner Loop Foreach ou um contêiner Sequência, e clique em **Editar Pontos de Interrupção**.  
  
    -   Para definir pontos de interrupção em um manipulador de eventos, clique na guia **Manipulador de Eventos** , clique com o botão direito do mouse em uma tarefa, um contêiner Loop For, um contêiner Loop Foreach ou um contêiner Sequência e clique em **Editar Pontos de Interrupção**.  
  
4.  Na caixa de diálogo **Definir Pontos de Interrupção de \<container name>**, selecione os pontos de interrupção a serem habilitados.  
  
5.  Opcionalmente, modifique o tipo de contagem de ocorrências e o número de contagem de ocorrências para cada ponto de interrupção.  
  
6.  Para salvar o pacote, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte também  
 [Solucionando problemas de ferramentas para desenvolvimento de pacotes](troubleshooting/troubleshooting-tools-for-package-development.md)   
 [Depurar um Script definindo pontos de interrupção em uma tarefa Script e componente Script](data-flow/transformations/script-component.md)   
 [Codificando e depurando a tarefa Script](control-flow/script-task.md)   
 [Codificar e depurar o componente de Script](extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  
