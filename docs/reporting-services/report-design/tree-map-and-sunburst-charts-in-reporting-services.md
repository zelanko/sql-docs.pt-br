---
title: "Gráficos de mapa de árvore e explosão solar no SQL Server Reporting Services | Microsoft Docs"
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
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 5e15fa8674a09821becd437e78cfb0bb472e3bc8
ms.openlocfilehash: 50224e926c08951887a6423ab1c95eb7ac23a944
ms.contentlocale: pt-br
ms.lasthandoff: 10/30/2017

---
# <a name="treemap-and-sunburst-charts-in-reporting-services"></a>Gráficos de mapa de árvore e explosão solar no Reporting Services
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

O SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] visualizações de mapa de árvore e explosão solar são ótimas para representar visualmente os dados hierárquicos. Este artigo é uma visão geral de como adicionar um gráfico de mapa de árvore ou explosão solar a um [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] relatório. O artigo também inclui uma consulta de exemplo AdventureWorks para ajudá-lo a começar.  
  
##  <a name="bkmk_treemap_chart"></a>Gráfico de mapa de árvore  

Um gráfico de mapa de árvore divide a área do gráfico em retângulos que representam os diferentes níveis e os tamanhos relativos da hierarquia de dados. O mapa é semelhante às ramificações de uma árvore, começando com um tronco e dividindo-se em galhos menores. Cada retângulo é dividido em retângulos menores que representam o próximo nível na hierarquia. Os retângulos de nível superior do mapa de árvore são organizados com o retângulo maior no canto superior esquerdo do gráfico para o retângulo menor no canto inferior direito.  Dentro de um retângulo, o próximo nível mais alto também é disposto com retângulos do canto superior esquerdo para o canto inferior direito.  

Por exemplo, na imagem do mapa de árvore de exemplo a seguir, a região Southwest é a maior e Germany é a menor. Dentro da região Southwest, Road Bikes são maiores do que Mountain Bikes.  
 
![ssrs_treemap_example](../../reporting-services/report-design/media/ssrs-treemap-example.png "ssrs_treemap_example")  
  
### <a name="to-insert-a-treemap-chart-and-set-up-the-sample-adventureworks-data"></a>Para inserir um gráfico de mapa de árvore e configurar os dados de exemplo AdventureWorks  
   
