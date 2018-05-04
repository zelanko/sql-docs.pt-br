---
title: Programando objetos OLAP AMO básicos | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: amo
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6df874fb1819f2360991d19557090aa30dec1a42
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="programming-amo-olap-basic-objects"></a>Programando objetos OLAP AMO básicos
  A criação de objetos complexos do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] é simples e direta, mas requer atenção aos detalhes. Este tópico explica os detalhes de programação de objetos OLAP básicos. Este tópico contém as seguintes seções:  
  
-   [Objetos de dimensão](#Dim)  
  
-   [Objetos de cubo](#Cub)  
  
-   [Objetos MeasureGroup](#MG)  
  
-   [Objetos de partição](#Part)  
  
-   [Objetos de agregação](#AD)  
  
##  <a name="Dim"></a> Objetos de dimensão  
 Para administrar ou processar uma dimensão, você programa o objeto <xref:Microsoft.AnalysisServices.Dimension>.  
  
### <a name="creating-dropping-and-finding-a-dimension"></a>Criando, descartando e localizando uma dimensão  
 A criação de um objeto <xref:Microsoft.AnalysisServices.Dimension> é realizada em quatro etapas:  
  
1.  Crie o objeto de dimensão e preencha os atributos básicos.  
  
     Os atributos básicos são Name, Dimension Type, Storage Mode, Data Source Binding, Attribute All Member Name, entre outros.  
  
     Antes de criar uma dimensão, verifique se ela já não existe. Se a dimensão existir, então será descartada e recriada.  
  
2.  Crie os atributos que definem a dimensão.  
  
     Cada atributo precisa ser adicionado individualmente ao esquema antes de poder ser usado (localize o método CreateDataItem no final do código de exemplo) e depois poderá ser adicionado à coleção de atributos da dimensão.  
  
     As colunas Key e Name devem ser definidas em todos os atributos.  
  
     O atributo de chave primária da dimensão deve ser definido como AttributeUsage.Key para tornar claro de que esse atributo é o principal acesso à dimensão.  
  
3.  Crie as hierarquias que o usuário usará para navegar na dimensão.  
  
     Quando estiver criando hierarquias, a ordem dos níveis será definida pela ordem na qual os níveis são criados, de cima para baixo. O nível mais alto será o primeiro a ser acrescentado à coleção de níveis da hierarquia.  
  
4.  Atualize o servidor usando o método Update da dimensão atual.  
  
 O código de exemplo a seguir cria a dimensão de produto da tabela Produtos Adventure Works no banco de dados de exemplo.  
  
```  
static void CreateProductDimension(Database db, string datasourceName)  
{  
    // Create the Product dimension  
    Dimension dim = db.Dimensions.FindByName("Product");  
    if ( dim != null)  
       dim.Drop();  
    dim = db.Dimensions.Add("Product");  
    dim.Type = DimensionType.Products;  
    dim.UnknownMember = UnknownMemberBehavior.Hidden;  
    dim.AttributeAllMemberName = "All Products";  
    dim.Source = new DataSourceViewBinding(datasourceName);  
    dim.StorageMode = DimensionStorageMode.Molap;  
  
    #region Create attributes  
  
    DimensionAttribute attr;  
  
    attr = dim.Attributes.Add("Product Name");  
    attr.Usage = AttributeUsage.Key;  
    attr.Type = AttributeType.Product;  
    attr.OrderBy = OrderBy.Name;  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ProductKey"));  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProduct", "EnglishProductName");  
  
    attr = dim.Attributes.Add("Product Line");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ProductLine"));  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProduct", "ProductLineName");  
  
    attr = dim.Attributes.Add("Model Name");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ModelName"));  
    attr.AttributeRelationships.Add(new AttributeRelationship("Product Line"));  
    attr.AttributeRelationships.Add(new AttributeRelationship("Subcategory"));  
  
    attr = dim.Attributes.Add("Subcategory");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProductSubcategory", "ProductSubcategoryKey"));  
    attr.KeyColumns[0].NullProcessing = NullProcessing.UnknownMember;  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProductSubcategory", "EnglishProductSubcategoryName");  
    attr.AttributeRelationships.Add(new AttributeRelationship("Category"));  
  
    attr = dim.Attributes.Add("Category");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProductCategory", "ProductCategoryKey"));  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProductCategory", "EnglishProductCategoryName");  
  
    attr = dim.Attributes.Add("List Price");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ListPrice"));  
    attr.AttributeHierarchyEnabled = false;  
  
    attr = dim.Attributes.Add("Size");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "Size"));  
    attr.AttributeHierarchyEnabled = false;  
  
    attr = dim.Attributes.Add("Weight");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "Weight"));  
    attr.AttributeHierarchyEnabled = false;  
  
    #endregion  
  
    #region Create hierarchies  
  
    Hierarchy hier;  
  
    hier = dim.Hierarchies.Add("Product Model Categories");  
    hier.AllMemberName = "All Products";  
    hier.Levels.Add("Category").SourceAttributeID = "Category";  
    hier.Levels.Add("Subcategory").SourceAttributeID = "Subcategory";  
    hier.Levels.Add("Model Name").SourceAttributeID = "Model Name";  
  
    hier = dim.Hierarchies.Add("Product Categories");  
    hier.AllMemberName = "All Products";  
    hier.Levels.Add("Category").SourceAttributeID = "Category";  
    hier.Levels.Add("Subcategory").SourceAttributeID = "Subcategory";  
    hier.Levels.Add("Model Name").SourceAttributeID = "Product Name";  
  
    hier = dim.Hierarchies.Add("Product Model Lines");  
    hier.AllMemberName = "All Products";  
    hier.Levels.Add("Subcategory").SourceAttributeID = "Product Line";  
    hier.Levels.Add("Model Name").SourceAttributeID = "Model Name";  
  
    #endregion  
  
    dim.Update();  
}  
  
static DataItem CreateDataItem(DataSourceView dsv, string tableName, string columnName)  
{  
    DataTable dataTable = ((DataSourceView)dsv).Schema.Tables[tableName];  
    DataColumn dataColumn = dataTable.Columns[columnName];  
    return new DataItem(tableName, columnName,  
        OleDbTypeConverter.GetRestrictedOleDbType(dataColumn.DataType));  
}  
  
```  
  
### <a name="processing-a-dimension"></a>Processando uma dimensão  
 O processamento de uma dimensão é tão simples quanto usar o método Process do objeto <xref:Microsoft.AnalysisServices.Dimension>.  
  
 O processamento de uma dimensão pode afetar todos os cubos que usam a dimensão. Para obter mais informações sobre opções de processamento, consulte [processando um modelo multidimensional &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 O código a seguir faz uma atualização incremental de todas as dimensões do banco de dados fornecido:  
  
```  
static void UpdateAllDimensions(Database db)  
{  
    foreach (Dimension dim in db.Dimensions)  
        dim.Process(ProcessType.ProcessUpdate);  
}  
```  
  
##  <a name="Cub"></a> Objetos de cubo  
 Para administrar ou processar um cubo, você programa o objeto <xref:Microsoft.AnalysisServices.Cube>.  
  
### <a name="creating-dropping-and-finding-a-cube"></a>Criando, descartando e localizando um cubo  
 O gerenciamento de cubos é semelhante ao de dimensões. A criação de um objeto <xref:Microsoft.AnalysisServices.Cube> é realizada em quatro etapas:  
  
1.  Crie o objeto de cubo e preencha os atributos básicos.  
  
     Os atributos básicos são Name, Storage Mode, Data Source Binding, Default Measure, entre outros atributos de cubo.  
  
     Antes de criar um cubo, verifique se ele já não existe. No exemplo, se o cubo existir, será descartado e recriado.  
  
2.  Adicione as dimensões do cubo.  
  
     As dimensões são adicionadas à coleção de dimensões de cubo atual do banco de dados; dimensões no cubo são referências à coleção de dimensões de banco de dados. Cada dimensão tem de ser mapeada individualmente para o cubo. No exemplo, as dimensões são mapeadas fornecendo: o identificador interno da dimensão de banco de dados, um nome para a dimensão no cubo e uma ID para a dimensão nomeada no cubo.  
  
     No código de exemplo, observe que a dimensão "Date" é adicionada três vezes, sempre é adicionada por meio de um nome de dimensão de cubo diferente: Date, Ship Date, Delivery Date. Essas dimensões são chamadas de dimensões "com funções múltiplas". A dimensão base é a mesma (Date), mas a tabela de fatos é usada pela dimensão em "funções" diferentes (Order Date, Ship Date, Delivery Date) - consulte "Criando, descartando e localizando um MeasureGroup", mais adiante neste documento, para compreender como as dimensões "com funções múltiplas" são definidas.  
  
3.  Crie os grupos de medidas que o usuário acessará para procurar os dados do cubo.  
  
     A criação do grupo de medidas será explicada em "Criando, descartando e localizando um MeasureGroup", mais adiante neste documento. O exemplo encapsula a criação do grupo de medidas em métodos diferentes, um para cada grupo de medidas.  
  
4.  Atualize o servidor usando o método Update do cubo atual.  
  
     O método de atualização é usado com a opção ExpandFull de Update para garantir que todos os objetos estejam totalmente atualizados no servidor.  
  
 O exemplo de código a seguir cria as partes do cubo da Adventure Works. O exemplo de código não cria todas as dimensões ou grupos de medidas incluídos no exemplo de projeto Adventure Works do Analysis Services.  
  
```  
static void CreateAdventureWorksCube(Database db, string datasourceName)  
{  
    // Create the Adventure Works cube  
    Cube cube = db.Cubes.FindByName("Adventure Works");  
    if ( cube != null)  
       cube.Drop();  
    db.Cubes.Add("Adventure Works");  
    cube.DefaultMeasure = "[Reseller Sales Amount]";  
    cube.Source = new DataSourceViewBinding(datasourceName);  
    cube.StorageMode = StorageMode.Molap;  
  
    #region Create cube dimensions  
  
    Dimension dim;  
  
    dim = db.Dimensions.GetByName("Date");  
    cube.Dimensions.Add(dim.ID, "Date", "Order Date Key - Dim Time");  
    cube.Dimensions.Add(dim.ID, "Ship Date",  
        "Ship Date Key - Dim Time");  
    cube.Dimensions.Add(dim.ID, "Delivery Date",  
        "Delivery Date Key - Dim Time");  
  
    dim = db.Dimensions.GetByName("Customer");  
    cube.Dimensions.Add(dim.ID);  
  
    dim = db.Dimensions.GetByName("Reseller");  
    cube.Dimensions.Add(dim.ID);  
    #endregion  
  
    #region Create measure groups  
  
    CreateSalesReasonsMeasureGroup(cube);  
    CreateInternetSalesMeasureGroup(cube);  
    CreateResellerSalesMeasureGroup(cube);  
    CreateCustomersMeasureGroup(cube);  
    CreateCurrencyRatesMeasureGroup(cube);  
  
    #endregion  
  
    cube.Update(UpdateOptions.ExpandFull);  
}  
```  
  
### <a name="processing-a-cube"></a>Processando um cubo  
 O processamento de um cubo é tão simples quanto usar o método Process do objeto <xref:Microsoft.AnalysisServices.Cube>. O processamento de um cubo também processa todos os grupos de medidas no cubo e todas as partições no grupo de medidas. Em um cubo, as partições são os únicos objetos que podem ser processados; para fins de processamento, os grupos de medidas só serão contêineres de partições. O tipo especificado de processamento para o cubo se propaga para as partições. O processamento interno de cubos e de grupos de medidas é resolvido para o processamento de dimensões e de partições.  
  
 Para obter mais informações sobre opções de processamento, consulte [processar objetos &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md), e [processando um modelo multidimensional &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 O código a seguir fará um processamento completo em todos os cubos de um banco de dados especificado:  
  
```  
foreach (Cube cube in db.Cubes)  
             cube.Process(ProcessType.ProcessFull);  
     }  
```  
  
##  <a name="MG"></a> Objetos MeasureGroup  
 Para administrar ou processar um grupo de medidas, você programa o objeto <xref:Microsoft.AnalysisServices.MeasureGroup>.  
  
### <a name="creating-dropping-and-finding-a-measuregroup"></a>Criando, descartando e localizando um MeasureGroup  
 O gerenciamento de grupos de medidas é semelhante ao gerenciamento de dimensões e de cubos. A criação de um objeto <xref:Microsoft.AnalysisServices.MeasureGroup> é realizada nas seguintes etapas:  
  
1.  Crie o objeto de grupo de medidas e preencha os atributos básicos.  
  
     Os atributos básicos incluem Name, Storage Mode, Processing Mode, Default Measure, entre atributos de grupo de medidas.  
  
     Antes de criar um grupo de medidas, verifique se ele já não existe. No código de exemplo a seguir, se o grupo de medidas existir, será descartado e recriado.  
  
2.  Crie as medidas do grupo de medidas. Para cada medida criada, os atributos a seguir são atribuídos: nome, função de agregação, coluna de origem, cadeira de caracteres de formato. Outros atributos também podem ser atribuídos. Observe que no código de exemplo a seguir, o método CreateDataItem adiciona a coluna ao esquema.  
  
3.  Adicione as dimensões do grupo de medidas.  
  
4.  As dimensões são adicionadas à coleção de dimensões de grupo de medidas atual da coleção de dimensões do cubo pai. Assim que a dimensão é incluída na coleção de dimensões do grupo de medidas, uma coluna de chave da tabela de fatos poderá ser mapeada para a dimensão para que o grupo de medidas possa ser navegado por meio da dimensão.  
  
     No código de exemplo a seguir, consulte as linhas sob "Mapeando a dimensão e coluna de chave a partir da tabela de fatos". As dimensões com funções múltiplas são implementadas pela vinculação de chaves substitutas diferentes à mesma dimensão sob nomes diferentes. Para cada uma das dimensões com funções múltiplas (Date, Ship Date, Delivery Date), uma chave substituta diferente será vinculada (OrderDateKey, ShipDateKey, DueDateKey). Todas as chaves derivam da tabela de fatos FactInternetSales.  
  
5.  Adicione as partições criadas do grupo de medidas.  
  
     No código de exemplo a seguir, a criação da partição será encapsulada em um método.  
  
6.  Atualize o servidor usando o método Update do grupo de medidas atual.  
  
     No código de exemplo a seguir, todos os grupos de medidas serão atualizados quando o cubo for atualizado.  
  
 O código de exemplo a seguir criará o grupo de medidas InternetSales do exemplo de projeto Adventure Works do Analysis Services.  
  
```  
static void CreateInternetSalesMeasureGroup(Cube cube)  
{  
    // Create the Internet Sales measure group  
    Database db = cube.Parent;  
    MeasureGroup mg = cube.MeasureGroups.FindByName("Internet Sales");  
    if ( mg != null)  
       mg.Drop();  
    mg = cube.MeasureGroups.Add("Internet Sales");  
    mg.StorageMode = StorageMode.Molap;  
    mg.ProcessingMode = ProcessingMode.LazyAggregations;  
    mg.Type = MeasureGroupType.Sales;  
  
    #region Create measures  
  
    Measure meas;  
  
    meas = mg.Measures.Add("Internet Sales Amount");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    meas.FormatString = "Currency";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "SalesAmount");  
  
    meas = mg.Measures.Add("Internet Order Quantity");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    meas.FormatString = "#,#";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "OrderQuantity");  
  
    meas = mg.Measures.Add("Internet Unit Price");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    meas.FormatString = "Currency";  
    meas.Visible = false;  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "UnitPrice");  
  
    meas = mg.Measures.Add("Internet Total Product Cost");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    //meas.MeasureExpression = "[Internet Total Product Cost] * [Average Rate]";  
    meas.FormatString = "Currency";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "TotalProductCost");  
  
    meas = mg.Measures.Add("Internet Order Count");  
    meas.AggregateFunction = AggregationFunction.Count;  
    meas.FormatString = "#,#";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "ProductKey");  
  
    #endregion  
  
    #region Create measure group dimensions  
  
    CubeDimension cubeDim;  
    RegularMeasureGroupDimension regMgDim;  
    ManyToManyMeasureGroupDimension mmMgDim;  
    MeasureGroupAttribute mgAttr;  
  
    //   Mapping dimension and key column from fact table  
    //      > select dimension and add it to the measure group  
    cubeDim = cube.Dimensions.GetByName("Date");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
  
    //      > add key column from dimension and map it with   
    //        the surrogate key in the fact table  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Date").ID);   // this is dimension key column  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "OrderDateKey"));   // this surrogate key in fact table  
  
    cubeDim = cube.Dimensions.GetByName("Ship Date");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Date").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "ShipDateKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Delivery Date");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Date").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "DueDateKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Customer");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Full Name").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "CustomerKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Product");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Product Name").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "ProductKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Source Currency");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Currency").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "CurrencyKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Sales Reason");  
    mmMgDim = new ManyToManyMeasureGroupDimension();  
    mmMgDim.CubeDimensionID = cubeDim.ID;  
    mmMgDim.MeasureGroupID = cube.MeasureGroups.GetByName("Sales Reasons").ID;  
    mg.Dimensions.Add(mmMgDim);  
  
    cubeDim = cube.Dimensions.GetByName("Internet Sales Order Details");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Sales Order Key").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "SalesOrderNumber"));  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "SalesOrderLineNumber"));  
  
    #endregion  
  
    #region Create partitions  
  
    CreateInternetSalesMeasureGroupPartitions( mg)  
  
    #endregion  
}  
```  
  
### <a name="processing-a-measure-group"></a>Processando um grupo de medidas  
 O processamento de um grupo de medidas é tão simples quanto usar o método Process do objeto <xref:Microsoft.AnalysisServices.MeasureGroup>. O processamento de um grupo de medidas incluirá todas as partições que pertencem ao grupo de medidas. O processamento interno de grupos de medidas é resolvido para o processamento de dimensões e de partições. Consulte [Processando uma partição](#ProcPart) neste documento.  
  
 Para obter mais informações sobre opções de processamento, consulte [processar objetos &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md), e [processando um modelo multidimensional &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 O código a seguir fará um processamento completo em todos os grupos de medidas de um cubo fornecido.  
  
```  
static void FullProcessAllMeasureGroups(Cube cube)  
{  
    foreach (MeasureGroup mg in cube.MeasureGroups)  
        mg.Process(ProcessType.ProcessFull);  
}  
```  
  
##  <a name="Part"></a> Objetos de partição  
 Para administrar ou processar uma partição, você programa o objeto <xref:Microsoft.AnalysisServices.Partition>.  
  
### <a name="creating-dropping-and-finding-a-partition"></a>Criando, descartando e localizando uma partição  
 As partições são objetos simples que podem ser criados em duas etapas.  
  
1.  Crie o objeto de partição e preencha os atributos básicos.  
  
     Os atributos básicos são Name, Storage Mode, partition source, Slice, entre outros atributos de grupo de medidas. A origem da partição define a instrução select SQL para a partição atual. Slice é uma expressão MDX que especifica uma tupla ou um conjunto que delimita uma parte das dimensões do grupo de medidas pai contido na partição atual. Para partições MOLAP, a fatia é determinada automaticamente sempre que a partição for processada.  
  
     Antes de criar uma partição, verifique se ela já não existe. No código de exemplo a seguir, se a partição existir, será descartada e recriada.  
  
2.  Atualize o servidor usando o método Update da partição atual.  
  
     No código de exemplo a seguir, todas as partições serão atualizadas quando o cubo for atualizado.  
  
 O exemplo de código a seguir cria partições para o grupo de medidas 'InternetSales'.  
  
```  
static void CreateInternetSalesMeasureGroupPartitions(MeasureGroup mg)  
{  
    Partition part;  
    part = mg.Partitions.FindByName("Internet_Sales_184");  
    if ( part != null)  
       part.Drop();  
    part = mg.Partitions.Add("Internet_Sales_184");  
    part.StorageMode = StorageMode.Molap;  
    part.Source = new QueryBinding(db.DataSources[0].ID, "SELECT * FROM [dbo].[FactInternetSales] WHERE OrderDateKey <= '184'");  
    part.Slice = "[Date].[Calendar Year].&[2001]";  
    part.Annotations.Add("LastOrderDateKey", "184");  
  
    part = mg.Partitions.FindByName("Internet_Sales_549");  
    if ( part != null)  
       part.Drop();  
    part = mg.Partitions.Add("Internet_Sales_549");  
    part.StorageMode = StorageMode.Molap;  
    part.Source = new QueryBinding(db.DataSources[0].ID, "SELECT * FROM [dbo].[FactInternetSales] WHERE OrderDateKey > '184' AND OrderDateKey <= '549'");  
    part.Slice = "[Date].[Calendar Year].&[2002]";  
    part.Annotations.Add("LastOrderDateKey", "549");  
  
    part = mg.Partitions.FindByName("Internet_Sales_914");  
    if ( part != null)  
       part.Drop();  
    part = mg.Partitions.Add("Internet_Sales_914");  
    part.StorageMode = StorageMode.Molap;  
    part.Source = new QueryBinding(db.DataSources[0].ID, "SELECT * FROM [dbo].[FactInternetSales] WHERE OrderDateKey > '549' AND OrderDateKey <= '914'");  
    part.Slice = "[Date].[Calendar Year].&[2003]";  
    part.Annotations.Add("LastOrderDateKey", "914");  
}  
```  
  
###  <a name="ProcPart"></a> Processando uma partição  
 O processamento de uma partição é tão simples quanto usar o método Process do objeto <xref:Microsoft.AnalysisServices.Partition>.  
  
 Para obter mais informações sobre opções de processamento, consulte [processar objetos &#40;XMLA&#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md) e [processando um modelo multidimensional &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 O exemplo de código faz um processamento completo de todas as partições de um grupo de medidas especificado.  
  
```  
static void FullProcessAllPartitions(MeasureGroup mg)  
{  
    foreach (Partition part in mg.Partitions)  
        part.Process(ProcessType.ProcessFull);  
}  
```  
  
### <a name="merging-partitions"></a>Mesclando partições  
 A mesclagem de partições significa executar qualquer operação que resulta em duas ou mais partições se tornando uma partição.  
  
 A mesclagem de partições é um método do objeto <xref:Microsoft.AnalysisServices.Partition>. Esse comando mescla os dados de uma ou mais partições de origem em uma partição de destino e exclui as partições de origem.  
  
 As partições só poderão ser mescladas se satisfizerem todos os critérios a seguir:  
  
-   As partições estão no mesmo grupo de medidas.  
  
-   As partições estão armazenadas no mesmo modo (MOLAP, HOLAP e ROLAP).  
  
-   As partições residem no mesmo servidor; as partições remotas poderão ser mescladas se estiverem no mesmo servidor.  
  
 Diferentemente das versões anteriores, em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] não é necessário que todas as partições de origem tenham um design de agregações idêntico.  
  
 O conjunto resultante de agregações para a partição de destino será o mesmo conjunto de agregações quanto ao estado anterior à execução do comando de mesclagem.  
  
 O exemplo de código a seguir mescla todas as partições de um grupo de medidas especificado. As partições são mescladas na primeira partição do grupo de medidas.  
  
```  
static void MergeAllPartitions(MeasureGroup mg)  
{  
    if (mg.Partitions.Count > 1)  
    {  
        Partition[] partArray = new Partition[mg.Partitions.Count - 1];  
        for (int i = 1; i < mg.Partitions.Count; i++)  
            partArray[i - 1] = mg.Partitions[i];  
        mg.Partitions[0].Merge(partArray);  
        //To have last changes in the server reflected in AMO  
        mg.Refresh();  
    }  
```  
  
##  <a name="AD"></a> Objetos de agregação  
 Para criar uma agregação e aplicá-la a uma ou mais partições, você programa o objeto <xref:Microsoft.AnalysisServices.Aggregation>.  
  
### <a name="creating-and-dropping-aggregations"></a>Criando e descartando agregações  
 As agregações podem ser facilmente criadas e atribuídas a grupos de medidas ou a partições usando o método DesignAggregations do objeto <xref:Microsoft.AnalysisServices.AggregationDesign>. O objeto <xref:Microsoft.AnalysisServices.AggregationDesign> é um objeto separado da partição, o objeto <xref:Microsoft.AnalysisServices.AggregationDesign> está contido no objeto <xref:Microsoft.AnalysisServices.MeasureGroup>. As agregações podem ser criadas até o nível especificado de otimização (0 a 100) ou até nível especificado de armazenamento (bytes). Várias partições podem usar o mesmo design de agregação.  
  
 O exemplo de código a seguir cria agregações para todas as partições de um grupo de medidas fornecido. Qualquer agregação existente em partições será descartada.  
  
```  
static public String DesignAggregationsOnPartitions(MeasureGroup mg, double optimizationWanted, double maxStorageBytes)  
{  
    double optimization = 0;  
    double storage = 0;  
    long aggCount = 0;  
    bool finished = false;  
    AggregationDesign ad = null;  
    String aggDesignName;  
    String AggregationsDesigned = "";  
    aggDesignName = mg.AggregationPrefix + "_" + mg.Name;  
    ad = mg.AggregationDesigns.Add();  
    ad.Name = aggDesignName;  
    ad.InitializeDesign();  
    while ((!finished) && (optimization < optimizationWanted) && (storage < maxStorageBytes))  
    {  
        ad.DesignAggregations(out optimization, out storage, out aggCount, out finished);  
    }  
    ad.FinalizeDesign();  
    foreach (Partition part in mg.Partitions)  
    {  
        part.AggregationDesignID = ad.ID;  
        AggregationsDesigned += aggDesignName + " = " + aggCount.ToString() + " aggregations designed\r\n\tOptimization: " + optimization.ToString() + "/" + optimizationWanted.ToString() + "\n\r\tStorage: " + storage.ToString() + "/" + maxStorageBytes.ToString() + " ]\n\r";  
     }  
     return AggregationsDesigned;  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices>   
 [Introdução às Classes AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [Classes OLAP AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-olap-classes.md)   
 [Arquitetura lógica &#40; Analysis Services - dados multidimensionais &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Objetos de banco de dados &#40; Analysis Services - dados multidimensionais &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [Processando um modelo multidimensional &#40;do Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Instalar dados de exemplo e projetos do Analysis Services Multidimensional Modeling Tutorial](../../../analysis-services/install-sample-data-and-projects.md)  
  
  
