---
title: Adicionar visualizações a relatórios móveis do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 09/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: mobile-reports
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3b220b74-9ecd-4084-93fb-545208d5d7a2
caps.latest.revision: 15
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: be7412693c221c8436e0751414c5c615b6d23448
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="add-visualizations-to-reporting-services-mobile-reports"></a>Adicionar visualizações a relatórios móveis do Reporting Services
Os gráficos são uma parte essencial da visualização de dados. Saiba mais sobre os gráficos que você pode usar nos relatórios móveis do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] para cobrir diversos cenários. 

[!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-long.md)] tem três tipos de gráficos básicos: hora, categoria e totais. Esses três tipos de gráficos contêm gráficos de comparação correspondentes, que são úteis para comparar dois conjuntos de série distintos.  

## <a name="shared-chart-properties"></a>Propriedades de gráfico compartilhadas

Algumas propriedades se aplicam a todos os gráficos e outras somente a gráficos específicos. Estas são algumas das propriedades compartilhadas.

### <a name="number-format"></a>Formato de número
Você pode atribuir uma variedade de formatos a números em um gráfico do [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] – por exemplo, geral, moeda, com ou sem casas decimais, percentuais com e sem casas decimais e assim por diante. Em um gráfico, a formatação de número se aplica a anotações de eixo, bem como a pop-ups de ponto de dados. Você define a formatação de número em cada gráfico individualmente, não no relatório móvel como um todo. 

* Para definir o formato de número, selecione a guia **Layout** , selecione um gráfico na superfície de design e no painel **Propriedades visuais** , selecione um **Formato de número**. 
  
### <a name="legend"></a>Legenda
* Para mostrar a legenda de um gráfico, selecione a guia **Layout** , selecione um gráfico na superfície de design e, no painel **Propriedades visuais** , defina **Mostrar legenda** como **Ativado**
  
### <a name="series"></a>Série
Cada métrica ou valor individual exibido em um gráfico é conhecido como uma série: várias séries podem e compartilham um eixo x e y em comum. A série é definida no painel de propriedades de dados da exibição de dados, selecionando uma ou mais tabelas de dados e campos. Cada campo resultará em uma série individual de pontos de dados na visualização do gráfico com sua própria cor.  

### <a name="change-aggregation"></a>Agregação de alteração 
Para campos numéricos em gráficos, a agregação padrão é soma. Você pode alterá-lo para média, contagem, mínimo, máximo, primeiro ou último.

* Selecione a guia **Dados** e, em **Propriedades de dados**, selecione **Opções** ao lado do campo numérico > selecione uma agregação diferente.

### <a name="set-or-clear-filters"></a>Definir ou limpar filtros

Se você adicionar um navegador para filtrar o relatório móvel, poderá decidir quais gráficos você quer filtrar.

1. Selecione a guia **Dados** e, em **Propriedades de dados**, selecione **Opções**.

2. Em **Filtrado por**, você vê os navegadores que você pode marcar ou desmarcar.

Leia mais sobre [como adicionar navegadores para filtrar um relatório móvel](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md).
   
## <a name="time-charts"></a>Gráficos de tempo  
  
O gráfico de tempo é o gráfico mais básico do [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)]. O eixo de hora (e data) do gráfico é definido automaticamente para o primeiro campo de data/hora válido na tabela de dados.  

![mobile-report-time-chart](../../reporting-services/mobile-reports/media/mobile-report-time-chart.png)

1. Arraste um **Gráfico em tempo** da guia **Layout** para a superfície de design e redimensione-o.

2. Por padrão, ele é um gráfico de barras empilhadas. É possível alterar isso em **Visualização da série**.

3. Se o gráfico precisar de dados que ainda não estão no relatório, selecione a guia **Dados** > **Adicionar dados** para [obter dados do Excel ou de um conjunto de dados compartilhado](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md).

3. No painel **Propriedades de dados** , a **Série Principal** é **SimulatedTable**. Clique a seta na caixa > selecione a tabela.

5. Se você definir **Estrutura de dados** como **Por colunas** (na guia **Layout** > painel **Propriedades de visual**), no painel **Propriedades de dados**, poderá selecionar várias colunas de valores numéricos.

   Se você definir **Estrutura de dados** como **Por linhas**, aqui no painel **Propriedades de dados** , você poderá selecionar um **Campo de Nome da Série** e uma coluna de valores numéricos.
   
Leia mais sobre [como agrupar dados por colunas ou linhas](../../reporting-services/mobile-reports/group-data-by-columns-or-rows-in-a-mobile-report-reporting-services.md).
  
## <a name="category-charts"></a>Gráficos de categoria  
  
