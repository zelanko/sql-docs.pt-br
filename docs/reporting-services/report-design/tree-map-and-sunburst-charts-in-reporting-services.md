---
title: Gráficos de mapa de árvore e explosão solar no SQL Server Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 12307c8f-bca7-4d21-8ad5-0c07d819865b
caps.latest.revision: 17
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 106d85def85002e9cb917cf3cc9be7ac55c57ee4
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2018
ms.locfileid: "40405868"
---
# <a name="treemap-and-sunburst-charts-in-reporting-services"></a>Gráficos de mapa de árvore e explosão solar no Reporting Services
[!INCLUDE[feedback-stackoverflow-msdn-connect-md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]
As visualizações de mapa de árvore e explosão solar do SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] são ótimas para representar dados hierárquicos visualmente. Este artigo é uma visão geral de como adicionar um gráfico de mapa de árvore ou explosão solar a um relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. O artigo também inclui uma consulta de exemplo do AdventureWorks para ajudá-lo a começar.  
  
##  <a name="bkmk_treemap_chart"></a> Gráfico de mapa de árvore  

Um gráfico de mapa de árvore divide a área do gráfico em retângulos que representam os diferentes níveis e os tamanhos relativos da hierarquia de dados. O mapa é semelhante às ramificações de uma árvore, começando com um tronco e dividindo-se em galhos menores. Cada retângulo é dividido em retângulos menores que representam o próximo nível na hierarquia. Os retângulos de nível superior do mapa de árvore são organizados com o retângulo maior no canto superior esquerdo do gráfico até o retângulo menor no canto inferior direito.  Dentro de um retângulo, o próximo nível mais alto também é disposto com retângulos do canto superior esquerdo para o canto inferior direito.  

Por exemplo, na imagem do mapa de árvore de exemplo a seguir, a região Sudoeste é a maior e a Alemanha é a menor. Dentro da região Southwest, Road Bikes são maiores do que Mountain Bikes.  
 
![ssrs_treemap_example](../../reporting-services/report-design/media/ssrs-treemap-example.png "ssrs_treemap_example")  
  
### <a name="to-insert-a-treemap-chart-and-set-up-the-sample-adventureworks-data"></a>Para inserir um gráfico de mapa de árvore e configurar os dados de exemplo do AdventureWorks  
   
