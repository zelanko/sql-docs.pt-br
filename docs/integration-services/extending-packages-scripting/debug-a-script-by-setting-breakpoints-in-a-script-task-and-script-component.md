---
title: "Depurar um Script definindo pontos de interrupção em uma tarefa Script e componente Script | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- breakpoints [Integration Services]
- scripts [Integration Services], breakpoints
ms.assetid: 6c03464f-3f7d-4882-b7f8-8e396f8e2944
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 96815b337311c4ba8d16e10c25891c728e7a0c74
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="debug-a-script-by-setting-breakpoints-in-a-script-task-and-script-component"></a>Depurar um script definindo pontos de interrupção em uma tarefa Script e um componente Script
  Este procedimento descreve como definir pontos de interrupção nos scripts que são usados na tarefa Script e componente Script.  
  
 Depois que você definir pontos de interrupção no script, o **definir pontos de interrupção - \<nome do objeto >** caixa de diálogo lista os pontos de interrupção, junto com os pontos de interrupção internos.  
  
> [!IMPORTANT]  
>  Em determinadas circunstâncias, os pontos de interrupção na tarefa Script e no componente Script são ignorados. Para obter mais informações, consulte o **depurando a tarefa Script** seção [codificando e depurando a tarefa Script](../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md) e **depurando o componente Script** seção [codificando e depurando o componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="to-set-a-breakpoint-in-script"></a>Para definir um ponto de interrupção em script  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  Clique duas vezes no pacote que contém o script em que você quer definir pontos de interrupção.  
  
3.  Para abrir a tarefa Script, clique o **fluxo de controle** guia e, em seguida, duas vezes na tarefa de Script.  
  
4.  Para abrir o componente Script, clique o **de fluxo de dados** guia e, em seguida, clique duas vezes no componente Script.  
  
5.  Clique em **Script** e, em seguida, clique em **Editar Script**.  
  
6.  Em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA), localize a linha do script no qual você deseja definir um ponto de interrupção, clique nessa linha, aponte para **ponto de interrupção**e, em seguida, clique em **Inserir ponto de interrupção**.  
  
     O ícone de ponto de interrupção é exibido na linha de código.  
  
7.  No menu **Arquivo** , clique em **Sair**.  
  
8.  Clique em **OK**.  
  
9. Para salvar o pacote, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
  
