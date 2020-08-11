---
title: Filtrar, agrupar e classificar dados (Construtor de Relatórios) | Microsoft Docs
description: Saiba mais sobre maneiras de controlar, organizar e classificar dados de relatório com expressões baseadas em campos de conjunto de dados, parâmetros no painel Dados do Relatório do Construtor de Relatórios.
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- sql13.rtp.rptdesigner.categorygroupproperties.general.f1
- "10403"
- sql13.rtp.rptdesigner.categorygroupproperties.sorting.f1
- sql13.rtp.rptdesigner.seriesgroupproperties.general.f1
- "10402"
- "10410"
- sql13.rtp.rptdesigner.seriesgroupproperties.sorting.f1
- "10412"
ms.assetid: 4dda2a7f-3f31-47e9-a88b-28d770ebd65e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: eca67966ff36c2100df7d46f07e150ed6aa32d1c
ms.sourcegitcommit: 02b22274da4a103760a376c4ddf26c4829018454
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681385"
---
# <a name="filter-group-and-sort-data-report-builder-and-ssrs"></a>Filtrar, agrupar e classificar dados (Construtor de Relatórios e SSRS)
  Em um relatório, as expressões são usadas para ajudar a controlar, organizar e classificar dados de relatório. Por padrão, quando você cria conjuntos de dados e cria o layout de relatório, as propriedades de itens de relatório são definidas automaticamente como expressões baseadas nos campos de conjuntos de dados, parâmetros e outros itens que aparecem no painel de dados do relatório. Também é possível adicionar um botão de classificação interativo a uma tabela ou célula de matriz para permitir que um usuário altere a ordem de classificação de linha interativamente para grupos ou linhas em grupos.  
  
-   **Expressões de filtro** Uma expressão de filtro testa dados para inclusão ou exclusão com base em uma comparação que você especifica. Os filtros são aplicados aos dados em um relatório depois que os dados são recuperados de uma conexão de dados. É possível adicionar qualquer combinação de filtros aos seguintes itens: uma definição de conjunto de dados compartilhada no servidor de relatório, uma instância de conjunto de dados compartilhada ou conjunto de dados incluído em um relatório, uma região de dados como uma tabela ou um gráfico ou um grupo de regiões de dados, como um grupo de linhas em uma tabela ou um grupo de categorias em um gráfico.  
  
-   **Expressões de grupo** Uma expressão de grupo organiza dados com base em um campo de conjunto de dados ou outro valor. As expressões de grupo são criadas automaticamente conforme você compila o layout de relatório. O processador de relatório avalia as expressões de grupo depois que os filtros são aplicados aos dados e conforme os dados de relatório e as regiões de dados são combinados. É possível personalizar uma expressão de grupo depois que ela é criada.  
  
-   **Expressões de classificação** Uma expressão de classificação controla a ordem na qual os dados aparecem em uma região de dados. As expressões de classificação são criadas automaticamente conforme você compila o layout de relatório. Por padrão, uma expressão de classificação para um grupo é definida com o mesmo valor que a expressão de grupo. É possível personalizar uma expressão de classificação depois que ela é criada.  
  
-   **Classificação interativa** Para permitir que um usuário classifique ou inverta a ordem de classificação de uma coluna, você pode adicionar um botão de classificação interativo a um cabeçalho de coluna ou célula de cabeçalho de grupo em uma tabela ou matriz.  
  
 Para ajudar seus usuários a personalizar o filtro, o grupo ou as expressões de classificação, você pode alterar uma expressão para adicionar uma referência a um parâmetro de relatório. Para obter mais informações, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
 Para obter mais informações e exemplos, consulte os seguintes tópicos:  
  
-   [Exemplos de expressões de grupo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)  
  
-   [Exemplos de equações de filtro &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)  
  
-   [Tutoriais do Construtor de Relatórios](../../reporting-services/report-builder-tutorials.md)  
  
-   [Tutoriais do Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)  
  
