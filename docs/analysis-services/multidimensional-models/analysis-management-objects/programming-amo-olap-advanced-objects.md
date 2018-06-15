---
title: Objetos de programação AMO OLAP avançados | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: amo
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 03114f3f88d53efa01580e07db164c679b324661
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34024353"
---
# <a name="programming-amo-olap-advanced-objects"></a>Programando objetos OLAP AMO avançados
  Este tópico explica os detalhes de programação AMO (Objetos de Gerenciamento de Análise) de objetos OLAP avançados. Este tópico contém as seguintes seções:  
  
-   [Objetos de ação](#Action)  
  
-   [Objetos KPI](#KPI)  
  
-   [Objetos de perspectiva](#Persp)  
  
-   [Objetos ProactiveCaching](#PC)  
  
-   [Objetos de tradução](#Transl)  
  
##  <a name="Action"></a> Objetos de ação  
 As classes de ação são usadas para criar uma resposta ativa durante a navegação em certas áreas do cubo. Os objetos de ação podem ser definidos usando AMO, mas são usados do aplicativo cliente que procura os dados. As ações podem ser de tipos diferentes e devem ser criadas de acordo com seu tipo. As ações podem ser:  
  
-   Ações de detalhamento, que retornam o conjunto de linhas que representa os dados subjacentes das células selecionadas do cubo onde a ação ocorre.  
  
-   Ações de relatório, que retornam um relatório do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] associado a uma seção selecionada do cubo onde a ação ocorre.  
  
-   Ações padrão, que retornam o elemento de ação (URL, HTML, DataSet, RowSet e outros elementos) associado a uma seção selecionada do cubo onde a ação ocorre.  
  
 A criação de um objeto de ação exige as seguintes etapas:  
  
1.  Crie o objeto de ação derivado e preencha os atributos básicos.  
  
     A seguir, os atributos básicos: tipo de ação, tipo de destino ou de seção do cubo, área de destino ou específica do cubo onde a ação está disponível, legenda e onde a legenda será uma expressão MDX.  
  
2.  Preencha os atributos específicos do tipo de ação.  
  
     Os atributos são diferentes para os três tipos de ações, consulte o exemplo de código a seguir para obter os parâmetros.  
  
3.  Adicione a ação à coleção de cubos e atualize o cubo. A ação não é um objeto atualizável.  
  
 O teste da ação exige um aplicativo de programa diferente. Você pode testar a sua ação no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. Primeiro, você deve instalar [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] exemplos, consulte [processando um modelo multidimensional &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 O código de exemplo a seguir replica três ações diferentes do exemplo de projeto Adventure Works do Analysis Services. Você pode diferenciar as ações porque as que serão introduzidas por meio do exemplo a seguir começam por "My".  
  
```  
static public void CreateActions(Cube cube)  
{  
    #region Adding a drillthrough action  
    // Verify That action exists and drop it  
    if (cube.Actions.ContainsName("My Reseller Details"))  
        cube.Actions.Remove("My Drillthrough Action",true);  
  
    //Create a Drillthrough action  
    DrillThroughAction dtaction = new DrillThroughAction("My Reseller Details", "My Drillthrough Action");  
  
    //Define the Action  
    dtaction.Type = ActionType.DrillThrough;  
    dtaction.TargetType = ActionTargetType.Cells;  
    dtaction.Target = "MeasureGroupMeasures(\"Reseller Sales\")";  
    dtaction.Caption = "My Drillthrough...";  
    dtaction.CaptionIsMdx = false;  
  
    #region create drillthrough action specifics  
    //Adding Drillthrough columns  
    //Adding Measure columns to the drillthrough  
    MeasureGroup mg = cube.MeasureGroups.FindByName("Reseller Sales");  
    MeasureBinding mb1 = new MeasureBinding();  
    mb1.MeasureID = mg.Measures.FindByName( "Reseller Sales Amount").ID;  
    dtaction.Columns.Add(mb1);  
  
    MeasureBinding mb2 = new MeasureBinding();  
    mb2.MeasureID = mg.Measures.FindByName("Reseller Order Quantity").ID;  
    dtaction.Columns.Add(mb2);  
  
    MeasureBinding mb3 = new MeasureBinding();  
    mb3.MeasureID = mg.Measures.FindByName("Reseller Unit Price").ID;  
    dtaction.Columns.Add(mb3);  
  
    //Adding Dimension Columns to the drillthrough  
    CubeAttributeBinding cb1 = new CubeAttributeBinding();  
    cb1.CubeID = cube.ID;  
    cb1.CubeDimensionID = cube.Dimensions.FindByName("Reseller").ID;  
    cb1.AttributeID = "Reseller Name";  
    cb1.Type = AttributeBindingType.All;  
    dtaction.Columns.Add(cb1);  
  
    CubeAttributeBinding cb2 = new CubeAttributeBinding();  
    cb2.CubeID = cube.ID;  
    cb2.CubeDimensionID = cube.Dimensions.FindByName("Product").ID;  
    cb2.AttributeID = "Product Name";  
    cb2.Type = AttributeBindingType.All;  
    dtaction.Columns.Add(cb2);  
    #endregion  
  
    //Add the defined action to the cube  
    cube.Actions.Add(dtaction);  
    #endregion  
  
    #region Adding a Standard action  
    // Verify That action exists and drop it  
    if (cube.Actions.ContainsName("My City Map"))  
        cube.Actions.Remove("My Action", true);  
  
    //Create a Drillthrough action  
    StandardAction stdaction = new StandardAction("My City Map", "My Action");  
  
    //Define the Action  
    stdaction.Type = ActionType.Url;  
    stdaction.TargetType = ActionTargetType.AttributeMembers;  
    stdaction.Target = "[Geography].[City]";  
    stdaction.Caption = "\"My View Map for \" + [Geography].[City].CurrentMember.Member_Caption + \"...\"";  
    stdaction.CaptionIsMdx = true;  
  
    #region create standard action specifics  
    stdaction.Expression = "\"http://maps.msn.com/home.aspx?plce1=\" + " +  
        "[Geography].[City].CurrentMember.Name + \",\" + " +  
        "[Geography].[State-Province].CurrentMember.Name + \",\" + " +  
        "[Geography].[Country].CurrentMember.Name + " +  
        "\"&regn1=\" + " +  
        "Case " +  
            "When [Geography].[Country].CurrentMember Is " +  
                    "[Geography].[Country].&[Australia] " +  
                "Then \"3\" " +  
            "When [Geography].[Country].CurrentMember Is " +  
                    "[Geography].[Country].&[Canada] " +  
                "Or [Geography].[Country].CurrentMember Is " +  
                    "[Geography].[Country].&[United States] " +  
                "Then \"0\" " +  
                "Else \"1\" " +  
        "End ";  
    #endregion  
  
    //Add the defined action to the cube  
    cube.Actions.Add(stdaction);  
  
    #endregion  
  
    #region Adding a Reporting action  
    // Verify That action exists and drop it  
    if (cube.Actions.ContainsName("My Sales Reason Comparisons"))  
        cube.Actions.Remove("My Report Action", true);  
  
    //Create a Report action  
    ReportAction rsaction = new ReportAction("My Sales Reason Comparisonsp", "My Report Action");  
  
    //Define the Action  
    rsaction.Type = ActionType.Report;  
    rsaction.TargetType = ActionTargetType.AttributeMembers;  
    rsaction.Target = "[Product].[Category]";  
    rsaction.Caption = "\"My Sales Reason Comparisons for \" + [Product].[Category].CurrentMember.Member_Caption + \"...\"";  
    rsaction.CaptionIsMdx = true;  
  
    #region create Report action specifics  
    rsaction.ReportServer = "MyRSSamplesServer";  
    rsaction.Path = "ReportServer?/AdventureWorks Sample Reports/Sales Reason Comparisons";  
    rsaction.ReportParameters.Add("ProductCategory", "UrlEscapeFragment( [Product].[Category].CurrentMember.UniqueName )");  
    rsaction.ReportFormatParameters.Add("rs:Command", "Render");  
    rsaction.ReportFormatParameters.Add("rs:Renderer", "HTML5");  
    #endregion  
  
    //Add the defined action to the cube  
    cube.Actions.Add(rsaction);  
  
    #endregion  
}  
```  
  
##  <a name="KPI"></a> Objetos KPI  
 Um KPI (indicador chave de desempenho) é uma coleção de cálculos associada a um grupo de medidas em um cubo e é usado para avaliar sucesso nos negócios. Os objetos <xref:Microsoft.AnalysisServices.Kpi> podem ser definidos pelo AMO, mas são usados a partir do aplicativo cliente que procura os dados.  
  
 A criação de um objeto <xref:Microsoft.AnalysisServices.Kpi> exige as seguintes etapas:  
  
1.  Criar o objeto <xref:Microsoft.AnalysisServices.Kpi> e preencha os atributos básicos.  
  
     A seguir, uma lista de atributos básicos: Description, Display Folder, Associated Measure Group e Value. Display Folder diz ao aplicativo cliente onde o KPI deve ser localizado para que o usuário final possa encontrá-lo. Associated Measure Group indica o grupo de medidas onde todos os cálculos MDX devem ser referenciados. Value mostra o valor real do indicador de desempenho como uma expressão MDX.  
  
2.  Defina indicadores KPI: Goal, Status e Trend.  
  
     Os indicadores são expressões MDX que devem ser avaliadas entre -1 e 1, mas é o aplicativo de navegação que definirá o intervalo de valores para os indicadores.  
  
3.  Quando você procura por KPIs no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], os valores menores do que -1 são tratados como -1 e os valores maiores do que 1 são tratados como 1.  
  
4.  Defina imagens gráficas.  
  
     As imagens gráficas são valores de cadeia de caracteres, usados como referência no aplicativo cliente para identificar o conjunto correto de imagens a serem exibidas. A cadeia de imagens gráficas também define o comportamento da função de exibição. Normalmente, o intervalo é dividido em um número ímpar de estados, do ruim para o bom e para cada estado será atribuída uma imagem do conjunto.  
  
     Se você usar o [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] para procurar seu KPIs, dependendo dos nomes, o intervalo de indicadores será dividido em três ou em cinco estados. Além disso, existem nomes onde o intervalo é invertido, ou seja, -1 é 'Bom' e 1 é 'Ruim'. No [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], três estados do intervalo são os seguintes:  
  
    -   Ruim = -1 a -0,5  
  
    -   OK = -0,4999 a 0,4999  
  
    -   Bom = 0,50 a 1  
  
     No [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], cinco estados do intervalo são os seguintes:  
  
    -   Inválido = -1 a -0,75  
  
    -   Risco = -0,7499 a -0,25  
  
    -   OK = -0,2499 a 0,2499  
  
    -   Subindo = 0,25 a 0,7499  
  
    -   Bom = 0,75 a 1  
  
 A tabela a seguir lista o uso, o nome e o número de estados associados à imagem.  
  
|Uso da imagem|Nome da imagem|Número de estados|  
|-----------------|----------------|----------------------|  
|Status|Formas|3|  
|Status|Sinal de trânsito|3|  
|Status|Placas de trânsito|3|  
|Status|Medidor|3|  
|Status|Medidor invertido|5|  
|Status|Termômetro|3|  
|Status|Cilindro|3|  
|Status|Faces|3|  
|Status|Seta de variação|3|  
|Tendência|Seta padrão|3|  
|Tendência|Seta de status|3|  
|Tendência|Seta de status invertida|5|  
|Tendência|Faces|3|  
  
1.  Adicione o KPI à coleção de cubos e atualize o cubo, já que o KPI não é um objeto atualizável.  
  
 O teste do KPI exige um aplicativo de programa diferente. Você pode testar o seu KPI no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].  
  
 O exemplo de código a seguir cria um KPI na pasta "Financial Perspective/Grow Revenue" do cubo Adventure Works incluído no exemplo de projeto Adventure Works do Analysis Services.  
  
```  
static public void CreateKPIs(Cube cube)  
{  
    Kpi kpi = cube.Kpis.Add("My Internet Revenue", "My Internet Revenue");  
    kpi.Description = "(My) Revenue achieved through direct sales via Interner";  
    kpi.DisplayFolder = "\\Financial Perspective\\Grow Revenue";  
    kpi.AssociatedMeasureGroupID = "Internet Sales";  
    kpi.Value = "[Measures].[Internet Sales Amount]";  
    #region Goal  
    kpi.Goal = "Case" +  
               "     When IsEmpty" +  
               "          (" +  
               "            ParallelPeriod" +  
               "            (" +  
               "              [Date].[Fiscal Time].[Fiscal Year]," +  
               "              1," +  
               "              [Date].[Fiscal Time].CurrentMember" +  
               "            )" +  
               "          )" +   
               "     Then [Measures].[Internet Sales Amount]" +  
               "     Else 1.10 *" +  
               "          (" +  
               "            [Measures].[Internet Sales Amount]," +  
               "            ParallelPeriod" +  
               "            (" +  
               "              [Date].[Fiscal Time].[Fiscal Year]," +  
               "              1," +  
               "              [Date].[Fiscal Time].CurrentMember" +  
               "            )" +  
               "          ) " +  
               " End";  
    #endregion  
    #region Status  
    kpi.Status = "Case" +  
                 "   When KpiValue( \"Internet Revenue\" ) / KpiGoal ( \"Internet Revenue\" ) >= .95 " +  
                 "   Then 1 " +  
                 "   When KpiValue( \"Internet Revenue\" ) / KpiGoal ( \"Internet Revenue\" ) <  .95 " +  
                 "        And  " +  
                 "        KpiValue( \"Internet Revenue\" ) / KpiGoal ( \"Internet Revenue\" ) >= .85 " +  
                 "   Then 0 " +  
                 "   Else -1 " +  
                 "End";  
    #endregion  
    #region Trend  
    kpi.Trend = "Case " +  
                "    When VBA!Abs " +  
                "         ( " +  
                "           KpiValue( \"Internet Revenue\" ) -  " +  
                "           ( " +  
                "             KpiValue ( \"Internet Revenue\" ), " +  
                "             ParallelPeriod " +  
                "             (  " +  
                "               [Date].[Fiscal Time].[Fiscal Year], " +  
                "               1, " +  
                "               [Date].[Fiscal Time].CurrentMember " +  
                "             ) " +  
                "           ) / " +  
                "           ( " +  
                "             KpiValue ( \"Internet Revenue\" ), " +  
                "             ParallelPeriod " +  
                "             (  " +  
                "               [Date].[Fiscal Time].[Fiscal Year], " +  
                "               1, " +  
                "               [Date].[Fiscal Time].CurrentMember " +  
                "             ) " +  
                "           )   " +  
                "         ) <=.02  " +  
                "    Then 0 " +  
                "    When KpiValue( \"Internet Revenue\" ) -  " +  
                "         ( " +  
                "           KpiValue ( \"Internet Revenue\" ), " +  
                "           ParallelPeriod " +  
                "           (  " +  
                "             [Date].[Fiscal Time].[Fiscal Year], " +  
                "             1, " +  
                "             [Date].[Fiscal Time].CurrentMember " +  
                "           ) " +  
                "         ) / " +  
                "         ( " +  
                "           KpiValue ( \"Internet Revenue\" ), " +  
                "           ParallelPeriod " +  
                "           (  " +  
                "             [Date].[Fiscal Time].[Fiscal Year], " +  
                "             1, " +  
                "             [Date].[Fiscal Time].CurrentMember " +  
                "           ) " +  
                "         )  >.02 " +  
                "    Then 1 " +  
                "    Else -1 " +  
                "End";  
    #endregion  
    kpi.TrendGraphic = "Standard Arrow";  
    kpi.StatusGraphic = "Cylinder";  
}.  
```  
  
##  <a name="Persp"></a> Objetos de perspectiva  
 Os objetos <xref:Microsoft.AnalysisServices.Perspective> podem ser definidos pelo AMO, mas são usados a partir do aplicativo cliente que procura os dados.  
  
 A criação de um objeto <xref:Microsoft.AnalysisServices.Perspective> exige as seguintes etapas:  
  
1.  Criar o objeto <xref:Microsoft.AnalysisServices.Perspective> e preencha os atributos básicos.  
  
     A seguir, uma lista de atributos básicos: Name, Default Measure, Description e Annotations.  
  
2.  Adicione todos os objetos do cubo pai que devem ser vistos pelo usuário final.  
  
     Adicione dimensões de cubo (atributos e hierarquias), grupos de medidas (medida e grupo de medidas), ações, KPIs e cálculos.  
  
3.  Adicione a perspectiva à coleção de cubos e atualize o cubo, já que a perspectiva não é um objeto atualizável.  
  
 O teste da perspectiva exige um aplicativo de programa diferente. Você pode testar a sua perspectiva no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].  
  
 O exemplo de código a seguir cria uma perspectiva chamada "Direct Sales" para o cubo fornecido.  
  
```  
static public void CreatePerspectives(Cube cube)  
{  
    Perspective perspective = cube.Perspectives.Add("Direct Sales", "Direct Sales");  
    CubeDimension dim1 = cube.Dimensions.GetByName("Date");  
    PerspectiveDimension pdim1 = perspective.Dimensions.Add(dim1.DimensionID);  
    pdim1.Attributes.Add("Date");  
    pdim1.Attributes.Add("Calendar Year");  
    pdim1.Attributes.Add("Fiscal Year");  
    pdim1.Attributes.Add("Calendar Quarter");  
    pdim1.Attributes.Add("Fiscal Quarter");  
    pdim1.Attributes.Add("Calendar Month Number");  
    pdim1.Attributes.Add("Fiscal Month Number");  
    pdim1.Hierarchies.Add("Calendar Time");  
    pdim1.Hierarchies.Add("Fiscal Time");  
  
    CubeDimension dim2 = cube.Dimensions.GetByName("Product");  
    PerspectiveDimension pdim2 = perspective.Dimensions.Add(dim2.DimensionID);  
    pdim2.Attributes.Add("Product Name");  
    pdim2.Attributes.Add("Product Line");  
    pdim2.Attributes.Add("Model Name");  
    pdim2.Attributes.Add("List Price");  
    pdim2.Attributes.Add("Size");  
    pdim2.Attributes.Add("Weight");  
    pdim2.Hierarchies.Add("Product Model Categories");  
    pdim2.Hierarchies.Add("Product Categories");  
  
    PerspectiveMeasureGroup pmg = perspective.MeasureGroups.Add("Internet Sales");  
    pmg.Measures.Add("Internet Sales Amount");  
    pmg.Measures.Add("Internet Order Quantity");  
    pmg.Measures.Add("Internet Unit Price");  
  
    pmg = perspective.MeasureGroups.Add("Reseller Sales");  
    pmg.Measures.Add("Reseler Sales Amount");  
    pmg.Measures.Add("Reseller Order Quantity");  
    pmg.Measures.Add("Reseller Unit Price");  
  
    PerspectiveAction pact = perspective.Actions.Add("Drillthrough Action");  
  
    PerspectiveKpi pkpi = perspective.Kpis.Add("Internet Revenue");  
    Cube.Update();  
}  
```  
  
##  <a name="PC"></a> Objetos ProactiveCaching  
 Os objetos <xref:Microsoft.AnalysisServices.ProactiveCaching> podem ser definidos pelo AMO.  
  
 A criação de um objeto <xref:Microsoft.AnalysisServices.ProactiveCaching> exige as seguintes etapas:  
  
1.  Crie o objeto <xref:Microsoft.AnalysisServices.ProactiveCaching>.  
  
     Não há nenhum atributo básico a ser definido.  
  
2.  Adicione especificações de cache.  
  
|Especificação|Description|  
|-------------------|-----------------|  
|AggregationStorage|O tipo de armazenamento para agregações.<br /><br /> Aplica-se somente a partições. Na dimensão, deve ser **Regular.**|  
|SilenceInterval|Quantidade mínima de tempo em que o cache existirá antes do início do processo de imagens MOLAP.|  
|Latência|O período de tempo entre a primeira notificação e o momento em que as imagens MOLAP são destruídas.|  
|SilenceOverrideInterval|O tempo depois de uma notificação inicial depois da qual o processamento de imagens MOLAP é acionado incondicionalmente.|  
|ForceRebuildInterval|O tempo (começando depois que uma imagem MOLAP atualizada é descartada) depois do qual o processamento de imagens MOLAP é iniciado incondicionalmente (sem notificações).|  
|OnlineMode|Quando a imagem MOLAP está disponível.<br /><br /> Pode ser **Immediate** ou **OnCacheComplete**.|  
  
1.  Adicione o objeto <xref:Microsoft.AnalysisServices.ProactiveCaching> à coleção pai. Você precisará atualizar o pai, porque <xref:Microsoft.AnalysisServices.ProactiveCaching> não é um objeto atualizável.  
  
 O exemplo de código a seguir cria um objeto <xref:Microsoft.AnalysisServices.ProactiveCaching> em todas as partições a partir do grupo de medidas Internet Sales do cubo Adventure Works em um banco de dados especificado.  
  
```  
static public void SetProactiveCachingSettings(Database db)  
{  
    ProactiveCaching pc;  
    if (db.Cubes.ContainsName("Adventure Works") && db.Cubes.FindByName("Adventure Works").MeasureGroups.ContainsName("Internet Sales"))  
    {  
        ProactiveCachingTablesBinding pctb;  
        TableNotification tn;  
  
        MeasureGroup mg = db.Cubes.FindByName("Adventure Works").MeasureGroups.FindByName("Internet Sales");  
        foreach(Partition part in mg.Partitions)  
        {  
            pc = new ProactiveCaching();  
            pc.AggregationStorage = ProactiveCachingAggregationStorage.MolapOnly;  
            pc.SilenceInterval = TimeSpan.FromSeconds(10);  
            pc.Latency = TimeSpan.FromSeconds(-1);  
            pc.SilenceOverrideInterval = TimeSpan.FromMinutes(10);  
            pc.ForceRebuildInterval = TimeSpan.FromSeconds(-1);  
            pc.Enabled = true;  
            pc.OnlineMode = ProactiveCachingOnlineMode.OnCacheComplete;  
            pctb = new ProactiveCachingTablesBinding();  
            pctb.NotificationTechnique = NotificationTechnique.Server;  
            tn = new TableNotification("[FactInternetSales]", "dbo");  
            pctb.TableNotifications.Add( tn);  
            pc.Source = pctb;  
  
            part.ProactiveCaching = pc;  
            part.Update();  
        }  
    }  
}  
```  
  
##  <a name="Transl"></a> Objetos de tradução  
 Os objetos de tradução podem ser definidos pelo AMO, mas são usados a partir do aplicativo cliente que procura os dados. Os objetos de tradução são objetos simples de codificar. As traduções para legendas de objeto são fornecidas em pares de Identificador de Localidade e Legenda Traduzida. Para qualquer legenda, podem ser habilitadas várias traduções. As traduções podem ser fornecidas para a maioria dos objetos do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], como dimensões, atributos, hierarquias, cubos, grupos de medidas, medidas e outros.  
  
 O exemplo de código a seguir oferece uma tradução de espanhol para o nome do atributo Product Name.  
  
```  
static public void CreateTranslations(Database db)  
{  
    //Spanish Tranlations for Product Category in Product Dimension  
    Dimension dim = db.Dimensions["Product"];  
    DimensionAttribute atr = dim.Attributes["Product Name"];  
    Translation tran = atr.Translations.Add(3082);  
    tran.Caption = "Nombre Producto";  
  
    dim.Update(UpdateOptions.ExpandFull);  
  
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
  
  
