---
title: Minigráficos e barras de dados (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- sql13.rtp.rptdesigner.sparklines.f1
- "10544"
ms.assetid: b287436b-fa48-4970-a1a7-1dbcb86e7411
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 71458d579b710b282f75fd10d4006b737632d266
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47710814"
---
# <a name="sparklines-and-data-bars-report-builder-and-ssrs"></a>Minigráficos e barras de dados (Construtor de Relatórios e SSRS)
  Minigráficos e barras de dados são gráficos pequenos e simples que transmitem muitas informações em um espaço pequeno, geralmente embutidas com o texto.   
    
  No [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , os minigráficos e as barras de dados são usados em tabelas e matrizes. Seu impacto resulta da possibilidade de exibir vários deles juntos e compará-los uns sobre os outros, em vez de exibi-los individualmente. Eles facilitam a visualização das exceções, as linhas cujo desempenho se distingue das outras. Embora sejam pequenos, cada minigráfico costuma representar vários pontos de dados, geralmente durante um período de tempo. As barras de dados podem representar vários pontos de dados, mas normalmente ilustram apenas um. Cada minigráfico geralmente apresenta uma única série. Você não pode adicionar um minigráfico a um grupo de detalhes em uma tabela. Como os minigráficos exibem dados agregados, eles devem entrar em uma célula associada a um grupo. Minigráficos e barras de dados têm os mesmos elementos de gráficos básicos de categorias, séries e valores, mas não possuem legenda, linhas de eixo, rótulos nem marcas de escala.  
  
 ![rs_SparklineExample](../../reporting-services/report-design/media/rs-sparklineexample.gif "rs_SparklineExample")  
  
 Como introdução rápida aos minigráficos, consulte [Tutorial: Adicionar um minigráfico ao relatório &#40;Construtor de Relatórios&#41;](../../reporting-services/tutorial-add-a-sparkline-to-your-report-report-builder.md) e os vídeos [Como criar um minigráfico em uma tabela](http://go.microsoft.com/fwlink/?LinkId=197092) e [Minigráficos, gráficos de barras e indicadores no Construtor de Relatórios](http://technet.microsoft.com/bi/video/ff877165) .  
  
> [!NOTE]  
>  Você pode publicar minigráficos e barras de dados com suas tabelas, matrizes ou lista pai, separadamente de um relatório como uma parte de relatório. Leia mais sobre as [Partes do relatório](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md).  
  
##  <a name="KindsofSparklines"></a> Tipos de minigráficos  
 Você pode criar praticamente tantos tipos de minigráficos quanto gráficos normais. Em geral, você não pode fazer minigráficos em 3D. Você pode fazer versões de minigráfico destes gráficos completos:  
  
-   [Gráficos de colunas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md): os gráficos de coluna básicos, empilhados e 100% empilhados.  
  
-   [Gráficos de linhas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/line-charts-report-builder-and-ssrs.md): todos os gráficos, exceto o gráfico de linhas 3D.  
  
-   [Gráficos de áreas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/area-charts-report-builder-and-ssrs.md): todos os gráficos, exceto o gráfico de áreas 3D  
  
-   [Gráficos de pizza &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md): e gráficos de rosca, simples e 3D, mas não as outras formas como gráficos de funil e de pirâmide.  
  
-   [Gráficos de intervalo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/range-charts-report-builder-and-ssrs.md): as ações, velas, barra de erros e gráficos de caixa.  
  
##  <a name="DataBars"></a> Barras de dados  
 Barras de dados geralmente representam um único ponto de dados, apesar de poderem representar vários pontos de dados, como os gráficos de barras normais. Normalmente contêm várias séries sem categoria ou possuem agrupamento de série.  
  
 ![rs_DataBars](../../reporting-services/report-design/media/rs-databars.gif "rs_DataBars")  
  
 Neste exemplo que usa barras de dados empilhadas, cada barra de dados, embora somente uma barra, ilustra mais de um ponto de dados. Por exemplo, as três cores diferentes da barra poderiam representar tarefas de três níveis de prioridade com o comprimento da barra representando o número total de tarefas atribuídas a cada pessoa. Se você fez estas barras de dados 100% empilhadas, cada barra preencheria a célula e as cores diferentes representariam o percentual do todo para cada nível de prioridade.  
  
 Você pode fazer versões de barra de dados destes gráficos completos:  
  
-   [Gráficos de barras &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md): os gráficos de barras básicos, empilhados e 100% empilhados.  
  
-   [Gráficos de colunas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md): os gráficos de coluna básicos, empilhados e 100% empilhados. Os gráficos de coluna podem ser minigráficos ou barras de dados.  
  
##  <a name="AlignDatainTableMatrix"></a> Alinhando dados de minigráfico em uma tabela ou matriz  
 Quando você insere um minigráfico em uma tabela ou matriz, é geralmente importante que os pontos de dados em cada minigráfico alinhem-se com os pontos de dados dos outros minigráficos naquela coluna. Caso contrário, será difícil comparar os dados nas linhas diferentes. Por exemplo, quando você compara dados de vendas por mês para vendedores diferentes em sua empresa, é importante que os meses estejam alinhados. Se um funcionário esteve fora durante o mês de abril, não haveria dados para aquele funcionário naquele mês. Você esperaria ver um intervalo para aquele mês e ver os dados durante os meses subsequentes alinhados com os dados para os outros funcionários. Você pode fazer isto alinhando o eixo horizontal. Para obter mais informações, consulte a seção sobre minigráficos em [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md) e consulte [Alinhar os dados de um gráfico em uma tabela ou matriz &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md).  
  
 Da mesma maneira, para estarem comparáveis por todas as linhas, os dados devem se alinhar também verticalmente, ou seja, a altura das barras ou linhas em um minigráfico ou barra de dados deve ser relativa à altura de barras e linhas em todos os outros minigráficos ou barras de dados. Caso contrário, você não poderá comparar as linhas entre si.  
  
 ![rs_SparklineAlignData](../../reporting-services/report-design/media/rs-sparklinealigndata.gif "rs_SparklineAlignData")  
  
 Nesta imagem, o gráfico de coluna mostra vendas diárias para cada funcionário. Observe que, para os dias em que um funcionário não tem vendas, o gráfico deixa um espaço em branco e alinha os dias seguintes. Este é um exemplo de alinhamento horizontal. Também observe que, para alguns funcionários, toda barra é curta, e nenhuma barra alcança a parte superior da célula. Este é um exemplo de alinhamento vertical; sem isto, nas linhas sem barras altas, as barras curtas expandiriam para preencher a altura da célula.  
  
##  <a name="UnderstandScope"></a> Entendendo os dados fornecidos a um minigráfico ou barra de dados  
 Quando você adiciona um minigráfico ou barra de dados a uma tabela ou matriz, isso se chama *aninhar* uma região de dados dentro da outra. Aninhar significa que os dados fornecidos para o minigráfico ou barra de dados são controlados pelo conjunto de dados no qual a tabela ou matriz se baseia, e por onde você os coloca na tabela ou matriz. Para obter mais informações, consulte [Regiões de dados aninhadas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md).  
  
##  <a name="ConvertSparklinetoChart"></a> Convertendo um minigráfico ou barra de dados a um gráfico completo  
 Como minigráficos e barras de dados são apenas um tipo de gráfico, se você decidir que prefere ter a funcionalidade de gráfico completo, faça a conversão clicando com o botão direito do mouse no gráfico e clicando em **Converter em Gráfico Completo**. Quando você fizer isso, as linhas de eixo, os rótulos, as marcas de escala e a legenda serão adicionados automaticamente.  
  
> [!NOTE]  
>  Você não pode converter um gráfico completo em um minigráfico ou barra de dados com um clique. Porém, você pode fazer um minigráfico ou barra de dados a partir de um gráfico completo bastando excluir todos os elementos de gráfico que não estão em minigráficos e barras de dados.  
  
##  <a name="HowTo"></a> Tópicos de instruções  
 [Adicionar minigráficos e barras de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
 [Alinhar os dados de um gráfico em uma tabela ou matriz &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md)  
  
### <a name="other-how-to-topics-for-charts"></a>Outros tópicos de instruções para gráficos  
 Como minigráficos e barras de dados são um tipo de gráfico, você também pode achar os tópicos de instruções a seguir úteis e pertinentes:  
  
 [Adicionar um gráfico a um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md)  
  
 [Adicionar pontos vazios a um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-empty-points-to-a-chart-report-builder-and-ssrs.md)  
  
 [Adicionar ou remover margens de um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-or-remove-margins-from-a-chart-report-builder-and-ssrs.md)  
  
 [Alterar um tipo de gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/change-a-chart-type-report-builder-and-ssrs.md)  
  
 [Definir cores em um gráfico usando uma paleta &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)  
  
 [Mostrar dicas de ferramenta em uma série &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)  
  
 [Especificar uma escala logarítmica &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/specify-a-logarithmic-scale-report-builder-and-ssrs.md)  
  
 [Especificar um intervalo do eixo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/specify-an-axis-interval-report-builder-and-ssrs.md)  
  
 [Especificar cores consistentes em gráficos com várias formas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Tutorial: Adicionar um minigráfico ao relatório &#40;Construtor de Relatórios&#41;](../../reporting-services/tutorial-add-a-sparkline-to-your-report-report-builder.md)   
  
  
