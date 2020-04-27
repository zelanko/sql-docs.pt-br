---
title: Programação da caixa de mensagem de exceção | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- ExceptionMessageBox class, about ExceptionMessageBox class
- exception message box [SQL Server], about exception message box
- exception message box [SQL Server]
- interfaces [SQL Server]
- exceptions [SQL Server]
- messages [SQL Server], exception message box
ms.assetid: 0b1ba514-6959-4e69-bfd2-3cf3c1ac4b9c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 205638b82e8d0d71a3d674bd970e4bf8d2e3ea5f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62753368"
---
# <a name="exception-message-box-programming"></a>Programação da caixa de mensagem de exceção
  A caixa de mensagem de exceção é uma interface programática que é instalada com o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e usada por componentes gráficos. A caixa de mensagem de exceção é um assembly gerenciado com suporte que você pode usar em aplicativos para proporcionar um controle significativamente maior sobre a experiência de troca de mensagens e oferecer aos usuários as opções de salvar o conteúdo da mensagem de erro para referência futura e obter ajuda sobre mensagens. Como a caixa de mensagem de exceção é instalada por todas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] as [!INCLUDE[ssEW](../../includes/ssew-md.md)]edições do, exceto, você pode usá-la sem nenhuma configuração adicional [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em qualquer computador em que os componentes cliente tenham sido instalados.  
  
 A classe <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> no namespace <xref:Microsoft.SqlServer.MessageBox> tem todas as funcionalidades da classe <xref:System.Windows.Forms.MessageBox> e muito mais. Ideal para qualquer tarefa na qual <xref:System.Windows.Forms.MessageBox> possa ser usado, a <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> foi projetada para tratar exceções de código gerenciado de forma esmerada. A caixa de mensagem de exceção permite que você faça o seguinte:  
  
-   Forneça texto de botão personalizado para até cinco botões. Os botões e a caixa de diálogo são redimensionados automaticamente para diferentes comprimentos de texto.  
  
-   Permita que os usuários copiem o título da mensagem, o texto, o texto do botão e os links de ajuda (se houver) com facilidade para a Área de Transferência ou envie essas informações em uma mensagem de email.  
  
-   Exibe todas as exceções e erros subjacentes em uma árvore de relações hierárquica quando os usuários clicam em **informações adicionais**.  
  
-   Permita que os usuários decidam se a mensagem deverá ser exibida quando a mesma exceção ocorrer novamente.  
  
-   Acesse um sistema de ajuda online usando um link de ajuda associado à exceção.  
  
 Para obter mais informações, consulte [caixa de mensagem de exceção do programa](../../../2014/database-engine/dev-guide/program-exception-message-box.md).  
  
  
