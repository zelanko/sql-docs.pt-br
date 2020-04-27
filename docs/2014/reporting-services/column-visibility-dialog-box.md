---
title: Caixa de diálogo visibilidade da coluna | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.columnvisibility.f1
- "10127"
ms.assetid: ca59d1cd-d782-4298-aa61-4f312c32eb50
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 246189cf3b49212379c5c87f5600388097a2fb11
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109765"
---
# <a name="column-visibility-dialog-box"></a>Caixa de diálogo Visibilidade da Coluna
  Use a caixa de diálogo **Visibilidade da Coluna** para mostrar ou ocultar a coluna selecionada quando o relatório for executado pela primeira vez ou para usar outro item de relatório para alternar a visibilidade da coluna.  
  
## <a name="options"></a>Opções  
 **Quando o relatório for executado inicialmente**  
 Selecione uma opção para indicar como o item de relatório é exibido inicialmente no relatório.  
  
 **Mostrar**  
 Escolha esta opção para mostrar o item de relatório.  
  
 **Ocultar**  
 Escolha esta opção para ocultar o item de relatório.  
  
 **Mostrar ou ocultar com base em uma expressão**  
 Escolha esta opção para variar a visibilidade inicial usando uma expressão.  
  
 Digite uma expressão que seja avaliada como um valor `Boolean``True` para ocultar o item e `False` para mostrar o item. Clique no botão expressão (*FX*) para editar a expressão.  
  
 **A exibição pode ser alternada por este item de relatório**  
 Escolha esta opção para exibir uma imagem de alternância que permite que o usuário mostre ou oculte este item de relatório em um visualizador de relatórios HTML.  
  
 Digite ou selecione o nome de uma caixa de texto no relatório no qual exibir a imagem de alternância, por exemplo, Textbox1. A caixa de texto escolhida deve estar no escopo atual ou no escopo de contenção desse item de relatório. Por exemplo, para alternar a visibilidade de linhas associadas a um grupo filho, selecione uma caixa de texto em uma linha associada ao grupo pai. Para alternar a visibilidade de um gráfico, selecione uma caixa de texto que esteja no mesmo escopo de contenção que o gráfico. Por exemplo, o corpo do relatório ou um retângulo.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [Adicionar uma ação de expandir ou recolher a um item &#40;Construtor de Relatórios e SSRS&#41;](report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [Imagens &#40;Construtor de Relatórios e SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [Ajuda F1 do Designer de Relatórios](tools/report-designer-f1-help.md)  
  
  
