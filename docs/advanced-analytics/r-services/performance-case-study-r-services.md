---
title: "Estudo de caso de desempenho (R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0e902312-ad9c-480d-b82f-b871cd1052d9
caps.latest.revision: 8
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 6
---
# Estudo de caso de desempenho (R Services)

Para demonstrar o efeito das diretrizes fornecidas nas seções anteriores, os testes foram executados usando as tabelas do conjunto de dados de viagens. 

## Testes e dados de exemplo

Há seis tabelas com 10 milhões de linhas em cada tabela:

| Nome da tabela | Description |
| ---------- | ----------- |
| _companhia aérea_ | Os dados convertidos de original usando o arquivo xdf *rxDataStep*. |
| _airlineWithIntCol_ | *DayOfWeek* convertido em um número inteiro em vez de uma cadeia de caracteres. Também adiciona uma *rowNum* coluna. |
| _airlineWithIndex_ | Os mesmos dados que o *airlineWithIntCol* tabela, mas com um único índice clusterizado usando o *rowNum* coluna. |
| _airlineWithPageComp_ | Os mesmos dados que o *airlineWithIndex* tabela, mas com a compactação de página habilitada. Também adiciona duas colunas, *CRSDepHour* e *atrasada*, que é calculado de *CRSDepTime* e *ArrDelay*. |
| _airlineWithRowComp_ | Os mesmos dados que o *airlineWithIndex* tabela, mas com compactação de linha ativado. Também adiciona duas colunas, *CRSDepHour* e *atrasada* que é calculado de *CRSDepTime* e *ArrDelay*. 
| _airlineColumnar_ | Um repositório de coluna com um único índice clusterizado. Essa tabela é populada com dados de um csv limpo arquivo. |

Os scripts usados para executar os testes descritos nessa seção, bem como links para os dados de exemplo usados para testes, estão disponíveis em [https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning).

Cada teste foi executado seis vezes, a hora da primeira execução (executar, cold) foi descartado. Para permitir a exceção ocasional, o tempo máximo para o restante cinco executa também foi descartado. A média das execuções restantes quatro foi feita para calcular o tempo de execução decorrido médio de cada teste. Coleta de lixo R foi induzida antes de cada teste. O valor de *rowsPerRead* para cada teste foi definido como 500000.

## Tamanho dos dados ao usar a compactação e uma tabela de armazenamento Colunar

Estes são os resultados do uso de compactação e uma tabela Colunar para reduzir o tamanho dos dados:

| Nome da tabela | Linhas | Reservado | Data | index_size | Não usado | % Salvando (reservado) |
| ---------- | ---- | -------- | ---- | ---------- | ------ | ------------------- |
| airlineWithIndex | 10000000 | 2978816 KB | 2972160 KB | 6128 KB | KB 528 | 0 |
| airlineWithPageComp | 10000000 | 625784 KB | 623744 KB | 1352 KB | 688 KB | 79% |
| airlineWithRowComp | 10000000 | 1262520 KB | 1258880 KB | 2552 KB | 1088 KB | 58% |
| airlineColumnar | 9999999 | 201992 KB | 201624 KB | n/d | KB 368 | 93% |

## Usando o vs inteiro. Cadeia de caracteres na fórmula

Nesse experimento, `rxLinMod` foi usado com a tabela de companhia aérea (onde *DayOfWeek* é uma cadeia de caracteres) e *airlineWithIndex* (onde *DayOfWeek* é um inteiro). Para o primeiro caso, `colInfo` foi usado para especificar os níveis de fator (`Monday`, `Tuesday`, ...). Para o segundo, `colInfo` não foi especificado. Em ambos os casos, a mesma fórmula foi usada. A fórmula usada é `ArrDelay ~ CRSDepTime + DayOfWeek`. Os resultados a seguir mostra claramente a vantagem de usar a cadeia de caracteres de vs inteiro:

| Nome da tabela | Nome do teste | Tempo médio |
| ---------- | --------- | ------------ |
| companhia aérea | FactorCol | 10.72 |
| airlineWithIntCol | IntCol | 3.4475 |

## Usar a compactação

Nesse experimento, `rxLinMod` foi usado com o *airlineWithIndex*, *airlineWithPageComp*, e *airlineWithRowComp* tabelas. A mesma fórmula e consulta foi usado para todas as tabelas. 

