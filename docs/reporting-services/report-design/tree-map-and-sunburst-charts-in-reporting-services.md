---
title: "Mapa de árvore e gráficos explosão solar no Reporting Services | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/31/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 12307c8f-bca7-4d21-8ad5-0c07d819865b
caps.latest.revision: 17
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: e09afe4634c02db6e74413e7c1c10565450b3559
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="tree-map-and-sunburst-charts-in-reporting-services"></a>Gráficos de mapa de árvore e explosão solar no Reporting Services
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

  As visualizações de mapa de árvore e explosão solar do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] são ótimas para representar visualmente os dados hierárquicos.   Este tópico é uma visão geral de como adicionar um gráfico de mapa de árvore ou explosão solar a um relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . O tópico também inclui um exemplo de consulta do Adventureworks para ajudar você a começar.  
  
##  <a name="bkmk_treemap_chart"></a> Gráfico de mapa de árvore  
 ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon")  
  
 Um gráfico de mapa de árvore divide a área do gráfico em retângulos que representam os diferentes níveis e os tamanhos relativos da hierarquia de dados. O mapa é semelhante às ramificações de uma árvore, começando com um tronco e dividindo-se em galhos menores. Cada retângulo é dividido em retângulos menores que representa o próximo nível na hierarquia. Os retângulos superiores do mapa de árvore são organizados com o retângulo maior no canto superior esquerdo do gráfico até o retângulo menor no canto inferior direito.  Dentro de um retângulo, o próximo nível mais alto também é disposto com retângulos do canto superior esquerdo para o canto inferior direito.  
  
 Por exemplo, na imagem do exemplo de mapa de árvore a seguir, a região Southwest é a maior, e Germany é a menor. Dentro da região Southwest, Road Bikes são maiores do que Mountain Bikes.  
  
 ![ssrs_treemap_example](../../reporting-services/report-design/media/ssrs-treemap-example.png "ssrs_treemap_example")  
  
