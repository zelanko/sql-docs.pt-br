---
title: Mensagem de exceção programação da caixa | Microsoft Docs
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
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62753368"
---
# <a name="exception-message-box-programming"></a>Programação da caixa de mensagem de exceção
  A caixa de mensagem de exceção é uma interface programática que é instalada com o e usada por [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componentes gráficos. A caixa de mensagem de exceção é um assembly gerenciado com suporte que você pode usar em aplicativos para proporcionar um controle significativamente maior sobre a experiência de troca de mensagens e oferecer aos usuários as opções de salvar o conteúdo da mensagem de erro para referência futura e obter ajuda sobre mensagens. Como a caixa de mensagem de exceção é instalada por todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exceto [!INCLUDE[ssEW](../../includes/ssew-md.md)], você pode usá-lo sem nenhuma configuração adicional em qualquer computador no qual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cliente componentes foram instalados.  
  
 A classe <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> no namespace <xref:Microsoft.SqlServer.MessageBox> tem todas as funcionalidades da classe <xref:System.Windows.Forms.MessageBox> e muito mais. Ideal para qualquer tarefa na qual <xref:System.Windows.Forms.MessageBox> possa ser usado, a <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> foi projetada para tratar exceções de código gerenciado de forma esmerada. A caixa de mensagem de exceção permite que você faça o seguinte:  
  
-   Forneça texto de botão personalizado para até cinco botões. Os botões e a caixa de diálogo são redimensionados automaticamente para diferentes comprimentos de texto.  
  
-   Permita que os usuários copiem o título da mensagem, o texto, o texto do botão e os links de ajuda (se houver) com facilidade para a Área de Transferência ou envie essas informações em uma mensagem de email.  
  
-   Exibir todos os erros e exceções de subjacentes em uma árvore de relações hierárquicas quando os usuários clicam **informações adicionais**.  
  
-   Permita que os usuários decidam se a mensagem deverá ser exibida quando a mesma exceção ocorrer novamente.  
  
-   Acesse um sistema de ajuda online usando um link de ajuda associado à exceção.  
  
 Para obter mais informações, consulte [caixa de mensagem de exceção de programa](../../../2014/database-engine/dev-guide/program-exception-message-box.md).  
  
  
