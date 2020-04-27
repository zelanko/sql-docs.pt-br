---
title: Escopo de expressão para totais, agregações e coleções internas (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a8d24287-8557-4b03-bea7-ca087f449b62
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b8d9838306090cf219fed799c5982481ac3365a9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66105920"
---
# <a name="expression-scope-for-totals-aggregates-and-built-in-collections-report-builder-and-ssrs"></a>Escopo das expressões para totais, agregações e coleções internas (Construtor de Relatórios e SSRS)
  Quando você escrever expressões, descobrirá que o termo *escopo* é usado em vários contextos. O escopo pode especificar os dados a serem usados para avaliar uma expressão, o conjunto de caixas de texto em uma página renderizada, o conjunto de itens de relatório que podem ser mostrados ou ocultados com base em uma alternância. Você verá o termo *escopo* em tópicos relacionados a avaliações de expressão, sintaxe de função de agregação, visibilidade condicional e também em mensagens de erro relacionadas a estas áreas. Use as descrições a seguir para diferenciar qual significado de *escopo* se aplica:  
  
-   **Escopo de dados** É uma hierarquia de escopos que o processador de relatório usa ao se associar a dados de relatório e layout de relatório, e ao criar regiões de dados como tabelas e gráficos nos quais exibe os dados. Entender escopo de dados ajuda a obter os resultados desejados quando você fizer o seguinte:  
  
    -   **Escreva expressões que usam funções de agregação** Especifique quais dados devem ser agregados. O local da expressão no relatório influencia quais dados estarão no escopo para cálculos de agregação.  
  
    -   **Adicione minigráficos a uma tabela ou matriz** Especifique um intervalo mínimo e máximo para os eixos de gráfico alinharem instâncias aninhadas em uma tabela ou matriz.  
  
    -   **Adicione indicadores a uma tabela ou matriz** Especifique uma escala mínima e máxima para o medidor alinhar instâncias aninhadas em uma tabela ou matriz.  
  
    -   **Escreva expressões de classificação** Especifique um escopo de conteúdo que você possa usar para sincronizar a ordem de classificação entre vários itens de relatório relacionados.  
  
-   **Escopo de célula** É o conjunto de grupos de linhas e colunas em uma região de dados tablix à qual a célula pertence. Por padrão, cada célula tablix contém uma caixa de texto. O valor da caixa de texto é a expressão. O local da célula determina indiretamente quais escopos de dados você pode especificar para cálculos de agregação na expressão.  
  
-   **Escopo de item de relatório** Refere-se à coleção de itens em uma página de relatório renderizada. O processador do relatório combina dados e elementos de layout de relatório para produzir uma definição de relatório compilada. Durante este processo, as regiões de dados como tabelas e matrizes expandem-se conforme o necessário para exibir todos os dados do relatório. O relatório compilado é processado por um renderizador de relatório. O renderizador de relatório determina quais itens de relatório aparecem em cada página. Em um servidor de relatório, cada página é renderizada à medida que é visualizada. Ao exportar um relatório, todas as páginas são renderizadas. Entender escopo de item de relatório ajuda a obter os resultados desejados quando você fizer o seguinte:  
  
    -   **Adicione itens de alternância** Especifique uma caixa de texto para adicionar a alternância que controla a visibilidade de um item de relatório. Você somente poderá adicionar uma alternância a caixas de texto que estiverem no escopo do item de relatório que você deseja ativar /desativar.  
  
    -   **Escreva expressões em cabeçalhos e rodapés de página** Especifique valores em expressões em caixas de texto ou outros itens de relatório que aparecem na página renderizada.  
  
 Entender escopos ajuda a escrever expressões corretas que darão os resultados desejados.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="understanding-data-scope-and-data-hierarchy"></a><a name="DataScope"></a> Entendendo escopo de dados e hierarquia de dados  
 O escopo de dados especifica um conjunto de dados de relatório. O escopo de dados possui uma hierarquia natural com uma relação de contenção inerente. Escopos mais alto na hierarquia contêm escopos que são mais baixos na hierarquia. A lista de escopos de dados a seguir descreve a hierarquia de mais dados para menos dados:  
  
-   **Conjunto de dados, após a aplicação dos filtros de conjunto de dados** Especifica o conjunto de dados do relatório vinculado à região de dados ou a um item de relatório no corpo do relatório. Os dados usados para agregação são do conjunto de dados do relatório após as expressões de filtro de conjunto de dados serem aplicadas. Para conjuntos de dados compartilhados, isto significa os filtros na definição do conjunto de dados compartilhado e os filtros na instância do conjunto de dados compartilhada no relatório.  
  
-   **Regiões de dados** Especifica os dados da região de dados após as expressões de filtro e classificação serem aplicadas. Filtros de grupo não são usados ao calcular agregações para regiões de dados.  
  
-   **Grupos de região de dados, após serem aplicados os filtros de grupo** Especifica os dados após as expressões e os filtros de grupo serem aplicadas para os grupos pai e filho. Para uma tabela, esses são os grupos de linhas e colunas. Para um gráfico, esses são os grupos de séries e categorias. Para fins de identificação de contenção do escopo, cada grupo pai contém seus grupos filho.  
  
-   **Regiões de dados aninhadas** Especifica os dados da região de dados aninhada no contexto da célula para a qual eles foram adicionados e após as expressões de filtro e de classificação de região de dados aninhados tiverem sido aplicadas.  
  
-   **Grupos de linhas e colunas para as regiões de dados aninhadas** Especifica os dados após as expressões e os filtros de grupo de regiões de dados aninhadas terem sido aplicados.  
  
 Entender escopos de conteúdo e contidos é importante ao escrever expressões que incluem funções de agregação.  
  
##  <a name="cell-scope-and-expressions"></a><a name="Aggregates"></a> Escopo de célula e expressões  
 Ao especificar um escopo, você está indicando ao processador de relatório quais dados deseja usar para um cálculo de agregação. Dependendo da expressão e do local da expressão, escopos válidos podem ser *escopos de conteúdo*, também conhecidos como escopos pai, ou *escopos contidos*, também conhecidos como escopos filho ou aninhados. Em geral, você não pode especificar uma instância de grupo individual em um cálculo de agregação. Você pode especificar uma agregação em todas as instâncias de grupo.  
  
 Como o processador de relatório combina dados de um conjunto de dados de relatório com a região de dados tablix, ele avalia expressões de grupo e cria as linhas e as colunas necessárias para representar as instâncias de grupo. O valor de expressões em uma caixa de texto em cada célula do tablix é avaliado no contexto do escopo de célula. Dependendo da estrutura do tablix, uma célula pode pertencer a vários grupos de linhas e de colunas. Para funções de agregação, você pode especificar qual escopo desejado usando um dos escopos seguintes:  
  
-   **Escopo padrão** Os dados que estão no escopo para cálculo quando o processador de relatório avaliar uma expressão. O escopo padrão é o conjunto de grupos interno ao qual os pontos de células ou dados pertencem. Para uma região de dados do tablix, o conjunto pode incluir grupos de linhas e de colunas. Para uma região de dados do gráfico, o conjunto pode incluir grupos de categoria e série.  
  
-   **Escopo nomeado** O nome de um conjunto de dados, uma região de dados ou um grupo de região de dados que está no escopo para a expressão. Para cálculos de agregação, é possível especificar um escopo de conteúdo. Não é possível especificar um escopo nomeado para um grupo de linhas e colunas em uma única expressão. Você não pode especificar um escopo contido a menos que a expressão seja para uma agregação de uma agregação.  
  
     A expressão a seguir gera os anos de intervalo entre SellStartDate e LastReceiptDate. Esses campos estão em dois conjuntos de dados diferentes, DataSet1 e DataSet2. A [Função First &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-first-function.md), que é uma função de agregação, retorna o primeiro valor de SellStartDate em DataSet1 e o primeiro valor de LastReceiptDate em DataSet2.  
  
    ```  
    =DATEDIFF("yyyy", First(Fields!SellStartDate.Value, "DataSet1"), First(Fields!LastReceiptDate.Value, "DataSet2"))  
    ```  
  
-   **Escopo de domínio** Também chamado de escopo de sincronização. Um tipo de escopo de dados que se aplica à avaliação de expressão para regiões de dados aninhadas. O escopo de domínio é usado para especificar agregações em todas as instâncias de um grupo, de modo que instâncias aninhadas possam ser alinhadas e facilmente comparadas. Por exemplo, você pode alinhar o intervalo e a altura para minigráficos inseridos em uma tabela, de modo que os valores fiquem alinhados.  
  
 Em alguns locais de um relatório, você deve especificar um escopo. Por exemplo, para uma caixa de texto na superfície de design, você deve especificar o nome do conjunto de dados a ser usado: `=Max(Fields!Sales.Value,"Dataset1")`. Em outros locais, há um escopo padrão implícito. Por exemplo, se você não especificar uma agregação para uma caixa de texto em um escopo de grupo, a agregação padrão Primeira será usada.  
  
 Cada tópico de função de agregação lista os escopos que são válidos para uso. Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md).  
  