Ao contrário de um gráfico de tempo, em um gráfico de categoria, você agrupa um campo que não é um campo de data/hora no eixo x. Esse agrupamento, chamado de *coordenada de categoria*, precisa estar em um campo de cadeia de caracteres, não em um campo numérico.

![mobile-report-category-chart](../../reporting-services/mobile-reports/media/mobile-report-category-chart.png)   

1. Arraste um **Gráfico de categoria** da guia **Layout** para a superfície de design, redimensione-o e [obtenha dados para ele](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md), se necessário.

2. Selecione a guia **Dados** e, no painel **Propriedades de dados** , em **coordenada de categoria**, selecione uma tabela e um campo para o agrupamento. Este campo ficará no eixo x do gráfico resultante.

3. Em **Série Principal**, selecione a tabela e os campos numéricos a serem agregados para cada categoria. 
  
## <a name="totals-charts"></a>Gráfico de totais  

![mobile-report-totals-chart](../../reporting-services/mobile-reports/media/mobile-report-totals-chart.png)
  
Gráfico de totais realiza duas coisas distintas: 
* Ele não apresenta várias séries – apenas a soma ou o total da série principal definida. 
* Ele oferece a opção para agrupar dados por colunas ou linhas. Agrupar por colunas pode ser útil ao lidar com dados bidimensionais. Ao agrupar por colunas, apenas a propriedade da série principal está disponível, pois a coluna de categoria é determinada automaticamente pelo número de campos selecionados para a propriedade da série principal.  

Leia mais sobre [como agrupar dados por colunas ou linhas](../../reporting-services/mobile-reports/group-data-by-columns-or-rows-in-a-mobile-report-reporting-services.md). 
  
## <a name="comparison-charts"></a>Gráficos de comparação  
  
Gráficos de tempo, categoria e totais também estão disponíveis como *gráficos de comparação*. Em um gráfico de comparação, você pode especificar não apenas uma série principal, mas também uma segunda série de comparação. A série principal e a comparação podem ser exibidas de três maneiras diferentes.

![mobile-report-comparison-time-chart](../../reporting-services/mobile-reports/media/mobile-report-comparison-time-chart.png)

1. Arraste um dos **Gráficos de comparação** (tempo, categoria ou totais) da guia **Layout** para a superfície de design, redimensione-o e [obtenha dados para ele](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md), se necessário.

2. No painel **Propriedades visuais** , em **Visualização da série**, selecione um dos seguintes: 
   * Barra versus barra fina
   * Linha versus barra
   * Barra versus área de etapa 

Em gráficos de comparação, você pode optar por ter as mesmas cores do gráfico nos valores principal e de comparação de uma série.

* No painel **Propriedades visuais** , defina **Reutilizar cores na série de comparação** para **Ativado**.

   Se for definido como **Ativado**, a paleta de cores será reiniciada entre o desenho das séries principal e de comparação e, portanto, os valores relacionados nas séries principal e de comparação serão os mesmos. 

   Se for definido como **Desativado**, a paleta de cores continuará sua rotação normal ao desenhar a série principal após a série de comparação, impedindo a coordenação de cores potencialmente confusa entre os dois conjuntos da série.  
  
## <a name="pie-and-funnel-charts"></a>Gráficos de pizza e de funil  
  
Gráficos de pizza e funil estão entre as visualizações mais simples. Você pode estruturar os dados por linhas ou colunas. 
* Os **gráficos de pizza** nos relatórios móveis do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] podem ser pizza, rosca ou rosca com um total no centro. Os gráficos de pizza são úteis para mostrar o tamanho relativo das diferentes partes de um todo. Um número excessivo de fatias dificulta a leitura.
* Em geral, os**gráficos de funil** são usados para mostrar os estágios de um processo, como vendas.

![mobile-report-funnel-chart](../../reporting-services/mobile-reports/media/mobile-report-funnel-chart.png)

### <a name="structure-pie-and-funnel-chart-data-by-rows-or-by-columns"></a>Estruturar dados do gráfico de pizza e de funil por linhas ou colunas
1. Arraste um **Gráfico de pizza** ou um **Gráfico de funil** da guia **Layout** para a superfície de design, redimensione-o e [obtenha dados para ele](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md), se necessário.
2. No painel **Propriedades visuais** , em **Estrutura de dados**, selecione:
   * **Por colunas**
   * **Por linhas**
3. Se você selecionou **Por colunas**, selecione a guia **Dados** e, no painel **Propriedades de dados** em **Série Principal**, selecione a tabela e todos os campos que você quer agregar no gráfico de pizza ou de funil. Os nomes de campo serão usados para rotular cada área do gráfico resultante.

   Se você selecionou **Por linhas**, selecione a guia **Dados** e, no painel **Propriedades de dados** em **Coluna da Categoria**, selecione a tabela e a coluna com os valores a serem usados para o agrupamento e os rótulos da pizza. Em Coluna da Série Principal, selecione um campo numérico para os valores no gráfico.

