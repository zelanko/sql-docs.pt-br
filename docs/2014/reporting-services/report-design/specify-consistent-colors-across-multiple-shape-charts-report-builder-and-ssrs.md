---
title: Especificar cores consistentes em vários gráficos de forma (construtor de relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: d52f68e9-2ba7-4bff-9053-4089e5164ab4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8595050b478743b7092787acf880425b24c5b1e3
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56011288"
---
# <a name="specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs"></a>Especificar cores consistentes em gráficos com várias formas (Construtor de Relatórios e SSRS)
  Em gráficos não forma, uma cor nova é selecionada na paleta com base no índice da série no gráfico. Por exemplo, a primeira série do gráfico é mapeada para a primeira cor da paleta. No entanto, esse comportamento é diferente em gráficos com forma. Em gráficos com forma, todas as cores da paleta são mapeadas para um ponto de dados no conjunto de dados. Por exemplo, o ponto de dados 1 é mapeado para a primeira cor da paleta, o ponto de dados 2 é mapeado para a segunda paleta de cores e assim por diante.  
  
 Caso não tenha nenhum valor, um ponto de dados é omitido na exibição de um gráfico com forma. Isso significa que o ponto de dados deixa de ser colorido. Por exemplo, se o ponto de dados 2 tiver um valor igual a zero, o ponto de dados 1 será mapeado para a primeira cor da paleta e o ponto 3, para a segunda cor da paleta. Essa abordagem é útil porque os pontos vazios no conjunto de dados de um gráfico de pizza não necessariamente usam uma cor da paleta quando o ponto vazio não precisa ser desenhado.  
  
 Como efeito colateral, quando vários gráficos de pizza são exibidos em um relatório, os gráficos de pizza podem exibir cores diferentes dos pontos de dados com o mesmo agrupamento da categoria. Para resolver isso, você precisa definir cores individuais mapeadas para um grupo de categorias, e não valores de dados individuais. A maneira como você faz isto vai depender se os gráficos de formas são minigráficos em uma tabela ou matriz, ou se eles são gráficos de formas no próprio relatório.  
  
 Como a legenda é conectada à série, todas as cores especificadas para a série serão mostradas automaticamente na legenda.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-consistent-colors-across-multiple-sparkline-shape-charts-in-a-table-or-matrix"></a>Para especificar cores consistentes em minigráficos de várias formas em uma tabela ou matriz  
  
1.  Clique no gráfico para exibir o painel Dados do Gráfico.  
  
2.  Na área **Grupos de Categorias** , clique com o botão direito do mouse em uma categoria e clique em **Propriedades de Grupos de Categorias**.  
  
3.  Na guia Geral, na caixa **Sincronizar grupos em** , clique no nome da categoria para a qual você gostaria de sincronizar cores e clique em **OK**.  
  
### <a name="to-specify-consistent-colors-across-multiple-shape-charts"></a>Para especificar cores consistentes em vários gráficos com forma  
  
1.  Clique com o botão direito do mouse fora do corpo do relatório e selecione **Propriedades do Relatório**.  
  
2.  Em **Código**, digite o seguinte código na caixa de texto.  
  
    ```  
    Private colorPalette As String() = {"Color1", "Color2", "Color3"}  
    Private count As Integer = 0  
    Private mapping As New System.Collections.Hashtable()  
    Public Function GetColor(ByVal groupingValue As String) As String  
        If mapping.ContainsKey(groupingValue) Then  
            Return mapping(groupingValue)  
        End If  
        Dim c As String = colorPalette(count Mod colorPalette.Length)  
        count = count + 1  
        mapping.Add(groupingValue, c)  
        Return c  
    End Function  
    ```  
  
    > [!NOTE]  
    >  Você precisará substituir as cadeias de caracteres "Color1" por cores próprias. É possível usar cores nomeadas, por exemplo "Vermelho" ou usar valor hexadecimal de seis dígitos que representam a cor como "#FFFFFF" para preto. Se tiver mais de três cores definidas, você precisará estender a matriz de cores para que o número de cores na matriz corresponda ao número de pontos do gráfico com forma. É possível adicionar novas cores à matriz especificando uma lista separada por vírgulas dos valores da cadeia de caracteres que contêm cores nomeadas ou representações hexadecimais das cores.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  Clique com o botão direito do mouse no gráfico com forma e selecione **Propriedades da Série**.  
  
5.  Em **Preenchimento**, clique no botão **Expressão** (*fx*) para editar a expressão de acordo com a propriedade **Cor** .  
  
6.  Digite a seguinte expressão em que "MyCategoryField" é o campo exibido na área **Grupos de Categorias** :  
  
    ```  
    =Code.GetColor(Fields!MyCategoryField)  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Formatando as cores da série em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [Adicionar estilos de bisel, alto-relevo e textura a um gráfico &#40;Construtor de Relatórios e SSRS&#41;](chart-effects-add-bevel-emboss-or-texture-report-builder.md)   
 [Definir cores em um gráfico usando uma paleta &#40;Construtor de Relatórios e SSRS&#41;](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)   
 [Adicionar pontos vazios ao gráfico &#40;relatórios e SSRS&#41;](add-empty-points-to-a-chart-report-builder-and-ssrs.md)   
 [Gráficos de forma &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Vinculando várias regiões de dados ao mesmo conjunto de dados &#40;Construtor de Relatórios e SSRS&#41;](linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [Regiões de dados aninhadas &#40;Construtor de Relatórios e SSRS&#41;](nested-data-regions-report-builder-and-ssrs.md)   
 [Minigráficos e barras de dados &#40;Construtor de Relatórios e SSRS&#41;](sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
  
