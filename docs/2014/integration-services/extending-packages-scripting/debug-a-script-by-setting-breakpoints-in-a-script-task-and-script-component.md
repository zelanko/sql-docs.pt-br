---
title: Depurar um script configurando pontos de interrupção em uma tarefa Script e um componente de Script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- breakpoints [Integration Services]
- scripts [Integration Services], breakpoints
ms.assetid: 6c03464f-3f7d-4882-b7f8-8e396f8e2944
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f6327983f42efbf0b8d891495c9048d1ab963d0e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37306206"
---
# <a name="debug-a-script-by-setting-breakpoints-in-a-script-task-and-script-component"></a>Depurar um script definindo pontos de interrupção em uma tarefa Script e um componente Script
  Este procedimento descreve como definir pontos de interrupção nos scripts que são usados na tarefa Script e componente Script.  
  
 Depois que você definir pontos de interrupção no script, a caixa de diálogo **Definir Pontos de Interrupção – \<nome do objeto>** listará os pontos de interrupção, junto com os pontos de interrupção inseridos.  
  
> [!IMPORTANT]  
>  Em determinadas circunstâncias, os pontos de interrupção na tarefa Script e no componente Script são ignorados. Para obter mais informações, consulte o **depurando a tarefa Script** seção [codificando e depurando a tarefa Script](../control-flow/script-task.md) e o **depurando o componente Script** seção [codificação e depurando o componente Script] (... / extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md.  
  
### <a name="to-set-a-breakpoint-in-script"></a>Para definir um ponto de interrupção em script  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  Clique duas vezes no pacote que contém o script em que você quer definir pontos de interrupção.  
  
3.  Para abrir a tarefa Script, clique nela duas vezes após abrir a guia **Fluxo de Controle**.  
  
4.  Para abrir o componente Script, clique na guia **Fluxo de Dados** e então clique duas vezes no componente Script.  
  
5.  Clique em **Script** e então clique em **Editar Script**.  
  
6.  No VSTA ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications), localize a linha de script em que você quer definir um ponto de interrupção, clique com o botão direito do mouse na linha, aponte para **Ponto de Interrupção** e, em seguida, clique em **Inserir Ponto de Interrupção**.  
  
     O ícone de ponto de interrupção é exibido na linha de código.  
  
7.  No menu **Arquivo** , clique em **Sair**.  
  
8.  Clique em **OK**.  
  
9. Para salvar o pacote, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
  