Leia mais sobre [como agrupar dados por colunas ou linhas](../../reporting-services/mobile-reports/group-data-by-columns-or-rows-in-a-mobile-report-reporting-services.md). 

## <a name="treemaps"></a>Mapas de árvore  
  
Os mapas de árvore exibem métricas aplicando seus valores ao tamanho e à cor dos blocos em uma grade retangular. 

![mobile-report-group-treemap](../../reporting-services/mobile-reports/media/mobile-report-group-treemap.png)

1. Arraste um **Mapa de árvore** da guia **Layout** para a superfície de design, redimensione-o e [obtenha dados para ele](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md), se necessário.
2.  Selecione a guia **Dados** e, no painel **Propriedades de dados** : 

     * Em **O Tamanho Representa** , selecione um campo numérico para o tamanho dos blocos.
     * Em **A Cor Representa** , selecione um campo numérico para a cor dos blocos. 
     * [opcional] **Valor central personalizado**: só é possível usar o **Valor central personalizado** quando o tipo de visualização é HeatMapWithCustomCenterValue.
     
         O valor central decide a cor de uma caixa. Quanto melhor a métrica comparada ao valor central, mais verde ela ficará. Quanto pior a métrica, mais vermelha ela ficará.
     
     * [opcional] Para exibir um pop-up quando os visualizadores selecionarem um bloco na grade, em **Rótulos Pop-up** , selecione um ou mais campos. Os pop-ups do mapa de árvore podem exibir campos de texto e campos numéricos.  

Por padrão, os mapas de árvore são hierárquicos, agrupando os blocos por categoria primeiramente e, em seguida, por tamanho e cor.
* Ainda na guia **Dados** , em **Agrupar por** , selecione uma tabela e um campo.

Você pode desativar o agrupamento, para que os blocos sejam organizados somente por tamanho e cor. 

* Selecione a guia **Layout** e defina **Mapa de árvore de dois níveis** para **Desativado**.   

## <a name="waterfall-charts"></a>Gráficos de cascata

Um gráfico de cascata mostra um total cumulativo à medida que os valores são adicionados ou subtraídos. Ele é útil para entender como um valor inicial (por exemplo, receita líquida) é afetado por uma série de alterações positivas e negativas.

As colunas são codificadas com a cor verde para aumentos e com vermelho para subtrações, assim você pode identificar rapidamente. As colunas de valor inicial final geralmente começam em zero, enquanto os valores intermediários são colunas flutuante. Devido a essa "aparência", os gráficos de cascata também são chamados de gráficos de ponte.

### <a name="when-to-use-a-waterfall-chart"></a>Quando usar um gráfico de cascata

Os gráficos de cascata são uma boa opção:
* Quando houver alterações na medição em séries de tempo, ou categorias diferentes para auditar as principais alterações que contribuem com o valor total.
* Para plotar lucros anuais de sua empresa mostrando várias fontes de receita e chegar ao lucro (ou perda) total.
* Para ilustrar o início e o fim da força de trabalho final de sua empresa em um ano.
* Para visualizar a quantidade de dinheiro produzida e gasta todo mês, e o balanço de sua conta. 

### <a name="create-a-waterfall-chart"></a>Criar um gráfico de cascata

1. Arraste um **Gráfico de cascata** da guia **Layout** para a superfície de design, redimensione-o e [obtenha dados para ele](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md), se necessário.

    ![mobile-report-waterfall-chart-icon](../../reporting-services/mobile-reports/media/mobile-report-waterfall-chart-icon.png)
    
2.  Selecione a guia **Dados** e, no painel **Propriedades de Dados** , selecione um campo de categoria em seus dados para **Coordenada de Categoria**, e um campo numérico para **Série Principal**: 

    ![mobile-report-waterfall-data](../../reporting-services/mobile-reports/media/mobile-report-waterfall-data.png)
    
3. Selecione a guia **Layout** para ver o gráfico de cascata na visualização.

   ![mobile-report-waterfall-chart](../../reporting-services/mobile-reports/media/mobile-report-waterfall-chart.png)
   
   Os meses com perda, como fevereiro, junho e julho, estão em vermelho. 
   Os meses com ganho, como setembro, outubro e novembro, estão em verde. 

## <a name="see-also"></a>Confira também 
* [Mapas nos relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Navegadores nos relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)
* [Grades de dados nos relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/add-data-grids-to-mobile-reports-reporting-services.md)
* [Medidores nos relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)
  

