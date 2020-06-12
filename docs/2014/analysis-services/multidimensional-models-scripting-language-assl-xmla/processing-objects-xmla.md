---
title: Objetos de processamento (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
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
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2e59c7953ae8fc7d3cfceafa7b0e9d8c7186daf8
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544899"
---
# <a name="processing-objects-xmla"></a>Processando objetos (XMLA)
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , o processamento é a etapa ou série de etapas que transforma dados em informações para análise de negócios. O processamento será diferente dependendo do tipo de objeto, mas sempre fará parte da transformação de dados em informações.  
  
 Para processar um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objeto, você pode usar o comando [process](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla) . O comando `Process` pode processar os seguintes objetos de uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
-   Cubes  
  
-   Bancos de dados  
  
-   Dimensões  
  
-   Grupos de medidas  
  
-   Modelos de mineração  
  
-   Estruturas de mineração  
  
-   Partições  
  
 Para controlar o processamento de objetos, o comando `Process` tem várias propriedades que podem ser definidas. O comando `Process` tem propriedades que controlam: quanto processamento será feito, que objetos serão processados, se as associações fora de linha serão usadas, como manipular erros e como gerenciar tabelas de write-back.  
  
## <a name="specifying-processing-options"></a>Especificando opções de processamento  
 A propriedade [Type](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla) do `Process` comando especifica a opção de processamento a ser usada ao processar o objeto. Para obter mais informações sobre as opções de processamento, consulte [Opções e configurações de processamento &#40;Analysis Services&#41;](../multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
 A tabela a seguir lista as constantes para a propriedade `Type` e os vários objetos que podem ser processados usando cada constante.  
  
|`Type` valor|Objetos aplicáveis|  
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
  
 Para obter mais informações sobre o processamento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objetos, consulte [processamento de objeto de modelo multidimensional](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
## <a name="specifying-objects-to-be-processed"></a>Especificando objetos a serem processados  
 A propriedade [Object](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) do `Process` comando contém o identificador de objeto do objeto a ser processado. Somente um objeto pode ser especificado em um comando `Process`, mas processar um objeto também processará qualquer objeto filho. Por exemplo, o processamento de um grupo de medidas em um cubo processará todas as partições desse grupo de medidas, enquanto que o processamento de um banco de dados processará todos os objetos, incluindo cubos, dimensões e estruturas de mineração, contidos nele.  
  
 Se você definir o atributo `ProcessAffectedObjects` do comando `Process` como verdadeiro, qualquer objeto relacionado afetado pelo processamento do objeto especificado também será processado. Por exemplo, se uma dimensão é atualizada incrementalmente usando a opção de processamento *ProcessUpdate* no `Process` comando, qualquer partição cujas agregações são invalidadas devido aos membros sendo adicionados ou excluídos também são processados pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] If `ProcessAffectedObjects` é definido como true. Nesse caso, um único comando `Process` pode processar vários objetos de uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], mas o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determinará que objetos, além do objeto único especificado no comando `Process`, também serão processados.  
  
 Porém, você pode processar vários objetos, como as dimensões, ao mesmo tempo usando vários comandos `Process` dentro de um comando `Batch`. As operações em lotes oferece um nível mais refinado de controle para o processamento em série ou em paralelo de objetos em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] do que a utilização do atributo `ProcessAffectedObjects`, além de permitir que você ajuste a sua abordagem de processamento para bancos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] maiores. Para obter mais informações sobre como executar operações em lote, consulte [executando operações em lote &#40;XMLA&#41;](performing-batch-operations-xmla.md).  
  
## <a name="specifying-out-of-line-bindings"></a>Especificando associações fora de linha  
 Se o `Process` comando não estiver contido em um `Batch` comando, você pode opcionalmente especificar associações fora de linha nas propriedades [bindings](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/bindings-element-xmla), [DataSource](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)e [DataSourceView](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourceview-element-xmla) do `Process` comando para os objetos a serem processados. As associações fora de linha são referências a fontes de dados, exibições de fonte de dados e outros objetos nos quais a associação só existe durante a execução do comando `Process` e que substitui qualquer associação associada aos objetos processados. Se associações fora de linha não forem especificadas, serão usadas as associações atualmente associadas aos objetos a serem processados.  
  
 As associações fora de linha são usadas nas seguintes circunstâncias:  
  
-   No processamento incremental de uma partição, no qual uma tabela de fatos alternativa ou um filtro da tabela de fatos existente deve ser especificado para garantir que as linhas não sejam contadas duas vezes.  
  
-   Usar uma tarefa de fluxo de dados no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para fornecer dados durante o processamento de uma dimensão, um modelo de mineração ou uma partição.  
  
 As associações fora de linha são descritas como parte da ASSL (Analysis Services Scripting Language). Para obter mais informações sobre associações fora de linha no ASSL, consulte [fontes de dados e associações &#40;&#41;multidimensional do SSAS ](../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
### <a name="incrementally-updating-partitions"></a>Atualizando partições incrementalmente  
 Atualizar incrementalmente uma partição já processada normalmente exige uma associação fora de linha, já que a associação especificada para a partição faz referência aos dados da tabela de fatos já agregados na partição. Ao atualizar incrementalmente uma partição já processada por meio do comando `Process`, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] executa as seguintes ações:  
  
-   Cria uma partição temporária com uma estrutura idêntica à da partição a ser atualizada incrementalmente.  
  
-   Processa a partição temporária, usando a associação fora de linha especificada no comando `Process`.  
  
-   Mescla a partição temporária com a partição selecionada existente.  
  
 Para obter mais informações sobre como mesclar partições usando XML for Analysis (XMLA), consulte [mesclando partições &#40;xmla&#41;](merging-partitions-xmla.md).  
  
## <a name="handling-processing-errors"></a>Manipulando erros de processamento  
 A propriedade [ErrorConfiguration](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/errorconfiguration-element-xmla) do `Process` comando permite que você especifique como tratar os erros encontrados durante o processamento de um objeto. Por exemplo, durante o processamento de uma dimensão, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] encontra um valor duplicado na coluna de chave do atributo de chave. Como as chaves de atributo devem ser exclusivas, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] descarta os registros duplicados. Com base na propriedade [KeyDuplicate](https://docs.microsoft.com/bi-reference/assl/properties/keyduplicate-element-assl) do `ErrorConfiguration` , o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] poderia:  
  
-   Ignorar o erro e continuar o processamento da dimensão.  
  
-   Retornar uma mensagem declarando que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] encontrou uma chave duplicada e continuar o processamento.  
  
 Existem muitas condições semelhantes para as quais `ErrorConfiguration` oferece opções durante um comando `Process`.  
  
