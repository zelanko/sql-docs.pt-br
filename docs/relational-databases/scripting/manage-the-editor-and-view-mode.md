---
title: "Gerenciar o Editor e o modo de exibição | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Query Editor [SQL Server Management Studio], managing window behavior
- workbench view modes [SQL Server Management Studio]
- full screen mode [SQL Server Management Studio]
- fonts [SQL Server Management Studio]
- word wraps [SQL Server Management Studio]
- virtual space mode [SQL Server Management Studio]
- splitting document views
- displaying line numbers
- view modes [SQL Server Management Studio]
ms.assetid: 25c58a14-9f94-4296-9770-7d84c6bc3969
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 364c8e7db9d336df91b984d62aaf62cff19da4ac
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="manage-the-editor-and-view-mode"></a>Gerenciar o editor e o modo de exibição
  O Editor fornece várias maneiras para controlar a exibição do código.  
  
## <a name="changing-the-view-mode"></a>Alterando o modo de exibição  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] possui um modo de exibição denominado **Documentos com Guias**, que permite abrir vários editores e documentos simultaneamente e acessá-los por guias no topo do editor. Como alternativa, você pode abrir o ambiente do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] no modo interface de documentos múltiplos (MDI), que une as janelas sem guias e permite organizar as janelas lado a lado, minimizá-las etc.  
  
#### <a name="to-switch-between-view-modes"></a>Para alternar entre modos de exibição  
  
1.  Clique em **Opções** no menu **Ferramentas** .  
  
2.  Clique em **Ambiente**. Clique em **Geral**.  
  
3.  Clique em **Documentos com Guias** ou **Ambiente MDI**.  
  
    > [!NOTE]  
    >  As mudanças não entrarão em vigor até que o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] seja reinicializado.  
  
## <a name="splitting-the-view"></a>Dividindo a exibição  
 Uma janela do Editor pode ser dividida em duas partes separadas para facilitar a edição.  
  
#### <a name="to-split-a-window"></a>Para dividir uma janela  
  
1.  Clique na barra de divisão (localizada sobre a barra de rolagem).  
  
2.  Arraste a barra de divisão para baixo.  
  
3.  Para voltar para um único painel, clique duas vezes na barra de divisão que divide os dois painéis.  
  
 O painel novo contém o mesmo documento e quaisquer mudanças feitas em um painel são refletidas no outro painel, contanto que aquele painel exiba o mesmo lugar no documento.  
  
## <a name="word-wrap"></a>Quebra automática de linha  
 Quando você ativa a quebra automática de linha, a barra de rolagem horizontal é afastada e as linhas de código que excedem a largura do tamanho da janela do Editor são automaticamente quebradas para a próxima linha exibida em vez de fornecer uma barra de rolagem externa.  
  
#### <a name="to-activate-word-wrap"></a>Para ativar a quebra automática de linha  
  
1.  Clique em **Opções** no menu **Ferramentas** .  
  
2.  Clique em **Editor de Texto**.  
  
3.  Abra a pasta de idiomas apropriada (ou **Todos os Idiomas** para afetar todos os idiomas).  
  
4.  Selecione **Quebra Automática de Linha**.  
  
## <a name="enabling-virtual-space-mode"></a>Ativando o modo Espaço Virtual  
 No modo **Espaço Virtual** , o Editor age como se o espaço após o término de cada linha estivesse cheio com um número infinito de espaços, permitindo que as linhas de código continuem fora da área visível da tela.  
  
#### <a name="to-enable-virtual-space-mode"></a>Para habilitar o modo Espaço Virtual  
  
1.  Clique em **Opções** no menu **Ferramentas** .  
  
2.  Clique em **Editor de Texto**.  
  
3.  Abra a pasta de idiomas apropriada (ou **Todos os Idiomas** para afetar todos os idiomas).  
  
4.  Selecione **Habilitar espaço virtual**.  
  
 Quando o modo Espaço Virtual não é habilitado, o cursor faz uma quebra automática do final da primeira linha até o primeiro caractere da próxima linha e vice-versa.  
  
## <a name="displaying-line-numbers"></a>exibindo números de linha  
 Você pode ativar a numeração de linhas em seu código. Os números de linha são úteis para navegar por código. Para obter mais informações, veja [Navegar em código e texto](../../relational-databases/scripting/navigate-code-and-text.md).  
  
> [!NOTE]  
>  Ativar a numeração de linhas não significa que o documento será impresso com números de linha. Para imprimir os números de linha, marque a caixa de seleção **Números de linha** no comando **Configurar Página** no menu **Arquivo** .  
  
#### <a name="to-display-line-numbers-in-code"></a>Para exibir números de linha em código  
  
1.  Clique em **Opções** no menu **Ferramentas** .  
  
2.  Clique em **Editor de Texto**.  
  
3.  Clique em **Todos os Idiomas**.  
  
4.  Clique em **Geral**.  
  
5.  Selecione **Números de linha**.  
  
 Para especificar a numeração de linhas para apenas algumas linguagens de programação, selecione **Números de Linha** na pasta apropriada.  
  
## <a name="enabling-full-screen-mode"></a>Ativando o modo de tela inteira  
 Você pode optar por ocultar todas as janelas de ferramenta e exibir apenas janelas de documentos habilitando o modo de tela inteira.  
  
#### <a name="to-enable-full-screen-mode"></a>Para habilitar o modo de tela inteira  
  
1.  Pressione ALT+SHIFT+ENTER para alternar para o modo de tela inteira.  
  
## <a name="using-auto-hide-all"></a>Usando Ocultar Tudo Automaticamente  
  
#### <a name="to-hide-all-the-tool-windows-at-once"></a>Para ocultar todas as janelas de ferramentas de uma só vez  
  
1.  Selecione **Ocultar Tudo Automaticamente** no menu **Janela** .  
  
  
