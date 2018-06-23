---
title: Gerenciar arquivos com codificação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- files [SQL Server Management Studio]
- encoding [SQL Server Management Studio]
- files [SQL Server Management Studio], encoding
ms.assetid: 919544c9-59f0-4cc6-bb2a-f1ad671eb74b
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e7a252e4e766b85c83c97ee55a5204932932ee3d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116861"
---
# <a name="manage-files-with-encoding"></a>Gerenciar arquivos com codificação
  Para facilitar a exibição de seu código em uma determinada linguagem ou plataforma, você pode associar uma codificação de caracteres em particular a um arquivo.  
  
## <a name="opening-files"></a>Abrindo arquivos  
 Você pode escolher o editor que deseja usar para editar o arquivo.  
  
#### <a name="to-open-a-file-with-a-specific-editor"></a>Para abrir um arquivo com um editor específico  
  
1.  No menu **Arquivo** , aponte para **Abrir**e clique em **Arquivo**.  
  
2.  Na caixa de diálogo **Abrir arquivo** , selecione o nome do arquivo.  
  
3.  Clique na seta próxima ao botão **Abrir** e clique em**Abrir com** no menu exibido.  
  
4.  Na lista **Selecione um programa para abrir** , selecione um editor e clique em **Abrir**. Para abrir o arquivo com uma codificação em particular, selecione um editor com suporte a codificação, como o SQL Query Editor With Encoding ou o XML Editor With Encoding.  
  
## <a name="saving-files"></a>Salvando arquivos  
 Você também pode salvar seu código com uma codificação Unicode em uma página de código diferente para dar suporte a vários idiomas, como Europeu Ocidental ou Europeu Oriental. É possível associar uma codificação de caracteres em particular a um arquivo para facilitar a exibição do código naquela linguagem, além de um tipo de fim de linha que dê suporte a um determinado sistema operacional. Além disso, alguns caracteres, quando usados em nomes de arquivo, não podem ser salvos a menos que sejam salvos com codificação Unicode.  
  
#### <a name="to-save-a-file-with-a-different-encoding-or-line-ending-type"></a>Para salvar um arquivo com codificação ou tipo de fim de linha diferente  
  
1.  Sobre o **arquivo** menu, clique em **salvar \<filename > como**.  
  
2.  Na caixa de diálogo **Salvar Arquivo Como** , expanda o botão **Salvar** e clique em **Salvar com Codificação**.  
  
3.  Na caixa de diálogo **Opções Avançadas de Gravação** , selecione a codificação desejada na lista **Codificação** .  
  
4.  Na lista **Finais de Linha**, selecione o tipo de final de linha desejado.  
  
    > [!NOTE]  
    >  Se você salvar seu arquivo com codificação Unicode, o arquivo deverá ter feito check-in no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual SourceSafe como um arquivo binário porque o Visual SourceSafe não dá suporte à mesclagem, comparação e exibição de diferenças entre arquivos salvos como Unicode.  
  
 Se você estiver usando o Visual SourceSafe para armazenar arquivos com ANSI, UTF8 ou Unicode, observe as seguintes limitações para cada uma das opções:  
  
-   Arquivos ANSI só permitem caracteres suportados pela página de código atual, o que limita o uso internacional.  
  
-   Arquivos Unicode não podem usar check-out compartilhado, verificação de diferenças ou funcionalidade de mesclagem porque são tratados como arquivos binários. Você pode usar esse formato em arquivos internacionais.  
  
-   Arquivos UTF8 não funcionam bem com o Visual SourceSafe porque as alterações que criam problemas para editores UTF8 são feitas durante o check-in, o check-out, a verificação de diferenças e a mesclagem.  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos que gerenciam soluções e projetos](files-that-manage-solutions-and-projects.md)   
 [Associar extensões de arquivo a um Editor de Códigos](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md)  
  
  