---
title: "Adicionar, mover ou excluir uma caixa de texto (construtor de relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f042cf81-d933-4ac7-9287-c074a46bde98
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 75444343968c9901a24c1a4d431d4d8cfacb1567
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="add-move-or-delete-a-text-box-report-builder-and-ssrs"></a>Adicionar, mover ou excluir uma caixa de texto (Construtor de Relatórios e SSRS)
  As caixas de texto constituem o item de relatório mais utilizado em relatórios paginados do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] . Você pode adicionar uma caixa de texto ao corpo do relatório para exibir informações como títulos, opções de parâmetro, campos internos e datas.  
  
 Cada célula de uma tabela ou matriz é uma caixa de texto. Quase todos os dados exibidos em um relatório com tabelas e matrizes são o resultado do processador que avalia o conteúdo de cada caixa de texto no relatório. Desse modo, você pode formatar células da mesma maneira como formataria outras caixas de texto fora da região de dados.  
  
 Para adicionar uma caixa de texto a uma região de dados lista, você deve adicionar a caixa de texto e arrastá-la para a lista.  
  
> [!NOTE]  
>  Quando você clica em uma caixa de texto, está editando o texto imediatamente na caixa de texto. Para selecionar a caixa de texto propriamente dita, não o texto contido, pressione ESC.  
  
## <a name="to-add-a-text-box"></a>Para adicionar uma caixa de texto  
  
1.  Na guia **Inserir** , na exibição Design, clique em **Caixa de Texto**.  
  
2.  Na superfície de design, clique e arraste uma caixa até obter o tamanho desejado da caixa de texto.  
  
## <a name="to-add-a-text-box-in-a-list"></a>Para adicionar uma caixa de texto a uma lista  
  
1.  Na guia **Inserir** , na exibição de design de relatório, clique em **Lista**.  
  
2.  Na superfície de design, clique e arraste uma caixa até obter o tamanho desejado da lista.  
  
3.  Na guia **Inserir** , clique em **Caixa de Texto**.  
  
4.  Na superfície de design, clique e arraste uma caixa até obter o tamanho desejado da caixa de texto na lista que você adicionou na etapa 1.   
  
5.  Para confirmar se a caixa de texto está aninhada corretamente dentro da lista, selecione-a.  
  
    > [!NOTE]  
    >  Se você clicar na caixa de texto e estiver no modo de edição, pressione ESC para selecionar a caixa de texto.  
  
6.  No painel Propriedades, verifique se a propriedade **Pai** é um retângulo que foi adicionado automaticamente à região de dados da lista.  
  
    > [!NOTE]  
    >  Se o painel Propriedades não estiver visível, marque **Propriedades** na guia **Exibir** .  
  
## <a name="to-move-a-text-box"></a>Para mover uma caixa de texto  
  
1.  Na exibição de design de relatório, clique em um espaço vazio dentro da caixa de texto para selecionar a caixa de texto.  
  
    > [!NOTE]  
    >  Se você clicar na caixa de texto e estiver no modo de edição, pressione ESC para selecionar a caixa de texto.  
  
2.  Clique na alça da caixa de texto e arraste-a para o novo local.   
    Se preferir, use as teclas de seta para mover a caixa de texto selecionada nas direções horizontal e vertical. Para mover a caixa de texto na superfície de design em incrementos menores, pressione a tecla CTRL e as teclas de seta.  
  
## <a name="to-delete-a-text-box"></a>Para excluir uma caixa de texto  
  
1.  No modo de exibição de Design de relatório, clique com o botão direito do mouse em um espaço vazio dentro da caixa de texto para selecioná-la e clique em **Excluir**. Se preferir, clique em um espaço vazio dentro da caixa de texto e pressione DELETE.  
  
    > [!NOTE]  
    >  Se você clicar na caixa de texto e estiver no modo de edição, pressione ESC para selecionar a caixa de texto.  
  
## <a name="see-also"></a>Consulte também  
 [Caixas de texto &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Atalhos de teclado &#40;Construtor de Relatórios&#41;](../../reporting-services/report-builder/keyboard-shortcuts-report-builder.md)  
  
  
