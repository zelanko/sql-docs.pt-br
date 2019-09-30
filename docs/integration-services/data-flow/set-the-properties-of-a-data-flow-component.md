---
title: Definir as propriedades de um componente de fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], properties
ms.assetid: 73000ef6-52a2-4dec-8320-0e79acf0c2c5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 10b397e4fdabefe333854fe04ab37c4bdd92cf38
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291839"
---
# <a name="set-the-properties-of-a-data-flow-component"></a>Definir as propriedades de um componente de fluxo de dados

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Para definir as propriedades de componentes de fluxo de dados, que incluem origens, destinos e transformações, use um dos seguintes recursos:  
  
-   Os editores de componente fornecidos pelo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Esses editores incluem somente as propriedades personalizadas de cada componente de fluxo de dados.  
  
-   A janela **Propriedades** lista as propriedades personalizadas no nível do componente de cada elemento, bem como as propriedades comuns a todos os elementos do fluxo de dados.  
  
-   A caixa de diálogo **Editor Avançado** fornece acesso a propriedades personalizadas para cada componente. A caixa de diálogo **Editor Avançado** também fornece acesso a propriedades comuns a todos os componentes de fluxo de dados: as propriedades de entradas, saídas, saídas de erro, colunas e colunas externas.  
  
## <a name="set-the-properties-of-a-data-flow-component-with-a-component-editor"></a>Definir as propriedades de um componente de fluxo de dados com um editor de componente  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** e clique duas vezes na tarefa Fluxo de Dados que contém o fluxo de dados com os componentes cujas propriedades você deseja exibir e modificar.  
  
4.  Clique duas vezes no componente de fluxo de dados.  
  
5.  No editor de componente, exiba ou modifique os valores de propriedade e feche o editor.  
  
6.  Para salvar o pacote atualizado, no menu **Arquivo** , clique em **Salvar Itens Selecionados**.  
  
## <a name="set-the-properties-of-a-data-flow-component-in-the-properties-window"></a>Definir as propriedades de um componente de fluxo de dados na janela Propriedades  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** e clique duas vezes na tarefa Fluxo de Dados que contém os componentes cujas propriedades você deseja exibir e modificar.  
  
4.  Clique com o botão direito do mouse no componente do fluxo de dados e clique em **Propriedades**.  
  
5.  Exiba ou modifique os valores de propriedade e então feche a janela **Propriedades** .  
  
    > [!NOTE]  
    >  Muitas propriedades são somente leitura e não podem ser modificadas.  
  
6.  Para salvar o pacote atualizado, no menu **Arquivo** , clique em **Salvar Itens Selecionados**.  
  
## <a name="set-the-properties-of-a-data-flow-component-with-the-advanced-editor"></a>Definir as propriedades de um componente de fluxo de dados com o Editor Avançado  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** e clique duas vezes na tarefa Fluxo de Dados que contém o componente que deseja exibir ou modificar.  
  
4.  No designer de fluxo de dados, clique com o botão direito do mouse no componente de fluxo de dados e clique em **Mostrar Editor Avançado**.  
  
    > [!NOTE]  
    >  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os componentes de fluxo de dados que dão suporte a diversas entradas não podem usar o **Editor Avançado**.  
  
5.  Na caixa de diálogo **Editor Avançado** , execute uma das seguintes etapas:  
  
    -   Para exibir e especificar a conexão usada pelo componente, clique na guia **Gerenciadores de Conexões** .  
  
        > [!NOTE]  
        >  A guia **Gerenciadores de Conexões** está disponível apenas para componentes de fluxo de dados que usam gerenciadores de conexões para se conectar com fontes de dados como arquivos e bancos de dados  
  
    -   Para exibir e modificar propriedades no nível do componente, clique na guia **Propriedades do Componente** .  
  
    -   Para exibir ou modificar mapeamentos entre colunas externas e a saída disponível, clique na guia **Mapeamentos de Coluna** .  
  
        > [!NOTE]  
        >  A guia **Mapeamentos de Coluna** está disponível apenas ao exibir ou editar origens ou destinos.  
  
    -   Para exibir uma lista das colunas de entrada disponíveis e atualizar os nomes das colunas de saída, clique na guia **Colunas de Entrada** .  
  
        > [!NOTE]  
        >  A guia Colunas de Entrada só fica disponível ao trabalhar com transformações ou destinos. Para obter mais informações, consulte [Integration Services Transformations](../../integration-services/data-flow/transformations/integration-services-transformations.md).  
  
    -   Para exibir e modificar as propriedades de entradas, saídas e saídas de erro e as propriedades das colunas que elas contêm, clique na guia **Propriedades de Entrada e Saída** .  
  
        > [!NOTE]  
        >  Origens não têm entradas. Destinos não têm saídas, exceto uma saída de erro opcional.  
  
