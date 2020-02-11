---
title: Caixa de diálogo visibilidade da linha | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.rowvisibility.f1
- "10126"
ms.assetid: 557ecf70-62b1-47f5-9322-0ebdc809d018
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fe9af16c34fa70bb8fcda0dcaae64a39786e3cd3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66102413"
---
# <a name="row-visibility-dialog-box"></a>Caixa de diálogo Visibilidade da Linha
  Use a caixa de diálogo **Visibilidade da Linha** para mostrar ou ocultar a linha selecionada quando o relatório for executado pela primeira vez ou para usar outro item de relatório para alternar a visibilidade da linha.  
  
## <a name="options"></a>Opções  
 **Quando o relatório for executado inicialmente**  
 Selecione uma opção para indicar como o item de relatório é exibido inicialmente no relatório.  
  
 **Mostrar**  
 Selecione esta opção para mostrar o item de relatório.  
  
 **Ocultar**  
 Selecione esta opção para ocultar o item de relatório.  
  
 **Mostrar ou ocultar com base em uma expressão**  
 Escolha esta opção para variar a visibilidade inicial usando uma expressão.  
  
 Digite uma expressão que seja avaliada como um valor `Boolean``True` para ocultar o item e `False` para mostrar o item. Clique no botão expressão (**FX**) para editar a expressão.  
  
 **A exibição pode ser alternada por este item de relatório**  
 Escolha esta opção para exibir uma imagem de alternância que permite que o usuário mostre ou oculte este item de relatório em um visualizador de relatórios HTML.  
  
 Digite ou selecione o nome de uma caixa de texto no relatório no qual exibir a imagem de alternância, por exemplo, Textbox1. A caixa de texto escolhida deve estar no escopo atual ou no escopo de contenção desse item de relatório. Por exemplo, para alternar a visibilidade de linhas associadas a um grupo filho, selecione uma caixa de texto em uma linha associada ao grupo pai. Para alternar a visibilidade de um gráfico, selecione uma caixa de texto que esteja no mesmo escopo de contenção que o gráfico. Por exemplo, o corpo do relatório ou um retângulo.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [Adicionar uma ação de expandir ou recolher a um item &#40;Construtor de Relatórios e SSRS&#41;](report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [Imagens &#40;Construtor de Relatórios e SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [Ajuda F1 do Designer de Relatórios](tools/report-designer-f1-help.md)  
  
  
