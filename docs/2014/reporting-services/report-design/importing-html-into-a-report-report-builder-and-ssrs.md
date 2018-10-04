---
title: Importando HTML para um relatório (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: dd0410ea-8839-4e8c-9944-8cdfe5465591
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 4176e9dc902ae4c83024ba5e659a2467585d71c8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48115706"
---
# <a name="importing-html-into-a-report-report-builder-and-ssrs"></a>Importando HTML para um relatório (Construtor de Relatórios e SSRS)
  É possível usar uma caixa de texto para inserir em um relatório um texto formatado em HTML recuperado de um campo em seu conjunto de dados. O texto pode ser de qualquer expressão simples ou complexa avaliada como HTML formatado corretamente. O texto formatado pode ser renderizado em todos os formatos de saída com suporte, inclusive PDF.  
  
 ![rs_HTMLFormatting](../media/rs-htmlformatting.gif "rs_HTMLFormatting")  
  
 Esta ilustração mostra texto com formatação HTML em uma exibição de design de relatório, além do mesmo texto como é renderizado quando o relatório é executado.  
  
> [!NOTE]  
>  Ao importar texto contendo marcação HTML, os dados sempre devem ser analisados primeiro pela caixa de texto. Como apenas um subconjunto de marcas HTML possui suporte, o HTML mostrado no relatório renderizado pode ser diferente do HTML original.  
  
 Para começar a usar rapidamente, consulte [Tutorial: Formatar texto &#40;Construtor de Relatórios&#41;](../tutorial-format-text-report-builder.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="supported-html-tags"></a>Tags HTML Suportadas  
 A seguir, há uma lista completa de marcas que são renderizadas como HTML quando definidas como texto de espaço reservado:  
  
-   Elementos de cabeçalho, estilo e bloco: \<H {n} >, \<DIV >, \<SPAN >,\<P >, \<LI >  
  
 Qualquer outra marcação HTML será ignorada durante o processamento de relatório. Se o HTML representado pela expressão no texto de espaço reservado não for bem formado, o espaço reservado será processado como texto sem-formatação. Todas as marcas HTML não diferenciam maiúsculas de minúsculas.  
  
 Se o texto na sua caixa de texto tiver apenas um bloco de texto, qualquer HTML no espaço reservado que define os elementos do bloco será renderizado corretamente. Entretanto, se a caixa de texto tiver vários blocos de texto, as marcas HTML serão ignoradas e a estrutura do texto será definida pelos blocos de texto.  
  
 Se mais de uma marca for definida para texto, e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] detectar um conflito entre o HTML e as restrições de relatório existentes, somente a marca HTML mais interna será tratada como HTML.  
  
 Ao utilizar a lista de manipulação de rótulos, a fonte e o estilo de todos os prefixos de números e marcadores serão corrigidos para Arial black.  
  
 Para obter mais informações, consulte [Adicionar HTML a um relatório &#40;Construtor de Relatórios e SSRS&#41;](add-html-into-a-report-report-builder-and-ssrs.md).  
  
## <a name="limitations-of-cascading-style-sheet-attributes"></a>Limitações de atributos de folha de estilos em cascata  
 Ao usar atributos de folha de estilos em cascata (CSS), somente um conjunto básico de marcas é definido. Estes são os atributos com suporte:  
  
-   alinhamento de texto, recuo de texto  
  
-   font-family  
  
-   font-size  
  
    -   Há suporte somente para valores de tamanho RDL válido em unidades de comprimento CSS absoluto. Unidades com suporte: in, cm, mm, pt, pc.  
  
    -   As unidades de comprimento CSS relativas são ignoradas e não têm suporte. As unidades com suporte são em, ex, px,%,rem.  
  
     Para saber mais sobre as unidades CSS, veja: [Valores CSS e referência de unidades](http://msdn.microsoft.com/en-us/library/ms531211\(VS.85\).aspx) (http://msdn.microsoft.com/library/ms531211(VS.85).aspx).  
  
-   color  
  
-   preenchimento, preenchimento inferior, preenchimento superior, preenchimento à direita, preenchimento à esquerda  
  
-   espessura da fonte  
  
 Eis algumas considerações quanto ao uso de CSS:  
  
-   Valores CSS malformados são ignorados da mesma maneira que HTML malformado.  
  
-   Quando o atributo e os atributos de estilo CSS existirem na mesma marca, a propriedade CSS tem maior precedência. Por exemplo, se o texto for **\<p style="text-align: right" align="left">**, somente o atributo de alinhamento de texto será aplicado e o texto será alinhado à direita.  
  
-   Para atributos e a estilos CSS, se uma propriedade for especificada mais de uma vez, somente sua última instância será aplicada. Por exemplo, se o texto for **\<p align="left" align="right">**, ele será alinhado à direita.  
  
## <a name="see-also"></a>Consulte também  
 [Renderizando para HTML &#40;relatórios e SSRS&#41;](../report-builder/rendering-to-html-report-builder-and-ssrs.md)  
  
  