6.  Exiba ou modifique os valores de propriedade.  
  
7.  Clique em **OK**.  
  
8.  Para salvar o pacote atualizado, no menu **Arquivo** , clique em **Salvar Itens Selecionados**.  

## <a name="common-properties-of-data-flow-components"></a>Propriedades comuns de componentes de fluxo de dados
Os objetos de fluxo de dados no modelo de objeto do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] têm propriedades comuns e personalizadas no componente, na entrada e saída e nos níveis de colunas de entrada e saída. Muitas propriedades têm valores somente leitura, atribuídos em tempo de execução pelo mecanismo de fluxo de dados.  
  
 Este tópico lista e descreve as propriedades comuns de objetos de fluxo de dados.  
  
-   [Componentes](#components)  
  
-   [Entradas](#inputs)  
  
-   [Input columns](#inputcolumns)  
  
-   [Saídas](#outputs)  
  
-   [Colunas de saída](#outputcolumns)  
  
 
###  <a name="components"></a> Component properties  
 No modelo de objeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], um componente no fluxo de dados implementa a interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>.  
  
 A tabela a seguir descreve as propriedades dos componentes em um fluxo de dados. Algumas propriedades têm valores somente leitura que são atribuídos no tempo de execução pelo mecanismo de fluxo de dados.  
  
|Propriedade|Tipo de Dados|Descrição|  
|--------------|---------------|-----------------|  
|ComponentClassID|Cadeia de caracteres|O CLSID do componente.|  
|ContactInfo|Cadeia de caracteres|Informações de contato para o desenvolvedor de um componente.|  
|Descrição|Cadeia de caracteres|Descrição do componente de fluxo de dados. O valor padrão dessa propriedade é o nome do componente de fluxo de dados.|  
|ID|Integer|Valor que identifica essa instância do componente com exclusividade.|  
|IdentificationString|Cadeia de caracteres|Identifica o componente.|  
|IsDefaultLocale|Booliano|Indica se o componente usa a localidade da tarefa de Fluxo de Dados à qual pertence.|  
|LocaleID|Integer|A localidade usada pelo componente de fluxo de dados quando o pacote é executado. Todas as localidades do Windows estão disponíveis para uso em componentes de fluxo de dados.|  
|Nome|Cadeia de caracteres|Nome do componente de fluxo de dados.|  
|PipelineVersion|Integer|Versão da tarefa de fluxo de dados dentro da qual um componente é projetado para ser executado.|  
|UsesDispositions|Booliano|Indica se um componente tem uma saída com erro.|  
|ValidateExternalMetadata|Booliano|Indica se os metadados de colunas externas foram validados. O valor padrão dessa propriedade é **True**.|  
|Versão|Integer|Versão de um componente.|  
  
###  <a name="inputs"></a> Propriedades de entrada  
 No modelo de objeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , transformações e destinos têm entradas. Uma entrada de um componente no fluxo de dados implementa a interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>.  
  
 A tabela a seguir descreve as propriedades das entradas de componentes em um fluxo de dados. Algumas propriedades têm valores somente leitura que são atribuídos no tempo de execução pelo mecanismo de fluxo de dados.  
  
|Propriedade|Tipo de Dados|Descrição|  
|--------------|---------------|-----------------|  
|Descrição|Cadeia de caracteres|Descrição da entrada.|  
|ErrorOrTruncationOperation|Cadeia de caracteres|Cadeia de caracteres opcional que especifica os tipos de erros ou truncamentos que podem ocorrer no processamento de uma linha.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que especifica a manipulação de erros. Os valores são **Fail component**, **Ignore failure**e **Redirect row**.|  
|HasSideEffects|Booliano|Indica se um componente pode ser removido do plano de execução do fluxo de dados quando não é anexado a um componente downstream e quando **RunInOptimizedMode** é **true**.|  
|ID|Integer|Valor que identifica a entrada com exclusividade.|  
|IdentificationString|Cadeia de caracteres|Cadeia de caracteres que identifica a entrada.|  
|IsSorted|Booliano|Indica se os dados na entrada são classificados.|  
|Nome|Cadeia de caracteres|Nome da entrada.|  
|SourceLocale|Integer|ID de localidade (LCID) dos dados de entrada.|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que determina como o componente manipula os truncamentos que ocorrem no processamento de linhas. . Os valores são **Fail component**, **Ignore failure**e **Redirect row**.|  
  
 Os destinos e algumas transformações não oferecem suporte a saídas de erro e as propriedades ErrorRowDisposition e TruncationRowDisposition dos componentes são somente leitura.  
  
###  <a name="inputcolumns"></a> Propriedades da coluna de entrada  
 No modelo de objeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , uma entrada contém uma coleção de colunas de entrada. Uma coluna de entrada de um componente no fluxo de dados implementa a interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInputColumn100>.  
  
 A tabela a seguir descreve as propriedades das colunas de entrada de componentes em um fluxo de dados. Algumas propriedades têm valores somente leitura que são atribuídos no tempo de execução pelo mecanismo de fluxo de dados.  
  
|Propriedade|Tipo de Dados|Descrição|  
|--------------|---------------|-----------------|  
|ComparisonFlags|Integer|Um conjunto de sinalizadores que especifica a comparação de colunas que têm um tipo de dado de caractere. Para obter mais informações, consulte [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md).|  
|Descrição|Cadeia de caracteres|Descreve a coluna de entrada.|  
|ErrorOrTruncationOperation|Cadeia de caracteres|Cadeia de caracteres opcional que especifica os tipos de erros ou truncamentos que podem ocorrer no processamento de uma linha.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que especifica a manipulação de erros. Os valores são **Fail component**, **Ignore failure**e **Redirect row**.|  
|ExternalMetadataColumnID|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100>|ID da coluna de metadados externa atribuída a uma coluna de entrada.|  
|ID|Integer|Valor que identifica a coluna com exclusividade.|  
|IdentificationString|Cadeia de caracteres|Cadeia de caracteres que identifica a coluna de entrada.|  
|LineageID|Integer|ID da coluna upstream.|  
|LineageIdentificationString|Cadeia de caracteres|A cadeia de caracteres de identificação que inclui o nome da coluna de upstream.|  
|Nome|Cadeia de caracteres|Nome da coluna de entrada.|  
|SortKeyPosition|Integer|Valor que indica se uma coluna está classificada, sua ordem de classificação e a sequência em que diversas colunas são classificadas. O valor **0** indica que a coluna não está classificada.  Para obter mais informações, consulte [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que determina como o componente manipula os truncamentos que ocorrem no processamento de linhas. Os valores são **Fail component**, **Ignore failure**e **Redirect row**.|  
|UpstreamComponentName|Cadeia de caracteres|Nome do componente upstream.|  
|UsageType|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSUsageType>|Valor que determina como uma coluna de entrada é usada pelo componente.|  
  
 As colunas de entrada também têm as propriedades de tipo de dados descritas no item "Propriedades de Tipo de Dados".  
  
###  <a name="outputs"></a> Propriedades de saída  
 No modelo de objeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , origens e transformações têm saídas. Uma saída de um componente no fluxo de dados implementa a interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>.  
  
 A tabela a seguir descreve as propriedades das saídas de componentes em um fluxo de dados. Algumas propriedades têm valores somente leitura que são atribuídos no tempo de execução pelo mecanismo de fluxo de dados.  
  
|Propriedade|Tipo de Dados|Descrição|  
|--------------|---------------|-----------------|  
|DeleteOutputOnPathDetached|Booliano|Valor que determina se o mecanismo de fluxo de dados exclui a saída quando ela é desanexada de um caminho.|  
|Descrição|Cadeia de caracteres|Descreve a saída.|  
|ErrorOrTruncationOperation|Cadeia de caracteres|Cadeia de caracteres opcional que especifica os tipos de erros ou truncamentos que podem ocorrer no processamento de uma linha.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que especifica a manipulação de erros. Os valores são **Fail component**, **Ignore failure**e **Redirect row**.|  
|ExclusionGroup|Integer|Valor que identifica um grupo de saídas mutuamente exclusivas.|  
|HasSideEffects|Booliano|Valor que indica se um componente pode ser removido do plano de execução do fluxo de dados quando não é anexado a um componente upstream e quando **RunInOptimizedMode** é **true**.|  
|ID|Integer|Valor que identifica a saída com exclusividade.|  
|IdentificationString|Cadeia de caracteres|Cadeia de caracteres que identifica a saída.|  
|IsErrorOut|Booliano|Indica se a saída é uma saída de erro.|  
|IsSorted|Booliano|Indica se a saída está classificada. O valor padrão é **Falso**.<br /><br /> **\*\* Importante \*\*** Configurar o valor da propriedade **IsSorted** como **True** não classifica os dados. Esta propriedade apenas fornece uma dica aos componentes downstream de que os dados foram classificados previamente. Para obter mais informações, consulte [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).|  
|Nome|Cadeia de caracteres|Nome da saída.|  
|SynchronousInputID|Integer|ID de uma entrada que é síncrona à saída.|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que determina como o componente manipula os truncamentos que ocorrem no processamento de linhas. Os valores são **Fail component**, **Ignore failure**e **Redirect row**.|  
  
###  <a name="outputcolumns"></a> Propriedades da coluna de saída  
 No modelo de objeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , uma saída contém uma coleção de colunas de saída. Uma coluna de saída de um componente no fluxo de dados implementa a interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100>.  
  
 A tabela a seguir descreve as propriedades das colunas de saída de componentes em um fluxo de dados. Algumas propriedades têm valores somente leitura que são atribuídos no tempo de execução pelo mecanismo de fluxo de dados.  
  
|Propriedade|Tipo de Dados|Descrição|  
|--------------|---------------|-----------------|  
|ComparisonFlags|Integer|Um conjunto de sinalizadores que especifica a comparação de colunas que têm um tipo de dado de caractere. Para obter mais informações, consulte [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md).|  
|Descrição|Cadeia de caracteres|Descreve a coluna de saída.|  
|ErrorOrTruncationOperation|Cadeia de caracteres|Cadeia de caracteres opcional que especifica os tipos de erros ou truncamentos que podem ocorrer no processamento de uma linha.|  
|ErrorRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que especifica a manipulação de erros. Os valores são **Fail component**, **Ignore failure**e **Redirect row**. O valor padrão é **Fail component**.|  
|ExternalMetadataColumnID|Integer|ID da coluna de metadados externa atribuída a uma coluna de entrada.|  
|ID|Integer|Valor que identifica a coluna de saída com exclusividade.|  
|IdentificationString|Cadeia de caracteres|Cadeia de caracteres que identifica a coluna de saída.|  
|LineageID|Integer|ID da coluna de saída. Os componentes downstream referem-se à coluna usando esse valor.|  
|LineageIdentificationString|Cadeia de caracteres|A cadeia de caracteres de identificação que inclui o nome da coluna.|  
|Nome|Cadeia de caracteres|Nome da coluna de saída.|  
|SortKeyPosition|Integer|Valor que indica se uma coluna está classificada, sua ordem de classificação e a sequência em que diversas colunas são classificadas. O valor **0** indica que a coluna não está classificada. Para obter mais informações, consulte [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).|  
|SpecialFlags|Integer|Valor que contém os sinalizadores especiais da coluna de saída.|  
|TruncationRowDisposition|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSRowDisposition>|Valor que determina como o componente manipula os truncamentos que ocorrem no processamento de linhas. Os valores são **Fail component**, **Ignore failure**e **Redirect row**. O valor padrão é **Fail component**.|  
  
 As colunas de saída também incluem um conjunto de propriedades de tipo de dados.  
  
### <a name="external-metadata-column-properties"></a>Propriedades da coluna de metadados externa  
 No modelo de objeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , entradas e saídas podem conter uma coleção de colunas de metadados externas. Uma coluna de metadados externa de um componente no fluxo de dados implementa a interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumn100>.  
  
 A tabela a seguir descreve as propriedades das colunas de metadados externas de componentes em um fluxo de dados. Algumas propriedades têm valores somente leitura que são atribuídos no tempo de execução pelo mecanismo de fluxo de dados.  
  
|Propriedade|Tipo de Dados|Descrição|  
|--------------|---------------|-----------------|  
|Descrição|Cadeia de caracteres|Descreve a coluna externa.|  
|ID|Integer|Valor que identifica a coluna com exclusividade.|  
|IdentificationString|Cadeia de caracteres|Cadeia de caracteres que identifica a coluna.|  
|Nome|Cadeia de caracteres|Nome da coluna externa.|  
  
 As colunas de metadados externas também incluem um conjunto de propriedades de tipo de dados.  
  
### <a name="data-type-properties"></a>Propriedades de tipo de dados  
 As colunas de saída e as colunas de metadados externas incluem um conjunto de propriedades de tipo de dados. Dependendo do tipo de dados da coluna, as propriedades podem ser leitura/gravação ou somente leitura.  
  
 A tabela a seguir descreve as propriedades de tipo de dados de colunas de saída e de colunas de metadados externas.  
  
|Propriedade|Tipo de Dados|Descrição|  
|--------------|---------------|-----------------|  
|CodePage|Integer|Especifica a página de código para dados de cadeia de caracteres que não são Unicode.|  
|DataType|Inteiro (enumeração)|Tipo de dados da coluna do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|Comprimento|Integer|Comprimento, medido em caracteres, de uma coluna.|  
|Precisão|Integer|Precisão de uma coluna numérica.|  
|Escala|Integer|Escala de uma coluna numérica.|  

## <a name="custom-properties-of-data-flow-components"></a>Propriedades personalizadas de componentes de fluxo de dados
Para obter informações sobre propriedades personalizadas, consulte os tópicos a seguir  
  
-   [Propriedades personalizadas do ADO NET](../../integration-services/data-flow/ado-net-custom-properties.md)  
  
-   [Propriedades personalizadas da tarefa Controle de CDC](../../integration-services/control-flow/cdc-control-task-custom-properties.md)  
  
-   [Propriedades personalizadas da origem CDC](../../integration-services/data-flow/cdc-source-custom-properties.md)  
  
-   [Propriedades personalizadas do destino treinamento do modelo de mineração de dados](../../integration-services/data-flow/data-mining-model-training-destination-custom-properties.md)  
  
-   [Propriedades personalizadas do destino DataReader](../../integration-services/data-flow/datareader-destination-custom-properties.md)  
  
-   [Propriedades personalizadas do destino de processamento de dimensões](../../integration-services/data-flow/dimension-processing-destination-custom-properies.md)  
  
-   [Propriedades personalizadas do Excel](../../integration-services/data-flow/excel-custom-properties.md)  
  
-   [Propriedades personalizadas de arquivo simples](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
-   [Propriedades personalizadas de destino ODBC](../../integration-services/data-flow/odbc-destination-custom-properties.md)  
  
-   [Propriedades personalizadas da origem ODBC](../../integration-services/data-flow/odbc-source-custom-properties.md)  
  
-   [OLE DB Custom Properties](../../integration-services/data-flow/ole-db-custom-properties.md)Propriedades personalizadas OLE DB  
  
-   [Propriedades personalizadas do destino processamento de partições](../../integration-services/data-flow/partition-processing-destination-custom-properties.md)  
  
-   [Propriedades personalizadas de arquivo bruto](../../integration-services/data-flow/raw-file-custom-properties.md)  
  
-   [Propriedades personalizadas do destino do conjunto de registros](../../integration-services/data-flow/recordset-destination-custom-properties.md)  
  
-   [Propriedades personalizadas do destino SQL Server Compact Edition](../../integration-services/data-flow/sql-server-compact-edition-destination-custom-properties.md)  
  
-   [Propriedades personalizadas do destino SQL Server](../../integration-services/data-flow/sql-server-destination-custom-properties.md)  
  
-   [Propriedades personalizadas de Transformação](../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
-   [Propriedades personalizadas de origem XML](../../integration-services/data-flow/xml-source-custom-properties.md)  
  
## <a name="use-an-expression-in-a-data-flow-component"></a>Usar uma expressão em um componente de fluxo de dados
Este procedimento descreve como adicionar uma expressão à transformação Divisão Condicional ou à transformação Coluna derivada. A transformação Divisão Condicional usa expressões para definir as condições que direcionam linhas de dados a uma saída de transformação e a transformação Coluna Derivada usa expressões para definir valores atribuídos a colunas.  
  
 Para implementar uma expressão em uma transformação, o pacote já deve incluir pelo menos uma tarefa Fluxo de Dados e uma fonte. 
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , clique na guia **Fluxo de Controle** e clique na tarefa Fluxo de Dados que contém o fluxo de dados no qual você deseja implementar uma expressão.  
  
4.  Clique na guia **Fluxo de Dados** e arraste uma transformação Divisão Condicional ou Coluna Derivada da **Caixa de Ferramentas** para a superfície de design.  
  
5.  Arraste o conector verde da fonte ou uma transformação para a transformação Divisão Condicional ou Coluna Derivada.  
  
6.  Clique duas vezes na transformação para abrir sua caixa de diálogo.  
  
7.  No painel à esquerda, expanda **Variáveis** para exibir variáveis definidas pelo sistema e pelo usuário e expanda **Colunas** para exibir as colunas de entrada de transformação.  
  
8.  No painel à direita, expanda **Funções Matemáticas**, **Funções de Cadeia de Caracteres**, **Funções de Data/Hora**, **Funções NULL**, **Conversões de Tipo**e **Operadores** para acessar as funções, as conversões e os operadores fornecidos pela gramática de expressão.  
  
9. Dependendo da transformação, execute uma das seguintes ações para criar uma expressão:  
  
    -   Na caixa de diálogo **Editor de Transformação Divisão Condicional** , arraste variáveis, colunas, funções, operadores e conversões até a coluna **Condição** . Se preferir, digite uma expressão diretamente na coluna **Condição** .  
  
    -   Na caixa de diálogo **Editor de Transformação Coluna Derivada** , arraste variáveis, colunas, funções, operadores e conversões até a coluna **Expressão** . Como alternativa, é possível digitar uma expressão diretamente na coluna **Expressão** .  
  
        > [!NOTE]  
        >  Ao remover o foco da coluna **Condição** ou da coluna **Expressão** , o texto da expressão pode ser realçado para indicar que a sintaxe da expressão está incorreta.  
  
10. Clique em **OK** para fechar a caixa de diálogo.  
  
    > [!NOTE]  
    >  Se a expressão não for válida, um alerta aparecerá descrevendo os erros de sintaxe na expressão.  

## <a name="data-flow-properties-that-you-can-set-with-an-expression"></a>Propriedades de fluxo de dados que podem ser definidas com uma expressão
Os valores de certas propriedades dos objetos de fluxo de dados podem ser especificados usando expressões de propriedades disponíveis no contêiner da tarefa de Fluxo de Dados.  
  
 Para obter informações sobre como usar expressões de propriedade, consulte [Usar expressões de propriedade em pacotes](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
 É possível usar expressões de propriedade para personalizar configurações para cada instância implantada de um pacote. Você também pode usar expressões de propriedades para especificar restrições de tempo de execução para um pacote, usando a opção **/set** com o utilitário de prompt de comando **dtexec** . Por exemplo, você pode restringir o **MaximumThreads** usado pela transformação Classificação ou o **MaxMemoryUsage** das transformações Agrupamento Difuso e Pesquisa Difusa. Se irrestritas, essas transformações podem armazenar em cache grandes quantias de dados na memória.  
  
 Para especificar uma expressão de propriedade para uma das propriedades de objetos de fluxo de dados listadas nesse tópico, exiba a janela **Propriedades** para a tarefa de Fluxo de Dados selecionando a tarefa de Fluxo de Dados na superfície **Fluxo de Controle** do designer, ou selecionando a guia **Fluxo de Dados** do designer sem selecionar nenhum componente individual ou caminho. Selecione a propriedade **Expressões** e clique nas reticências (...) para exibir a caixa de diálogo **Editor de Expressões de Propriedades** . Abra a lista suspensa **Propriedade** para selecionar uma propriedade e digite uma expressão na caixa de texto **Expressão** ou clique nas reticências (...) para exibir a caixa de diálogo **Construtor de Expressões** .  
  
 A lista **Propriedade** exibe as propriedades disponíveis para apenas esses objetos de fluxo de dados já colocados na superfície **Fluxo de Dados** do designer. Portanto, não é possível usar a lista **Propriedade** para exibir todas as possíveis propriedades de objetos de fluxo de dados que aceitam expressões de propriedades. Por exemplo, se você tiver colocado uma origem do ADO NET na superfície do designer, a lista **Propriedade** conterá uma entrada para a propriedade **[ADO NET Source].[SqlCommand]** . A lista também exibe muitas propriedades da própria tarefa de Fluxo de Dados.  
 
 Os valores das propriedades na lista a seguir podem ser especificados usando expressões de propriedades.  
  
### <a name="data-flow-sources"></a>Origens de fluxo de dados  
  
|Objeto de Fluxo de Dados|Propriedade|  
|----------------------|--------------|  
|Origem do ADO NET|Propriedade TableOrViewName<br /><br /> Propriedade SqlCommand|  
|Origem XML|Propriedade XMLData<br /><br /> Propriedade XMLSchemaDefinition|  
  
### <a name="data-flow-transformations"></a>Transformações de fluxo de dados  
 Para obter mais informações sobre essas propriedades personalizadas, consulte [Propriedades Personalizadas de Transformação](../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
|Objeto de Fluxo de Dados|Propriedade|  
|----------------------|--------------|  
|Transformação Divisão Condicional|Propriedade FriendlyExpression|  
|transformação Coluna Derivada|Propriedade FriendlyExpression|  
|transformação Agrupamento Difuso|Propriedade MaxMemoryUsage|  
|transformação Pesquisa Difusa|Propriedade MaxMemoryUsage|  
|transformação Pesquisa|Propriedade SqlCommand<br /><br /> Propriedade SqlCommandParam|  
|transformação Comando OLE DB|Propriedade SqlCommand|  
|transformação Amostragem Percentual|Propriedade SamplingValue|  
|transformação Dinâmica|Propriedade PivotKeyValue|  
|Transformação Amostragem de Linhas|Propriedade SamplingValue|  
|Transformação Classificação|Propriedade MaximumThreads|  
|Transformação Não Dinâmica|Propriedade PivotKeyValue|  
  
### <a name="data-flow-destinations"></a>Destinos de fluxo de dados  
  
|Objeto de Fluxo de Dados|Propriedade|  
|----------------------|--------------|  
|Destino do ADO NET|Propriedade TableOrViewName<br /><br /> Propriedade BatchSize<br /><br /> Propriedade CommandTimeout|  
|Destino de arquivo simples|Propriedade Header|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Destino Compact|Propriedade TableName|  
|Destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Propriedade BulkInsertTableName<br /><br /> Propriedade BulkInsertFirstRow<br /><br /> Propriedade BulkInsertLastRow<br /><br /> Propriedade BulkInsertOrder<br /><br /> Propriedade Timeout|  