-   [Exemplos de relatório (Construtor de Relatórios e SSRS)](https://go.microsoft.com/fwlink/?LinkId=198283)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="filtering-data-in-the-report"></a><a name="Filtering"></a> Filtrando dados no relatório  
 Os filtros são partes de um relatório que ajuda a controlar dados de relatório depois que eles são recuperados da conexão de dados. Use os filtros quando você não puder alterar uma consulta de conjunto de dados para filtrar os dados antes que eles sejam recuperados de uma fonte de dados externa.  
  
 Quando possível, compile as consultas de conjunto de dados que retornem apenas os dados que você precisa exibir no relatório. Quando você reduz a quantidade dos dados que devem ser recuperados e processados, ajuda a melhorar o desempenho de relatório. Para obter mais informações, consulte [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
 Depois que os dados são recuperados da fonte de dados externa, é possível adicionar filtros a conjuntos de dados, regiões de dados e grupos de regiões de dados, inclusive grupos de detalhes. Os filtros são aplicados em tempo de execução, primeiro, no conjunto de dados, depois, na região de dados e, em seguida, no grupo, de cima para baixo nas hierarquias de grupo. Em uma tabela, matriz ou lista, os filtros para grupos de linha, grupos de coluna e grupos adjacentes são aplicados de forma independente. Em um gráfico, os filtros para grupos de categoria e grupos de série são aplicados de forma independente. Para obter mais informações, consulte [Adicionar filtros de conjunto de dados, de região de dados e de grupo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md).  
  
 Para cada filtro, você especifica uma *equação de filtro*. Uma equação de filtro inclui um campo de conjunto de dados ou expressão que especifica os dados a serem filtrados, um operador e um valor para comparação. Apenas esses valores de dados que correspondem à condição do filtro são incluídos quando o item é processado.  
  
 Para permitir que os usuários ajudem a controlar os dados em um relatório, você pode incluir parâmetros em expressões de filtro. Para obter mais informações, consulte [Referências de coleções de parâmetros &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md).  
  
 Para personalizar uma exibição para cada usuário, é possível incluir uma referência ao campo UserID interno em um filtro. Para obter mais informações, consulte [Referências de globais internas e referências de usuários &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).  
  
  
##  <a name="grouping-data-in-the-report"></a><a name="Grouping"></a> Agrupando dados no relatório  
 Os grupos organizam dados em um relatório para exibir ou calcular os valores de agregação. O entendimento de como definir grupos e usar recursos de grupos ajuda a criar relatórios mais concisos.  
  
 As expressões de grupo são criadas automaticamente quando você faz o seguinte:  
  
-   Organiza campos de conjuntos de dados em um assistente de Tabela, Matriz, Gráfico ou campos de correspondência no assistente de Mapa.  
  
-   Em uma tabela, matriz ou lista, adicione um campo à área Grupos de Linhas ou Grupos de Colunas no painel Agrupamento.  
  
-   Em um gráfico, adicione um campo à área Grupos de Categorias ou de Grupos de Séries no painel de Dados do gráfico.  
  
-   Em um mapa, especifique um campo para corresponder a elementos de mapas com dados analíticos no item de menu de contexto Dados da Camada.  
  
 Um grupo é uma parte da definição de relatório. Cada grupo tem um nome. Por padrão, o nome de grupo é o campo de conjunto de dados no qual ele se baseia.  
  
 Em uma região de dados de tabela ou matriz, é possível criar vários grupos de linhas e de colunas. Você pode exibir seus dados em uma hierarquia visual organizando grupos aninhados, grupos adjacentes e grupos de hierarquia recursiva (como um organograma).  
  
 O nome de grupo identifica um escopo de expressão. Você pode especificar o nome de um grupo como um escopo no qual calcular agregações, organizar dados hierarquicamente e alternar a exibição para nós filho de nós pai em um relatório detalhado, mostrar exibições diferentes dos mesmos dados em várias regiões de dados e visualizar dados resumidos em uma tabela, matriz, gráfico, medidor ou mapa. Para obter mais informações, consulte [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Para agrupar em vários campos de conjunto de dados, adicione cada campo ao conjunto de expressões de grupo. Você também pode escrever suas próprias expressões de grupo em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. Por exemplo, você pode agrupar por um intervalo de valores ou usar um parâmetro de relatório para permitir que os usuários selecionem como agrupar os dados em uma região de dados. Para obter mais informações, consulte [Exemplos de expressões de grupo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md).  
  
 Para a apresentação do relatório, você pode adicionar quebras de página antes ou depois de cada grupo, ou de cada instância de um grupo, para reduzir a quantidade de dados em cada página e ajudar a gerenciar o desempenho da renderização do relatório. Para obter mais informações, consulte [Adicionar uma quebra de página &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-page-break-report-builder-and-ssrs.md).  
  
 A criação de grupos de regiões de dados é um modo de organizar dados em um relatório. Há vários outros modos de organizar dados, cada um com suas vantagens. Para obter mais informações, consulte [Detalhamento, busca detalhada, sub-relatórios e regiões de dados aninhadas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md).  
  
### <a name="defining-group-variables"></a>Definindo variáveis de grupo  
 Ao definir um grupo, você pode criar uma variável de grupo para usar em expressões cujo escopo seja o grupo e que seja acessada nos grupos aninhados. Uma variável de grupo é calculada uma vez por instância de grupo e é acessada de expressões em grupos filho. Por exemplo, para dados agrupados por região e sub-região, é possível calcular um imposto para cada região e usar esse imposto em cálculos do grupo de sub-regiões.  
  
 Para obter mais informações, consulte [Referências de coleções de variáveis de grupo e de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
### <a name="groups-and-scope-in-data-regions"></a>Grupos e escopo em regiões de dados  
 Para fornecer várias exibições de dados do mesmo conjunto de dados, é possível especificar as mesmas expressões de grupo para cada região de dados. Por exemplo, é possível exibir dados categorizados em uma tabela para mostrar todos os dados detalhados e em um gráfico de pizza para mostrar agregações e ajudar a visualizar cada categoria em relação ao conjunto de dados inteiro. Para obter mais informações, consulte [Vinculando várias regiões de dados ao mesmo conjunto de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md).  
  
 Quando você aninha uma região de dados em uma célula de uma tabela, matriz ou lista, automaticamente está definindo o escopo dos dados como as associações de grupo internas da célula. Por exemplo, suponha que você adicione um gráfico a uma célula que está tanto no grupo de linhas quanto no grupo de colunas. O escopo dos dados disponíveis do gráfico é a instância de grupo de linhas internas e de colunas internas em tempo de execução. Para obter mais informações, consulte [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
  
##  <a name="sorting-data-in-the-report"></a><a name="Sorting"></a> Classificando dados no relatório  
 Para controlar a ordem de classificação dos dados no relatório, é possível classificar dados em uma consulta de conjunto de dados ou definir uma expressão de classificação para um grupo ou região de dados. Você também pode adicionar botões de classificação interativos a tabelas e matrizes para permitir que um usuário altere a ordem das linhas.  
  
 Todos os três tipos de classificação podem ser combinados no mesmo relatório. Por padrão, a ordem de classificação é determinada pela ordem em que os dados são retornados pela consulta de conjunto de dados. As expressões de classificação são aplicadas na região de dados e no grupo de regiões de dados. As classificações interativas são aplicadas depois das expressões de classificação.  
  
 Para expressões que contêm funções de agregação, a maioria dos resultados não é afetada pela ordem de classificação. Os valores de retorno para as seguintes funções de agregação são afetados pela ordem de classificação: Primeiro, Último e Anterior. Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md).  
  
### <a name="sorting-data-in-a-dataset-query"></a>Classificando dados em uma consulta de conjunto de dados  
 Inclua a ordem de classificação na consulta de conjunto de dados para pré-classificar os dados antes que eles sejam recuperados para um relatório. Com a classificação de dados na consulta, o trabalho de classificação é feito pela fonte de dados em vez de pelo processador de relatório.  
  
 Para um tipo de fonte de dados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é possível adicionar uma cláusula ORDER BY à consulta de conjunto de dados. Por exemplo, a seguinte consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] classifica as colunas Sales e Region por Sales em ordem decrescente na tabela SalesOrders: `SELECT Sales, Region FROM SalesOrders ORDER BY Sales DESC`.  
  
> [!NOTE]  
>  Nem todas as fontes de dados dão suporte à capacidade de especificar a ordem de classificação na consulta.  
  
### <a name="sorting-data-with-sort-expressions"></a>Classificando dados com expressões de classificação  
 Para classificar dados no relatório após ele ser recuperado da fonte de dados, você pode definir expressões de classificação em um grupo ou em uma região de dados Tablix, incluindo o grupo de detalhes. A lista a seguir descreve o efeito da definição de expressões de classificação em diferentes itens:  
  
-   **Região de dados Tablix.** Defina expressões de classificação em uma tabela, matriz ou região de dados de lista para controlar a ordem de classificação dos dados na região de dados, após os filtros do conjunto de dados e da região de dados serem aplicados em tempo de execução.  
  
-   **Grupo de região de dados Tablix.** Defina expressões de classificação para cada grupo, incluindo o grupo de detalhes, para controlar a ordem de classificação de instâncias do grupo. Por exemplo, para o grupo de detalhes, você controla a ordem das linhas de detalhes. Para um grupo filho, você controla a ordem das instâncias do grupo filho dentro do grupo pai. Por padrão, quando você cria um grupo, a expressão de classificação é definida para a expressão de grupo e para a ordem crescente.  
  
     Se você tiver apenas um grupo de detalhes, poderá definir uma expressão de classificação na consulta, na região de dados ou no grupo de detalhes para obter o mesmo efeito.  
  
-   **Região de dados do gráfico.** Defina uma expressão de classificação para os grupos de categorias e de séries para controlar a ordem de classificação dos pontos de dados. Por padrão, a ordem dos pontos de dados também é a ordem das cores na legenda do gráfico. Para obter mais informações, consulte [Formatando as cores da série em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md).  
  
-   **Item de relatório de mapa.** Em geral, não é necessário classificar os dados para uma região de dados de mapa porque o mapa agrupa os dados para exibir em elementos de mapas.  
  
-   **Região de dados do medidor.** Normalmente, não é necessário classificar dados para uma região de dados do medidor porque ele exibe um único valor relativo para um intervalo. Se forem necessários dados de classificação em um medidor, você deverá definir um grupo primeiro e, em seguida, definir uma expressão de classificação para o grupo.  
  
#### <a name="sorting-by-a-different-value"></a>Classificando por um valor diferente  
 Talvez você queira classificar as linhas em uma região de dados por um valor que não seja o valor de campo. Por exemplo, suponha que o Tamanho do campo contenha valores de texto que correspondem a pequeno, médio, grande e extra grande. Por padrão, a expressão de classificação para uma linha de grupo se baseia em Tamanho que também é [Tamanho]. Para ter mais controle sobre a forma como os dados são classificado, é possível adicionar um campo à consulta do conjunto de dados que define a ordem de classificação desejada.  
  
 Se desejar, você pode definir um conjunto de dados que inclua apenas os tamanhos e um valor que especifique a ordem desejada. É possível alterar a expressão de classificação para usar a função Pesquisar para obter o valor de ordem de classificação.  
  
 Por exemplo, digamos que a consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir defina um conjunto de dados chamado Tamanhos. A consulta usa uma instrução CASE para definir um valor de ordem de classificação SizeSortOrder para obter cada valor de Tamanho:  
  
```  
SELECT Size,   
  CASE Size  
        WHEN 'S' THEN 1  
        WHEN 'M' THEN 2    
        WHEN 'L' THEN 3  
        WHEN 'XL' THEN 4  
        ELSE 0  
  END as SizeSortOrder  
FROM Production.Product  
```  
  
 Em uma tabela com um grupo de linhas baseado em `[Size]`, é possível alterar a expressão de classificação de grupo para usar uma função Pesquisar a fim de localizar o campo numérico que corresponde ao valor de tamanho. A expressão seria semelhante a esta:  
  
```  
=Lookup(Fields!Size.Value, Fields!Size.Value, Fields!SizeSortOrder.Value, "Sizes")  
```  
  
 Para obter mais informações, consulte [Classificar dados em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md) e [Função de pesquisa &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookup-function.md).  
  
###  <a name="adding-interactive-sorting-for-the-user"></a><a name="Interactive"></a> Adicionando classificação interativa para o usuário  
 Para permitir que um usuário altere a ordem de classificação de dados de relatório em uma tabela ou matriz, você pode adicionar botões de classificação interativos a cabeçalhos de coluna e cabeçalhos de grupo. Os usuários podem clicar no botão para alterar a ordem de classificação. A classificação interativa possui suporte em formatos de renderização que permitem a interação do usuário, como HTML.  
  
 Você adiciona botões de classificação interativos a uma caixa de texto em uma célula de região de dados tablix. Por padrão, toda célula contém uma caixa de texto. Nas propriedades da caixa de texto, você especifica qual parte de uma região de dados de tabela ou matriz classificar (os valores do grupo pai, os valores do grupo filho ou as linhas de detalhes), pelo que classificar, e se a expressão de classificação deve ser aplicada a outros itens de relatório que têm uma relação par. Por exemplo, se uma tabela e um gráfico que fornecem exibições sobre o mesmo conjunto de dados estiverem contidos em um retângulo, eles serão regiões de dados pares. Quando um usuário alterna a ordem de classificação na tabela, a ordem de classificação do gráfico também é alternada. Para obter mais informações, consulte [Classificação interativa e &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/interactive-sort-report-builder-and-ssrs.md).  
  
  
##  <a name="how-to-topics"></a><a name="HowTo"></a> Tópicos de instruções  
 [Manter os cabeçalhos visíveis ao rolar por um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
 [Exibir cabeçalhos e rodapés com um grupo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)  
  
 [Adicionar classificação interativa a uma tabela ou matriz &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)  
  
 [Definir uma mensagem Nenhum Dado para uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/set-a-no-data-message-for-a-data-region-report-builder-and-ssrs.md)  
  
 [Criar um grupo de hierarquia recursiva &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/create-a-recursive-hierarchy-group-report-builder-and-ssrs.md)  
  
 [Adicionar ou excluir um grupo em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)  
  
 [Exibir cabeçalhos e rodapés com um grupo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)  
  
 [Adicionar ou excluir um grupo em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-chart-report-builder-and-ssrs.md)  
  
 [Adicionar um total a um grupo ou a uma região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md)  
  
##  <a name="in-this-section"></a><a name="Section"></a> Nesta seção  
 [Exemplos de expressões de grupo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)  
  
 [Exemplos de equações de filtro &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)  
  
 [Adicionar filtros de conjunto de dados, de região de dados e de grupo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)  
  
##  <a name="related-sections"></a><a name="Related"></a> Seções relacionadas  
 [Noções básicas sobre grupos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)  
  
 [Criar grupos de hierarquia recursiva &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)  
  
 [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
 [Referências de coleções de variáveis de grupo e de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md)  
  
 [Como exibir uma série com vários intervalos de dados em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/displaying-a-series-with-multiple-data-ranges-on-a-chart.md)  
  
 [Vinculando várias regiões de dados ao mesmo conjunto de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Mapas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [Minigráficos e barras de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)   
 [Medidores &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)   
 [Indicadores &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
