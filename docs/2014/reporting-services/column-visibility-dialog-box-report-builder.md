---
title: Caixa de diálogo de visibilidade de coluna (construtor de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10127"
ms.assetid: 0c030cab-6087-45a5-99f0-c7bd693f20a1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 58381a9e56ed6ace1f8ff18109d9746072f76774
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66109804"
---
# <a name="column-visibility-dialog-box-report-builder"></a>Caixa de diálogo Visibilidade da Coluna (Construtor de Relatórios)
  Use a caixa de diálogo **Visibilidade da Coluna** para mostrar ou ocultar a coluna selecionada quando o relatório for executado pela primeira vez ou para usar outro item de relatório para alternar a visibilidade da coluna.  
  
## <a name="options"></a>Opções  
 **Quando o relatório for executado inicialmente**  
 Selecione uma opção para indicar como o item de relatório é exibido inicialmente no relatório.  
  
 **Mostrar**  
 Escolha esta opção para mostrar a coluna.  
  
 **Ocultar**  
 Escolha esta opção para ocultar a Coluna.  
  
 **Mostrar ou ocultar com base em uma expressão**  
 Escolha esta opção para variar a visibilidade inicial usando uma expressão.  
  
 Digite uma expressão que seja avaliada como um valor `Boolean` `True` para ocultar o item e `False` para mostrar o item. Clique no botão Expressão (*fx*) para editar a expressão.  
  
 **Exibição pode ser alternada por este item de relatório**  
 Escolha esta opção para exibir uma imagem de alternância que permite que o usuário mostre ou oculte essa coluna em um visualizador de relatórios HTML.  
  
 Digite ou selecione o nome de uma caixa de texto no relatório no qual exibir a imagem de alternância, por exemplo, Textbox1. A caixa de texto escolhida deve estar no escopo atual ou no escopo de contenção desse item de relatório. Por exemplo, para alternar a visibilidade de linhas associadas a um grupo filho, selecione uma caixa de texto em uma linha associada ao grupo pai. Para alternar a visibilidade de um gráfico, selecione uma caixa de texto que esteja no mesmo escopo de contenção que o gráfico. Por exemplo, o corpo do relatório ou um retângulo.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [Adicionar uma ação de expandir/recolher a um item &#40;Construtor de Relatórios e SSRS&#41;](report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [Imagens &#40;Construtor de Relatórios e SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [Ajuda do Construtor de Relatórios para caixas de diálogo, painéis e assistentes](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Caixa de diálogo Propriedades da Imagem, Geral &#40;Construtor de Relatórios e SSRS&#41;](../../2014/reporting-services/image-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
