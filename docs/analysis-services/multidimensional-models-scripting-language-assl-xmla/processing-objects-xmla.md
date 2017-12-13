---
title: Processando objetos (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- errors [XML for Analysis]
- objects [XML for Analysis]
- XML for Analysis, objects
- XMLA, partitions
- partitions [Analysis Services], XML for Analysis
- XML for Analysis, partitions
- writeback [Analysis Services], XML for Analysis
- out-of-line bindings
- processing objects [XML for Analysis]
- XMLA, objects
ms.assetid: a65b3249-303d-49c6-98af-6ac6eed11a03
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9d4b3c24a3bfe2b9babcc13d9e9263a4457676bb
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="processing-objects-xmla"></a>Processando objetos (XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o processamento é a etapa ou série de etapas que transformam dados em informações para análise de negócios. O processamento será diferente dependendo do tipo de objeto, mas sempre fará parte da transformação de dados em informações.  
  
 Para processar um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] do objeto, você pode usar o [processo](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) comando. O **processo** comando pode processar os seguintes objetos de um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância:  
  
-   Cubes  
  
-   Bancos de dados  
  
-   Dimensões  
  
-   Grupos de medidas  
  
-   Modelos de mineração  
  
-   Estruturas de mineração  
  
-   Partições  
  
 Para controlar o processamento de objetos, o **processo** comando possui diversas propriedades que podem ser definidas. O **processo** comando tem propriedades que controlam: quanto processamento será feito, quais objetos serão processados, se deseja usar associações fora de linha, como tratar erros e como gerenciar tabelas de write-back.  
  
## <a name="specifying-processing-options"></a>Especificando opções de processamento  
 O [tipo](../../analysis-services/xmla/xml-elements-properties/type-element-xmla.md) propriedade o **processo** comando Especifica a opção de processamento a ser usado ao processar o objeto. Para obter mais informações sobre as opções de processamento, consulte [Opções e configurações de processamento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
 A tabela a seguir lista as constantes para o **tipo** propriedade e os vários objetos que podem ser processados usando cada constante.  
  
|**Tipo** valor|Objetos aplicáveis|  
|--------------------|------------------------|  
|*ProcessFull*|Cubo, banco de dados, dimensão, grupo de medidas, modelo de mineração, estrutura de mineração, partição|  
|*ProcessAdd*|Dimensão, partição|  
|*ProcessUpdate*|Dimensão|  
|*ProcessIndexes*|Dimensão, cubo, grupo de medidas, partição|  
|*ProcessData*|Dimensão, cubo, grupo de medidas, partição|  
|*ProcessDefault*|Cubo, banco de dados, dimensão, grupo de medidas, modelo de mineração, estrutura de mineração, partição|  
|*ProcessClear*|Cubo, banco de dados, dimensão, grupo de medidas, modelo de mineração, estrutura de mineração, partição|  
|*ProcessStructure*|Cubo, estrutura de mineração|  
|*ProcessClearStructureOnly*|Estrutura de mineração|  
|*ProcessScriptCache*|Cube|  
  
 Para obter mais informações sobre o processamento [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objetos, consulte [processando um modelo multidimensional &#40; Analysis Services &#41; ](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
## <a name="specifying-objects-to-be-processed"></a>Especificando objetos a serem processados  
 O [objeto](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) propriedade o **processo** comando contém o identificador de objeto do objeto a ser processado. Apenas um objeto pode ser especificado em uma **processo** comando, mas o processamento de um objeto também processará qualquer objeto filho. Por exemplo, o processamento de um grupo de medidas em um cubo processará todas as partições desse grupo de medidas, enquanto que o processamento de um banco de dados processará todos os objetos, incluindo cubos, dimensões e estruturas de mineração, contidos nele.  
  
 Se você definir o **ProcessAffectedObjects** atributo o **processo** comando como true, todas relacionadas a objeto afetado pelo processamento do objeto especificado também é processado. Por exemplo, se uma dimensão for atualizada incrementalmente usando o *ProcessUpdate* opção de processamento de **processo** de comando, qualquer partição cuja agregação for invalidada por causa de membros que está sendo Para adicionar ou excluir também será processada pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se **ProcessAffectedObjects** é definido como true. Em um único caso, **processo** comando pode processar vários objetos em um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância, mas [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determina quais objetos além do objeto único especificado no **processo** comando também deve ser processado.  
  
 No entanto, você pode processar vários objetos, como dimensões, ao mesmo tempo usando vários **processo** comandos dentro de um **lote** comando. Operações em lotes oferece um nível mais refinado de controle para processamento serial ou paralelo de objetos em um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância usando o **ProcessAffectedObjects** de atributos e permitir que você ajuste sua abordagem de processamento maior [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bancos de dados. Para obter mais informações sobre como executar operações em lote, consulte [executando operações de lote &#40; XMLA &#41; ](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md).  
  
## <a name="specifying-out-of-line-bindings"></a>Especificando associações fora de linha  
 Se o **processo** comando não está contido em um **lote** comando, você pode opcionalmente especificar associações fora de linha no [associações](../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md), [defontededados](../../analysis-services/xmla/xml-elements-properties/datasource-element-xmla.md), e [DataSourceView](../../analysis-services/xmla/xml-elements-properties/datasourceview-element-xmla.md) propriedades do **processo** comando para os objetos a serem processados. Associações fora de linha são referências a fontes de dados, exibições da fonte de dados e outros objetos no qual a associação existe somente durante a execução do **processo** comando e que substitui qualquer associação associada a objetos que estão sendo processados. Se associações fora de linha não forem especificadas, serão usadas as associações atualmente associadas aos objetos a serem processados.  
  
 As associações fora de linha são usadas nas seguintes circunstâncias:  
  
-   No processamento incremental de uma partição, no qual uma tabela de fatos alternativa ou um filtro da tabela de fatos existente deve ser especificado para garantir que as linhas não sejam contadas duas vezes.  
  
-   Usando uma tarefa de fluxo de dados em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para fornecer dados durante o processamento de uma dimensão, um modelo de mineração ou uma partição.  
  
 As associações fora de linha são descritas como parte da ASSL (Analysis Services Scripting Language). Para obter mais informações sobre associações fora de linha em ASSL, consulte [fontes de dados e associações &#40; SSAS Multidimensional &#41; ](../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
### <a name="incrementally-updating-partitions"></a>Atualizando partições incrementalmente  
 Atualizar incrementalmente uma partição já processada normalmente exige uma associação fora de linha, já que a associação especificada para a partição faz referência aos dados da tabela de fatos já agregados na partição. Ao atualizar incrementalmente uma partição já processada usando a **processo** comando [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] executa as seguintes ações:  
  
-   Cria uma partição temporária com uma estrutura idêntica à da partição a ser atualizada incrementalmente.  
  
-   Processa a partição temporária, usando a associação fora de linha especificada no **processo** comando.  
  
-   Mescla a partição temporária com a partição selecionada existente.  
  
 Para obter mais informações sobre como mesclar partições usando XML for Analysis (XMLA), consulte [mesclando partições &#40; XMLA &#41; ](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/merging-partitions-xmla.md).  
  
## <a name="handling-processing-errors"></a>Manipulando erros de processamento  
 O [ErrorConfiguration](../../analysis-services/xmla/xml-elements-properties/errorconfiguration-element-xmla.md) propriedade o **processo** comando permite que você especifique como tratar erros encontrados durante o processamento de um objeto. Por exemplo, durante o processamento de uma dimensão, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] encontra um valor duplicado na coluna de chave do atributo de chave. Como as chaves de atributo devem ser exclusivas, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] descarta os registros duplicados. Com base no [KeyDuplicate](../../analysis-services/scripting/properties/keyduplicate-element-assl.md) propriedade **ErrorConfiguration**, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] foi:  
  
-   Ignorar o erro e continuar o processamento da dimensão.  
  
-   Retornar uma mensagem declarando que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] encontrou uma chave duplicada e continuar o processamento.  
  
 Há muitas condições semelhantes para o qual **ErrorConfiguration** oferece opções durante uma **processo** comando.  
  
## <a name="managing-writeback-tables"></a>Gerenciando tabelas de write-back  
 Se o **processo** comando encontra uma partição habilitada para gravação, ou um cubo ou grupo de medidas para uma partição, que não é totalmente processada, uma tabela de write-back não existir para essa partição. O [WritebackTableCreation](../../analysis-services/xmla/xml-elements-properties/writebacktablecreation-element-xmla.md) propriedade o **processo** comando determina se [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devem criar uma tabela de write-back.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="description"></a>Description  
 O exemplo a seguir processa totalmente o banco de dados [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] de exemplo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
### <a name="code"></a>Código  
  
```  
<Process xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Object>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
  </Object>  
  <Type>ProcessFull</Type>  
  <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
</Process>  
```  
  
### <a name="description"></a>Description  
 O exemplo a seguir processa incrementalmente a **Internet_Sales_2004** partição o **vendas pela Internet** grupo de medidas do **Adventure Works DW** cubo no [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] exemplo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados. O **processo** comando está adicionando agregações para ordem datas depois de 31 de dezembro de 2006 à partição usando uma associação de consulta fora de linha no **associações** propriedade o **processo**  comando para recuperar as linhas da tabela de fatos da qual gerar agregações para adicionar à partição.  
  
### <a name="code"></a>Código  
  
```  
<Process ProcessAffectedObjects="true" xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Object>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    <CubeID>Adventure Works DW</CubeID>  
    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
    <PartitionID>Internet_Sales_2006</PartitionID>  
  </Object>  
  <Bindings>  
    <Binding>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2006</PartitionID>  
      <Source xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="QueryBinding">  
        <DataSourceID>Adventure Works DW</DataSourceID>  
        <QueryDefinition>  
          SELECT  
            [dbo].[FactInternetSales].[ProductKey],  
            [dbo].[FactInternetSales].[OrderDateKey],  
            [dbo].[FactInternetSales].[DueDateKey],  
            [dbo].[FactInternetSales].[ShipDateKey],   
            [dbo].[FactInternetSales].[CustomerKey],   
            [dbo].[FactInternetSales].[PromotionKey],  
            [dbo].[FactInternetSales].[CurrencyKey],  
            [dbo].[FactInternetSales].[SalesTerritoryKey],  
            [dbo].[FactInternetSales].[SalesOrderNumber],  
            [dbo].[FactInternetSales].[SalesOrderLineNumber],  
            [dbo].[FactInternetSales].[RevisionNumber],  
            [dbo].[FactInternetSales].[OrderQuantity],  
            [dbo].[FactInternetSales].[UnitPrice],  
            [dbo].[FactInternetSales].[ExtendedAmount],  
            [dbo].[FactInternetSales].[UnitPriceDiscountPct],  
            [dbo].[FactInternetSales].[DiscountAmount],  
            [dbo].[FactInternetSales].[ProductStandardCost],  
            [dbo].[FactInternetSales].[TotalProductCost],  
            [dbo].[FactInternetSales].[SalesAmount],  
            [dbo].[FactInternetSales].[TaxAmt],  
            [dbo].[FactInternetSales].[Freight],  
            [dbo].[FactInternetSales].[CarrierTrackingNumber],  
            [dbo].[FactInternetSales].[CustomerPONumber]  
          FROM [dbo].[FactInternetSales]  
          WHERE OrderDateKey > '1280'  
        </QueryDefinition>  
      </Source>  
    </Binding>  
  </Bindings>  
  <Type>ProcessAdd</Type>  
  <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
</Process>  
```  
  
  