## <a name="managing-writeback-tables"></a>Gerenciando tabelas de write-back  
 Se o comando `Process` encontrar uma partição de write-back, ou um cubo ou um grupo de medidas para essa partição, ela não será totalmente processada, pois pode ainda não haver uma tabela de write-back para ela. A propriedade [WriteBackTableCreation](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/writebacktablecreation-element-xmla) do `Process` comando determina se o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deve criar uma tabela de write-back.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="description"></a>Description  
 O exemplo a seguir processa totalmente o banco de dados [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] de exemplo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
### <a name="code"></a>Código  
  
```  
<Process xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
  <Object>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
  </Object>  
  <Type>ProcessFull</Type>  
  <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
</Process>  
```  
  
### <a name="description"></a>Descrição  
 O exemplo a seguir processa incrementalmente a partição de **Internet_Sales_2004** no grupo de medidas **vendas pela Internet** do cubo do **Adventure Works DW** no [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] banco de dados de exemplo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . O `Process` comando está adicionando agregações para datas de pedido posteriores a 31 de dezembro de 2006 para a partição usando uma associação de consulta fora de linha na `Bindings` Propriedade do `Process` comando para recuperar as linhas da tabela de fatos das quais gerar agregações para adicionar à partição.  
  
### <a name="code"></a>Código  
  
```  
<Process ProcessAffectedObjects="true" xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
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
  
  
