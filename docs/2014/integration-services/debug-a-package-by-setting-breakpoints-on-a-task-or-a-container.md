---
title: Depurar um pacote definindo pontos de interrupção em uma tarefa ou contêiner | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], breakpoints
- breakpoints [Integration Services]
- tasks [Integration Services], breakpoints
ms.assetid: e7fa106a-2221-403a-bb74-efc9f12bb450
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 9ef85c2744475a2f55af2abc3514aa3167473ff7
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84951844"
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
  
4.  Na caixa de diálogo **definir \<container name> pontos de interrupção** , selecione os pontos de interrupção a serem habilitados.  
  
5.  Opcionalmente, modifique o tipo de contagem de ocorrências e o número de contagem de ocorrências para cada ponto de interrupção.  
  
6.  Para salvar o pacote, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte Também  
 [Ferramentas de solução de problemas para desenvolvimento de pacotes](troubleshooting/troubleshooting-tools-for-package-development.md)   
 [Depurar um script definindo pontos de interrupção em uma tarefa Script e um componente Script](data-flow/transformations/script-component.md)   
 [Codificando e Depurando a tarefa Script](control-flow/script-task.md)   
 [Codificando e depurando o componente Script](extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  