##  <a name="example-aggregate-expressions-for-a-table-data-region"></a><a name="Examples"></a> Expressões de agregação de exemplo para uma região de dados de tabela  
 Escrever expressões que especificam escopos não padrão exige alguma prática. Para ajudar a entender escopos diferentes, use a figura e a tabela a seguir. A figura rotula cada célula em uma tabela de informações de vendas que exibe a quantidade de itens vendidos por ano e trimestre, e também por território de vendas. Observe as sugestões visuais nos identificadores de linha e coluna que exibem a estrutura de grupo de linha e coluna, indicando grupos aninhados. A tabela possui a seguinte estrutura:  
  
-   Um cabeçalho de tabela que contém a célula de canto e três linhas que incluem os cabeçalhos de grupo de coluna.  
  
-   Dois grupos de linhas aninhados com base na categoria chamada Cat e na subcategoria chamada SubCat.  
  
-   Dois grupos de colunas aninhados com base no ano chamado Year e trimestre chamado Qtr.  
  
-   Uma coluna estática de totais rotulada de Totals.  
  
-   Um grupo de colunas adjacente com base no território de vendas chamado Territory.  
  
 O cabeçalho de coluna para o grupo de território foi dividido em duas células para fins de exibição. A primeira célula exibe o nome do território e os totais, e a segunda célula possui texto do espaço reservado que calculou a contribuição percentual de cada território para todas as vendas.  
  
 ![rs_BasicTableSumCellScope](../media/rs-basictablesumcellscope.gif "rs_BasicTableSumCellScope")  
  
 Suponha que o conjunto de dados seja chamado DataSet1 e a tabela seja chamada Tablix1. A tabela a seguir lista o rótulo de célula, o escopo padrão e exemplos. Os valores para texto do espaço reservado são mostrados em sintaxe de expressão.  
  
