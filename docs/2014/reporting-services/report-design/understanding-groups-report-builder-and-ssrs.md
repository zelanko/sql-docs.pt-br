---
title: Noções básicas sobre grupos (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10056"
- "10424"
ms.assetid: c32d4d89-45e4-4f77-a3e9-0429f53f9d6f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ccdef0ccb338f268abd205a95421382eb554fce9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66104534"
---
# <a name="understanding-groups-report-builder-and-ssrs"></a>Compreendendo grupos (Construtor de Relatórios e SSRS)
  No Construtor de Relatórios, um grupo é um conjunto nomeado de dados do conjunto de dados de relatório associado a uma região de dados. Basicamente, um grupo organiza uma exibição de um conjunto de dados de relatório. Todos os grupos de uma região de dados especificam exibições diferentes do mesmo conjunto de dados de relatório.  
  
 Para ajudar a visualizar o que é um grupo, consulte a figura a seguir, que mostra a região de dados tablix em Visualização. Nessa figura, os grupos de linhas categorizam o conjunto de dados por tipo de produto e os grupos de colunas categorizam o conjunto de dados por região geográfica e ano.  
  
 ![Áreas da região de dados Tablix](../media/rs-tablixareas.gif "Áreas da região de dados Tablix")  
  
 As seguintes seções ajudam a descrever os vários aspectos dos grupos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="what-makes-a-group"></a>O que forma um grupo?  
 Um grupo apresenta um nome e um conjunto de expressões de grupo especificados por você. O conjunto de expressões de grupo pode ser uma referência de campo de conjunto de dados única ou uma combinação entre várias expressões. Em runtime, as expressões de grupo são combinadas, se o grupo tiver várias expressões, e for aplicado a dados em um grupo. Por exemplo, você tem um grupo que usa um campo de data para organizar os dados na região de dados. Em tempo de execução, os dados são organizados por data e exibem com os totais outros valores do conjunto de dados para cada data.  
  
## <a name="when-do-i-create-groups"></a>Quando crio grupos?  
 Na maior parte dos casos, o Construtor de Relatórios e o Designer de Relatórios criam automaticamente um grupo quando você cria uma região de dados. Para uma tabela, matriz ou lista, são criados grupos quando você descarta campos no painel Agrupamento. Para um gráfico, são criados grupos quando você descarta campos nas áreas para arrastar e soltar do gráfico. Para um medidor, você deve usar a caixa de diálogo de propriedades do medidor. Para uma tabela, matriz ou lista, também é possível criar manualmente um grupo. Para obter mais informações, consulte [Adicionar ou excluir um grupo em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md). Para obter um exemplo de como adicionar grupos ao criar um relatório, consulte [Tutorial: Criando um relatório de tabela básico &#40;Construtor de Relatórios&#41;](../tutorial-creating-a-basic-table-report-report-builder.md) ou [Criar um relatório de tabela básico &#40;Tutorial do SSRS&#41;](../create-a-basic-table-report-ssrs-tutorial.md).  
  
## <a name="how-can-i-modify-a-group"></a>Como posso modificar um grupo?  
 Após a criação de um grupo, é possível definir propriedades específicas da região de dados como, por exemplo, expressões de filtro e de classificação, quebras de página e variáveis do grupo para manter dados específicos do escopo. Para obter mais informações, consulte [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
 Para modificar um grupo existente, abra a caixa de diálogo de propriedades do grupo apropriada. É possível alterar o nome do grupo. Além disso, você pode especificar expressões de grupo com base em um ou em vários campos, ou em um parâmetro de relatório que especifica um valor em tempo de execução. Também é possível basear um grupo em um conjunto de expressões como, por exemplo, o conjunto de expressões que especificam faixas etárias referentes a dados demográficos. Para obter mais informações, consulte [Exemplos de expressões de grupo &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  Caso altere o nome de um grupo, você deve atualizar manualmente todas as expressões do grupo que se referem ao nome anterior do grupo.  
  
## <a name="how-are-groups-organized"></a>Como os grupos são organizados?  
 Compreender a organização do grupo pode ajudar você a criar regiões de dados que mostrem exibições diferentes dos mesmos dados, especificando expressões de grupo idênticas.  
  
 Os grupos são organizados internamente como membros de uma ou mais hierarquias de cada região de dados. Uma hierarquia tem grupos pai/filho que são aninhados e pode apresentar grupos adjacentes.  
  
 Se você considerar os grupos pai/filho como uma estrutura de árvore, cada hierarquia do grupo é uma floresta de estruturas de árvore. Uma região de dados tablix inclui uma hierarquia de grupo de linhas e uma hierarquia de grupo de colunas. Os dados associados a membros de grupo de linhas se expandem horizontalmente na página e os dados associados a membros de grupo de colunas, verticalmente pela página. O painel Agrupamento exibe membros dos grupos de linhas e de colunas referentes à região de dados tablix selecionada na superfície de design. Para obter mais informações, consulte [Painel Agrupamento &#40;Construtor de Relatórios&#41;](grouping-pane-report-builder.md).  
  
 Uma região de dados do gráfico inclui hierarquias do grupo de categorias do grupo de séries. São exibidos membros do grupo de categorias no eixo de categoria e os membros do grupo de séries no eixo de série.  
  
 Embora normalmente não sejam necessários a regiões de dados do medidor, os grupos permitem especificar como agrupar dados a serem agregados ao medidor.  
  
## <a name="what-types-of-groups-are-available-per-data-region"></a>Quais são os tipos de grupos disponíveis por região de dados?  
 Regiões de dados que se expandem como uma grade dão suporte a grupos diferentes daqueles que têm o suporte de regiões de dados que exibem dados resumidos visualmente. Portanto, uma região de dados tablix, bem como as tabelas, listas e matrizes baseadas nessa região dão suporte a grupos diferentes daqueles que têm o suporte de um gráfico ou medidor. As seguintes seções abordam o tipo e a finalidade do agrupamento em cada tipo de região de dados.  
  
> [!NOTE]  
>  Embora os grupos tenham nomes diferentes em regiões de dados diferentes, os princípios por trás de como você cria e usa grupos são os mesmos. Ao criar um grupo para uma região de dados, você especifica uma forma de organizar os dados detalhados do conjunto vinculado à região. Cada região de dados oferece suporte a uma estrutura de grupo em que os dados agrupados são exibidos.  
  
### <a name="groups-in-a-tablix-data-region-details-row-and-column-groups"></a>Grupos em uma região de dados tablix: grupos de detalhes, de linhas e de colunas  
 Como mostrado anteriormente neste tópico, uma região de dados tablix permite organizar os dados em grupos por linhas ou colunas. No entanto, os grupos de linhas e de colunas não são os únicos disponíveis em uma região de dados tablix. Essa região de dados pode ter os seguintes tipos de grupo:  
  
-   **Grupo Detalhes** O grupo Detalhes consiste em todos os dados de um conjunto de dados de relatório depois que o Construtor de Relatórios ou o Designer de Relatórios aplica filtros de conjunto de dados e de região de dados. Dessa forma, o grupo Detalhes é o único que não tem nenhuma expressão de grupo.  
  
     Basicamente, o grupo de detalhes especifica os dados que você veria quando executasse uma consulta de conjunto de dados em um designer de consulta. Por exemplo, você tem uma consulta que recupera todas as colunas de uma tabela com pedidos de venda. Por isso, os dados desse grupo de detalhes incluem todos os valores referentes a todas as linhas de todas as colunas na tabela. Os dados desse grupo de detalhes também incluem valores referentes a campos de conjunto de dados calculados criados por você.  
  
    > [!NOTE]  
    >  Os dados em um grupo Detalhes também podem incluir agregações de servidor, que são calculadas na fonte de dados e recuperadas na consulta. Por padrão, o Construtor de Relatórios e o Designer de Relatórios tratam agregações de servidor como dados detalhados, a menos que o relatório inclua uma expressão que use a função Aggregate. Para obter mais informações, consulte [Agregação](report-builder-functions-aggregate-function.md).  
  
     Por padrão, quando você adiciona uma tabela ou lista ao relatório, o Construtor de Relatórios e o Designer de Relatórios criam automaticamente o grupo Detalhes e adicionam uma linha para exibir os dados detalhados. Por padrão, ao adicionar campos de conjunto de dados a células nessa linha, você vê expressões simples referentes aos campos; por exemplo, [Sales]. Quando você exibe a região de dados, a linha detalhada se repete uma vez para todos os valores do conjunto de resultados.  
  
-   **Grupos de linhas e de colunas** É possível organizar dados em grupos por linhas ou colunas. Os grupos de linhas se expandem verticalmente em uma página. Os grupos de colunas se expandem horizontalmente em uma página. Os grupos podem ser aninhados, por exemplo, primeiro por [Year] e depois por [Quarter] e por [Month]. Os grupos também podem ser adjacentes, por exemplo, em [Territory] e independentemente em [ProductCategory].  
  
     Quando você cria um grupo para uma região de dados, o Construtor de Relatórios e o Designer de Relatórios adicionam automaticamente linhas ou colunas à região de dados e usam essas linhas ou colunas para exibir dados de grupo.  
  
-   **Grupos de hierarquia recursiva** Um grupo de hierarquia recursiva organiza os dados de um único conjunto de dados de relatório que inclui vários níveis. Por exemplo, um grupo de hierarquia recursiva pode exibir a hierarquia de uma organização, como [Employee] que se reporta a [Employee]. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece propriedades de grupo e funções internas para permitir a criação de grupos para esse tipo de dados de relatório. Para obter mais informações, consulte [Criar grupos de hierarquias recursivas &#40;Construtor de Relatórios e SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
 A seguinte lista resume a maneira com que você trabalha com grupos de cada região de dados:  
  
-   **Tabela** Define grupos de linhas aninhados, grupos de linhas adjacentes e grupos de linhas de hierarquia recursiva (como, por exemplo, em um organograma). Por padrão, uma tabela inclui um grupo detalhado. Adicione grupos arrastando campos de conjunto de dados para o painel Agrupamento referente a uma tabela selecionada.  
  
-   **Matriz** Define grupos de linhas e de colunas aninhados e adjacentes. Adicione grupos arrastando campos de conjunto de dados para o painel Agrupamento referente a uma matriz selecionada.  
  
-   **Lista** Por padrão, ela oferece suporte ao grupo detalhado. O uso típico é para oferecer suporte a um nível de agrupamento. Adicione grupos arrastando campos de conjunto de dados para o painel Agrupamento referente a uma lista selecionada.  
  
 Depois que você adiciona um grupo, os identificadores de linha e de coluna da região de dados são alterados para refletir a associação a um grupo. Ao excluir um grupo, você tem a opção de excluir apenas a definição de grupo ou excluir o grupo e todas as linhas e colunas associadas. Para obter mais informações, consulte [Células, linhas e colunas da região de dados Tablix &#40;Construtor de Relatórios&#41; e SSRS](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
 Para limitar os dados a serem exibidos ou usados em cálculos para detalhar ou agrupar dados, defina filtros no grupo. Para obter mais informações, consulte [Adicionar filtros de conjunto de dados, de região de dados e de grupo &#40;Construtor de Relatórios e SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md).  
  
 Por padrão, quando você cria um grupo, a expressão de classificação do grupo é igual à expressão de grupo. Para alterar a ordem de classificação, altere a expressão de classificação. Para obter mais informações, consulte [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
#### <a name="understanding-group-membership-for-tablix-cells"></a>Compreendendo a associação de grupo para células tablix  
 As células de uma linha ou coluna de uma região de dados tablix podem pertencer a vários grupos de linhas e de colunas. Quando você define uma expressão na caixa de texto de uma célula que usa uma função de agregação (por exemplo, `=Sum(Fields!FieldName.Value`), o escopo do grupo padrão de uma célula é o grupo filho mais interno ao qual ele pertence. Quando uma célula pertence a grupos de linhas e de colunas, o escopo é ambos os grupos internos. Também é possível escrever expressões que calculam subtotais de agregação cujo escopo é um grupo relativo a outro conjunto de dados. Por exemplo, você pode calcular a porcentagem de um grupo em relação ao grupo de colunas ou a todos os dados da região de dados (como `=Sum(Fields!FieldName.Value)/Sum(Fields!FieldName.Value,"ColumnGroup")`). Para obter mais informações, consulte [Região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar ou excluir um grupo em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)   
 [Adicionar um total a um grupo ou a uma região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md)   
 [Classificar dados em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [Ação de análise detalhada &#40;Construtor de Relatórios e SSRS&#41;](drilldown-action-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
