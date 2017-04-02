---
title: "Editor de Transforma&#231;&#227;o Agrega&#231;&#227;o (guia Agrega&#231;&#245;es) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.aggregationtransformation.aggregations.f1"
helpviewer_keywords: 
  - "Editor de Transformação Agregação"
ms.assetid: a01cb124-ec79-4673-b1a1-bf4d60ee1b45
caps.latest.revision: 30
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 30
---
# Editor de Transforma&#231;&#227;o Agrega&#231;&#227;o (guia Agrega&#231;&#245;es)
  Use a guia **Agregações** da caixa de diálogo **Editor de Transformação Agregação** para especificar colunas para agregação e propriedades de agregação. Você pode aplicar diversas agregações. Esta transformação não gera uma saída de erro.  
  
> [!NOTE]  
>  As opções de contagem de chaves, escala de chave, contagem de chaves distintas e escala de chave distinta são aplicadas em nível de componente quando especificado na guia **Avançado**, em nível de saída quando especificado na exibição avançada da guia **Agregações** e em nível de coluna quando especificado na lista de colunas na parte inferior da guia **Agregações**.  
>   
>  Na transformação Agregação, **Chaves** e **Escala de Chave** fazem referência ao número de grupos que são esperados como resultado de uma operação **Agrupar porz** . **Chaves de distinção de contagem** e **Escala de distinção de contagem** fazem referência ao número de valores distintos que são esperados como resultado de uma operação de **Contagem de distinção** .  
  
 Para obter mais informações sobre a transformação Agregação, consulte [Aggregate Transformation](../../../integration-services/data-flow/transformations/aggregate-transformation.md).  
  
## Opções  
 **Avançado/Básico**  
 Exiba ou oculte opções para configurar várias agregações para diversas saídas. Por padrão, as opções Avançadas são ocultas.  
  
 **Nome da Agregação**  
 Na exibição avançada, digite um nome amigável para a agregação.  
  
 **Agrupar por Colunas**  
 Na exibição avançada, selecione as colunas a serem agrupadas usando a lista **Colunas de Entrada Disponíveis** como descrito abaixo.  
  
 **Escala de Chave**  
 Na exibição avançada, especifique, opcionalmente, o número aproximado de chaves que a agregação pode gravar. Por padrão, o valor desta opção é **Não Especificado**. Se as propriedades **Escala de Chave** e **Chaves** forem definidas, o valor de **Chaves** terá precedência.  
  
|Value|Description|  
|-----------|-----------------|  
|Não Especificado|A propriedade Chave de Escala não é usada.|  
|Baixa|A agregação pode gravar aproximadamente 500.000 chaves.|  
|Média|A agregação pode gravar aproximadamente 5.000.000 de chaves.|  
|Alta|A agregação pode gravar mais de 25.000.000 de chaves.|  
  
 **Chaves**  
 Na exibição avançada, especifique, opcionalmente, o número exato de chaves que a agregação pode gravar. Se forem especificadas **Escala de Chave** e **Chaves**, **Chaves** terá precedência.  
  
 **Colunas de Entrada Disponíveis**  
 Selecione na lista de colunas de entrada disponíveis usando as caixas de seleção nesta tabela.  
  
 **Coluna de Entrada**  
 Selecione na lista de colunas de entrada disponíveis.  
  
 **Alias de Saída**  
 Digite um alias para cada coluna. O padrão é o nome da coluna de entrada; no entanto, é possível escolher qualquer nome descritivo exclusivo.  
  
 **Operação**  
 Escolha na lista de operações disponíveis, usando a tabela abaixo como guia.  
  
|Operação|Description|  
|---------------|-----------------|  
|**GroupBy**|Divide conjuntos de dados em grupos. Colunas que contêm qualquer tipo de dados podem ser utilizadas para agrupamento. Para obter mais informações, consulte GROUP BY.|  
|**Sum**|Soma os valores em uma coluna. Somente colunas com tipos de dados numéricos podem ser somadas. Para obter mais informações, consulte SUM.|  
|**Médio**|Retorna a média dos valores da coluna em uma coluna. A média só poderá ser obtida em colunas com tipos de dados numéricos. Para obter mais informações, consulte AVG.|  
|**Count**|Retorna o número de itens de um grupo. Para obter mais informações, consulte COUNT.|  
|**CountDistinct**|Retorna o número de valores não nulos exclusivos de um grupo. Para obter mais informações, consulte COUNT e Distinct.|  
|**Mínimo**|Retorna o valor mínimo de um grupo. Restrito a tipos de dados numéricos.|  
|**Máximo**|Retorna o valor máximo em um grupo. Restrito a tipos de dados numéricos.|  
  
 **Sinalizadores de Comparação**  
 Se você escolher **Agrupar por**, use as caixas de seleção para controlar como a transformação executa a comparação. Para obter mais informações sobre as opções de comparação de cadeias de caracteres, consulte [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md) (Comparando dados de cadeia de caracteres).  
  
 **Escala de distinção de contagem**  
 Especifique, opcionalmente, o número aproximado de valores de distinção que a agregação pode gravar. Por padrão, o valor desta opção é **Não Especificado**. Se forem especificadas **CountDistinctScale** e **CountDistinctKeys**, **CountDistinctKeys** terá precedência.  
  
|Value|Description|  
|-----------|-----------------|  
|Não Especificado|A propriedade **CountDistinctScale** não é usada.|  
|Baixa|A agregação pode gravar aproximadamente 500.000 valores de distinção.|  
|Média|A agregação pode gravar aproximadamente 5.000.000 valores distintos.|  
|Alta|A agregação pode gravar mais de 25.000.000 de valores de distinção.|  
  
 **Chaves de distinção de contagem**  
 Especifique, opcionalmente, o número exato de valores de distinção que a agregação pode gravar. Se forem especificadas **CountDistinctScale** e **CountDistinctKeys**, **CountDistinctKeys** terá precedência.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de Transformação Agregação &#40;guia Avançado&#41;](../../../integration-services/data-flow/transformations/aggregate-transformation-editor-advanced-tab.md)   
 [Agregar valores em um conjunto de dados por meio da transformação Agregação](../../../integration-services/data-flow/transformations/aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
  