|Célula|Escopo padrão|Rótulos de espaço reservado|Texto ou valores de espaço reservado|  
|----------|-------------------|------------------------|--------------------------------|  
|C01|Tablix1|[Sum(Qty)]|Agregações e escopo<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C02|Grupo "Year" de colunas externas|[Year]<br /><br /> ([YearQty])|`=Fields!Year.Value`<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C03|Tablix1|[Sum(Qty)]|Totals<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C04|Grupo "Territory" de colunas pares|([Total])|Territory<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C05|Grupo "Qtr" interno|[Qtr]<br /><br /> ([QtrQty])|Q<br /><br /> `=Fields!Qtr.Value`<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C06|Grupo "Territory" de colunas pares|[Territory]<br /><br /> ([Tty])<br /><br /> [Pct]|`=Fields!Territory.Value`<br /><br /> `=Sum(Fields!Qty.Value)`<br /><br /> `=FormatPercent(Sum(Fields!Qty.Value,"Territory")/Sum(Fields!Qty.Value,"Tablix1"),0) & " of " & Sum(Fields!Qty.Value,"Tablix1")`|  
|C07|Grupo "Cat" de linhas externas|[Cat]<br /><br /> [Sum(Qty)]|`=Fields!Cat.Value`<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C08|O mesmo que C07|||  
|C09|Grupo "Cat" de linhas externas e grupo "Qtr" de colunas internas|[Sum(Qty)]|`=Sum(Fields!Qty.Value)`|  
|C10|O mesmo que C07|<\<Expr>>|`=Sum(Fields!Qty.Value) & ": " & FormatPercent(Sum(Fields!Qty.Value)/Sum(Fields!Qty.Value,"Tablix1"),0) & " of " & Sum(Fields!Qty.Value,"Tablix1")`|  
|C11|Grupo "Cat" de linhas externas e grupo "Territory" de colunas|<\<Expr>>|`=Sum(Fields!Qty.Value) & ": " & FormatPercent(Sum(Fields!Qty.Value)/Sum(Fields!Qty.Value,"Territory"),0) & " of " & Sum(Fields!Qty.Value,"Territory")`|  
|C12|Grupo "Subcat" de linhas internas|[Subcat]<br /><br /> [Sum(Qty)]|`=Fields!SubCat.Value`<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C13|Grupo "Subcat" de linhas internas e grupo "Qtr" de colunas internas|[Sum(Qty)]|`=Sum(Fields!Qty.Value)`|  
|C14|Grupo "Subcat" de linhas internas|<\<Expr>>|`=Sum(Fields!Qty.Value) & ": " & FormatPercent(Sum(Fields!Qty.Value)/Sum(Fields!Qty.Value,"Cat"),0) & " of " & Sum(Fields!Qty.Value,"Cat")`|  
|C15|Grupo "Subcat" de linhas internas e grupo "Territory" de colunas|<\<Expr>>|`=Sum(Fields!Qty.Value) & ": " & FormatPercent(Code.CalcPercentage(Sum(Fields!Qty.Value),Sum(Fields!Qty.Value,"Cat")),0) & " of " & Sum(Fields!Qty.Value,"Cat")`|  
  
 Para obter mais informações sobre como interpretar indicações visuais nas regiões de dados tablix, consulte [Células, linhas e colunas da região de dados Tablix &#40;Construtor de Relatórios&#41; e SSRS](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md). Para obter mais informações sobre a região de dados Tablix, consulte [Células, linhas e colunas da região de dados Tablix &#40;Construtor de Relatórios&#41; e SSRS](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md). Para obter mais informações, consulte [Expressão Uses em relatórios &#40;Construtor de Relatórios e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md) e [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md).  
  
  
  
##  <a name="synchronizing-scales-for-sparklines"></a><a name="Sparklines"></a> Sincronizando escalas para minigráficos  
 Para comparar valores por tempo no eixo horizontal para um gráfico de minigráfico que é aninhado em uma tabela ou matriz, você pode sincronizar os valores de grupo de categorias. Isto é chamado de alinhar eixos. Ao selecionar a opção para alinhar eixos, o relatório automaticamente define os valores mínimo e máximo para um eixo e fornece espaços reservados para valores de agregação que não existem em todas as categorias. Isto faz os valores no minigráfico se alinharem em todas as categorias e permite comparar valores para cada linha de dados agregados. Ao selecionar esta opção, você está alterando o escopo da avaliação de expressão para o *escopo de domínio*. Definir o escopo de domínio para um gráfico aninhado também controla indiretamente a atribuição de cores para cada categoria na legenda.  
  
 Por exemplo, em um minigráfico que mostra tendências semanais, suponha que uma cidade tenha dados de vendas por 3 meses e outra cidade tenha dados de vendas por 12 meses. Sem escalas sincronizadas, o minigráfico para a primeira cidade teria somente 3 barras e elas seriam muito mais largas e ocupariam o mesmo espaço que o conjunto de barras de 12 meses para a segunda cidade.  
  
 Para obter mais informações, consulte [Alinhar os dados de um gráfico em uma tabela ou matriz &#40;Construtor de Relatórios e SSRS&#41;](align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md).  
  
  
  
##  <a name="synchronizing-ranges-for-indicators"></a><a name="Indicators"></a> Sincronizando intervalos para indicadores  
 Para especificar os valores de dados a serem usados para um conjunto de indicadores, você deve especificar um escopo. Dependendo do layout da região de dados que contém o indicador, especifique um escopo ou um escopo de conteúdo. Por exemplo, em uma linha de cabeçalho de grupo associada a vendas de categoria, um conjunto de setas (para cima, para baixo, para os lados) pode indicar valores de vendas relativos a um limite. O escopo de conteúdo é o nome da tabela ou matriz que contém os indicadores.  
  
 Para obter mais informações, consulte [Definir o escopo da sincronização &#40;Construtor de Relatórios e SSRS&#41;](set-synchronization-scope-report-builder-and-ssrs.md).  
  
  
  
##  <a name="specifying-scopes-from-the-page-header-or-page-footer"></a><a name="Page"></a> Especificando escopos a partir do cabeçalho ou rodapé de página  
 Para exibir dados que são diferentes em cada página de um relatório, adicione expressões a um item de relatório que deve estar na página renderizada. Como um relatório é dividido em páginas enquanto é renderizado, somente durante a renderização podem ser determinados quais itens existem em uma página. Por exemplo, uma célula em uma linha de detalhes possui uma caixa de texto que tem muitas instâncias em uma página.  
  
 Para este propósito, existe uma coleção global chamada ReportItems. Este é o conjunto de caixas de texto na página atual.  
  
 Para obter mais informações, consulte [Cabeçalhos e rodapés de página &#40;Construtor de Relatórios e SSRS&#41;](page-headers-and-footers-report-builder-and-ssrs.md) e [Referências da coleção ReportItems &#40;Construtor de Relatórios e SSRS&#41;](built-in-collections-reportitems-collection-references-report-builder.md).  
  
  
  
##  <a name="specifying-a-toggle-item-for-drilldown-and-conditional-visibility"></a><a name="Toggles"></a> Especificando um item de alternância para busca detalhada e visibilidade condicional  
 Alternâncias são sinais de adição ou subtração adicionados a uma caixa de texto e nos quais um usuário pode clicar para mostrar ou ocultar outros itens de relatório. Na página **Visibilidade** para a maioria das propriedades de item de relatório, você pode especificar a qual item de relatório deseja adicionar a alternância. O item de alternância deve estar em um escopo de contenção mais alto que o item para mostrar ou ocultar.  
  
 Em uma região de dados do tablix, para criar um efeito de busca detalhada em que você clica em uma caixa de texto para expandir a tabela e mostrar mais dados, você deve definir a propriedade **Visibilidade** no grupo e selecionar como alternância uma caixa de texto em um cabeçalho de grupo que é associado a um grupo de conteúdo.  
  
 Para obter mais informações, consulte [Adicionar uma ação de expandir/recolher a um item &#40;Construtor de Relatórios e SSRS&#41;](add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md).  
  
  
  
##  <a name="specifying-a-sort-expression-to-synchronize-sort-order"></a><a name="Sort"></a> Especificando uma expressão de classificação para sincronizar a ordem de classificação  
 Ao adicionar um botão de classificação interativo a uma coluna de tabela, você pode sincronizar a classificação para vários itens que têm um escopo de conteúdo comum. Por exemplo, você pode adicionar um botão de classificação a um cabeçalho de coluna em uma matriz e especificar o escopo de conteúdo como o nome do conjunto de dados que é associado à matriz. Quando um usuário clicar no botão de classificação, não somente as linhas da matriz serão classificadas, mas também os grupos de série de gráficos que são associados ao mesmo conjunto de dados. Deste modo, todas as regiões de dados que dependem daquele conjunto de dados podem ser sincronizadas para apresentar a mesma ordem de classificação.  
  
 Para obter mais informações, consulte [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
  
  
##  <a name="suppressing-null-or-zero-values-in-a-cell"></a><a name="Nulls"></a> Suprimindo valores nulos ou zeros em uma célula  
 Para muitos relatórios, cálculos com escopo de grupos podem criar muitas células que têm valores nulos ou zeros (0). Para reduzir a desordem em relatórios, adicione uma expressão para retornar espaços em branco se o valor de agregação for 0. Para obter mais informações, consulte "Exemplos que suprimem valores nulos ou zeros" em [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md).  
  
  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Exemplos de expressões de grupo &#40;Construtor de Relatórios e SSRS&#41;](group-expression-examples-report-builder-and-ssrs.md)   
 [Criar grupos de hierarquia recursiva &#40;Construtor de Relatórios e SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)   
 [Lista &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Formatando texto e espaços reservados &#40;Construtor de Relatórios e SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)  
  
  