> [!NOTE]
> Antes de adicionar um gráfico ao relatório, crie uma fonte de dados e um conjunto de dados.  Para obter dados e uma consulta de exemplo, consulte [Dados de exemplo do AdventureWorks](#bkmk_sample_data).  
  
1.  Clique com o botão direito do mouse na área de design e, em seguida, selecione **Inserir** > **Gráfico**. Selecione o ícone **Mapa de árvore**.

    ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon")  
   
2.  Reposicione e redimensione o gráfico. Para uso com os dados de exemplo, um gráfico com cinco polegadas de largura é um bom começo.  
  
3.  Adicione os seguintes campos dos exemplos de dados:  
  
    * **Valores**: LineTotal
    * **Grupos de Categorias** (na seguinte ordem):
        1. CategoryName
        2. SubcategoryName
    * **Grupos de Séries**: TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4.  Para otimizar o tamanho da página para uma forma geral de um mapa de árvore, defina a posição da legenda na parte inferior.  
  
5.  Para adicionar dicas de ferramenta que exibem a subcategoria e o total de linhas, clique com o botão direito do mouse em **LineTotal** e, em seguida, selecione **Propriedades da Série**.  
  
     ![ssrs_visualization_seriesproperties](../../reporting-services/report-design/media/ssrs-visualization-seriesproperties.png "ssrs_visualization_seriesproperties")  
  
     Defina a propriedade **Dica de Ferramenta** com o seguinte valor:  
  
    ```  
    =Fields!SubcategoryName.Value &": " &Format(Sum(Fields!LineTotal.Value),"C")  
    ```  
  
    Para obter mais informações, consulte [Mostrar ToolTips em uma série &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md).  
  
6.  Altere o título padrão do gráfico para **Vendas Categorizadas por Região**.  
  
7.  A quantidade de valores de rótulo exibidos é afetada pelo tamanho da fonte, o tamanho da área geral do gráfico e o tamanho de retângulos específicos. Para ver mais rótulos, altere a propriedade **Fonte do Rótulo** de **LineTotal** para **10pt**, do padrão de **8pt**.  
  
  
##  <a name="bkmk_sunburst_chart"></a> Gráfico de explosão solar  
 
Em um gráfico de explosão solar, a hierarquia é representada por uma série de círculos. O nível mais alto da hierarquia está no centro e os níveis inferiores da hierarquia são anéis exibidos fora do centro.  O nível mais baixo da hierarquia é o anel externo.  
  
![ssrs_sunburst_example](../../reporting-services/report-design/media/ssrs-sunburst-example.png "ssrs_sunburst_example")  
  
### <a name="to-insert-a-sunburst-chart-and-set-up-the-sample-adventureworks-data"></a>Para inserir um gráfico de explosão solar e configurar os dados de exemplo do AdventureWorks  
> [!NOTE] 
> Antes de adicionar um gráfico ao relatório, crie uma fonte de dados e um conjunto de dados. Para obter dados e uma consulta de exemplo, consulte [Dados de exemplo do AdventureWorks](#bkmk_sample_data).  
  
1.  Clique com o botão direito do mouse na área de design e, em seguida, selecione **Inserir** > **Gráfico**. Selecione o ícone **Explosão solar**.
     
     ![ssrs_sunburst_icon](../../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon")  
  
2.  Reposicione e redimensione o gráfico. Para uso com os dados de exemplo, um gráfico com cinco polegadas de largura é um bom começo.  
  
3.  Adicione os seguintes campos dos exemplos de dados:  

    * **Valores**: LineTotal
    * **Grupos de Categorias** (na seguinte ordem):
        1. CategoryName
        2. SubcategoryName
        3. SalesReasonName
    * **Grupos de Séries**: TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4.  Para otimizar o tamanho da página para uma forma geral de um mapa de explosão solar, defina a posição da legenda na parte inferior.  
  
5.  Altere o título padrão do gráfico para **Vendas Categorizadas por Região, com o motivo das vendas**.  
  
6. Para adicionar os valores dos grupos de categorias como rótulos à explosão solar, defina a propriedade do rótulo **Visible=true** e **UseValueAsLabel=false**.<br /><br /> Os valores de rótulo exibidos é afetada pelo tamanho da fonte, o tamanho da área geral do gráfico e o tamanho de retângulos específicos.  Para ver mais rótulos, altere a propriedade **Fonte do Rótulo** de **LineTotal** para **10pt**, do padrão de **8pt**.

    ![ssrs_sunburst_linetotalproperties](../../reporting-services/report-design/media/ssrs-sunburst-linetotalproperties.png "ssrs_sunburst_linetotalproperties")
  
7.  Se você quiser uma variedade de cores diferente, mude a propriedade **Paleta** do gráfico.  
    
     ![ssrs_visualization_palette](../../reporting-services/report-design/media/ssrs-visualization-palette.png "ssrs_visualization_palette")  
  
  
##  <a name="bkmk_sample_data"></a> Dados de exemplo do AdventureWorks  
 Esta seção inclui uma consulta de exemplo e as etapas básicas para criação de uma fonte de dados e um conjunto de dados no [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]. Se o relatório já contiver uma fonte de dados e um conjunto de dados, ignore esta seção.  
  
 A consulta retorna dados de detalhes de ordem de venda do AdventureWorks, com região de vendas, categoria de produto, subcategoria de produto e dados do motivo das vendas.  
  
1.  **Obter os dados**.  
  
     A consulta desta seção se baseia no banco de dados AdventureWorks, disponível para download no GitHub: [Backup completo de banco de dados do AdventureWorks 2016](https://github.com/Microsoft/sql-server-samples/releases).  
  
  
2.  **Criar uma fonte de dados**.  
  
    1.  Em **Dados de Relatório**, clique com o botão direito do mouse em **Fontes de Dados** e, em seguida, selecione **Adicionar fonte de dados**.  
  
    2.  Escolha **Usar uma conexão inserida em meu relatório**.  
  
    3.  Para tipo de conexão, selecione **Microsoft SQL Server**.  
  
    4.  Insira a cadeia de conexão do servidor e do banco de dados. Por exemplo:  
  
        ```  
        Data Source=[server name];Initial Catalog=AdventureWorks2016  
        ```  
  
    5.  Para verificar a conexão, selecione o botão **Testar Conexão** e, em seguida, selecione **OK**.  
  
     Para obter mais informações sobre como criar uma fonte de dados, consulte [Adicionar e verificar uma conexão de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
3.  **Criar um conjunto de dados**.  
  
    1. Em **Dados de Relatório**, clique com o botão direito do mouse em **Conjuntos de Dados** e, em seguida, selecione **Adicionar conjunto de dados**.  
  
    2. Escolha **Usar um conjunto de dados inserido em meu relatório**.  
  
    3. Selecione a fonte de dados criada.  
  
    4. Selecione o tipo de consulta **Texto** e copie e cole a seguinte consulta na caixa de texto **Consulta**:  
  
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
  
     Para obter mais informações sobre como criar um conjunto de dados, consulte [Criar um conjunto de dados compartilhado ou inserido &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  
  
  
## <a name="see-also"></a>Confira também  
* [Modo de exibição de Design de conjunto de dados compartilhado &#40;Construtor de Relatórios&#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)   
* [Mostrar ToolTips em uma série &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)
* [Tutorial: Mapas de árvore no Power BI](https://support.powerbi.com/knowledgebase/articles/556200-tutorial-treemaps-in-power-bi)
* [Mapa de árvore: aplicativos de visualização de dados do Microsoft Research para Office](http://research.microsoft.com/en-us/projects/msrdatavis/treemap.aspx)  
<br>  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