| Nome da tabela | Nome do teste | numTasks | Tempo médio |
| ---------- | --------- | -------- | ------------ |
| airlineWithIndex | NoCompression | 1 | 5.6775 |
| &nbsp; | &nbsp; | 4 | 5.1775 |
| airlineWithPageComp | PageCompression | 1 | 6.7875 |
| &nbsp; | &nbsp; | 4 | 5.3225 |
| airlineWithRowComp | RowCompression | 1 | 6.1325 |
| &nbsp; | &nbsp; | 4 | 5.2375 |

Observe que apenas a compactação (*numTasks* definido como 1,) parece não ajuda nesse exemplo, como o aumento de CPU para lidar com a compactação compensa a redução no tempo de e/s. No entanto, quando o teste é executado em paralelo, definindo *numTasks* a 4, diminui o tempo médio. Para conjuntos de dados maiores, o efeito de compactação pode ser mais visível. Compactação depende do conjunto de dados e valores, portanto experimentação pode ser necessária para determinar que a compactação de efeito tem no seu conjunto de dados.

## Evitando a função de transformação

Nesse experimento, `rxLinMod` é usada com a tabela de airlineWithIndex com e sem usar uma função de transformação.  

| Nome do teste | Tempo médio |
| --------- | ------------ |
| WithTransformation | 5.1675 |
| WithoutTransformation | 4.7 |

Observe que há uma melhoria no tempo quando não estiver usando uma função de transformação (usando colunas computadas previamente e persistidos na tabela). A economia será muito maior se houver muitas transformações mais e o conjunto de dados é maior (> 100M).

## Usando armazenamento Colunar

Nesse experimento, `rxLinMod` foi usado com as tabelas airlineWithIndex e airlineColumnar sem usar qualquer transformação. Os resultados indicam que o armazenamento Colunar pode executar melhor do que o repositório de linha. Haverá uma diferença significativa no desempenho em um conjunto de dados maior (> 100 M).  

| Nome da tabela | Nome do teste |Tempo médio |
| ---------- | --------- | ------------ |
| airlineWithIndex | RowStore | 4.67 |
| airlineColumnar | ColStore | 4.555 |

## Efeito do parâmetro de cubo

Nesse experimento, `rxLinMod` é usada com a tabela de companhia aérea onde `DayOfWeek` é armazenado como cadeia de caracteres. A fórmula usada é `ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime`. Os resultados mostram claramente que o uso de `cube` parâmetro ajuda no desempenho. 

| Nome do teste | Parâmetro de cubo | numTasks | Tempo médio | Uma linha prever (ArrDelay_Pred) |
| --------- | -------------- | -------- | ------------ | ------------------------------- |
| CubeArgEffect | `cube = F` | 1 | 91.0725 | 9.959204 |
| &nbsp; | &nbsp; | 4 | 44.09 | 9.959204 |
| &nbsp; | `cube = T` | 1 | 21.1125 | 9.959204 |
| &nbsp; | &nbsp; | 4 | 8.08 | 9.959204 |

## Efeito de maxDepth para rxDTree

Nesse experimento, `rxDTree` é usada com a tabela airlineColumnar. Vários valores diferentes para *maxDepth* foram usados para demonstrar como isso afeta a complexidade de tempo de execução. Como a profundidade aumenta, o número total de nós aumenta exponencialmente e o tempo decorrido aumentará significativamente. Para este teste *numTasks* foi definida como 4.

| Nome do teste | maxDepth | Tempo médio |
| --------- | -------- | ------------ |
| TreeDepthEffect | 1 | 10.1975 |
| &nbsp; | 2 | 13.2575 |
| &nbsp; | 4 | 19.27 |
| &nbsp; | 8 | 45.5775 |
| &nbsp; | 16 | 339.54 |

## Efeito da opção de energia

Nesse experimento, `rxLinMod` foi usado com a tabela de airlineWithIntCol com o Windows foi definido como equilibrado, bem como de alto desempenho, opções de energia. Para todos os testes, *numTasks* foi definido como 1. O teste foi executado 6 vezes e foi executado duas vezes em ambas as opções de energia para demonstrar a variabilidade de resultados ao usar a opção de energia Equilibrado. Os resultados mostram que os números são mais consistente e mais rápido para a opção de reinicialização de alto desempenho. 

__Alto desempenho__ opção de energia:

