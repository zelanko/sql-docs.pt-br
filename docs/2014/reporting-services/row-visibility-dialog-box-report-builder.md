---
title: Linha caixa de diálogo visibilidade (construtor de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "10126"
ms.assetid: 117fb20c-2fda-437e-bcc5-9010d6d4b53b
caps.latest.revision: 13
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: b1ed0f9298810713038d722a7b2e28c9982f63ca
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130499"
---
# <a name="row-visibility-dialog-box-report-builder"></a>Caixa de diálogo Visibilidade da Linha (Construtor de Relatórios)
  Use a caixa de diálogo **Visibilidade da Linha** para mostrar ou ocultar a linha selecionada quando o relatório for executado pela primeira vez ou para usar outro item de relatório para alternar a visibilidade da linha.  
  
## <a name="options"></a>Opções  
 **Quando o relatório for executado inicialmente**  
 Selecione uma opção para indicar como a linha é exibida inicialmente no relatório.  
  
 **Mostrar**  
 Selecione essa opção para mostrar a linha.  
  
 **Ocultar**  
 Selecione essa opção para ocultar a linha.  
  
 **Mostrar ou ocultar com base em uma expressão**  
 Escolha esta opção para variar a visibilidade inicial usando uma expressão.  
  
 Digite uma expressão que é avaliada como um `Boolean` valor `True` para ocultar o item e `False` para mostrar o item. Clique no botão **Expressão** (*fx*) para editar a expressão.  
  
 **Exibição pode ser alternada por este item de relatório**  
 Escolha essa opção para exibir uma imagem de alternância que permite que o usuário mostre ou oculte a linha em um visualizador de relatórios HTML.  
  
 Digite ou selecione o nome de uma caixa de texto no relatório no qual exibir a imagem de alternância, por exemplo, Textbox1. A caixa de texto escolhida deve estar no escopo atual ou no escopo de contenção desse item de relatório. Por exemplo, para alternar a visibilidade de linhas associadas a um grupo filho, selecione uma caixa de texto em uma linha associada ao grupo pai. Para alternar a visibilidade de um gráfico, selecione uma caixa de texto que esteja no mesmo escopo de contenção que o gráfico. Por exemplo, o corpo do relatório ou um retângulo.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [Adicionar uma ação de expandir/recolher a um item &#40;Construtor de Relatórios e SSRS&#41;](report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [Imagens &#40;SSRS e construtor de relatórios&#41;](report-design/images-report-builder-and-ssrs.md)   
 [Ajuda do Construtor de Relatórios para caixas de diálogo, painéis e assistentes](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Caixa de diálogo Propriedades da Imagem, Geral &#40;Construtor de Relatórios e SSRS&#41;](../../2014/reporting-services/image-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  