> [!NOTE]
> Antes de adicionar um gráfico ao relatório, crie uma fonte de dados e o conjunto de dados.  Para dados de exemplo e um exemplo de consulta, consulte [dados de exemplo AdventureWorks](#bkmk_sample_data).  
  
1.  Clique na superfície de design, selecione **inserir** > **gráfico**. Selecione o **Treemap** ícone.

    ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon")  
   
2.  Reposicione e redimensione o gráfico. Para usar com os dados de exemplo, um gráfico de 5 polegadas de largura é um bom começo.  
  
3.  Adicione os seguintes campos dos exemplos de dados:  
  
    * **Valores**: LineTotal
    * **Grupos de categorias** (na seguinte ordem):
        1. Nome da categoria
        2. SubcategoryName
    * **Grupos de séries**: TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4.  Para otimizar o tamanho da página de forma geral de um mapa de árvore, defina a posição da legenda na parte inferior.  
  
5.  Para adicionar dicas de ferramenta que exibem a subcategoria e o total da linha, clique com botão direito **LineTotal**e, em seguida, selecione **propriedades da série**.  
  
     ![ssrs_visualization_seriesproperties](../../reporting-services/report-design/media/ssrs-visualization-seriesproperties.png "ssrs_visualization_seriesproperties")  
  
     Definir o **dica de ferramenta** propriedade para o seguinte valor:  
  
    ```  
    =Fields!SubcategoryName.Value &": " &Format(Sum(Fields!LineTotal.Value),"C")  
    ```  
  
    Para obter mais informações, consulte [Mostrar dicas de ferramenta em uma série &#40; Construtor de relatórios e SSRS &#41; ](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md).  
  
6.  Altere o título de gráfico padrão para **vendas categorizadas por região**.  
  
7.  A quantidade de valores de rótulo exibidos é afetada pelo tamanho da fonte, o tamanho da área geral do gráfico e o tamanho de retângulos específicos. Para ver mais rótulos, altere o **fonte do rótulo** propriedade **LineTotal** para **10pt** do padrão de **8pt**.  
  
  
##  <a name="bkmk_sunburst_chart"></a>Gráfico de explosão solar  
 
Em um gráfico de explosão solar, a hierarquia é representada por uma série de círculos. É o nível mais alto da hierarquia no centro e os níveis inferiores da hierarquia são anéis exibidos fora do centro.  O nível mais baixo da hierarquia é o anel externo.  
  
![ssrs_sunburst_example](../../reporting-services/report-design/media/ssrs-sunburst-example.png "ssrs_sunburst_example")  
  
### <a name="to-insert-a-sunburst-chart-and-set-up-the-sample-adventureworks-data"></a>Para inserir um gráfico de explosão solar e configurar os dados de exemplo AdventureWorks  
> [!NOTE] 
> Antes de adicionar um gráfico ao relatório, crie uma fonte de dados e o conjunto de dados. Para dados de exemplo e um exemplo de consulta, consulte [dados de exemplo AdventureWorks](#bkmk_sample_data).  
  
1.  A superfície de design e, em seguida, selecione **inserir** > **gráfico**. Selecione o **explosão solar** ícone.
     
     ![ssrs_sunburst_icon](../../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon")  
  
2.  Reposicione e redimensione o gráfico. Para usar com os dados de exemplo, um gráfico de 5 polegadas de largura é um bom começo.  
  
3.  Adicione os seguintes campos dos exemplos de dados:  

    * **Valores**: LineTotal
    * **Grupos de categorias** (na seguinte ordem):
        1. Nome da categoria
        2. SubcategoryName
        3. SalesReasonName
    * **Grupos de séries**: TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4.  Para otimizar o tamanho da página para a forma geral de um gráfico de explosão solar, defina a posição da legenda na parte inferior.  
  
5.  Altere o título de gráfico padrão para **vendas categorizadas por região, com o motivo de vendas**.  
  
6. Para adicionar os valores dos grupos de categoria à explosão solar como rótulos, defina as propriedades de rótulo **visível = true** e **UseValueAsLabel = false**.<br /><br /> Os valores de rótulo exibidos é afetada pelo tamanho da fonte, o tamanho da área geral do gráfico e o tamanho de retângulos específicos.  Para ver mais rótulos, altere o **fonte do rótulo** propriedade **LineTotal** para **10pt** do padrão de **8pt**.

    ![ssrs_sunburst_linetotalproperties](../../reporting-services/report-design/media/ssrs-sunburst-linetotalproperties.png "ssrs_sunburst_linetotalproperties")
  
7.  Se você quiser uma variedade de cores diferente, mude a propriedade **Paleta** do gráfico.  
    
     ![ssrs_visualization_palette](../../reporting-services/report-design/media/ssrs-visualization-palette.png "ssrs_visualization_palette")  
  
  
##  <a name="bkmk_sample_data"></a>Dados de exemplo do AdventureWorks  
 Esta seção inclui um exemplo de consulta e as etapas básicas para criar uma fonte de dados e o conjunto de dados no [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]. Se o relatório já contiver uma fonte de dados e o conjunto de dados, você poderá ignorar esta seção.  
  
 A consulta retorna dados de detalhes de pedido de vendas do AdventureWorks com território de vendas, categoria de produto, subcategoria de produto e dados do motivo de vendas.  
  
1.  **Obter os dados**.  
  
     A consulta nesta seção é baseada no banco de dados AdventureWorks, que está disponível para download do GitHub: [backup de banco de dados completo AdventureWorks 2016](https://github.com/Microsoft/sql-server-samples/releases).  
  
  
2.  **Criar uma fonte de dados**.  
  
    1.  Em **dados de relatório**, clique com botão direito **fontes de dados**e, em seguida, selecione **adicionar fonte de dados**.  
  
    2.  Escolha **Usar uma conexão inserida em meu relatório**.  
  
    3.  Para o tipo de conexão, selecione **Microsoft SQL Server**.  
  
    4.  Insira a cadeia de conexão do servidor e banco de dados. Por exemplo:  
  
        ```  
        Data Source=[server name];Initial Catalog=AdventureWorks2016  
        ```  
  
    5.  Para verificar a conexão, selecione o **Conexão de teste** botão e, em seguida, selecione **Okey**.  
  
     Para obter mais informações sobre como criar uma fonte de dados, consulte [adicionar e verificar uma conexão de dados &#40; Construtor de relatórios e SSRS &#41; ](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
3.  **Criar um conjunto de dados**.  
  
    1. Em **dados de relatório**, clique com botão direito **conjuntos de dados**e, em seguida, selecione **Adicionar conjunto de dados**.  
  
    2. Escolha **Usar um conjunto de dados inserido em meu relatório**.  
  
    3. Selecione a fonte de dados que você criou.  
  
    4. Selecione o **texto** tipo, de consulta e, em seguida, copie e cole a consulta a seguir para o **consulta** caixa de texto:  
  
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
  
    5. Escolha **OK**.  
  
     Para obter mais informações sobre como criar um conjunto de dados, consulte [criar um conjunto de dados compartilhado ou conjunto de dados inserido &#40; Construtor de relatórios e SSRS &#41; ](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  
  
  
## <a name="see-also"></a>Consulte também  
* [Compartilhado de exibição de design de conjunto de dados &#40; Construtor de relatórios &#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)   
* [Mostrar dicas de ferramenta em uma série &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)
* [Tutorial: Treemaps no Power BI](https://support.powerbi.com/knowledgebase/articles/556200-tutorial-treemaps-in-power-bi)
* [Mapa de árvore: aplicativos de visualização de dados do Microsoft Research para Office](http://research.microsoft.com/en-us/projects/msrdatavis/treemap.aspx)  
<br>  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]


