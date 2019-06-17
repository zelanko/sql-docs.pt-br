---
title: Transformação Agregação | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.aggregatetrans.f1
helpviewer_keywords:
- IsBig property
- aggregate functions [Integration Services]
- Aggregate transformation [Integration Services]
- large data, SSIS transformations
ms.assetid: 2871cf2a-fbd3-41ba-807d-26ffff960e81
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4759050a9453e1925ea47bc3dbf66d13aa821feb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770632"
---
# <a name="aggregate-transformation"></a>Transformação Agregação
  A transformação Agregação aplica funções de agregação, como Average, a valores de coluna e copia os resultados na saída da transformação. Além de funções de agregação, a transformação fornece a cláusula GROUP BY que você pode utilizar para especificar grupos a serem agregados.  
  
## <a name="operations"></a>Operations  
 A transformação Agregação oferece suporte às seguintes operações.  
  
|Operação|Descrição|  
|---------------|-----------------|  
|Agrupar por|Divide conjuntos de dados em grupos. As colunas contendo qualquer tipo de dados podem ser utilizadas para agrupamento. Para obter mais informações, veja [GROUP BY &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-group-by-transact-sql).|  
|Sum|Soma os valores em uma coluna. Somente colunas com tipos de dados numéricos podem ser somadas. Para obter mais informações, veja [SUM &#40;Transact-SQL&#41;](/sql/t-sql/functions/sum-transact-sql).|  
|Média|Retorna a média dos valores da coluna em uma coluna. A média só poderá ser obtida em colunas com tipos de dados numéricos. Para obter mais informações, veja [AVG &#40;Transact-SQL&#41;](/sql/t-sql/functions/avg-transact-sql).|  
|Count|Retorna o número de itens de um grupo. Para obter mais informações, veja [COUNT &#40;Transact-SQL&#41;](/sql/t-sql/functions/count-transact-sql).|  
|Distinção de Contagem|Retorna o número de valores não nulos exclusivos de um grupo.|  
|Mínimo|Retorna o valor mínimo de um grupo. Para obter mais informações, veja [MIN &#40;Transact-SQL&#41;](/sql/t-sql/functions/min-transact-sql). Ao contrário da função Transact-SQL MIN, essa operação pode ser usada apenas com tipos de dados de data, hora e numéricos.|  
|Máximo|Retorna o valor máximo em um grupo. Para obter mais informações, veja [MAX &#40;Transact-SQL&#41;](/sql/t-sql/functions/max-transact-sql). Ao contrário da função Transact-SQL MIN, essa operação pode ser usada apenas com tipos de dados de data, hora e numéricos.|  
  
 A transformação Agregação lida com os valores nulos da mesma maneira que o Mecanismo de Banco de Dados relacional do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . O comportamento é definido de acordo com os padrões do SQL-92. As seguintes regras se aplicam:  
  
-   Em uma cláusula GROUP BY, os nulos são tratados da mesma forma que os outros valores da coluna. Se a coluna de agrupamento contiver mais de um valor nulo, os valores nulos serão colocados em um único grupo.  
  
-   Nas funções COUNT (nome de coluna) e COUNT (DISTINCT nome de coluna), os nulos são ignorados e o resultado exclui as linhas que contêm os valores nulos da coluna nomeada.  
  
-   Na função COUNT (*), todas as linhas são contadas, incluindo as linhas com valores nulos.  
  
## <a name="big-numbers-in-aggregates"></a>Números grandes em agregações  
 Uma coluna pode conter valores numéricos que necessitem de uma análise especial devido a seu alto valor ou requisitos de precisão. A transformação Agregação inclui a propriedade IsBig, que pode ser definida em colunas de saída para invocar um tratamento especial em números de valor elevado ou de alta precisão. Se um valor de coluna exceder 4 bilhões ou se uma precisão maior que a de um tipo de dados flutuante for necessária, IsBig deverá ser definido como 1.  
  
 A configuração da propriedade IsBig como 1 afeta a saída da transformação agregação das seguintes maneiras:  
  
-   O tipo de dados DT_R8 é utilizado em vez do tipo de dados DT_R4.  
  
-   Os resultados da contagem são armazenados como tipo de dados DT_UI8.  
  
-   Os resultados de contagem distinta são armazenados como tipo de dados DT_UI4.  
  
> [!NOTE]  
>  Não é possível definir IsBig como 1 em colunas que são utilizadas nas operações GROUP BY, Máximo ou Mínimo.  
  
## <a name="performance-considerations"></a>Considerações sobre desempenho  
 A transformação Agregação inclui um conjunto de propriedades que você pode definir para aprimorar o desempenho da transformação.  
  
-   Ao executar uma operação **Agrupar por** , defina as propriedades Keys ou KeysScale do componente e as saídas do componente. Com o uso de Keys, especifique o número exato de chaves com as quais a transformação deverá lidar. (Neste contexto, Keys se refere ao número de grupos que deverá resultar de uma operação **Agrupar por**.) Com o uso de KeysScale, especifique um número aproximado de chaves. Quando você especifica um valor apropriado para Keys ou KeyScale, o desempenho melhora porque a transformação pode alocar memória adequada para os dados armazenados em cache.  
  
-   Ao realizar uma operação **Contagem distinta** , defina as propriedades CountDistinctKeys ou CountDistinctScale do componente. Com o uso de CountDistinctKeys, especifique o número exato de chaves que a transformação deverá tratar em uma operação de contagem distinta. (Neste contexto, CountDistinctKeys se refere ao número de valores distintos que deverá resultar de uma operação **Contagem distinta**.) Com o uso de CountDistinctScale, você pode especificar um número aproximado de chaves para uma operação de contagem distinta. Quando você especifica um valor apropriado para CountDistinctKeys ou CountDistinctScale, o desempenho melhora porque a transformação pode alocar memória adequada para os dados armazenados em cache.  
  
## <a name="aggregate-transformation-configuration"></a>Configuração da transformação Agregação  
 Você configura a transformação Agregação na transformação, na saída e nos níveis de coluna.  
  
-   No nível da transformação, configure a transformação Agregação para o desempenho especificando os seguintes valores:  
  
    -   O número de grupos que deverá resultar de uma operação **Agrupar por** .  
  
    -   O número de valores distintos que deverá resultar de uma operação **Contagem distinta** .  
  
    -   A porcentagem pela qual é possível estender a memória durante a agregação.  
  
     A transformação Agregação também pode ser configurada para gerar um aviso em vez de falhar quando o valor de um divisor for zero.  
  
-   No nível de saída, configure a transformação Agregação para o desempenho especificando o número de grupos que deverá resultar de uma operação **Agrupar por** . A transformação Agregação dá suporte a várias saídas e cada uma delas pode ser configurada de modo diferente.  
  
-   No nível da coluna, especifique os seguintes valores:  
  
    -   A agregação executada pela coluna.  
  
    -   As opções de comparação da agregação.  
  
 Também é possível configurar a transformação Agregação para o desempenho especificando estes valores:  
  
-   O número de grupos que deverá resultar de uma operação **Agrupar por** na coluna.  
  
-   O número de valores distintos que deverá resultar de uma operação **Contagem distinta** na coluna.  
  
 Também será possível identificar colunas como IsBig se uma coluna contiver valores numéricos grandes ou valores numéricos com alta precisão.  
  
 A transformação Agregação é assíncrona. Isto significa que ela não consome e publica dados linha por linha. Em vez de consumir o conjunto de linhas inteiro, ela executa seus agrupamentos e agregações e, depois, publica os resultados.  
  
 Essa transformação não transpassa nenhuma coluna, mas cria colunas novas no fluxo de dados para os dados que publica. Somente as colunas de entrada às quais se aplicam funções de agregação ou as que a transformação usa para agrupamento são copiadas para a saída da transformação. Por exemplo, uma entrada da transformação Agregação pode ter três colunas: **CountryRegion**, **City** e **Population**. A transformação faz o agrupamento pela coluna **CountryRegion** e aplica a função Sum à coluna **Population** . Por isso, a saída não inclui a coluna **City** .  
  
 Você também pode adicionar várias saídas à transformação Agregação e direcionar cada agregação a uma saída diferente. Por exemplo, se a transformação Agregação aplicar as funções Sum e Average, cada agregação poderá ser direcionada para uma saída diferente.  
  
 Você pode aplicar várias agregações a uma única coluna de entrada. Por exemplo, se você quiser os valores da soma e da média para uma coluna de entrada denominada **Vendas**, será possível configurar a transformação para aplicar as funções Sum e Average à coluna **Vendas** .  
  
 A transformação Agregação tem uma entrada e uma ou mais saídas. Não dá suporte a uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Transformação Agregação** , clique em um dos seguintes tópicos:  
  
-   [Editor de Transformação Agregação &#40;guia Agregações&#41;](../../aggregate-transformation-editor-aggregations-tab.md)  
  
-   [Editor de Transformação Agregação &#40;guia Avançado&#41;](../../aggregate-transformation-editor-advanced-tab.md)  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../../common-properties.md)  
  
-   [Propriedades personalizadas de Transformação](transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir propriedades, clique em um dos seguintes tópicos:  
  
-   [Agregar valores em um conjunto de dados por meio da transformação Agregação](aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
-   [Definir as propriedades de um componente de fluxo de dados](../set-the-properties-of-a-data-flow-component.md)  
  
-   [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [Agregar valores em um conjunto de dados por meio da transformação Agregação](aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
## <a name="see-also"></a>Consulte também  
 [Fluxo de Dados](../data-flow.md)   
 [Transformações do Integration Services](integration-services-transformations.md)  
  
  
