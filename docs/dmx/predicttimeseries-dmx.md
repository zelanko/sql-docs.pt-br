---
title: PredictTimeSeries (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 60c55373a1647f6a2f12526e308d6ca45aeebb7b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041706"
---
# <a name="predicttimeseries-dmx"></a>PredictTimeSeries (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna previsões de valores futuros para os dados das séries temporais. Os dados de séries temporais são contínuos e podem ser armazenados em uma tabela aninhada ou em uma tabela de caso. O **PredictTimeSeries** função sempre retorna uma tabela aninhada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PredictTimeSeries(<table column reference>)  
PredictTimeSeries(<table column reference>, n)  
PredictTimeSeries(<table column reference>, n-start, n-end)  
PredictTimeSeries(<scalar column reference>)  
PredictTimeSeries(<scalar column reference>, n)  
PredictTimeSeries(<scalar column reference>, n-start, n-end)  
PredictTimeSeries(<table column reference>, n, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
PredictTimeSeries(<table column reference>, n-start, n-end, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
PredictTimeSeries(<scalar column reference>, n, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
PredictTimeSeries(<scalar column reference>, n-start, n-end, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
```  
  
## <a name="arguments"></a>Argumentos  
 *\<referência de coluna de tabela >* ,  *\<referência de coluna escalar >*  
 Especifica o nome da coluna a ser prevista. A coluna pode conter dados escalares ou tabulares.  
  
 *n*  
 Especifica o número de etapas seguintes a serem previstas. Se um valor não for especificado para *n*, o padrão é 1.  
  
 *n* não pode ser 0. A função retornará um erro se você não fizer pelo menos uma previsão.  
  
 *n-start, n-end*  
 Especifica um intervalo de etapas de série temporal.  
  
 *n-início* deve ser um inteiro e não pode ser 0.  
  
 *n-end* deve ser um número inteiro maior que *n-início*.  
  
 *\<consulta de origem >*  
 Define os dados externos usados para fazer previsões.  
  
 REPLACE_MODEL_CASES | EXTEND_MODEL_CASES  
 Indica como manipular novos dados.  
  
 REPLACE_MODEL_CASES especifica que os pontos de dados no modelo devem ser substituídos pelos novos dados. No entanto as previsões são baseadas nos padrões do modelo de mineração existentes.  
  
 EXTEND_MODEL_CASES especifica que os novos dados devem ser adicionados ao conjunto de dados de treinamento original. As previsões futuras são feitas no conjunto de dados composto somente depois que os novos dados foram usados.  
  
 Estes argumentos só podem ser usados quando os novos dados são adicionados usando uma instrução PREDICTION JOIN. Se você usar uma consulta PREDICTION JOIN e não especificar um argumento, o padrão será EXTEND_MODEL_CASES.  
  
## <a name="return-type"></a>Tipo de retorno  
 Um \< *expressão de tabela*>.  
  
## <a name="remarks"></a>Comentários  
 O algoritmo Time Series da [!INCLUDE[msCoName](../includes/msconame-md.md)] não suporta a previsão histórica ao usar a instrução PREDICTION JOIN para adicionar novos dados.  
  
 Em um PREDICTION JOIN, o processo de previsão sempre começa no período imediatamente após o final da série de treinamento original. Isso é verdadeiro mesmo se você adicionar novos dados. Portanto, o *n* parâmetro e *n início* valores de parâmetro devem ser um inteiro maior que 0.  
  
> [!NOTE]  
>  O comprimento dos dados novos não afeta o ponto de partida da previsão. Portanto, se você quiser adicionar novos dados e também fazer novas previsões, certifique-se de definir o ponto de partida da previsão com um valor maior do que o comprimento dos dados novos ou estenda o ponto final da previsão com base no comprimento dos dados novos.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos seguintes mostram como fazer previsões com relação a um modelo de série temporal existente:  
  
-   O primeiro exemplo mostra como fazer um número especificado de previsões com base no modelo atual.  
  
-   O segundo exemplo mostra como usar o parâmetro REPLACE_MODEL_CASES para aplicar os padrões do modelo especificado a um novo conjunto de dados.  
  
-   O terceiro exemplo mostra como usar o parâmetro EXTEND_MODEL_CASES para atualizar um modelo de mineração com dados novos.  
  
 Para saber mais sobre como trabalhar com modelos de série temporal, consulte o tutorial de mineração de dados, [lição 2: Criando um cenário de previsão &#40;Tutorial de mineração de dados intermediário&#41; ](https://msdn.microsoft.com/library/9a988156-c900-4c22-97fa-f6b0c1aea9e2) e [Tutorial DMX de previsão de série de tempo](https://msdn.microsoft.com/library/38ea7c03-4754-4e71-896a-f68cc2c98ce2).  
  
> [!NOTE]  
>  Você pode obter diferentes resultados do seu modelo. Os resultados dos exemplos a seguir são fornecidos somente para ilustrar o formato do resultado.  
  
### <a name="example-1-predicting-a-number-of-time-slices"></a>Exemplo 1: Prevendo um número de intervalos de tempo  
 O exemplo a seguir usa o **PredictTimeSeries** função para retornar uma previsão para as próximas três próximas etapas e restringe os resultados para a série M200 nas regiões da Europa e Pacífico. Neste modelo específico, o atributo previsível é Quantity, portanto, você deve usar `[Quantity]` como o primeiro argumento para a função PredictTimeSeries.  
  
```  
SELECT FLATTENED  
    [Forecasting].[Model Region],  
    PredictTimeSeries([Forecasting].[Quantity],3)AS t   
FROM  
    [Forecasting]  
WHERE [Model Region] = 'M200 Europe'  
OR [Model Region] = 'M200 Pacific'  
```  
  
 Resultados esperados:  
  
|Região de modelo|t.$TIME|t.Quantity|  
|------------------|-------------|----------------|  
|M200 Europa|7/25/2008 12:00:00 AM|121|  
|M200 Europa|8/25/2008 12:00:00 AM|142|  
|M200 Europa|9/25/2008 12:00:00 AM|152|  
|M200 Pacífico|7/25/2008 12:00:00 AM|46|  
|M200 Pacífico|8/25/2008 12:00:00 AM|44|  
|M200 Pacífico|9/25/2008 12:00:00 AM|42|  
  
 Neste exemplo, a palavra-chave FLATTENED foi usada para facilitar a leitura dos resultados.  Se você não usar a palavra-chave FLATTENED e, em vez disso, retornar um conjunto de linhas hierárquico, esta consulta retornará duas colunas. A primeira coluna contém o valor de [ModelRegion] e a segunda coluna contém uma tabela aninhada com duas colunas: $TIME, que mostra as frações de tempo que estão sendo previstas, e Quantity, que contém os valores previstos.  
  
### <a name="example-2-adding-new-data-and-using-replacemodelcases"></a>Exemplo 2: Adicionando novos dados e usando REPLACE_MODEL_CASES  
 Suponha que você acha que os dados estavam incorretos para uma região específica e deseja usar os padrões no modelo, mas ajustar as previsões para que correspondam aos novos dados. Ou, você pode achar que outra região tenha mais tendências confiáveis e desejar aplicar o modelo mais confiável aos dados de uma região diferente.  
  
 Nestes cenários, você pode usar o parâmetro REPLACE_MODEL_CASES e especificar um novo conjunto de dados a serem usados como dados históricos. Dessa maneira, as projeções serão baseadas nos padrões do modelo especificado, mas continuarão naturalmente a partir do final dos novos pontos de dados. Para obter uma explicação completa desse cenário, consulte [previsões de série temporal avançadas &#40;Tutorial intermediário de mineração de dados&#41;](https://msdn.microsoft.com/library/b614ebdb-07ca-44af-a0ff-893364bd4b71).  
  
 A seguinte consulta PREDICTION JOIN ilustra a sintaxe para substituir dados e fazer novas previsões. Para os dados de substituição, o exemplo recupera o valor das colunas Amount e Quantity e multiplica cada um deles por dois:  
  
```  
SELECT [Forecasting].[Model Region],  
    PredictTimeSeries([Forecasting].[Quantity], 3, REPLACE_MODEL_CASES)   
FROM  
    [Forecasting]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
    'SELECT [ModelRegion],   
    ([Quantity] * 2) as Quantity,  
    ([Amount] * 2) as Amount,  
      [ReportingDate]  
    FROM [dbo].vTimeSeries  
    WHERE ModelRegion = N''M200 Pacific''  
    ') AS t  
ON  
  [Forecasting].[Model Region] = t.[ Model Region] AND  
[Forecasting].[Reporting Date] = t.[ReportingDate] AND  
[Forecasting].[Quantity] = t.[Quantity] AND  
[Forecasting].[Amount] = t.[Amount]  
```  
  
 As tabelas a seguir comparam os resultados da previsão.  
  
 Previsões originais:  
  
||||  
|-|-|-|  
|M200 Pacífico|7/25/2008 12:00:00 AM|46|  
|M200 Pacífico|8/25/2008 12:00:00 AM|44|  
|M200 Pacífico|9/25/2008 12:00:00 AM|42|  
  
 Previsões atualizadas:  
  
||||  
|-|-|-|  
|M200 Pacífico|7/25/2008 12:00:00 AM|91|  
|M200 Pacífico|8/25/2008 12:00:00 AM|89|  
|M200 Pacífico|9/25/2008 12:00:00 AM|84|  
  
### <a name="example-3-adding-new-data-and-using-extendmodelcases"></a>Exemplo 3: Adicionando novos dados e usando EXTEND_MODEL_CASES  
 Exemplo 3 ilustra o uso do *EXTEND_MODEL_CASES* opção para fornecer novos dados, que são adicionados ao final de uma série de dados existente. Em vez de substituir os pontos de dados existentes, os novos dados são adicionados no modelo.  
  
 No exemplo a seguir, os novos dados são fornecidos na instrução SELECT que segue NATURAL PREDICTION JOIN. Você pode fornecer várias linhas da nova entrada com esta sintaxe, mas cada nova linha de entrada deve ter um carimbo de data/hora exclusivo:  
  
```  
SELECT [Model Region],  
    PredictTimeSeries([Forecasting].[Quantity], 5, EXTEND_MODEL_CASES)   
FROM  
    [Forecasting]  
NATURAL PREDICTION JOIN  
    (SELECT  
        1 as [Reporting Date],  
        10 as [Quantity],  
        'M200 Europe' AS [Model Region]  
    UNION SELECT   
        2 as [Reporting Date],  
        15 as [Quantity],  
        'M200 Europe' AS [Model Region]  
) AS T  
WHERE ([Model Region] = 'M200 Europe'  
 OR [Model Region] = 'M200 Pacific')  
```  
  
 Como a consulta usa o *EXTEND_MODEL_CASES* opção, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] realiza as seguintes ações para suas previsões:  
  
-   Aumenta o tamanho total dos casos de treinamento adicionando os dois novos meses de dados ao modelo.  
  
-   Inicia as previsões no final dos dados do caso anterior. Portanto as duas primeiras previsões representam os novos dados de vendas reais que você acabou de adicionar ao modelo.  
  
-   Retorna novas previsões para as três frações de tempo restantes com base no modelo recém-expandido.  
  
 A seguinte tabela lista os resultados da consulta do Exemplo 2. Observe que os dois primeiros valores retornados para M200 Europa são exatamente os mesmos dos novos valores fornecidos. Esse comportamento ocorre por design. Se você desejar iniciar as previsões após o final dos novos dados, deverá especificar um período de início e de término. Para obter um exemplo de como fazer isso, consulte [lição 5: Estendendo a série temporal de modelo](https://msdn.microsoft.com/library/7aad4946-c903-4e25-88b9-b087c20cb67d).  
  
 Além disso, observe que você não forneceu novos dados para a região do Pacífico. Portanto, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] retorna novas previsões para todas as cinco frações de tempo.  
  
 Quantidade: M200 Europe. EXTEND_MODEL_CASES:  
  
|$TIME|Quantidade|  
|-----------|--------------|  
|7/25/2008 0:00|10|  
|8/25/2008 0:00|15|  
|9/25/2008 0:00|72|  
|10/25/2008 0:00|69|  
|11/25/2008 0:00|68|  
  
 Quantidade:  M200 Pacífico. EXTEND_MODEL_CASES:  
  
|$TIME|Quantidade|  
|-----------|--------------|  
|7/25/2008 0:00|46|  
|8/25/2008 0:00|44|  
|9/25/2008 0:00|42|  
|10/25/2008 0:00|42|  
|11/25/2008 0:00|38|  
  
## <a name="example-4-returning-statistics-in-a-time-series-prediction"></a>Exemplo 4: Retornando estatísticas em uma previsão de série temporal  
 O **PredictTimeSeries** função não oferece suporte *INCLUDE_STATISTICS* como um parâmetro. No entanto, a seguinte consulta pode ser usada para retornar as estatísticas de previsão para uma consulta de série temporal. Esse método também pode ser usado com modelos que possuam colunas de tabela aninhada.  
  
 Neste modelo específico, o atributo previsível é Quantity, portanto, você deve usar `[Quantity]` como o primeiro argumento para a função PredictTimeSeries. Se seu modelo usa um atributo previsível diferente, você pode substituir um nome de coluna diferente.  
  
```  
SELECT FLATTENED [Model Region],  
(SELECT   
     $Time,  
     [Quantity] as [PREDICTION],   
     PredictVariance([Quantity]) AS [VARIANCE],  
     PredictStdev([Quantity]) AS [STDEV]  
FROM  
      PredictTimeSeries([Quantity], 3) AS t  
) AS t  
FROM Forecasting  
WHERE [Model Region] = 'M200 Europe'  
OR [Model Region] = 'M200 North America'  
```  
  
 Resultados do exemplo:  
  
|Região de modelo|t.$TIME|t.PREDICTION|t.VARIANCE|t.STDEV|  
|------------------|-------------|------------------|----------------|-------------|  
|M200 Europa|7/25/2008 12:00:00 AM|121|11.6050581415597|3.40661975300439|  
|M200 Europa|8/25/2008 12:00:00 AM|142|10.678201866621|3.26775180615374|  
|M200 Europa|9/25/2008 12:00:00 AM|152|9.86897842568614|3.14149302493037|  
|M200 América do Norte|7/25/2008 12:00:00 AM|163|1.20434529288162|1.20434529288162|  
|M200 América do Norte|8/25/2008 12:00:00 AM|178|1.65031343900634|1.65031343900634|  
|M200 América do Norte|9/25/2008 12:00:00 AM|156|1.68969399185442|1.68969399185442|  
  
> [!NOTE]  
>  A palavra-chave FLATTENED foi usada neste exemplo para facilitar a apresentação dos resultados em uma tabela; no entanto, se o provedor suportar conjuntos de linhas hierárquicos, você poderá omitir a palavra-chave FLATTENED. Se você omitir a palavra-chave FLATTENED, a consulta retornará duas colunas, a primeira contendo o valor que identifica a série de dados `[Model Region]` e a segunda contendo a tabela aninhada de estatísticas.  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Exemplos de consulta de modelo de série temporal](../analysis-services/data-mining/time-series-model-query-examples.md)   
 [Prever &#40;DMX&#41;](../dmx/predict-dmx.md)  
  
  
