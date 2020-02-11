---
title: Formatando cores da série em um gráfico (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10245"
- "10252"
- sql12.rtp.rptdesigner.serieslabelproperties.borders.f1
- sql12.rtp.rptdesigner.seriesproperties.borders.f1
ms.assetid: fe541501-cac5-47b1-b95f-c410db789190
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 445e6d2ccaba0d03de9f25d770ac22f35b628778
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66105764"
---
# <a name="formatting-series-colors-on-a-chart-report-builder-and-ssrs"></a>Formatando as cores da série em um gráfico (Construtor de Relatórios e SSRS)
  O Reporting Services fornece várias paletas internas para gráficos. Além disso, você pode definir uma paleta personalizada. Por padrão, os gráficos usam a paleta de cores **BrightPastel** interna para preencher cada série. Essas cores também aparecem na legenda. Se forem adicionadas várias séries ao gráfico, ele atribuirá um cor à série na ordem em que as cores foram definidas na paleta.  
  
 Se houver mais séries que o número de cores da paleta, o gráfico começará a reutilizar as cores, ou seja, poderão existir duas séries com a mesma cor. Isso ocorrerá frequentemente se você estiver usando um gráfico de Forma, no qual a cada ponto de dados é atribuído uma cor da paleta. Para evitar confusão, defina uma paleta personalizada que tenha, no mínimo, o mesmo número de cores que o número de séries do gráfico.  
  
 Você pode selecionar uma paleta nova ou definir uma paleta personalizada no painel Propriedades. Para obter mais informações, consulte [Definir cores em um gráfico usando uma paleta &#40;Construtor de Relatórios e SSRS&#41;](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-built-in-palettes"></a>Usando paletas internas  
 O Reporting Services fornece uma lista de paletas internas predefinidas que você pode usar para definir um conjunto de cores para as séries do gráfico. Todas as paletas internas contêm entre 10 e 16 valores de cor. Não é possível estender a paleta interna para incluir mais cores, portanto, se você precisar de mais de 16 cores, defina uma paleta personalizada.  
  
 Se você estiver imprimindo um relatório, considere o uso de uma paleta **Escala de cinza** . Essa paleta usa tons de preto e branco para representar cada série de um gráfico.  
  
 A paleta nomeada Padrão foi usada como a paleta de gráfico padrão nas versões anteriores do Reporting Services. Ela foi preservada com o mesmo nome para manter a consistência. A atualização dos gráficos será consistente usando a paleta Padrão, mas, após a atualização, considere alterá-la.  
  
## <a name="using-custom-palettes"></a>Usando paletas personalizadas  
 Para aplicar suas próprias cores ao gráfico, use uma paleta personalizada. Uma paleta personalizada permite que você adicione suas próprias cores na ordem que quiser que elas apareçam no gráfico. Uma paleta personalizada será especialmente útil se o número de séries do gráfico for desconhecido no momento da criação. Para obter mais informações, consulte [Definir cores em um gráfico usando uma paleta &#40;Construtor de Relatórios e SSRS&#41;](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md).  
  
## <a name="using-a-color-fill-on-each-series"></a>Usando uma cor preenchimento em cada série  
 Você também pode definir suas próprias cores no gráfico especificando uma cor para cada série no gráfico. Para isso, abra a caixa de diálogo **Propriedades da Série** e defina a propriedade **Cor** para **Preenchimento**. Essa abordagem anulará todas as paletas definidas. Geralmente, é melhor usar uma paleta personalizada para definir suas próprias cores porque o número de séries no conjunto de dados pode ser desconhecido até o processamento do relatório.  
  
 Essa abordagem é a mais adequada se você desejar definir a cor das séries condicionalmente com base em uma expressão.  Para obter mais informações, consulte [Formatando pontos de dados em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Especificar cores consistentes em gráficos com várias formas &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
 [Definir cores em um gráfico usando uma paleta &#40;Construtor de Relatórios e SSRS&#41;](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md))  
  
 [Realçar dados do gráfico adicionando faixas &#40;Construtor de Relatórios e SSRS&#41;](highlight-chart-data-by-adding-strip-lines-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Adicionar estilos de bisel, alto-relevo e textura a um gráfico &#40;Construtor de Relatórios e SSRS&#41;](chart-effects-add-bevel-emboss-or-texture-report-builder.md)   
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Formatando a legenda em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](chart-legend-formatting-report-builder.md)  
  
  
