---
title: Editor de formulário de membro calculado (guia cálculos, designer de cubo) (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.calculationexpression.calculatedmember.f1
ms.assetid: f7719b9e-b1e6-4792-90a6-30d9d8eb1196
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 432300f54a7678970f394b27712bcb28ba8a7e7d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66088366"
---
# <a name="calculated-member-form-editor-calculations-tab-cube-designer-analysis-services---multidimensional-data"></a>Editor de Formulário de Membro Calculado (guia Cálculos, Designer de Cubo) (Analysis Services - Dados Multidimensionais)
  Use o painel **Editor de Formulário de Membro Calculado** na guia **Cálculos** do Designer de Cubo para criar ou modificar um membro calculado.  
  
 **Observação** Esse painel é exibido apenas na exibição de formulário.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Digite o nome do membro calculado.  
  
 **Propriedades Pai**  
 Expanda para exibir as opções **Hierarquia pai**, **Membro pai**e **Alterar** .  
  
 **Hierarquia pai**  
 Selecione a dimensão e a hierarquia no cubo selecionado que deve incluir o membro calculado. Selecione MEASURES para definir uma medida calculada.  
  
 **Membro pai**  
 Selecione o membro abaixo do qual o membro calculado deve ser exibido.  
  
 **Observação** Essa opção estará disponível se **hierarquia pai** especificar uma hierarquia diferente de medidas.  
  
 **Alterar**  
 Selecione para exibir a caixa de diálogo **Selecionar Membro Pai** e escolher um membro para **Membro pai**. Para obter mais informações sobre a caixa de diálogo **Selecionar Membro Pai**, consulte [Caixa de diálogo Selecionar Membro Pai &#40;Analysis Services – Dados Multidimensionais&#41;](select-parent-member-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Expression**  
 Expanda para exibir ou editar a expressão MDX do membro calculado.  
  
 Arraste elementos selecionados do painel **Ferramentas de Cálculo** para esta opção para incluir a sintaxe MDX para o elemento selecionado.  
  
> [!NOTE]  
>  É recomendável que essa expressão avalie para uma cadeia de caracteres ou para um valor numérico.  
  
 **Propriedades adicionais**  
 Expanda para exibir as opções **Cadeia de formato**, **Visível**, **Comportamento não vazio**, **Expressões de Cores**e **Expressões de Fonte** .  
  
 **Cadeia de formato**  
 Digite a cadeia de formato MDX usada para formatar o valor retornado pelo membro calculado ou selecione uma cadeia de formato predefinida.  
  
 Para obter mais informações sobre cadeias de formato MDX, consulte [Conteúdo FORMAT_STRING &#40;MDX&#41;](multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md).  
  
 **Visível**  
 Selecione **Verdadeiro** para permitir que o membro calculado seja visível para aplicativos cliente.  
  
 **Comportamento não vazio**  
 Selecione o nome da medida usada para resolver consultas NÃO VAZIAS em MDX para o membro calculado. Se a propriedade **Comportamento Não Vazio** estiver em branco, o membro calculado deverá ser avaliado repetidamente para determinar se um membro está vazio. Se a propriedade **Comportamento Não Vazio** contiver o nome de uma medida, o membro calculado será tratado como vazio se a medida especificada estiver vazia.  
  
> [!WARNING]  
>  Essa propriedade é preterida. Evite configurá-la. Consulte [recursos de Analysis Services preteridos no SQL Server 2014](deprecated-analysis-services-features-in-sql-server-2014.md) para obter detalhes.  
  
 **Expressões de Cores**  
 Expanda para exibir as opções **Cor de primeiro plano** e **Cor de fundo** .  
  
 **Cor de primeiro plano**  
 Digite a expressão MDX que fornece a cor de primeiro plano do membro calculado.  
  
 Arraste elementos selecionados do painel **Ferramentas de Cálculo** para esta opção para incluir a sintaxe MDX para o elemento selecionado.  
  
 Clique no botão de seleção de cor para exibir a caixa de diálogo **Cor** e inserir o valor de RGB (Vermelho-Verde-Azul) para uma cor especificada na expressão MDX. Para obter mais informações sobre valores RGB, consulte [Conteúdo de FORE_COLOR e BACK_COLOR &#40;MDX&#41;](multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md).  
  
 **Cor de fundo**  
 Digite a expressão MDX que fornece a cor de fundo do membro calculado.  
  
 Arraste elementos selecionados do painel **Ferramentas de Cálculo** para esta opção para incluir a sintaxe MDX para o elemento selecionado.  
  
 Clique no botão de seleção de cor para exibir a caixa de diálogo **Cor** e inserir o valor de RGB (Vermelho-Verde-Azul) para uma cor especificada na expressão MDX. Para obter mais informações sobre valores RGB, consulte [Conteúdo de FORE_COLOR e BACK_COLOR &#40;MDX&#41;](multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md).  
  
 **Expressões de Fonte**  
 Expanda para exibir as opções **Nome da fonte**, **Tamanho da fonte**e **Sinalizadores de fonte** .  
  
 **Nome da fonte**  
 Digite a expressão MDX que fornece o nome da fonte usada para o membro calculado.  
  
 Arraste elementos selecionados do painel **Ferramentas de Cálculo** para esta opção para incluir a sintaxe MDX para o elemento selecionado.  
  
 Clique no botão de seleção de fonte para exibir a caixa de diálogo **Fonte** e inserir os valores de propriedades para uma fonte especificada na expressão MDX. Para obter mais informações sobre valores de propriedades, consulte [Criando e usando valores de propriedade &#40;MDX&#41;](creating-and-using-property-values-mdx.md).  
  
 **Tamanho da fonte**  
 Digite a expressão MDX que fornece o tamanho da fonte usada para o membro calculado.  
  
 Arraste elementos selecionados do painel **Ferramentas de Cálculo** para esta opção para incluir a sintaxe MDX para o elemento selecionado.  
  
 Clique no botão de seleção de fonte para exibir a caixa de diálogo **Fonte** e inserir os valores de propriedades para uma fonte especificada na expressão MDX. Para obter mais informações sobre valores de propriedades, consulte [Criando e usando valores de propriedade &#40;MDX&#41;](creating-and-using-property-values-mdx.md).  
  
 **Sinalizadores de fonte**  
 Digite a expressão MDX que fornece o valor de bitmap que contém os sinalizadores de fonte, como sublinhado ou negrito, da fonte usada para o membro calculado.  
  
 Arraste elementos selecionados do painel **Ferramentas de Cálculo** para esta opção para incluir a sintaxe MDX para o elemento selecionado.  
  
 Clique no botão de seleção de fonte para exibir a caixa de diálogo **Fonte** e inserir os valores de propriedades para uma fonte especificada na expressão MDX. Para obter mais informações sobre valores de propriedades, consulte [Criando e usando valores de propriedade &#40;MDX&#41;](creating-and-using-property-values-mdx.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Cálculos](multidimensional-models-olap-logical-cube-objects/calculations.md)   
 [Criar membros calculados](multidimensional-models/create-calculated-members.md)   
 [O designer de cubo &#40;Analysis Services-dados multidimensionais&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Cálculos &#40;designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](calculations-cube-designer-analysis-services-multidimensional-data.md)   
 [Barra de ferramentas &#40;guia cálculos, designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](toolbar-calculations-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Guia cálculos do organizador de script &#40;, designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](script-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [Ferramentas de cálculo &#40;guia cálculos, designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](calculation-tools-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulário de conjunto nomeado &#40;guia cálculos, designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](named-set-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de script &#40;guia cálculos, designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](script-editor-calculations-cube-designer-analysis-services-multidimensional-data.md)  
  
  
