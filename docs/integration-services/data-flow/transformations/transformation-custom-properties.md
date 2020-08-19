---
description: Propriedades personalizadas da transformação
title: Propriedades personalizadas de transformação | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- Slowly Changing Dimension transformation
- Import Column transformation [Integration Services]
- Sort transformation
- Unpivot transformation
- Merge Join transformation
- Data Mining Query transformation
- Fuzzy Grouping transformation
- Data Conversion transformation
- Fuzzy Lookup transformation
- Term Extraction transformation
- Row Count transformation custom properties [Integration Services]
- transformations [Integration Services], properties
- Pivot transformation
- Lookup transformation
- Percentage Sampling transformation
- Export Column transformation [Integration Services]
- Row Sampling transformation
- Conditional Split transformation custom properties [Integration Services]
- custom properties [Integration Services]
- Audit transformation
- Term Lookup transformation
- Script Component transformation custom properties [Integration Services]
- Derived Column transformation
- OLE DB Command transformation
- Copy Column transformation custom properties [Integration Services]
- Character Map transformation custom properties [Integration Services]
ms.assetid: 56f5df6a-56f6-43df-bca9-08476a3bd931
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1219bf8b502d7e91194b3413910aa7ae16ec09c8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425688"
---
# <a name="transformation-custom-properties"></a>Propriedades personalizadas da transformação

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  Além das propriedades comuns à maioria dos objetos de fluxo de dados no modelo de objeto do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], muitos objetos de fluxo de dados têm propriedades personalizadas específicas ao objeto. Essas propriedades personalizadas estão disponíveis somente em tempo de execução e não constam da Documentação de Referência de Programação Gerenciada do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] .  
  
 Este tópico lista e descreve as propriedades personalizadas de várias transformações de fluxo de dados. Para obter mais informações sobre as propriedades comuns à maioria dos objetos Data Flow, consulte [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796).  
  
 É possível definir algumas propriedades de transformações usando expressões de propriedade. Para obter mais informações, consulte [Propriedades de fluxo de dados que podem ser definidas usando expressões](https://msdn.microsoft.com/library/cd0e171a-08be-45d6-81dc-ed94f37698b8).  
  
## <a name="transformations-with-custom-properties"></a>Transformações com propriedades personalizadas  

:::row:::
    :::column:::
        [Aggregate](#aggregate)  
        [Auditoria](#audit)  
        [Transformação Cache](#cachetransform)  
        [Mapa de Caracteres](#charmap)  
        [Divisão Condicional](#condsplit)  
        [Copiar Coluna](#copymap)  
        [Conversão de Dados](#dataconv)  
        [Consulta de mineração de dados](#dmquery)  
        [Coluna Derivada](#derived)  
    :::column-end:::
    :::column:::
        [Exportar Coluna](#extract)  
        [Agrupamento Difuso](#fgroup)  
        [Pesquisa Difusa](#flookup)  
        [Importar Coluna](#insert)  
        [Pesquisar](#lookup)  
        [Junção de Mesclagem](#mjoin)  
        [Comando OLE DB](#oledbcmd)  
        [Amostragem Percentual](#percent)  
        [Dinâmico](#pivot)  
    :::column-end:::
    :::column:::
        [Contagem de Linhas](#rowcount)  
        [Amostragem de Linha](#rowsamp)  
        [Componente Script](#script)  
        [Dimensão de Alteração Lenta](#scd)  
        [Sort](#sort)  
        [Extração de Termos](#textract)  
        [Pesquisa de Termos](#tlookup)  
        [Não Dinâmico](#unpivot)  
    :::column-end:::
:::row-end:::

### <a name="transformations-without-custom-properties"></a>Transformações sem propriedades personalizadas  
 As transformações a seguir não têm nenhuma propriedade personalizada nos níveis do componente, da entrada ou da saída: [Transformação Mesclar](../../../integration-services/data-flow/transformations/merge-transformation.md), [Transformação Difusão Seletiva](../../../integration-services/data-flow/transformations/multicast-transformation.md), e [Transformação Unir Tudo](../../../integration-services/data-flow/transformations/union-all-transformation.md). Somente as propriedades comuns a todos os componentes de fluxo de dados são usadas.  
  
##  <a name="aggregate-transformation-custom-properties"></a><a name="aggregate"></a> Propriedades personalizadas da transformação Agregação  
 A transformação Agregação tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da transformação Agregação. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|AutoExtendFactor|Integer|Um valor entre 1 e 100 que especifica a porcentagem para a extensão da memória durante a agregação. O valor padrão dessa propriedade é **25**.|  
|CountDistinctKeys|Integer|Um valor que especifica o número exato de contagens diferentes que a agregação pode gravar. Se um valor de CountDistinctScale for especificado, o valor em CountDistinctKeys terá precedência.|  
|CountDistinctScale|Inteiro (enumeração)|Um valor que descreve o número aproximado de valores distintos em uma coluna que a agregação pode contar. Essa propriedade pode ter um dos seguintes valores:<br /><br /> **Baixo** (1) – indica até 500 mil valores de chave<br /><br /> **Médio** (2) – indica até 5 milhões de valores de chave<br /><br /> **Alto** (3) – indica mais de 25 milhões de valores de chave.<br /><br /> **Não especificado** (0) – indica que nenhum valor de CountDistinctScale foi usado. O uso da opção **Não Especificado** (0) pode afetar o desempenho em grandes conjuntos de dados.|  
|simétricas|Integer|Um valor que especifica o número exato de chaves Agrupar por que a agregação pode gravar. Se um valor de KeyScalevalue for especificado, o valor em Keys terá preferência.|  
|KeyScale|Inteiro (enumeração)|Um valor que descreve aproximadamente quantos valores de chave Agrupar por podem ser gravados pela agregação. Essa propriedade pode ter um dos seguintes valores:<br /><br /> **Baixo** (1) – indica até 500 mil valores de chave.<br /><br /> **Médio** (2) – indica até 5 milhões de valores de chave.<br /><br /> **Alto** (3) – indica mais de 25 milhões de valores de chave.<br /><br /> **Não especificado** (0) – indica que nenhum valor de KeyScale foi usado.|  
  
 A tabela a seguir descreve as propriedades personalizadas da saída da transformação Agregação. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|simétricas|Integer|Um valor que especifica o número exato de chaves Agrupar por que pode ser gravado pela agregação. Se um valor de KeyScale for especificado, o valor em Keys terá preferência.|  
|KeyScale|Inteiro (enumeração)|Um valor que descreve aproximadamente quantos valores de chave Agrupar por podem ser gravados pela agregação. Essa propriedade pode ter um dos seguintes valores:<br /><br /> **Baixo** (1) – indica até 500 mil valores de chave,<br /><br /> **Médio** (2) – indica até 5 milhões de valores de chave,<br /><br /> **Alto** (3) – indica mais de 25 milhões de valores de chave.<br /><br /> **Não especificado** (0) – indica que nenhum valor de KeyScale foi usado.|  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de saída da transformação Agregação. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|AggregationColumnId|Integer|O **LineageID** de uma coluna que participa de GROUP BY ou funções de agregação.|  
|AggregationComparisonFlags|Integer|Um valor que especifica como a transformação Agregação compara dados de cadeia de caracteres em uma coluna. Para obter mais informações, consulte [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).|  
|AggregationType|Inteiro (enumeração)|Um valor que especifica a operação de agregação a ser executada na coluna. Essa propriedade pode ter um dos seguintes valores:<br /><br /> **Agrupar por** (0)<br /><br /> **Contagem** (1)<br /><br /> **Contagem total** (2)<br /><br /> **Countdistinct** (3)<br /><br /> **Soma** (4)<br /><br /> **Médio** (5)<br /><br /> **Máximo** (7)<br /><br /> **Máximo** (6)|  
|CountDistinctKeys|Integer|Quando o tipo de agregação é **Contar distintos**, um valor que especifica o número exato de chaves que a agregação pode gravar. Se um valor de CountDistinctScale for especificado, o valor em CountDistinctKeys terá precedência.|  
|CountDistinctScale|Inteiro (enumeração)|Quando o tipo de agregação é **Contar distintos**, um valor que especifica o número aproximado de valores de chave que podem ser gravados pela agregação. Essa propriedade pode ter um dos seguintes valores:<br /><br /> **Baixo** (1) – indica até 500 mil valores de chave,<br /><br /> **Médio** (2) – indica até 5 milhões de valores de chave,<br /><br /> **Alto** (3) – indica mais de 25 milhões de valores de chave.<br /><br /> **Não especificado** (0) – indica que nenhum valor de CountDistinctScale foi usado.|  
|IsBig|Boolean|Um valor que indica se a coluna contém um valor superior a 4 bilhões ou com mais precisão que um valor de precisão dupla de ponto flutuante. O valor pode ser 0 ou 1. 0 indica que IsBig é **Falso** e a coluna não contém um valor grande ou preciso. O valor padrão desta propriedade é 1.|  
  
 A entrada e as colunas de entrada da transformação Agregação não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Aggregate Transformation](../../../integration-services/data-flow/transformations/aggregate-transformation.md).  
  
##  <a name="audit-transformation-custom-properties"></a><a name="audit"></a> Propriedades personalizadas da transformação Auditoria  
 A transformação Auditoria só tem as propriedades comuns a todos os componentes de fluxo de dados no nível do componente.  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de saída da transformação Auditoria. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de dados|Descrição|  
|-------------------|---------------|-----------------|  
|LineageItemSelected|Inteiro (enumeração)|O item de auditoria selecionado para saída. Essa propriedade pode ter um dos seguintes valores:<br /><br /> **GUID de instância de execução** (0)<br /><br /> **Hora de início de execução** (4)<br /><br /> **Nome do computador** (5)<br /><br /> **ID do Pacote** (1)<br /><br /> **Nome do pacote** (2)<br /><br /> **ID da Tarefa** (8)<br /><br /> **Nome da tarefa** (7)<br /><br /> **Nome de usuário** (6)<br /><br /> **ID da Versão** (3)|  
  
 A entrada, as colunas de entrada e a saída da transformação Auditoria não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Audit Transformation](../../../integration-services/data-flow/transformations/audit-transformation.md).  
  
##  <a name="cache-transform-transformation-custom-properties"></a><a name="cachetransform"></a> Propriedades personalizadas da transformação Cache  
 A transformação Cache tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades da transformação Cache. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|ConnectionManager|String|Especifica o nome do gerenciador de conexões.|  
|ValidateExternalMetadata|Boolean|Indica se a transformação Cache é validada usando fontes de dados externas no momento de design. Se a propriedade for definida como **False**, a validação das fontes de dados externas acontecerá em tempo de execução.<br /><br /> O valor padrão é **True**.|  
|AvailableInputColumns|String|Lista as colunas de entrada disponíveis.|  
|InputColumns|String|Lista das colunas de entrada selecionadas.|  
|CacheColumnName|String|Especifica o nome da coluna mapeada para uma coluna de entrada selecionada.<br /><br /> É necessário que o nome da coluna na propriedade CacheColumnName corresponda ao nome da coluna correspondente listada na página **Colunas** do **Editor do Gerenciador de Conexões do Cache**.<br /><br /> Para obter mais informações, consulte [Cache Connection Manager Editor](../../../integration-services/data-flow/transformations/cache-connection-manager-editor.md).|  
  
##  <a name="character-map-transformation-custom-properties"></a><a name="charmap"></a> Propriedades personalizadas da transformação Mapa de Caracteres  
 A transformação Mapa de Caracteres só tem as propriedades comuns a todos os componentes de fluxo de dados no nível do componente.  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de saída da transformação Mapa de Caracteres. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|InputColumnLineageId|Integer|Um valor que especifica o **LineageID** da coluna de entrada que é a fonte da coluna de saída.|  
|MapFlags|Inteiro (enumeração)|Um valor que especifica as operações de cadeia de caracteres que a transformação Mapa de Caracteres executa na coluna. Essa propriedade pode ter um dos seguintes valores:<br /><br /> **Inversão de byte** (2)<br /><br /> **Largura inteira** (6)<br /><br /> **Meia largura** (5)<br /><br /> **Hiragana** (3)<br /><br /> **Katakana** (4)<br /><br /> **Caixas linguísticas** (7)<br /><br /> **Minúsculas** (0)<br /><br /> **Chinês simplificado** (8)<br /><br /> **Chinês tradicional**(9)<br /><br /> **Letras maiúsculas** (1)|  
  
 A entrada, as colunas de entrada e a saída da transformação Mapa de Caracteres não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Character Map Transformation](../../../integration-services/data-flow/transformations/character-map-transformation.md).  
  
##  <a name="conditional-split-transformation-custom-properties"></a><a name="condsplit"></a> Propriedades personalizadas da transformação Divisão Condicional  
 A transformação Divisão Condicional só tem as propriedades comuns a todos os componentes de fluxo de dados no nível do componente.  
  
 A tabela a seguir descreve as propriedades personalizadas da saída da transformação Divisão Condicional. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|EvaluationOrder|Integer|Um valor que especifica a posição de uma condição, associado a uma saída, na lista de condições avaliada pela transformação Divisão Condicional. As condições são avaliadas do valor mais baixo para o valor mais alto.|  
|Expression|String|Uma expressão que representa a condição avaliada pela transformação Divisão Condicional. Colunas são representadas por identificadores de linhagem.|  
|FriendlyExpression|String|Uma expressão que representa a condição avaliada pela transformação Divisão Condicional. Colunas são representadas pelos nomes.<br /><br /> O valor dessa propriedade pode ser especificado com uma expressão de propriedades.|  
|IsDefaultOut|Boolean|Um valor que indica se a saída é a saída padrão.|  
  
 A entrada, as colunas de entrada e as colunas de saída da transformação Divisão Condicional não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Conditional Split Transformation](../../../integration-services/data-flow/transformations/conditional-split-transformation.md).  
  
##  <a name="copy-column-transformation-custom-properties"></a><a name="copymap"></a> Propriedades personalizadas da transformação Copiar Coluna  
 A transformação Copiar Coluna só tem as propriedades comuns a todos os componentes de fluxo de dados no nível do componente.  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de saída da transformação Copiar Coluna. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de dados|Descrição|  
|-------------------|---------------|-----------------|  
|copyColumnId|Integer|O **LineageID** da coluna de entrada da qual a coluna de saída é copiada.|  
  
 A entrada, as colunas de entrada e a saída da transformação Copiar Coluna não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Copy Column Transformation](../../../integration-services/data-flow/transformations/copy-column-transformation.md).  
  
##  <a name="data-conversion-transformation-custom-properties"></a><a name="dataconv"></a> Propriedades personalizadas da transformação Conversão de Dados  
 A transformação Conversão de Dados só tem as propriedades comuns a todos os componentes de fluxo de dados no nível do componente.  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de saída da transformação Conversão de Dados. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|FastParse|Boolean|Um valor que indica se as colunas usam as rotinas de análise mais rápidas, mas que não fazem distinção entre localidades, que o [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] fornece ou as rotinas de análise padrão que fazem distinção entre localidades. O valor padrão dessa propriedade é **False**. Para obter mais informações, consulte [Fast Parse](https://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95) e [Standard Parse](https://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013). .<br /><br /> Observação: Esta propriedade não está disponível no **Editor de transformação Conversão de Dados**, mas pode ser definida por meio do **Editor Avançado**.|  
|SourceInputColumnLineageId|Integer|O **LineageID** da coluna de entrada que é fonte da coluna de saída.|  
  
 A entrada, as colunas de entrada e a saída da transformação Conversão de Dados não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md).  
  
##  <a name="data-mining-query-transformation-custom-properties"></a><a name="dmquery"></a> Propriedades personalizadas da transformação Consulta de Mineração de Dados  
 A transformação Consulta de Mineração de Dados tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da transformação Consulta de Mineração de Dados. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|ASConnectionId|String|O identificador exclusivo do objeto de conexão.|  
|ASConnectionString|String|A cadeia de conexão com um projeto do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ou com um banco de dados do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .|  
|CatalogName|String|O nome de um banco de dados do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .|  
|ModelName|String|O nome do modelo de mineração de dados.|  
|ModelStructureName|String|O nome da estrutura de mineração.|  
|ObjectRef|String|Uma marca XML que identifica a estrutura de mineração de dados usada pela transformação.|  
|QueryText|String|A instrução de consulta de previsão usada pela transformação.|  
  
 A entrada, as colunas de entrada, a saída e as colunas de saída da transformação Consulta de Mineração de Dados não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Data Mining Query Transformation](../../../integration-services/data-flow/transformations/data-mining-query-transformation.md).  
  
##  <a name="derived-column-transformation-custom-properties"></a><a name="derived"></a> Propriedades personalizadas da transformação Coluna Derivada  
 A transformação Coluna Derivada só tem as propriedades comuns a todos os componentes de fluxo de dados no nível do componente.  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de entrada e das colunas de saída da transformação Coluna Derivada. Quando você opta por adicionar a coluna derivada como uma coluna nova, essas propriedades personalizadas se aplicam à nova coluna de saída; quando você opta por substituir o conteúdo de uma coluna de entrada existente com os resultados derivados, essas propriedades personalizadas se aplicam à coluna de entrada existente. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|Expression|String|Uma expressão que representa a condição avaliada pela transformação Divisão Condicional. Colunas são representadas pela propriedade **LineageID** da coluna.|  
|FriendlyExpression|String|Uma expressão que representa a condição avaliada pela transformação Divisão Condicional. Colunas são representadas pelos nomes.<br /><br /> O valor dessa propriedade pode ser especificado com uma expressão de propriedades.|  
  
 A entrada e a saída da transformação Coluna Derivada não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Derived Column Transformation](../../../integration-services/data-flow/transformations/derived-column-transformation.md).  
  
##  <a name="export-column-transformation-custom-properties"></a><a name="extract"></a> Propriedades personalizadas da transformação Exportar Coluna  
 A transformação Exportar Coluna só tem as propriedades comuns a todos os componentes de fluxo de dados no nível do componente.  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de entrada da transformação Exportar Coluna. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|AllowAppend|Boolean|Um valor que especifica se a transformação acrescenta dados a um arquivo existente. O valor padrão dessa propriedade é **False**.|  
|ForceTruncate|Boolean|Um valor que especifica se a transformação trunca arquivos existentes antes de gravar dados. O valor padrão dessa propriedade é **False**.|  
|FileDataColumnID|Integer|Um valor que identifica a coluna que contém os dados inseridos pela transformação em um arquivo. Em Extrair Coluna, essa propriedade tem um valor de **0**; na Coluna de Caminhos de Arquivos, essa propriedade contém o **LineageID** de Extrair Coluna.|  
|WriteBOM|Boolean|Um valor que especifica se uma marca de ordem de byte (BOM) é gravada no arquivo.|  
  
 A entrada, a saída e as colunas de saída da transformação Exportar Coluna não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Export Column Transformation](../../../integration-services/data-flow/transformations/export-column-transformation.md).  
  
##  <a name="import-column-transformation-custom-properties"></a><a name="insert"></a> Propriedades personalizadas da transformação Importar Coluna  
 A transformação Importar Coluna só tem as propriedades comuns a todos os componentes de fluxo de dados no nível do componente.  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de entrada da transformação Importar Coluna. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|ExpectBOM|Boolean|Um valor que especifica se a transformação Importar Coluna deve esperar por uma marca de ordem de byte (BOM). Uma BOM só será esperada se os dados tiverem o tipo de dados de DT_NTEXT.|  
|FileDataColumnID|Integer|Um valor que identifica a coluna que contém os dados inseridos pela transformação no fluxo de dados. Na coluna de dados a ser inserida, essa propriedade tem um valor de 0; na coluna que contém os caminhos de arquivo de origem, essa propriedade contém o **LineageID** da coluna de dados a ser inserida.|  
  
 A entrada, a saída e as colunas de saída da transformação Importar Coluna não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Import Column Transformation](../../../integration-services/data-flow/transformations/import-column-transformation.md).  
  
##  <a name="fuzzy-grouping-transformation-custom-properties"></a><a name="fgroup"></a> Propriedades personalizadas da transformação Agrupamento Difuso  
 A transformação Agrupamento Difuso tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da transformação Agrupamento Difuso. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|Delimitadores|String|Os delimitadores de token usados pela transformação. Os delimitadores padrão incluem os seguintes caracteres: espaço ( ), vírgula (,), ponto final (.), ponto e vírgula (;), dois-pontos (:), hífen (-), aspas ("), apóstrofo ('), E comercial (&), barra (/), barra invertida (\\), arroba (@), ponto de exclamação (!), ponto de interrogação (?), parêntese de abertura ((), parêntese de fechamento ()), menor que (\<), greater than (>), colchete de abertura ([), colchete de fechamento (]), chave de abertura ({), chave de fechamento (}), barra vertical ou pipe (&#124;), número (#), asterisco (*), circunflexo (^) e porcentagem (%).|  
|Exhaustive|Boolean|Um valor que especifica se cada registro de entrada é comparado a todos os outros registros de entrada. O valor de **True** destina-se especialmente a propósitos de depuração. O valor padrão dessa propriedade é **False**.<br /><br /> Observação: Esta propriedade não está disponível no **Editor de Transformação Agrupamento Difuso**, mas pode ser definida por meio do **Editor Avançado**.|  
|MaxMemoryUsage|Integer|A quantidade máxima de memória para uso pela transformação. O valor padrão dessa propriedade é **0**, que ativa o uso de memória dinâmica.<br /><br /> O valor dessa propriedade pode ser especificado com uma expressão de propriedades.<br /><br /> Observação: Esta propriedade não está disponível no **Editor de Transformação Agrupamento Difuso**, mas pode ser definida por meio do **Editor Avançado**.|  
|MinSimilarity|Double|O limite de semelhança usado pela transformação para identificar duplicatas, expresso como um valor entre 0 e 1.  O valor padrão dessa propriedade é 0.8.|  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de entrada da transformação Agrupamento Difuso. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|ExactFuzzy|Inteiro (enumeração)|Um valor que especifica se a transformação executa uma correspondência difusa ou uma correspondência exata. Os valores válidos são **Exato** e **Difuso**. O valor padrão para esta propriedade é **Difuso**.|  
|FuzzyComparisonFlags|Inteiro (enumeração)|Um valor que especifica como a transformação compara os dados de cadeia de caracteres em uma coluna. Essa propriedade pode ter um dos seguintes valores:<br /><br /> **FullySensitive**<br /><br /> **IgnoreCase**<br /><br /> **IgnoreKanaType**<br /><br /> **IgnoreNonSpace**<br /><br /> **IgnoreSymbols**<br /><br /> **IgnoreWidth**<br /><br /> <br /><br /> Para obter mais informações, consulte [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).|  
|LeadingTrailingNumeralsSignificant|Inteiro (enumeração)|Um valor que especifica o significado de numerais. Essa propriedade pode ter um dos seguintes valores:<br /><br /> **NumeralsNotSpecial** (0) – use se os numerais não forem significativos.<br /><br /> **LeadingNumeralsSignificant** (1) – use se os numerais à esquerda forem significativos.<br /><br /> **TrailingNumeralsSignificant** (2) – use se os numerais à direita forem significativos.<br /><br /> **LeadingAndTrailingNumeralsSignificant** (3) – use se os numerais à direita e à esquerda forem significativos.|  
|MinSimilarity|Double|O limite de similaridade usado para a junção na coluna, especificado como um valor entre 0 e 1. Somente linhas superiores ao limite são classificadas como correspondências.|  
|ToBeCleaned|Boolean|Um valor que especifica se a coluna é usada para identificar duplicatas; ou seja, se é uma coluna na qual está ocorrendo agrupamento. O valor padrão dessa propriedade é **False**.|  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de saída da transformação Agrupamento Difuso. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de dados|Descrição|  
|-------------------|---------------|-----------------|  
|ColumnType|Inteiro (enumeração)|Um valor que identifica o tipo de coluna de saída. Essa propriedade pode ter um dos seguintes valores:<br /><br /> **Undefined** (0)<br /><br /> **KeyIn** (1)<br /><br /> **KeyOut** (2)<br /><br /> **Similarity** (3)<br /><br /> **ColumnSimilarity** (4)<br /><br /> **PassThru** (5)<br /><br /> **Canonica**l (6)|  
|InputID|Integer|O **LineageID** da coluna de entrada correspondente.|  
  
 A entrada e a saída da transformação Agrupamento Difuso não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md).  
  
##  <a name="fuzzy-lookup-transformation-custom-properties"></a><a name="flookup"></a> Propriedades personalizadas da transformação Pesquisa Difusa  
 A transformação Pesquisa Difusa tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da transformação Pesquisa Difusa. Todas as propriedades, exceto **ReferenceMetadataXML** , são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|CopyReferenceTable|Boolean|Especifica se uma cópia da tabela de referência deve ser feita para a criação do índice de pesquisa difusa e pesquisas subsequentes. O valor padrão dessa propriedade é **True**.|  
|Delimitadores|String|Os delimitadores usados pela transformação para criar tokens de valores de coluna. Os delimitadores padrão incluem os seguintes caracteres: espaço ( ), vírgula (,), ponto final (.), ponto e vírgula (;), dois pontos (:), hífen (-), aspas ("), apóstrofo ('), E comercial (&), barra (/), barra invertida (\\), arroba (@), ponto de exclamação (!), ponto de interrogação (?), parêntese de abertura ((), parêntese de fechamento ()), menor que (\<), greater than (>), colchete de abertura ([), colchete de fechamento (]), chave de abertura ({), chave de fechamento (}), pipe (&#124;). sinal de número (#), asterisco (*), acento circunflexo (^) e porcentagem (%).|  
|DropExistingMatchIndex|Boolean|Um valor que especifica se o índice de correspondência especificado em MatchIndexName é excluído quando MatchIndexOptions não é definido como ReuseExistingIndex. O valor padrão para essa propriedade é **True**.|  
|Exhaustive|Boolean|Um valor que especifica se cada registro de entrada é comparado a todos os outros registros de entrada. O valor de **True** destina-se especialmente a propósitos de depuração. O valor padrão dessa propriedade é **False**.<br /><br /> Observação: Esta propriedade não está disponível no **Editor de Transformação Pesquisa Difusa**, mas pode ser definida por meio do **Editor Avançado**.|  
|MatchIndexName|String|O nome do índice de correspondência. O índice de correspondência é a tabela na qual a transformação cria e salva o índice usado. Se o índice de correspondência for reutilizado, MatchIndexName especificará o índice a ser reutilizado. MatchIndexName deve ser um nome de identificador válido do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Por exemplo, se o nome contiver espaços, deverá ser colocado entre colchetes.|  
|MatchIndexOptions|Inteiro (enumeração)|Um valor que especifica como a transformação gerencia o índice de correspondência. Essa propriedade pode ter um dos seguintes valores:<br /><br /> **ReuseExistingIndex** (0)<br /><br /> **GenerateNewIndex** (1)<br /><br /> **GenerateAndPersistNewIndex** (2)<br /><br /> **GenerateAndMaintainNewIndex** (3)|  
|MaxMemoryUsage|Integer|O tamanho máximo do cache para a tabela de pesquisa. O valor padrão desta propriedade é **0**, o que significa que não há limite para o tamanho do cache.<br /><br /> O valor dessa propriedade pode ser especificado com uma expressão de propriedades.<br /><br /> Observação: Esta propriedade não está disponível no **Editor de Transformação Pesquisa Difusa**, mas pode ser definida por meio do **Editor Avançado**.|  
|MaxOutputMatchesPerInput|Integer|O número máximo de correspondências que a transformação pode retornar para cada linha de entrada. O valor padrão desta propriedade é **1**.<br /><br /> Observação: Valores superiores a 100 só podem ser especificados usando o **Editor Avançado**.|  
|MinSimilarity|Integer|O limite de similaridade usado pela transformação no nível do componente, especificado como um valor entre 0 e 1. Somente linhas superiores ao limite são classificadas como correspondências.|  
|ReferenceMetadataXML|String|[!INCLUDE[ssInternalOnly](../../../includes/ssinternalonly-md.md)]|  
|ReferenceTableName|String|O nome da tabela de pesquisa. O nome deve ser um nome de identificador válido do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Por exemplo, se o nome contiver espaços, deverá ser colocado entre colchetes.|  
|WarmCaches|Boolean|Quando verdadeiro, a pesquisa carrega o índice e a tabela de referência parcialmente na memória antes do início da execução. Isso pode melhorar o desempenho.|  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de entrada da transformação Pesquisa Difusa. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|FuzzyComparisonFlags|Integer|Um valor que especifica como a transformação compara os dados de cadeia de caracteres em uma coluna. Para obter mais informações, consulte [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).|  
|FuzzyComparisonFlagsEx|Inteiro (enumeração)|Um valor que especifica quais sinalizadores de comparação estendida são usados pela transformação. Os valores podem incluir **MapExpandLigatures, MapFoldCZone**, **MapFoldDigits**, **MapPrecomposed**e **NoMapping**. **NoMapping** não pode ser usado com outros sinalizadores.|  
|JoinToReferenceColumn|String|Um valor que especifica o nome da coluna na tabela de referência à qual a coluna é unida.|  
|JoinType|Integer|Um valor que especifica se a transformação executa uma correspondência difusa ou uma correspondência exata. O valor padrão para esta propriedade é **Difuso**. O valor inteiro para o tipo de junção exata é **1** e o valor do tipo de junção difusa é **2**.|  
|MinSimilarity|Double|O limite de similaridade usado pela transformação no nível da coluna, especificado como um valor entre 0 e 1. Somente linhas superiores ao limite são classificadas como correspondências.|  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de saída da transformação Pesquisa Difusa. Todas as propriedades são de leitura/gravação.  
  
> [!NOTE]  
>  Em colunas de saída que contêm valores de passagem das colunas de entrada correspondentes, CopyFromReferenceColumn fica vazio e SourceInputColumnLineageID contém o **LineageID** da coluna de entrada correspondente. Em colunas de saída que contêm resultados de pesquisa, CopyFromReferenceColumn contém o nome da coluna de pesquisa e SourceInputColumnLineageID fica vazio.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|ColumnType|Inteiro (enumeração)|Um valor que identifica o tipo de coluna de saída para colunas que a transformação adiciona à saída. Essa propriedade pode ter um dos seguintes valores:<br /><br /> **Undefined** (0)<br /><br /> **Similarity** (1)<br /><br /> **Confiança** (2)<br /><br /> **ColumnSimilarity** (3)|  
|CopyFromReferenceColumn|String|Um valor que especifica o nome da coluna na tabela de referência que fornece o valor em uma coluna de saída.|  
|SourceInputColumnLineageId|Integer|Um valor que identifica a coluna de entrada que fornece valores a esta coluna de saída.|  
  
 A entrada e a saída da transformação Pesquisa Difusa não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Fuzzy Lookup Transformation](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md).  
  
##  <a name="lookup-transformation-custom-properties"></a><a name="lookup"></a> Propriedades personalizadas da transformação Pesquisa  
 A transformação Pesquisa tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da transformação Pesquisa. Todas as propriedades, exceto **ReferenceMetadataXML** , são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|CacheType|Inteiro (enumeração)|O tipo de cache da tabela de pesquisa. Os valores são **Cheio** (0), **Parcial** (1) e **Nenhum** (2). O valor padrão dessa propriedade é **Cheio**.|  
|DefaultCodePage|Integer|A página de código padrão a ser usada quando informações de página de código não estão disponíveis na fonte de dados.|  
|MaxMemoryUsage|Integer|O tamanho máximo do cache para a tabela de pesquisa. O valor padrão desta propriedade é **25**, o que significa que não há limite para o tamanho do cache.|  
|MaxMemoryUsage64|Integer|O tamanho máximo do cache para a tabela de pesquisa em um computador de 64 bits.|  
|NoMatchBehavior|Inteiro (enumeração)|Um valor que especifica se linhas sem entradas de correspondência no conjunto de dados de referência são tratadas como erros.<br /><br /> Quando a propriedade é definida como **Tratar as linhas sem entradas correspondentes como erros** (0), as linhas sem entradas correspondentes são tratadas como erros. É possível especificar o que deve acontecer quando esse tipo de erro ocorre usando a página **Saída de Erro** da caixa de diálogo **Editor de Transformação Pesquisa** . Para obter mais informações, consulte [Editor de Transformação Pesquisa &#40;página Saída de Erro&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md).<br /><br /> Quando a propriedade é definida como **Enviar linhas sem entradas correspondentes para a saída sem correspondência** (1), as linhas não são tratadas como erros.<br /><br /> O valor padrão é **Tratar as linhas sem entradas correspondentes como erros** (0).|  
|ParameterMap|String|Uma lista delimitada por ponto-e-vírgula de IDs de linhagem que são mapeadas para os parâmetros usados na instrução **SqlCommand** .|  
|ReferenceMetadataXML|String|Metadados para as colunas na tabela de pesquisa copiados pela transformação para a sua saída.|  
|SqlCommand|String|A instrução SELECT que popula a tabela de pesquisa.|  
|SqlCommandParam|String|A instrução SQL com parâmetros que popula a tabela de pesquisa.|  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de entrada da transformação Pesquisa. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|CopyFromReferenceColumn|String|O nome da coluna na tabela de referência da qual uma coluna é copiada.|  
|JoinToReferenceColumns|String|O nome da coluna na tabela de referência à qual uma de coluna de origem é unida.|  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de saída da transformação Pesquisa. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de dados|Descrição|  
|-------------------|---------------|-----------------|  
|CopyFromReferenceColumn|String|O nome da coluna na tabela de referência da qual uma coluna é copiada.|  
  
 A entrada e a saída da transformação Pesquisa não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md).  
  
##  <a name="merge-join-transformation-custom-properties"></a><a name="mjoin"></a> Propriedades personalizadas da transformação Mesclar Junção  
 A transformação Mesclar Junção tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da transformação Mesclar Junção.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|JoinType|Inteiro (enumeração)|Especifica se a junção é uma junção interna (2), esquerda externa (1) ou cheia (0).|  
|MaxBuffersPerInput|Integer|Não é mais preciso configurar o valor da propriedade **MaxBuffersPerInput** , pois a Microsoft fez alterações que reduzem o risco de a transformação Junção de Mesclagem consumir memória excessiva. Esse problema algumas vezes ocorria quando as várias entradas da Junção de Mesclagem geravam dados a taxas irregulares.|  
|NumKeyColumns|Integer|O número de colunas usadas na junção.|  
|TreatNullsAsEqual|Boolean|Um valor que especifica se a transformação controla valores nulos como valores iguais. O valor padrão dessa propriedade é **True**. Se o valor de propriedade for **False**, a transformação controlará valores nulos, como faz o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de saída da transformação Mesclar Junção. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de dados|Descrição|  
|-------------------|---------------|-----------------|  
|InputColumnID|Integer|O **LineageID** da coluna de entrada da qual são copiados dados para esta coluna de saída.|  
  
 A entrada, as colunas de entrada e a saída da transformação Mesclar Junção não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Merge Join Transformation](../../../integration-services/data-flow/transformations/merge-join-transformation.md).  
  
##  <a name="ole-db-command-transformation-custom-properties"></a><a name="oledbcmd"></a> Propriedades personalizadas da transformação Comando OLE DB  
 A transformação Comando OLE DB tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da transformação Comando OLE DB.  
  
|Nome da propriedade|Tipo de dados|Descrição|  
|-------------------|---------------|-----------------|  
|CommandTimeOut|Integer|O número máximo de segundos em que o comando SQL pode ser executado antes que o tempo limite seja excedido. O valor **0** indica que não há limite de tempo. O valor padrão dessa propriedade é **0**.|  
|DefaultCodePage|Integer|A página de código a ser usada quando informações de página de código não estão disponíveis na fonte de dados.|  
|SqlCommand|String|A instrução Transact-SQL executada pela transformação para cada linha no fluxo de dados.<br /><br /> O valor dessa propriedade pode ser especificado com uma expressão de propriedades.|  
  
 A tabela seguinte descreve as propriedades personalizadas das colunas externas da transformação Comando OLE DB. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de dados|Descrição|  
|-------------------|---------------|-----------------|  
|DBParamInfoFlag|Integer (bitmask)|Um conjunto de sinalizadores que descrevem características de parâmetro. Para obter mais informações, consulte o DBPARAMFLAGSENUM na documentação de OLE DB na Biblioteca MSDN.|  
  
 A entrada, as colunas de entrada, a saída e as colunas de saída da transformação Comando OLE DB não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [OLE DB Command Transformation](../../../integration-services/data-flow/transformations/ole-db-command-transformation.md).  
  
##  <a name="percentage-sampling-transformation-custom-properties"></a><a name="percent"></a> Propriedades personalizadas da transformação Amostragem Percentual  
 A transformação Amostragem Percentual tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da transformação Amostragem Percentual.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|SamplingSeed|Integer|A semente usada pelo gerador aleatório de números. O valor padrão desta propriedade é **0**, indicando que a transformação usa uma contagem de tiques.|  
|SamplingValue|Integer|O tamanho da amostra como uma porcentagem da fonte.<br /><br /> O valor dessa propriedade pode ser especificado com uma expressão de propriedades.|  
  
 A tabela a seguir descreve as propriedades personalizadas das saídas da transformação Amostragem Percentual. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de dados|Descrição|  
|-------------------|---------------|-----------------|  
|Selecionado|Boolean|Designa a saída para a qual as linhas de amostra são direcionadas. Na saída selecionada, Selecionado é definido como **True**, e na saída não selecionada, Selecionado é definido como **False**.|  
  
 A entrada, as colunas de entrada e as colunas de saída da transformação Amostragem Percentual não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Percentage Sampling Transformation](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md).  
  
##  <a name="pivot-transformation-custom-properties"></a><a name="pivot"></a> Propriedades personalizadas da transformação Dinâmica  
 A tabela a seguir descreve as propriedades personalizadas dos componentes da transformação Dinâmica.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|**PassThroughUnmatchedPivotKeyts**|Boolean|Defina como **True** para configurar a transformação Dinâmica para ignorar as linhas que contêm valores não reconhecidos na coluna Chave Dinâmica e gerar todos os valores de chave dinâmica para uma mensagem de log, quando o pacote é executado.|  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de entrada da transformação Dinâmica. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|PivotUsage|Inteiro (enumeração)|Um valor que especifica a função de uma coluna quando o conjunto de dados é dinamizado.<br /><br /> **0**:<br />                      A coluna não é dinamizada e os valores de coluna são passados para a saída de transformação.<br /><br /> **1**:<br />                      A coluna faz parte da chave definida que identifica uma ou mais linhas como parte de um conjunto. Todas as linhas de entrada com a mesma chave definida são combinadas em uma linha de saída.<br /><br /> **2**:<br />                      A coluna é dinâmica. Pelo menos uma coluna é criada a partir de cada valor da coluna.<br /><br /> **3**:<br />                      Os valores desta coluna são colocados em colunas, que são criadas como resultado da dinamização.|  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de saída da transformação Dinâmica. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|PivotKeyValue|String|Um dos possíveis valores da coluna assinalada como a chave dinâmica pelo valor de sua propriedade PivotUsage.<br /><br /> O valor dessa propriedade pode ser especificado com uma expressão de propriedades.|  
|SourceColumn|Integer|O **LineageID** de uma coluna de entrada que contém um valor dinâmico ou -1. O valor de -1 indica que a coluna não é usada em uma operação dinâmica.|  
  
 Para obter mais informações, consulte [Pivot Transformation](../../../integration-services/data-flow/transformations/pivot-transformation.md).  
  
##  <a name="row-count-transformation-custom-properties"></a><a name="rowcount"></a> Propriedades personalizadas da transformação Contagem de Linhas  
 A transformação Contagem de Linhas tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da transformação Contagem de Linhas. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de dados|Descrição|  
|-------------------|---------------|-----------------|  
|VariableName|String|O nome da variável que contém a contagem de linhas.|  
  
 A entrada, as colunas de entrada, a saída e as colunas de saída da transformação Contagem de Linhas não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Row Count Transformation](../../../integration-services/data-flow/transformations/row-count-transformation.md).  
  
##  <a name="row-sampling-transformation-custom-properties"></a><a name="rowsamp"></a> Propriedades personalizadas da transformação Amostragem de Linhas  
 A transformação Amostragem de Linhas tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da transformação Amostragem de Linhas. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|SamplingSeed|Integer|A semente usada pelo gerador aleatório de números. O valor padrão desta propriedade é **0**, indicando que a transformação usa uma contagem de tiques.|  
|SamplingValue|Integer|A contagem de linhas da amostra.<br /><br /> O valor dessa propriedade pode ser especificado com uma expressão de propriedades.|  
  
 A tabela a seguir descreve as propriedades personalizadas das saídas da transformação Amostragem de Linhas. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de dados|Descrição|  
|-------------------|---------------|-----------------|  
|Selecionado|Boolean|Designa a saída para a qual as linhas de amostra são direcionadas. Na saída selecionada, Selecionado é definido como **True**, e na saída não selecionada, Selecionado é definido como **False**.|  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de saída da transformação Amostragem de Linhas. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|InputColumnLineageId|Integer|Um valor que especifica o **LineageID** da coluna de entrada que é a fonte da coluna de saída.|  
  
 A entrada e as colunas de entrada da transformação Amostragem de Linhas não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Row Sampling Transformation](../../../integration-services/data-flow/transformations/row-sampling-transformation.md).  
  
##  <a name="script-component-custom-properties"></a><a name="script"></a> Propriedades personalizadas do Componente de Script  
 O Componente de Script tem propriedades personalizadas e as propriedades comum a todos os componentes de fluxo de dados. As mesmas propriedades personalizadas ficarão disponíveis se o Componente de Script funcionar como uma fonte, transformação ou destino.  
  
 A tabela a seguir descreve as propriedades personalizadas do Componente de Script. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de dados|Descrição|  
|-------------------|---------------|-----------------|  
|ReadOnlyVariables|String|Uma lista de variáveis separadas por vírgulas disponível para o Componente de Script para acesso em modo somente leitura.|  
|ReadWriteVariables|String|Uma lista de variáveis separadas por vírgulas disponível para o Componente de Script para acesso em modo leitura/gravação.|  
  
 A entrada, as colunas de entrada, a saída e as colunas de saída do Componente de Script não têm propriedades personalizadas, a menos que sejam criadas pelo desenvolvedor de scripts.  
  
 Para obter mais informações, consulte [Script Component](../../../integration-services/data-flow/transformations/script-component.md).  
  
##  <a name="slowly-changing-dimension-transformation-custom-properties"></a><a name="scd"></a> Propriedades personalizadas da transformação Dimensão de Alteração Lenta  
 A transformação Dimensão de Alteração Lenta tem propriedades personalizadas e as propriedades comum a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da transformação Dimensão de Alteração Lenta. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|CurrentRowWhere|String|A cláusula WHERE na instrução SELECT que seleciona a linha atual entre linhas com a mesma chave de negócio.|  
|EnableInferredMember|Boolean|Um valor que especifica se atualizações de membros inferidos foram detectadas. O valor padrão dessa propriedade é **True**.|  
|FailOnFixedAttributeChange|Boolean|Um valor que especifica se a transformação falha quando colunas de linha com atributos fixos contêm alterações ou a pesquisa na tabela da dimensão falha. Se você espera que linhas de entrada contenham novos registros, defina este valor como **True** para que a transformação continue após a falha na pesquisa, já que ela usa a falha para identificar novos registros. O valor padrão dessa propriedade é **False**.|  
|FailOnLookupFailure|Boolean|Um valor que especifica se a transformação falha quando a pesquisa de um registro existente falha. O valor padrão dessa propriedade é **False**.|  
|IncomingRowChangeType|Integer|Um valor que especifica se todas as linhas de entrada são novas ou se a transformação deve detectar o tipo de alteração.|  
|InferredMemberIndicator|String|O nome de coluna para o membro inferido.|  
|SqlCommand|String|A instrução SQL usada para criar um conjunto de linhas de esquema.|  
|UpdateChangingAttributeHistory|Boolean|Um valor que indica se atualizações de atributo de histórico são direcionadas à saída da transformação para alteração de atualizações de atributos.|  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de entrada da transformação Dimensão de Alteração Lenta. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|ColumnType|Inteiro (enumeração)|O tipo de atualização da coluna. Os valores são: **Atributo de Alteração** (2), **Atributo Fixo** (4), **Atributo Histórico** (3), **Chave** (1) e **Outro** (0).|  
  
 A entrada, as saídas e as colunas de saída da transformação Dimensão de Alteração Lenta não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md).  
  
##  <a name="sort-transformation-custom-properties"></a><a name="sort"></a> Propriedades personalizadas da transformação Classificar  
 A transformação Classificar tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da transformação Classificar. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|EliminateDuplicates|Boolean|Especifica se a transformação remove linhas duplicadas da saída da transformação. O valor padrão dessa propriedade é **False**.|  
|MaximumThreads|Integer|Contém o número máximo de threads que a transformação pode usar para classificar. Um valor **0** indica que não há limite de threads. O valor padrão dessa propriedade é **0**.<br /><br /> O valor dessa propriedade pode ser especificado com uma expressão de propriedades.|  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de entrada da transformação Classificar. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|NewComparisonFlags|Integer (bitmask)|Um valor que especifica como a transformação compara os dados de cadeia de caracteres em uma coluna. Para obter mais informações, consulte [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).|  
|NewSortKeyPosition|Integer|Um valor que especifica a ordem de classificação da coluna. Um valor de 0 indica que os dados não são classificados nesta coluna.|  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de saída da transformação Classificar. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|SortColumnID|Integer|O **LineageID** de uma coluna de classificação.|  
  
 A entrada e a saída da transformação Classificar não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Sort Transformation](../../../integration-services/data-flow/transformations/sort-transformation.md).  
  
##  <a name="term-extraction-transformation-custom-properties"></a><a name="textract"></a> Propriedades personalizadas da transformação Extração de Termos  
 A transformação Extração de Termos tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da transformação Extração de Termos. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|--------------|-----------------|  
|FrequencyThreshold|Integer|Um valor numérico que indica o número de vezes que um termo deve ocorrer antes de ser extraído. O valor padrão dessa propriedade é **2**.|  
|IsCaseSensitive|Boolean|Um valor que especifica se a diferenciação de maiúsculas e minúsculas é usada na extração de substantivos e frases nominais. O valor padrão dessa propriedade é **False**.|  
|MaxLengthOfTerm|Integer|Um valor numérico que indica o comprimento máximo de um termo. Esta propriedade só se aplica a frases. O valor padrão dessa propriedade é **12**.|  
|NeedRefenceData|Boolean|Um valor que especifica se a transformação usa uma lista de termos de exclusão armazenada em uma tabela de referência. O valor padrão dessa propriedade é **False**.|  
|OutTermColumn|String|O nome da coluna que contém os termos de exclusão.|  
|OutTermTable|String|O nome da tabela que contém a coluna com termos de exclusão.|  
|ScoreType|Integer|Um valor que especifica o tipo de pontuação a ser associado ao termo. Os valores válidos são 0 (frequência) e 1 (pontuação TFIDF). A contagem de TFIDF é o produto da Frequência de Termo e da Frequência de Documento Inversa, definido como: TFIDF de um termo T = (frequência de T) \* log ((nºs de linhas na Entrada) / (nº de linhas com T)). O valor padrão dessa propriedade é **0**.|  
|WordOrPhrase|Integer|Um valor que especifica o tipo de termo. Os valores válidos são 0 (somente palavras), 1 (somente frases nominais) e 2 (palavras e frases nominais). O valor padrão dessa propriedade é **0**.|  
  
 A entrada, as colunas de entrada, a saída e as colunas de saída da transformação Contagem de Linhas não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Term Extraction Transformation](../../../integration-services/data-flow/transformations/term-extraction-transformation.md).  
  
##  <a name="term-lookup-transformation-custom-properties"></a><a name="tlookup"></a> Propriedades personalizadas da transformação Pesquisa de Termos  
 A transformação Pesquisa de Termos tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da transformação Pesquisa de Termos. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|IsCaseSensitive|Boolean|Um valor que especifica se uma comparação que faz distinção entre letras maiúsculas e minúsculas é aplicável à correspondência do texto da coluna de entrada e do termo da pesquisa. O valor padrão dessa propriedade é **False**.|  
|RefTermColumn|String|O nome da coluna que contém os termos da pesquisa.|  
|RefTermTable|String|O nome da tabela que contém a coluna com termos da pesquisa.|  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de entrada da transformação Pesquisa de Termos. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|InputColumnType|Integer|Um valor que especifica o uso da coluna. Os valores válidos são 0 (coluna de passagem), 1 (coluna de pesquisa) e 2 (coluna de passagem e de pesquisa).|  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de saída da transformação Pesquisa de Termos. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de dados|Descrição|  
|-------------------|---------------|-----------------|  
|CustomLineageID|Integer|O **LineageID** da coluna de entrada correspondente se o **InputColumnType** dela for 0 ou 2.|  
  
 A entrada e a saída da transformação Pesquisa de Termos não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Term Lookup Transformation](../../../integration-services/data-flow/transformations/term-lookup-transformation.md).  
  
##  <a name="unpivot-transformation-custom-properties"></a><a name="unpivot"></a> Propriedades personalizadas da transformação Não Dinâmica  
 A transformação Não Dinâmica só tem as propriedades comuns a todos os componentes de fluxo de dados no nível do componente.  
  
> [!NOTE]  
>  Esta seção tem como base o cenário da transformação Não Dinâmica descrito em [Transformação Não Dinâmica](../../../integration-services/data-flow/transformations/unpivot-transformation.md) para ilustrar o uso das opções descritas aqui.  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de entrada da transformação Não Dinâmica. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|DestinationColumn|Integer|O **LineageID** da coluna de saída para a qual coluna de entrada é mapeada. Um valor de -1 indica que a coluna de entrada não é mapeada para uma coluna de saída.|  
|PivotKeyValue|String|Um valor que é copiado em uma coluna de saída de transformação.<br /><br /> O valor dessa propriedade pode ser especificado com uma expressão de propriedades.<br /><br /> No cenário da transformação Não Dinâmica descrito em [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md), os Valores Dinâmicos são os valores de texto Ham, Coke, Milk, Beer e Chips. Serão exibidos como valores de texto na nova coluna Produto designada pela opção **Nome da Coluna de Valores de Chaves Dinâmicas** .|  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de saída da transformação Não Dinâmica. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de dados|Descrição|  
|-------------------|---------------|-----------------|  
|PivotKey|Boolean|Indica se os valores na propriedade **PivotKeyValue** de colunas de entrada são gravados nesta coluna de saída.<br /><br /> No cenário da transformação Não Dinâmica descrito em [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md), o nome da coluna de Valores Dinâmicos é **Produto** e designa a nova coluna **Produto** , na qual as colunas Ham, Coke, Milk, Beer e Chips não são dinâmicos.|  
  
 A entrada e a saída da transformação Não Dinâmica não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)   
 [Propriedades do caminho](https://msdn.microsoft.com/library/89b1e347-9579-4f6b-af74-c6519ea08eea)   
 [Propriedades de fluxo de dados que podem ser definidas usando expressões](https://msdn.microsoft.com/library/cd0e171a-08be-45d6-81dc-ed94f37698b8)  
  
  
