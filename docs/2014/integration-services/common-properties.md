---
title: Propriedades comuns | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- external metadata column properties [Integration Services]
- output properties [Integration Services]
- data types [Integration Services], properties
- input properties [Integration Services]
- component properties [Integration Services]
ms.assetid: 51973502-5cc6-4125-9fce-e60fa1b7b796
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5b20a0d2f47e89070712a4063acba4da0225b85d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66060956"
---
# <a name="common-properties"></a>Propriedades comuns
  Os objetos de fluxo de dados [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no modelo de objeto têm propriedades comuns e propriedades personalizadas nos níveis de componente, entrada e saída e coluna de entrada e saída. Muitas propriedades têm valores somente leitura, atribuídos em tempo de execução pelo mecanismo de fluxo de dados.  
  
 Este tópico lista e descreve as propriedades comuns de objetos de fluxo de dados.  
  
-   [Componentes](#components)  
  
-   [Entradas](#inputs)  
  
-   [Colunas de entrada](#inputcolumns)  
  
-   [Saídas](#outputs)  
  
-   [Colunas de saída](#outputcolumns)  
  
 Para obter informações sobre propriedades de cliente, consulte os seguintes tópicos:  
  
-   [Propriedades personalizadas do ADO NET](data-flow/ado-net-custom-properties.md)  
  
-   [Propriedades personalizadas da tarefa Controle de CDC](control-flow/cdc-control-task-custom-properties.md)  
  
-   [Propriedades personalizadas da origem CDC](data-flow/cdc-source-custom-properties.md)  
  
-   [Propriedades personalizadas do destino Treinamento do Modelo de Mineração de Dados](data-flow/data-mining-model-training-destination-custom-properties.md)  
  
-   [Propriedades personalizadas do destino DataReader](data-flow/datareader-destination-custom-properties.md)  
  
-   [Propriedades personalizadas do destino de processamento de dimensões](data-flow/dimension-processing-destination-custom-properies.md)  
  
-   [Propriedades personalizadas do Excel](data-flow/excel-custom-properties.md)  
  
-   [Propriedades personalizadas de arquivo simples](data-flow/flat-file-custom-properties.md)  
  
-   [Propriedades personalizadas de destino ODBC](data-flow/odbc-destination-custom-properties.md)  
  
-   [Propriedades personalizadas da origem ODBC](data-flow/odbc-source-custom-properties.md)  
  
-   [OLE DB Propriedades personalizadas](data-flow/ole-db-custom-properties.md) OLE DB Propriedades personalizadas  
  
-   [Propriedades personalizadas do destino Processamento de Partições](data-flow/partition-processing-destination-custom-properties.md)  
  
-   [Propriedades personalizadas de arquivo bruto](data-flow/raw-file-custom-properties.md)  
  
-   [Propriedades personalizadas do destino do conjunto de registros](data-flow/recordset-destination-custom-properties.md)  
  
-   [Propriedades personalizadas do destino SQL Server Compact Edition](data-flow/sql-server-compact-edition-destination-custom-properties.md)  
  
-   [Propriedades personalizadas do destino SQL Server](data-flow/sql-server-destination-custom-properties.md)  
  
-   [Propriedades personalizadas de Transformação](data-flow/transformations/transformation-custom-properties.md)  
  
-   [Propriedades personalizadas da origem XML](data-flow/xml-source-custom-properties.md)  
  
##  <a name="components"></a>Propriedades do componente  
 No modelo de objeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], um componente no fluxo de dados implementa a interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>.  
  
 A tabela a seguir descreve as propriedades dos componentes em um fluxo de dados. Algumas propriedades têm valores somente leitura que são atribuídos no tempo de execução pelo mecanismo de fluxo de dados.  
  
|Propriedade|Tipo de Dados|DESCRIÇÃO|  
|--------------|---------------|-----------------|  
|ComponentClassID|String|O CLSID do componente.|  
|ContactInfo|String|Informações de contato para o desenvolvedor de um componente.|  
|DESCRIÇÃO|String|Descrição do componente de fluxo de dados. O valor padrão dessa propriedade é o nome do componente de fluxo de dados.|  
|ID|Integer|Valor que identifica essa instância do componente com exclusividade.|  
|IdentificationString|String|Identifica o componente.|  
|IsDefaultLocale|Boolean|Indica se o componente usa a localidade da tarefa de Fluxo de Dados à qual pertence.|  
|LocaleID|Integer|A localidade usada pelo componente de fluxo de dados quando o pacote é executado. Todas as localidades do Windows estão disponíveis para uso em componentes de fluxo de dados.|  
|Nome|String|Nome do componente de fluxo de dados.|  
|PipelineVersion|Integer|Versão da tarefa de fluxo de dados dentro da qual um componente é projetado para ser executado.|  
|UsesDispositions|Boolean|Indica se um componente tem uma saída com erro.|  
|ValidateExternalMetadata|Boolean|Indica se os metadados de colunas externas foram validados. O valor padrão dessa propriedade é `True`.|  
|Versão|Integer|Versão de um componente.|  
  
##  <a name="inputs"></a>Propriedades de entrada  
 No modelo de objeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , transformações e destinos têm entradas. Uma entrada de um componente no fluxo de dados implementa a interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>.  
  
 A tabela a seguir descreve as propriedades das entradas de componentes em um fluxo de dados. Algumas propriedades têm valores somente leitura que são atribuídos no tempo de execução pelo mecanismo de fluxo de dados.  
  
|Propriedade|Tipo de Dados|DESCRIÇÃO|  
|--------------|---------------|-----------------|  
|DESCRIÇÃO|String|Descrição da entrada.|  
|ErrorOrTruncationOperation|String|Cadeia de caracteres opcional que especifica os tipos de erros ou truncamentos que podem ocorrer no processamento de uma linha.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que especifica a manipulação de erros. Os valores são `Fail component`, `Ignore failure` e `Redirect row`.|  
|HasSideEffects|Boolean|Indica se um componente pode ser removido do plano de execução do fluxo de dados quando não está anexado a um componente downstream e quando `RunInOptimizedMode` é. `true`|  
|ID|Integer|Valor que identifica a entrada com exclusividade.|  
|IdentificationString|String|Cadeia de caracteres que identifica a entrada.|  
|IsSorted|Boolean|Indica se os dados na entrada são classificados.|  
|Nome|String|Nome da entrada.|  
|SourceLocale|Integer|ID de localidade (LCID) dos dados de entrada.|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que determina como o componente manipula os truncamentos que ocorrem no processamento de linhas. . Os valores são `Fail component`, `Ignore failure` e `Redirect row`.|  
  
 Os destinos e algumas transformações não oferecem suporte a saídas de erro e as propriedades ErrorRowDisposition e TruncationRowDisposition dos componentes são somente leitura.  
  
###  <a name="inputcolumns"></a>Propriedades da coluna de entrada  
 No modelo de objeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , uma entrada contém uma coleção de colunas de entrada. Uma coluna de entrada de um componente no fluxo de dados implementa a interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInputColumn100>.  
  
 A tabela a seguir descreve as propriedades das colunas de entrada de componentes em um fluxo de dados. Algumas propriedades têm valores somente leitura que são atribuídos no tempo de execução pelo mecanismo de fluxo de dados.  
  
|Propriedade|Tipo de Dados|DESCRIÇÃO|  
|--------------|---------------|-----------------|  
|ComparisonFlags|Integer|Um conjunto de sinalizadores que especifica a comparação de colunas que têm um tipo de dado de caractere. Para obter mais informações, consulte [Comparing String Data](data-flow/comparing-string-data.md).|  
|DESCRIÇÃO|String|Descreve a coluna de entrada.|  
|ErrorOrTruncationOperation|String|Cadeia de caracteres opcional que especifica os tipos de erros ou truncamentos que podem ocorrer no processamento de uma linha.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que especifica a manipulação de erros. Os valores são `Fail component`, `Ignore failure` e `Redirect row`.|  
|ExternalMetadataColumnID|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100>|ID da coluna de metadados externa atribuída a uma coluna de entrada.|  
|ID|Integer|Valor que identifica a coluna com exclusividade.|  
|IdentificationString|String|Cadeia de caracteres que identifica a coluna de entrada.|  
|LineageID|Integer|ID da coluna upstream.|  
|Nome|String|Nome da coluna de entrada.|  
|SortKeyPosition|Integer|Valor que indica se uma coluna está classificada, sua ordem de classificação e a sequência em que diversas colunas são classificadas. O valor **0** indica que a coluna não está classificada.  Para obter mais informações, consulte [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que determina como o componente manipula os truncamentos que ocorrem no processamento de linhas. Os valores são `Fail component`, `Ignore failure` e `Redirect row`.|  
|UpstreamComponentName|String|Nome do componente upstream.|  
|UsageType|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSUsageType>|Valor que determina como uma coluna de entrada é usada pelo componente.|  
  
 As colunas de entrada também têm as propriedades de tipo de dados descritas no item "Propriedades de Tipo de Dados".  
  
##  <a name="outputs"></a>Propriedades de saída  
 No modelo de objeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , origens e transformações têm saídas. Uma saída de um componente no fluxo de dados implementa a interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>.  
  
 A tabela a seguir descreve as propriedades das saídas de componentes em um fluxo de dados. Algumas propriedades têm valores somente leitura que são atribuídos no tempo de execução pelo mecanismo de fluxo de dados.  
  
|Propriedade|Tipo de Dados|DESCRIÇÃO|  
|--------------|---------------|-----------------|  
|DeleteOutputOnPathDetached|Boolean|Valor que determina se o mecanismo de fluxo de dados exclui a saída quando ela é desanexada de um caminho.|  
|DESCRIÇÃO|String|Descreve a saída.|  
|ErrorOrTruncationOperation|String|Cadeia de caracteres opcional que especifica os tipos de erros ou truncamentos que podem ocorrer no processamento de uma linha.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que especifica a manipulação de erros. Os valores são `Fail component`, `Ignore failure` e `Redirect row`.|  
|ExclusionGroup|Integer|Valor que identifica um grupo de saídas mutuamente exclusivas.|  
|HasSideEffects|Boolean|Valor que indica se um componente pode ser removido do plano de execução do fluxo de dados quando não é anexado a um componente upstream e quando `RunInOptimizedMode` é `true`.|  
|ID|Integer|Valor que identifica a saída com exclusividade.|  
|IdentificationString|String|Cadeia de caracteres que identifica a saída.|  
|IsErrorOut|Boolean|Indica se a saída é uma saída de erro.|  
|IsSorted|Boolean|Indica se a saída está classificada. O valor padrão é `False`.<br /><br /> ** \* Importante \* \* ** Definir o valor da `IsSorted` Propriedade como `True` não classifica os dados. Esta propriedade apenas fornece uma dica aos componentes downstream de que os dados foram classificados previamente. Para obter mais informações, consulte [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).|  
|Nome|String|Nome da saída.|  
|SynchronousInputID|Integer|ID de uma entrada que é síncrona à saída.|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que determina como o componente manipula os truncamentos que ocorrem no processamento de linhas. Os valores são `Fail component`, `Ignore failure` e `Redirect row`.|  
  
###  <a name="outputcolumns"></a>Propriedades da coluna de saída  
 No modelo de objeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , uma saída contém uma coleção de colunas de saída. Uma coluna de saída de um componente no fluxo de dados implementa a interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100>.  
  
 A tabela a seguir descreve as propriedades das colunas de saída de componentes em um fluxo de dados. Algumas propriedades têm valores somente leitura que são atribuídos no tempo de execução pelo mecanismo de fluxo de dados.  
  
|Propriedade|Tipo de Dados|DESCRIÇÃO|  
|--------------|---------------|-----------------|  
|ComparisonFlags|Integer|Um conjunto de sinalizadores que especifica a comparação de colunas que têm um tipo de dado de caractere. Para obter mais informações, consulte [Comparing String Data](data-flow/comparing-string-data.md).|  
|DESCRIÇÃO|String|Descreve a coluna de saída.|  
|ErrorOrTruncationOperation|String|Cadeia de caracteres opcional que especifica os tipos de erros ou truncamentos que podem ocorrer no processamento de uma linha.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que especifica a manipulação de erros. Os valores são `Fail component`, `Ignore failure` e `Redirect row`. O valor padrão é `Fail component`.|  
|ExternalMetadataColumnID|Integer|ID da coluna de metadados externa atribuída a uma coluna de entrada.|  
|ID|Integer|Valor que identifica a coluna de saída com exclusividade.|  
|IdentificationString|String|Cadeia de caracteres que identifica a coluna de saída.|  
|LineageID|Integer|ID da coluna de saída. Os componentes downstream referem-se à coluna usando esse valor.|  
|Nome|String|Nome da coluna de saída.|  
|SortKeyPosition|Integer|Valor que indica se uma coluna está classificada, sua ordem de classificação e a sequência em que diversas colunas são classificadas. O valor **0** indica que a coluna não está classificada. Para obter mais informações, consulte [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).|  
|SpecialFlags|Integer|Valor que contém os sinalizadores especiais da coluna de saída.|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que determina como o componente manipula os truncamentos que ocorrem no processamento de linhas. Os valores são `Fail component`, `Ignore failure` e `Redirect row`. O valor padrão é `Fail component`.|  
  
 As colunas de saída também incluem um conjunto de propriedades de tipo de dados.  
  
## <a name="external-metadata-column-properties"></a>Propriedades da coluna de metadados externa  
 No modelo de objeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , entradas e saídas podem conter uma coleção de colunas de metadados externas. Uma coluna de metadados externa de um componente no fluxo de dados implementa a interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100>.  
  
 A tabela a seguir descreve as propriedades das colunas de metadados externas de componentes em um fluxo de dados. Algumas propriedades têm valores somente leitura que são atribuídos no tempo de execução pelo mecanismo de fluxo de dados.  
  
|Propriedade|Tipo de Dados|DESCRIÇÃO|  
|--------------|---------------|-----------------|  
|DESCRIÇÃO|String|Descreve a coluna externa.|  
|ID|Integer|Valor que identifica a coluna com exclusividade.|  
|IdentificationString|String|Cadeia de caracteres que identifica a coluna.|  
|Nome|String|Nome da coluna externa.|  
  
 As colunas de metadados externas também incluem um conjunto de propriedades de tipo de dados.  
  
## <a name="data-type-properties"></a>Propriedades de tipo de dados  
 As colunas de saída e as colunas de metadados externas incluem um conjunto de propriedades de tipo de dados. Dependendo do tipo de dados da coluna, as propriedades podem ser leitura/gravação ou somente leitura.  
  
 A tabela a seguir descreve as propriedades de tipo de dados de colunas de saída e de colunas de metadados externas.  
  
|Propriedade|Tipo de Dados|DESCRIÇÃO|  
|--------------|---------------|-----------------|  
|CodePage|Integer|Especifica a página de código para dados de cadeia de caracteres que não são Unicode.|  
|Tipo de dados|Inteiro (enumeração)|Tipo de dados da coluna do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Para obter mais informações, consulte [Integration Services tipos de dados](data-flow/integration-services-data-types.md).|  
|Comprimento|Integer|Comprimento, medido em caracteres, de uma coluna.|  
|Precisão|Integer|Precisão de uma coluna numérica.|  
|Escala|Integer|Escala de uma coluna numérica.|  
  
## <a name="see-also"></a>Consulte Também  
 [Fluxo de Dados](data-flow/data-flow.md)   
 [Propriedades personalizadas da transformação](data-flow/transformations/transformation-custom-properties.md)   
 [Propriedades do caminho](../../2014/integration-services/path-properties.md)   
 [Propriedades de fluxo de dados que podem ser definidas usando expressões](../../2014/integration-services/data-flow-properties-that-can-be-set-by-using-expressions.md)  
  
  
