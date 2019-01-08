---
title: Minigráficos e barras de dados (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.sparklines.f1
- "10544"
ms.assetid: b287436b-fa48-4970-a1a7-1dbcb86e7411
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: b729d5fb711a855c0edbdac14101e1e04c3bc83f
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53362528"
---
# <a name="sparklines-and-data-bars-report-builder-and-ssrs"></a>Minigráficos e barras de dados (Construtor de Relatórios e SSRS)
  Minigráficos e barras de dados são gráficos pequenos e simples que transmitem muitas informações em um espaço pequeno, geralmente embutidas com o texto. Em geral, os minigráficos e as barras de dados são usados em tabelas e matrizes. Seu impacto resulta da possibilidade de exibir vários deles juntos e compará-los uns sobre os outros, em vez de exibi-los individualmente. Eles facilitam a visualização das exceções, as linhas cujo desempenho se distingue das outras. Embora sejam pequenos, cada minigráfico costuma representar vários pontos de dados, geralmente durante um período de tempo. As barras de dados podem representar vários pontos de dados, mas normalmente ilustram apenas um. Cada minigráfico geralmente apresenta uma única série. Você não pode adicionar um minigráfico a um grupo de detalhes em uma tabela. Como os minigráficos exibem dados agregados, eles devem entrar em uma célula associada a um grupo. Minigráficos e barras de dados têm os mesmos elementos de gráficos básicos de categorias, séries e valores, mas não possuem legenda, linhas de eixo, rótulos nem marcas de escala.  
  
 ![rs_SparklineExample](../media/rs-sparklineexample.gif "rs_SparklineExample")  
  
 Para começar rapidamente com minigráficos, consulte [Tutorial: Adicionar um minigráfico ao relatório &#40;construtor de relatórios&#41; ](../tutorial-add-a-sparkline-to-your-report-report-builder.md) e os vídeos [como: Criar um minigráfico em uma tabela](https://go.microsoft.com/fwlink/?LinkId=197092) e [minigráficos, gráficos de barras e indicadores no construtor de relatórios](https://technet.microsoft.com/bi/video/ff877165) .  
  
> [!NOTE]  
>  Você pode publicar minigráficos e barras de dados com suas tabelas, matrizes ou lista pai, separadamente de um relatório como uma parte de relatório. [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="KindsofSparklines"></a> Tipos de minigráficos  
 Você pode criar praticamente tantos tipos de minigráficos quanto gráficos normais. Em geral, você não pode fazer minigráficos em 3D. Você pode fazer versões de minigráfico destes gráficos completos:  
  
-   [Gráficos de colunas &#40;relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md): Os gráficos de coluna básicos, empilhados e 100% empilhados.  
  
-   [Gráficos de linhas &#40;relatórios e SSRS&#41;](line-charts-report-builder-and-ssrs.md): Todos exceto o gráfico de linha 3D.  
  
-   [Gráficos de área &#40;relatórios e SSRS&#41;](area-charts-report-builder-and-ssrs.md): Todos exceto os gráficos de área 3D  
  
-   [Gráficos de pizza &#40;relatórios e SSRS&#41;](pie-charts-report-builder-and-ssrs.md): E gráficos de rosca, simples e 3D, mas não as outras formas como e gráficos de funil e de pirâmide.  
  
-   [Gráficos de intervalos &#40;relatórios e SSRS&#41;](range-charts-report-builder-and-ssrs.md): Os gráficos de ações, velas, barra de erros e gráfico de caixa.  
  
##  <a name="DataBars"></a> Barras de dados  
 Barras de dados geralmente representam um único ponto de dados, apesar de poderem representar vários pontos de dados, como os gráficos de barras normais. Normalmente contêm várias séries sem categoria ou possuem agrupamento de série.  
  
 ![rs_DataBars](../media/rs-databars.gif "rs_DataBars")  
  
 Neste exemplo que usa barras de dados empilhadas, cada barra de dados, embora somente uma barra, ilustra mais de um ponto de dados. Por exemplo, as três cores diferentes da barra poderiam representar tarefas de três níveis de prioridade com o comprimento da barra representando o número total de tarefas atribuídas a cada pessoa. Se você fez estas barras de dados 100% empilhadas, cada barra preencheria a célula e as cores diferentes representariam o percentual do todo para cada nível de prioridade.  
  
 Você pode fazer versões de barra de dados destes gráficos completos:  
  
-   [Gráficos de barras &#40;relatórios e SSRS&#41;](bar-charts-report-builder-and-ssrs.md): Gráficos de barras básicos, empilhados 100% empilhadas.  
  
-   [Gráficos de colunas &#40;relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md): Gráficos de coluna básicos, empilhados e 100% empilhados. Os gráficos de coluna podem ser minigráficos ou barras de dados.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Voltar ao início](#BackToTop)  
  
##  <a name="AlignDatainTableMatrix"></a> Alinhando dados de minigráfico em uma tabela ou matriz  
 Quando você insere um minigráfico em uma tabela ou matriz, é geralmente importante que os pontos de dados em cada minigráfico alinhem-se com os pontos de dados dos outros minigráficos naquela coluna. Caso contrário, será difícil comparar os dados nas linhas diferentes. Por exemplo, quando você compara dados de vendas por mês para vendedores diferentes em sua empresa, é importante que os meses estejam alinhados. Se um funcionário esteve fora durante o mês de abril, não haveria dados para aquele funcionário naquele mês. Você esperaria ver um intervalo para aquele mês e ver os dados durante os meses subsequentes alinhados com os dados para os outros funcionários. Você pode fazer isto alinhando o eixo horizontal. Para obter mais informações, consulte a seção sobre minigráficos em [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md) e consulte [Alinhar os dados de um gráfico em uma tabela ou matriz &#40;Construtor de Relatórios e SSRS&#41;](align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md).  
  
 Da mesma maneira, para estarem comparáveis por todas as linhas, os dados devem se alinhar também verticalmente, ou seja, a altura das barras ou linhas em um minigráfico ou barra de dados deve ser relativa à altura de barras e linhas em todos os outros minigráficos ou barras de dados. Caso contrário, você não poderá comparar as linhas entre si.  
  
 ![rs_SparklineAlignData](../media/rs-sparklinealigndata.gif "rs_SparklineAlignData")  
  
 Nesta imagem, o gráfico de coluna mostra vendas diárias para cada funcionário. Observe que, para os dias em que um funcionário não tem vendas, o gráfico deixa um espaço em branco e alinha os dias seguintes. Este é um exemplo de alinhamento horizontal. Também observe que, para alguns funcionários, toda barra é curta, e nenhuma barra alcança a parte superior da célula. Este é um exemplo de alinhamento vertical; sem isto, nas linhas sem barras altas, as barras curtas expandiriam para preencher a altura da célula.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Voltar ao início](#BackToTop)  
  
##  <a name="UnderstandScope"></a> Entendendo os dados fornecidos a um minigráfico ou barra de dados  
 Quando você adiciona um minigráfico ou barra de dados a uma tabela ou matriz, isso se chama *aninhar* uma região de dados dentro da outra. Aninhar significa que os dados fornecidos para o minigráfico ou barra de dados são controlados pelo conjunto de dados no qual a tabela ou matriz se baseia, e por onde você os coloca na tabela ou matriz. Para obter mais informações, consulte [Regiões de dados aninhadas &#40;Construtor de Relatórios e SSRS&#41;](nested-data-regions-report-builder-and-ssrs.md).  
  
##  <a name="ConvertSparklinetoChart"></a> Convertendo um minigráfico ou barra de dados a um gráfico completo  
 Como minigráficos e barras de dados são apenas um tipo de gráfico, se você decidir que prefere ter a funcionalidade de gráfico completo, faça a conversão clicando com o botão direito do mouse no gráfico e clicando em **Converter em Gráfico Completo**. Quando você fizer isso, as linhas de eixo, os rótulos, as marcas de escala e a legenda serão adicionados automaticamente.  
  
> [!NOTE]  
>  Você não pode converter um gráfico completo em um minigráfico ou barra de dados com um clique. Porém, você pode fazer um minigráfico ou barra de dados a partir de um gráfico completo bastando excluir todos os elementos de gráfico que não estão em minigráficos e barras de dados.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Voltar ao início](#BackToTop)  
  
##  <a name="HowTo"></a> Tópicos de instruções  
 [Adicionar minigráficos e barras de dados &#40;Construtor de Relatórios e SSRS&#41;](sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
 [Alinhar os dados de um gráfico em uma tabela ou matriz &#40;Construtor de Relatórios e SSRS&#41;](align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md)  
  
### <a name="other-how-to-topics-for-charts"></a>Outros tópicos de instruções para gráficos  
 Como minigráficos e barras de dados são um tipo de gráfico, você também pode achar os tópicos de instruções a seguir úteis e pertinentes:  
  
 [Adicionar um gráfico a um relatório &#40;Construtor de Relatórios e SSRS&#41;](add-a-chart-to-a-report-report-builder-and-ssrs.md)  
  
 [Adicionar pontos vazios ao gráfico &#40;relatórios e SSRS&#41;](add-empty-points-to-a-chart-report-builder-and-ssrs.md)  
  
 [Adicionar ou remover margens de um gráfico &#40;Construtor de Relatórios e SSRS&#41;](add-or-remove-margins-from-a-chart-report-builder-and-ssrs.md)  
  
 [Alterar um tipo de gráfico &#40;Construtor de Relatórios e SSRS&#41;](change-a-chart-type-report-builder-and-ssrs.md)  
  
 [Definir cores em um gráfico usando uma paleta &#40;Construtor de Relatórios e SSRS&#41;](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)  
  
 [Mostrar dicas de ferramenta em uma série &#40;Construtor de Relatórios e SSRS&#41;](show-tooltips-on-a-series-report-builder-and-ssrs.md)  
  
 [Especificar uma escala logarítmica &#40;Construtor de Relatórios e SSRS&#41;](specify-a-logarithmic-scale-report-builder-and-ssrs.md)  
  
 [Especificar um intervalo do eixo &#40;Construtor de Relatórios e SSRS&#41;](specify-an-axis-interval-report-builder-and-ssrs.md)  
  
 [Especificar cores consistentes em gráficos com várias formas &#40;Construtor de Relatórios e SSRS&#41;](shape-charts-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Consulte também  
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Tutorial: Adicionar um minigráfico ao relatório &#40;construtor de relatórios&#41;](../tutorial-add-a-sparkline-to-your-report-report-builder.md)   
 [Minigráficos, gráficos de barras e indicadores no construtor de relatórios (vídeo)](https://technet.microsoft.com/bi/video/ff877165)   
 [Como: Criar um minigráfico em uma tabela (vídeo)](https://go.microsoft.com/fwlink/?LinkId=197092)  
  
  