| Nome do teste | Executar # | Tempo decorrido | Tempo médio |
| --------- | ----- | ------------ | ------------ |
| IntCol | 1 | 3,57 segundos | &nbsp; |
| &nbsp; | 2 | 3,45 segundos | &nbsp; |
| &nbsp; | 3 | 3,45 segundos | &nbsp; |
| &nbsp; | 4 | 3.55 segundos | &nbsp; |
| &nbsp; | 5 | 3.55 segundos | &nbsp; |
| &nbsp; | 6 | 3,45 segundos | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.475 |
| &nbsp; | 1 | 3,45 segundos | &nbsp; |
| &nbsp; | 2 | 3.53 segundos | &nbsp; |
| &nbsp; | 3 | 3.63 segundos | &nbsp; |
| &nbsp; | 4 | 3.49 segundos | &nbsp; |
| &nbsp; | 5 | 3.54 segundos | &nbsp; |
| &nbsp; | 6 | 3.47 segundos | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.5075 |

__Balanceamento__ opção de energia:

| Nome do teste | Executar # | Tempo decorrido | Tempo médio |
| --------- | ----- | ------------ | ------------ |
| IntCol | 1 | 3.89 segundos | &nbsp; |
| &nbsp; | 2 | 4.15 segundos | &nbsp; |
| &nbsp; | 3 | 3.77 segundos | &nbsp; |
| &nbsp; | 4 | 5 segundos | &nbsp; |
| &nbsp; | 5 | 3.92 segundos | &nbsp; |
| &nbsp; | 6 | 3,8 segundos | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.91 |
| &nbsp; | 1 | 3.82 segundos | &nbsp; |
| &nbsp; | 2 | 3.84 segundos | &nbsp; |
| &nbsp; | 3 | 3,86 segundos | &nbsp; |
| &nbsp; | 4 | 4.07 segundos | &nbsp; |
| &nbsp; | 5 | 4.86 segundos | &nbsp; |
| &nbsp; | 6 | 3,75 segundos | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.88 |

## Previsão usando um modelo armazenado

Nesse teste, um modelo é criado e armazenado em um banco de dados. Em seguida, o modelo armazenado é carregado do banco de dados e previsões criadas usando um quadro de dados em uma linha na memória (contexto do computador local). O tempo necessário para treinar, salvar, carregar o modelo e prever é mostrado abaixo. Isso é claramente uma maneira mais rápida de fazer a previsão. Os resultados mostram a hora de salvar o modelo e o tempo necessário para carregar o modelo e prever. 

| Nome da tabela | Nome do teste | Tempo médio (para treinar o modelo) | Tempo de carga/Salvar modelo |
| ---------- | --------- | ----- | ----- |
| companhia aérea | SaveModel | 21.59 | 2.08 | 
| &nbsp; | LoadModelAndPredict | &nbsp; |  2.09 (inclui o tempo para prever) |


## Solução de problemas de desempenho

Os testes usados nesta seção produzem arquivos de saída para cada execução usando o *reportProgress* parâmetro, que é passado para os testes com o valor `3`. A saída do console é direcionada para um arquivo no diretório de saída. O arquivo de saída contém informações sobre o tempo gasto em e/s, tempo de transição e tempo de computação. Esses tempos são úteis para diagnóstico e solução de problemas. Os scripts de teste esses tempos para as várias execuções propor o tempo médio em execuções de processo. Esses scripts de teste e técnicas também podem ser útil na solução de problemas ao usar funções analíticas rx em seu [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Por exemplo, o código a seguir mostra os tempos de exemplo para uma execução. Os intervalos principais de interesse são Total de leitura de e/s (tempo) e fazer a transição de tempo (sobrecarga na configuração de processos de computação).

    Running IntCol Test. Using airlineWithIntCol table.  
        run  1  took  3.66  seconds  
        run  2  took  3.44  seconds  
        run  3  took  3.44  seconds  
        run  4  took  3.44  seconds  
        run  5  took  3.45  seconds  
        run  6  took  3.75  seconds  

    Average Time:  3.4425  
                    metric   time    pct 
    1           Total time 3.4425 100.00 
    2 Overall compute time 2.8512  82.82 
    3      Total read time 2.5378  73.72 
    4      Transition time 0.5913  17.18 
    5    Total non IO time 0.3134   9.10 
 
 ## Consulte também
 [Guia de ajuste de desempenho do SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
 [Configuração do SQL Server para serviços de R](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
 
 [R e otimização de dados](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)