### <a name="to-insert-a-tree-map-chart-and-configure-for-the-sample-adventureworks-data"></a>Para inserir um gráfico de mapa de árvore e configurá-lo com os exemplos de dados de Adventureworks  
 **Observação:** antes de adicionar um gráfico ao relatório, crie uma fonte de dados e um conjunto de dados.  Para obter os exemplos de dados e um exemplo de consulta, confira a seção [Exemplo de dados do Adventureworks](#bkmk_sample_data) neste tópico.  
  
1.  Clique com o botão direito do mouse na superfície do design, clique em **Inserir**e em **Gráfico** .  
  
     Selecione mapa de árvore ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon").  
  
     ![ssrs_insert_treemap_sunburst](../../reporting-services/report-design/media/ssrs-insert-treemap-sunburst.png "ssrs_insert_treemap_sunburst")  
  
2.  Reposicione e redimensione o gráfico.   Para uso com os exemplos de dados, um gráfico com cinco polegadas de largura é um bom começo.  
  
3.  Adicione os seguintes campos dos exemplos de dados:  
  
    |||  
    |-|-|  
    |![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")|**Valores:** LineTotal<br /><br /> **Grupos de Categorias:** adicione-os na seguinte ordem:<br /><br /> 1) CategoryName<br /><br /> 2) SubcategoryName<br /><br /> **Grupos de Séries:** TerritoryName|  
  
4.  Para otimizar o tamanho da página para uma forma geral de um mapa de árvore, defina a posição da legenda na parte inferior.  
  
5.  Para adicionar dicas de ferramenta que exibem a subcategoria e o total da linhas, clique com o botão direito do mouse em **LineTotal** e clique em **Propriedades da Série**.  
  
     ![ssrs_visualization_seriesproperties](../../reporting-services/report-design/media/ssrs-visualization-seriesproperties.png "ssrs_visualization_seriesproperties")  
  
     Defina a propriedade **Dica de Ferramenta** para o seguinte:  
  
    ```  
    =Fields!SubcategoryName.Value &": " &Format(Sum(Fields!LineTotal.Value),"C")  
    ```  
  
     Para obter mais informações, consulte [Mostrar dicas de ferramenta em uma série &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md).  
  
6.  Altere o título de gráfico padrão para "Vendas categorizadas por região".  
  
7.  A quantidade de valores de rótulo exibidos é afetada pelo tamanho da fonte, o tamanho da área geral do gráfico e o tamanho de retângulos específicos.  Para ver mais rótulos, altere a propriedade de fonte do Rótulo de LineTotal para 10 pt, em vez do padrão de 8 pt.  
  
  
##  <a name="bkmk_sunburst_chart"></a> Gráfico explosão solar  
 ![ssrs_sunburst_icon](../../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon")  
  
 Em um gráfico de explosão solar, a hierarquia é representada por uma série de círculos, com o nível mais alto da hierarquia no centro e os níveis mais baixos da hierarquia como anéis exibidos fora do centro.  O nível mais baixo da hierarquia é o anel externo.  
  
 ![ssrs_sunburst_example](../../reporting-services/report-design/media/ssrs-sunburst-example.png "ssrs_sunburst_example")  
  
### <a name="to-insert-a-sunburst-chart-and-configure-for-the-sample-adventureworks-data"></a>Para inserir um gráfico de explosão solar e configurá-lo com os exemplos de dados de Adventureworks  
 **Observação:** antes de adicionar um gráfico ao relatório, crie uma fonte de dados e um conjunto de dados.  Para obter os exemplos de dados e um exemplo de consulta, confira a seção [Exemplo de dados do Adventureworks](#bkmk_sample_data) neste tópico.  
  
1.  Clique com o botão direito do mouse na superfície do design, clique em **Inserir**e em **Gráfico** .  
  
     Selecione explosão solar ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon").  
  
     ![ssrs_insert_treemap_sunburst](../../reporting-services/report-design/media/ssrs-insert-treemap-sunburst.png "ssrs_insert_treemap_sunburst")  
  
2.  Reposicione e redimensione o gráfico.   Para uso com os exemplos de dados, um gráfico com cinco polegadas de largura é um bom começo.  
  
3.  Adicione os seguintes campos dos exemplos de dados:  
  
    |||  
    |-|-|  
    |![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")|**Valores:** LineTotal<br /><br /> **Grupos de Categorias:** adicione-os na seguinte ordem:<br /><br /> 1) CategoryName<br /><br /> 2) SubcategoryName,<br /><br /> 3) SalesReasonName<br /><br /> **Grupos de Séries:** TerritoryName.|  
  
4.  Para otimizar o tamanho da página para uma forma geral de um mapa de Explosão solar, defina a posição da legenda na parte inferior.  
  
5.  Altere o título de gráfico padrão para "Vendas categorizadas por região, com o motivo das vendas".  
  
6.  |||  
    |-|-|  
    |![ssrs_sunburst_linetotalproperties](../../reporting-services/report-design/media/ssrs-sunburst-linetotalproperties.png "ssrs_sunburst_linetotalproperties")|Para adicionar os valores dos grupos de categorias como rótulos à explosão solar, defina a propriedade do rótulo **Visible** = true e **UseValueAsLabel**= false.<br /><br /> Os valores de rótulo exibidos é afetada pelo tamanho da fonte, o tamanho da área geral do gráfico e o tamanho de retângulos específicos.  Para ver mais rótulos, altere a propriedade de fonte do Rótulo de LineTotal para 8 pt, em vez do padrão de 10 pt.|  
  
7.  Se você quiser uma variedade de cores diferente, mude a propriedade **Paleta** do gráfico.  
  
     ![ssrs_visualization_palette](../../reporting-services/report-design/media/ssrs-visualization-palette.png "ssrs_visualization_palette")  
  
  
##  <a name="bkmk_sample_data"></a> Exemplo de dados do Adventureworks  
 Esta seção inclui um exemplo de consulta e as etapas básicas para criar uma fonte de dados e o conjunto de dados em [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]. Se o relatório já contiver uma fonte de dados e o conjunto de dados, ignore esta seção.  
  
 A consulta retorna dados de detalhes de pedido de vendas do Adventureworks, com território de vendas, categoria de produto, subcategoria de produto e dados do motivo das vendas.  
  
1.  **Obter os dados:**  
  
     A consulta nesta seção tem base no banco de dados Adventureworks, disponível para download no  [Adventure Works 2014 Full Database Backup](https://msftdbprodsamples.codeplex.com/releases/view/125550)(Backup completo do banco de dados do Adventure Works 2014).  
  
     Para saber mais sobre como instalar o banco de dados, confira [How to install Adventure Works 2014 Sample Databases.pdf](https://msftdbprodsamples.codeplex.com/releases/view/125550)(Como instalar os bancos de dados de exemplo do Adventure Works 2014.pdf).  
  
2.  **Criar uma fonte de dados:**  
  
    1.  No painel **Dados do Relatório** , clique com o botão direito do mouse em **Fonte de Dados** e clique em **Adicionar fonte de dados**.  
  
    2.  Escolha **Usar uma conexão inserida em meu relatório**.  
  
    3.  Escolha o tipo de conexão **Microsoft SQL Server**.  
  
    4.  Digite a cadeia de conexão do servidor e do banco de dados, por exemplo, a seguinte:  
  
        ```  
        Data Source=[server name];Initial Catalog=AdventureWorks2014  
        ```  
  
    5.  Convém verificar com o botão **Testar Conexão** e clicar em **OK**.  
  
     Para obter mais informações sobre como criar uma fonte de dados, consulte [Adicionar e verificar uma conexão de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
3.  **Criar um conjunto de dados:**  
  
    -   No painel **Dados do Relatório** , clique com o botão direito do mouse em **Conjuntos de Dados** e clique em **Adicionar conjunto de dados**.  
  
    -   Escolha **Usar um conjunto de dados inserido em meu relatório**.  
  
    -   Escolha a fonte de dados que você criou nas etapas anteriores.  
  
    -   Escolha o tipo de consulta **Texto** e copie e cole a consulta a seguir na caixa de texto **Consulta:** :  
  
        ```  
        SELECT    Sales.SalesOrderHeader.SalesOrderID, Sales.SalesOrderHeader.OrderDate, Sales.SalesOrderDetail.SalesOrderDetailID, Sales.SalesOrderDetail.ProductID, Sales.SalesOrderDetail.LineTotal,   
                                 Sales.SalesOrderDetail.UnitPrice, Sales.SalesOrderDetail.OrderQty, Production.Product.Name, Production.Product.ProductNumber, Sales.SalesTerritory.TerritoryID, lower(Sales.SalesTerritory.Name) AS TerritoryName,   
                                 Production.ProductSubcategory.Name AS SubcategoryName, Production.ProductCategory.Name AS CategoryName, Sales.SalesReason.SalesReasonID, Sales.SalesReason.Name AS SalesReasonName  
        FROM            Sales.SalesOrderDetail INNER JOIN  
                                 Sales.SalesOrderHeader ON Sales.SalesOrderDetail.SalesOrderID = Sales.SalesOrderHeader.SalesOrderID INNER JOIN  
                                 Production.Product ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID INNER JOIN  
                                 Sales.SalesTerritory ON Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID AND Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID AND   
                                 Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID INNER JOIN  
                                 Production.ProductSubcategory ON Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID AND   
                                 Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID AND   
                                 Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID INNER JOIN  
                                 Production.ProductCategory ON Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID AND   
                                 Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID AND   
                                 Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID INNER JOIN  
                                 Sales.SalesOrderHeaderSalesReason ON Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND   
                                 Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND   
                                 Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID INNER JOIN  
                                 Sales.SalesReason ON Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND   
                                 Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND   
                                 Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID  
        ```  
  
    -   clique em **OK**.  
  
     Para obter mais informações sobre como criar um conjunto de dados, consulte [Criar um conjunto de dados compartilhado ou um conjunto de dados inserido &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  
  
  
## <a name="see-also"></a>Consulte também  
 [Modo de exibição de Design de conjunto de dados compartilhados &#40;Construtor de Relatórios&#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)   
 [Mostrar dicas de ferramenta em uma série &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)   
 [Tutorial: mapas de árvore no Power BI](https://support.powerbi.com/knowledgebase/articles/556200-tutorial-treemaps-in-power-bi)   
 [Mapa de árvore: aplicativos de visualização de dados do Microsoft Research para Office](http://research.microsoft.com/en-us/projects/msrdatavis/treemap.aspx)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]


