---
title: Efeitos 3D, bisel e outros em um gráfico (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10156"
ms.assetid: 18ef2119-2931-43ae-9078-f39b460462dd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 26fbda6dacd20b3ec02061b41a7e1de2f3b2d1ff
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56038267"
---
# <a name="3d-bevel-and-other-effects-in-a-chart-report-builder-and-ssrs"></a>Efeitos 3D, inclinação e outros em um gráfico (Construtor de Relatórios e SSRS)
  É possível usar efeitos tridimensionais (3D) para fornecer intensidade e adicionar impacto visual ao seu gráfico. Por exemplo, para enfatizar uma fatia específica de um gráfico de pizza destacada, você pode girar e alterar a perspectiva do gráfico de modo que as pessoas observem essa fatia primeiro. Quando efeitos 3D são aplicados ao gráfico, todas as cores de gradiente e estilos de hachurado são desabilitados.  
  
 Os efeitos tridimensionais podem ser aplicados a gráficos individuais, e é possível exibir gráficos bidimensionais e tridimensionais no mesmo relatório.  
  
 Para todos os tipos de gráficos, é possível adicionar efeitos tridimensionais a uma área do gráfico na caixa de diálogo **Propriedades da Área do Gráfico** selecionando **Habilitar 3D**. Para obter mais informações, consulte [Adicionar efeitos 3D a um gráfico &#40;Construtor de Relatórios e SSRS&#41;](chart-effects-add-3d-effects-report-builder.md).  
  
 Outra maneira de adicionar impacto visual aos gráficos é adicionar estilos bisel, alto-relevo e textura a gráficos de barras, de colunas, de pizza e de rosca. Para obter mais informações, consulte [Como adicionar bisel, alto-relevo e estilos de textura a um gráfico &#40;Construtor de Relatórios e SSRS&#41;](chart-effects-add-bevel-emboss-or-texture-report-builder.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="coordinate-based-three-dimensional-charts"></a>Gráficos tridimensionais baseados em coordenadas  
 Ao trabalhar com tipos de gráficos baseados em coordenadas (Coluna, Barra, Área, Ponto, Linha e Intervalo), os efeitos tridimensionais exibem o gráfico com um terceiro eixo conhecido como "eixo z". A introdução desse terceiro eixo permite aplicar uma variedade de aprimoramentos visuais ao gráfico.  
  
### <a name="changing-the-white-space-in-a-3d-chart"></a>Alterando o espaço em branco em um gráfico 3D  
 Ao exibir uma área do gráfico no modo tridimensional, cada série é mostrada em uma linha separada ao longo do eixo z do gráfico. Para alterar a quantidade de espaço entre cada série, modifique a profundidade da lacuna do ponto do gráfico alterando a propriedade **Profundidade da Lacuna do Ponto** na caixa de diálogo Efeitos 3D.  
  
### <a name="changing-the-projection-of-a-3d-chart"></a>Alterando a projeção de um gráfico 3D  
 Há dois tipos de projeções 3D: oblíqua e perspectiva. Uma projeção oblíqua ao gráfico adiciona uma dimensão de profundidade a um gráfico bidimensional. O eixo z é desenhado em ângulos iguais a partir dos eixos horizontal e vertical que permanecem perpendiculares entre si, exatamente como em um gráfico bidimensional.  
  
 A projeção de perspectiva transforma o gráfico calculando o plano de visão e desenhando o gráfico novamente como se ele estivesse sendo exibido a partir daquele ponto. O valor de **Rotação** desloca a exibição verticalmente do “nível do chão” em 0 para sobrecarga em 90. O valor de **Inclinação** desloca o ângulo de exibição para a esquerda ou para a direita. O valor de 0 é equivalente a uma exibição bidimensional do gráfico. O valor de **Perspectiva** define o percentual de distorção que será usada ao exibir a projeção. Esse tipo de projeção mantém as proporções do gráfico, mas a aparência se torna distorcida. Portanto, é mais efetivo usar uma grau de perspectiva mais baixo.  
  
> [!NOTE]  
>  As projeções oblíqua e de perspectiva são tipos separados de projeções e portanto não podem ser usadas em conjunto no mesmo gráfico.  
  
### <a name="clustering-data"></a>Dados de clustering  
 Em gráficos 2D, várias séries de dados são exibidos lado a lado. O clustering mostra séries individuais em linhas separadas em um gráfico 3D. Por exemplo, se houver um gráfico que contenha três séries de pontos de dados, o clustering exibirá cada uma das três séries em uma linha separada ao longo do eixo z. Por padrão, todos os tipos de gráficos mostrados em 3D são clusterizados.  
  
 O clustering pode ser desabilitado para gráficos de barras e de colunas. Quando o clustering é desabilitado, várias séries de barras e de colunas são exibidas lado a lado em uma linha.  
  
## <a name="shape-based-three-dimensional-charts"></a>Gráficos tridimensionais baseados em forma  
 Os tipos de gráficos baseados em forma (pizza, rosca, funil, pirâmide) possuem menos efeitos tridimensionais disponíveis. Ao trabalhar com tipos de gráficos baseados em forma, é possível alterar apenas os valores da rotação e da inclinação.  
  
## <a name="rotations"></a>Rotações  
 Os gráficos podem ser girados horizontal e verticalmente de -90 a 90 graus. Um ângulo horizontal positivo gira o gráfico no sentido anti-horário em torno do eixo x, enquanto um ângulo vertical positivo gira o gráfico no sentido horário em torno do eixo y.  
  
## <a name="highlighting-3d-effects"></a>Realçando efeitos 3D  
 É possível adicionar estilos de realce a um gráfico 3D por meio da propriedade **Sombreamento** exibida em Area3DStyle no painel Propriedades quando a área do gráfico é selecionada. Um estilo de iluminação simples aplica o mesmo matiz aos elementos da área do gráfico. Um estilo realístico altera os matizes dos elementos da área do gráfico dependendo de um ângulo de iluminação especificado.  
  
## <a name="see-also"></a>Consulte também  
 [Formatando rótulos dos eixos de um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Formatando um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Adicionar efeitos 3D a um gráfico &#40;Construtor de Relatórios e SSRS&#41;](chart-effects-add-3d-effects-report-builder.md)  
  
  
