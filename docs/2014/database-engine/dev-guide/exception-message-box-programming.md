---
title: Mensagem de exceção caixa programação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ExceptionMessageBox class, about ExceptionMessageBox class
- exception message box [SQL Server], about exception message box
- exception message box [SQL Server]
- interfaces [SQL Server]
- exceptions [SQL Server]
- messages [SQL Server], exception message box
ms.assetid: 0b1ba514-6959-4e69-bfd2-3cf3c1ac4b9c
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0adef635d88a05925da924c4bab396f1da58e530
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013397"
---
# <a name="exception-message-box-programming"></a>Programação da caixa de mensagem de exceção
  A caixa de mensagem de exceção é uma interface programática que é instalada com e usada por [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componentes gráficos. A caixa de mensagem de exceção é um assembly gerenciado com suporte que você pode usar em aplicativos para proporcionar um controle significativamente maior sobre a experiência de troca de mensagens e oferecer aos usuários as opções de salvar o conteúdo da mensagem de erro para referência futura e obter ajuda sobre mensagens. Como a caixa de mensagem de exceção é instalada por todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exceto [!INCLUDE[ssEW](../../includes/ssew-md.md)], você pode usá-lo sem nenhuma configuração adicional em qualquer computador no qual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cliente componentes foram instalados.  
  
 A classe <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> no namespace <xref:Microsoft.SqlServer.MessageBox> tem todas as funcionalidades da classe <xref:System.Windows.Forms.MessageBox> e muito mais. Ideal para qualquer tarefa na qual <xref:System.Windows.Forms.MessageBox> possa ser usado, a <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> foi projetada para tratar exceções de código gerenciado de forma esmerada. A caixa de mensagem de exceção permite que você faça o seguinte:  
  
-   Forneça texto de botão personalizado para até cinco botões. Os botões e a caixa de diálogo são redimensionados automaticamente para diferentes comprimentos de texto.  
  
-   Permita que os usuários copiem o título da mensagem, o texto, o texto do botão e os links de ajuda (se houver) com facilidade para a Área de Transferência ou envie essas informações em uma mensagem de email.  
  
-   Exibir todos os erros e exceções de subjacente em uma árvore de relação hierárquica quando os usuários clicarem **informações adicionais**.  
  
-   Permita que os usuários decidam se a mensagem deverá ser exibida quando a mesma exceção ocorrer novamente.  
  
-   Acesse um sistema de ajuda online usando um link de ajuda associado à exceção.  
  
 Para obter mais informações, consulte [caixa de mensagem de exceção de programa](../../../2014/database-engine/dev-guide/program-exception-message-box.md).  
  
  