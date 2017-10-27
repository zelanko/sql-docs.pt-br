---
title: "Adicionando dados a uma região de dados Tablix (Construtor de Relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8f1d0a76-afed-480f-98fb-89e2d4eb09b1
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b6f41b4d1b42db5ca020841f9363df3f4cf3eb99
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="adding-data-to-a-tablix-data-region-report-builder-and-ssrs"></a>Adicionando dados a uma região de dados Tablix (Construtor de Relatórios e SSRS)
Em relatórios paginados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , para exibir dados de um conjunto de dados de relatório em uma tabela ou matriz, em cada célula de dados, especifique o nome de um campo do conjunto de dados a ser exibido. É possível exibir dados de detalhes ou dados agrupados. Se você adicionar grupos a uma tabela ou matriz, linhas e colunas para valores de grupo e dados de grupo serão adicionados automaticamente. Em seguida, é possível adicionar subtotais e totais aos dados.  
  
 Todos os dados em uma região de dados pertencem a pelo menos um grupo. Dados de detalhes são membros do grupo de detalhes. Para obter mais informações sobre dados agrupados e detalhes, [Noções básicas sobre grupos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="adding-detail-data"></a>Adicionando dados de detalhes  
 Dados de detalhes são todos os dados de um conjunto de dados de relatório depois da aplicação de filtros ao conjunto de dados, região de dados e grupo de detalhes. Todos os dados de detalhes exibidos em uma única região de dados tablix devem vir do mesmo conjunto de dados de relatório.  
  
 Para adicionar dados de detalhes de um conjunto de dados de relatório a uma região de dados tablix, arraste um campo do conjunto de dados do painel de dados do relatório para cada célula na linha de detalhes. Para células existentes em uma região de dados tablix, é possível adicionar ou editar uma expressão de conjunto de dados usando o seletor de campo em cada célula ou arrastando um campo do painel de dados do relatório para a célula. Para criar colunas adicionais, você pode arrastar o campo do painel de dados do relatório e inseri-lo em uma região de dados tablix existente.  
  
 Por padrão, em tempo de execução, uma célula na linha de detalhes exibe dados de detalhes e uma célula em uma linha de grupo exibe um valor de agregação. Para obter mais informações sobre as linhas e colunas tablix, consulte [Células, linhas e colunas da região de dados Tablix &#40;Construtor de Relatórios&#41; e SSRS](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
 Um modelo de tabela e um modelo de lista fornecem uma linha de detalhes. Um modelo de matriz não tem nenhuma linha de detalhes. Se sua região de dados tablix não tiver nenhuma linha de detalhes, você poderá adicionar uma linha definindo um grupo de detalhes. Para obter mais informações, consulte [Adicionar um grupo de detalhes &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-details-group-report-builder-and-ssrs.md).  
  
## <a name="adding-grouped-data"></a>Adicionando dados agrupados  
 Dados agrupados são todos os dados de detalhes especificados por uma expressão de grupo depois da aplicação de filtros ao conjunto de dados, região de dados e o grupo. Para organizar dados de detalhes em grupos, arraste campos do painel de dados do relatório para o painel Agrupamento. Quando você adiciona um grupo, o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] adiciona automaticamente linhas ou colunas relacionadas à região de dados tablix na qual exibir dados agrupados. As células dessas linhas ou colunas são associadas aos dados agrupados. Para obter mais informações, consulte [Adicionar ou excluir um grupo em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md).  
  
 Por padrão, quando você adiciona um campo de conjunto de dados que representa dados numéricos a uma célula em uma linha ou coluna do grupo, o valor da célula é a soma dos dados agrupados com o escopo das associações do grupo de linhas e colunas da célula. É possível alterar a função de agregação padrão Sum para qualquer outra função de agregação, como Avg ou Count. Também é possível alterar o escopo padrão para um cálculo de agregação, por exemplo, para calcular a porcentagem de contribuição de um valor para um grupo de linhas. Para obter mais informações, consulte [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Por padrão, todos os dados agrupados vêm do mesmo conjunto de dados de relatório. Em uma região de dados tablix, é possível incluir valores de agregação de outro conjunto de dados especificando o nome do conjunto de dados como um escopo. É possível especificar vários valores de agregação de vários conjuntos de dados dentro de uma única região de dados tablix. Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md).  
  
## <a name="adding-subtotals-and-totals"></a>Adicionando subtotais e totais  
 Para adicionar subtotais a um grupo e totais gerais à região de dados, use o recurso Adicionar Total no menu de atalho em uma célula ou no painel Agrupamento. As linhas e colunas nas quais exibir os totais são automaticamente adicionadas para você. Expressões de subtotais e totais são padronizadas usando a função de agregação [Sum](../../reporting-services/report-design/report-builder-functions-sum-function.md) . Depois de adicionar a expressão, é possível alterar a função padrão. Para obter mais informações, consulte [Adicionar um total a um grupo ou a uma região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="adding-labels"></a>Adicionando rótulos  
 Para adicionar rótulos para um grupo ou para a região de dados, adicione uma linha ou coluna fora do grupo a ser rotulado. Linhas e colunas de rótulo são semelhantes a linhas e colunas adicionadas para exibir totais. Para obter mais informações, consulte [Inserir ou excluir uma linha &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-row-report-builder-and-ssrs.md) ou [Inserir ou excluir uma coluna &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md).  
  
## <a name="adding-an-existing-tablix-data-region-from-another-report"></a>Adicionando uma região de dados Tablix existente de outro relatório  
 É possível copiar uma região de dados de outro relatório e colá-la em um relatório novo ou existente. Depois que colar a região de dados, você deve assegurar que o banco de dados usado pela região de dados seja definido e que os campos do conjunto de dados tenham nomes e tipos de dados idênticos aos do relatório original. Você não pode copiar conjuntos de dados de um relatório para outro, mas se seus relatórios usarem fontes de dados compartilhadas, você poderá duplicar o conjunto de dados rapidamente no outro relatório. Além disso, é possível importar o texto da consulta para as consultas que recuperam os dados do conjunto de dados, o que simplifica a duplicação de consultas nos relatórios. Para obter mais informações, consulte [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Expressões &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Parâmetros de relatório e &#40; Construtor de relatórios, Report Designer e &#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Classificação interativa, mapas de documentos e Links &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [Adicionar filtros de conjunto de dados, filtros de região de dados e filtros de grupo &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Adicionar, editar e atualizar campos no painel de dados de relatório &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)   
 [Adicionar uma expressão &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/add-an-expression-report-builder-and-ssrs.md)  
  
  

