---
title: Desempenho para SQL Server R Services-resultados e recursos
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: aa56a9367271df2172236b133d85b5771089b1ac
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715039"
---
# <a name="performance-for-r-services-results-and-resources"></a>Desempenho do R Services: resultados e recursos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo é a quarta e última etapa de uma série que descreve a otimização de desempenho para o R Services. Este artigo resume os métodos, as conclusões e as conclusões de dois estudos de caso que testaram vários métodos de otimização.

Os dois estudos de caso tinham diferentes metas:

+ O primeiro estudo de caso, pela equipe de desenvolvimento do R Services, procurou medir o impacto de técnicas de otimização específicas
+ O segundo estudo de caso, por uma equipe de cientista de dados, experimentou vários métodos para determinar as melhores otimizações para um cenário de Pontuação de alto volume específico.

Este tópico lista os resultados detalhados do primeiro estudo de caso. Para o segundo estudo de caso, um resumo descreve as conclusões gerais. No final deste tópico, há links para todos os scripts e dados de exemplo e os recursos usados pelos autores originais.

## <a name="performance-case-study-airline-dataset"></a>Estudo de caso de desempenho: Conjunto de linhas de companhia aérea

Este estudo de caso da equipe de desenvolvimento de SQL Server R Services testou os efeitos de várias otimizações. Um único modelo rxLogit foi criado e a pontuação foi executada no conjunto de dados de linhas aéreas. Otimizações foram aplicadas durante os processos de treinamento e pontuação para avaliar impactos individuais.

- GitHub Estudo de [dados de exemplo e scripts](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning) para SQL Server de otimização

### <a name="test-methods"></a>Métodos de teste

1. O conjunto de registros da companhia aérea consiste em uma única tabela de linhas 10 milhões. Ele foi baixado e carregado em massa no SQL Server.
2. Foram feitas seis cópias da tabela.
3. Várias modificações foram aplicadas às cópias da tabela para testar SQL Server recursos como compactação de página, compactação de linha, indexação, armazenamento de dados de coluna, etc.
4. O desempenho foi medido antes e após a aplicação de cada otimização.

| Nome da tabela| Descrição|
|------|------|
| *airline* | Dados convertidos do arquivo xdf original usando `rxDataStep`|                          |
| *airlineWithIntCol*   | *DayOfWeek* convertido em um número inteiro em vez de uma cadeia de caracteres. Também adiciona uma coluna *rowNum*.|
| *airlineWithIndex*    | Os mesmos dados que a tabela *airlineWithIntCol*, mas com um único índice clusterizado usando a coluna *rowNum*.|
| *airlineWithPageComp* | Os mesmos dados que a tabela *airlineWithIndex*, mas com a compactação de página habilitada. Também adiciona duas colunas, *CRSDepHour* e *Late*, que são calculadas de *CRSDepTime* e *ArrDelay*. |
| *airlineWithRowComp*  | Os mesmos dados que a tabela *airlineWithIndex*, mas com a compactação de linha habilitada. Também adiciona duas colunas, *CRSDepHour* e *Late*, que são calculadas de *CRSDepTime* e *ArrDelay*. |
| *airlineColumnar*     | Um repositório de colunas com um único índice clusterizado. Essa tabela é populada com os dados de um arquivo csv limpo.|

Cada teste consistiu nestas etapas:

1. A coleta de lixo de R foi induzida antes de cada teste.
2. Um modelo de regressão logística foi criado com base nos dados da tabela. O valor de *rowsPerRead* de cada teste foi definido como 500000.
3. As pontuações foram geradas usando o modelo treinado
4. Cada teste foi executado seis vezes. A hora da primeira execução (a "execução a frio") foi descartada. Para permitir a exceção ocasional, o tempo **máximo** entre as cinco execuções restantes também foi Descartado. A média das quatro execuções restantes foi obtida para calcular o tempo de execução decorrido médio de cada teste.
5. Os testes foram executados usando o parâmetro *reportProgress* com o valor 3 (= temporizações e progresso do relatório). Cada arquivo de saída contém informações sobre o tempo gasto em e/s, tempo de transição e tempo de computação. Esses tempos são úteis para diagnóstico e solução de problemas.
6. A saída do console também foi direcionada para um arquivo no diretório de saída.
7. Os scripts de teste processaram os horários nesses arquivos para calcular o tempo médio em execuções.

Por exemplo, os resultados a seguir são os horários de um único teste. Os intervalos principais de interesse são **Tempo total de leitura** (tempo de E/S) e **Tempo de transição** (sobrecarga na configuração de processos de computação).

**Intervalos de amostra**

```text
Running IntCol Test. Using airlineWithIntCol table.
run 1 took 3.66 seconds
run 2 took 3.44 seconds
run 3 took 3.44 seconds
run 4 took 3.44 seconds
run 5 took 3.45 seconds
run 6 took 3.75 seconds
  
Average Time: 3.4425
metric time pct
1 Total time 3.4425 100.00
2 Overall compute time 2.8512 82.82
3 Total read time 2.5378 73.72
4 Transition time 0.5913 17.18
5 Total non IO time 0.3134 9.10
```

Recomendamos que você baixe e modifique os scripts de teste para ajudá-lo a solucionar problemas com o R Services ou com as funções RevoScaleR.

### <a name="test-results-all"></a>Resultados de teste (todos)

Esta seção compara os resultados antes e depois de cada um dos testes.

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>Tamanho dos dados com compactação e um repositório de tabela colunar

O primeiro teste comparará o uso de compactação e uma tabela colunar para reduzir o tamanho dos dados.

| Nome da tabela            | Linhas     | Reservado   | Data       | index_size | Não usado  | % de economia (reservado) |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10000000 | 2978816 KB | 2972160 KB | 6128 KB    | 528 KB  | 0                   |
| *airlineWithPageComp* | 10000000 | 625784 KB  | 623744 KB  | 1352 KB    | 688 KB  | 79%                 |
| *airlineWithRowComp*  | 10000000 | 1262520 KB | 1258880 KB | 2552 KB    | 1088 KB | 58%                 |
| *airlineColumnar*     | 9999999  | 201992 KB  | 201624 KB  | n/d        | 368 KB  | 93%                 |

**Conclusões**

A maior redução no tamanho dos dados foi obtida com a aplicação de um índice columnstore, seguido pela compactação de página.

#### <a name="effects-of-compression"></a>Efeitos da compactação

Esse teste comparará os benefícios da compactação de linha, da compactação de página e de nenhuma compactação. Um modelo foi treinado usando `rxLinMod` dados de três tabelas de dados diferentes. A mesma fórmula e consulta foi usado para todas as tabelas.

| Nome da tabela            | Nome do teste       | numTasks | Tempo médio |
|-----------------------|-----------------|----------|--------------|
| *airlineWithIndex*    | NoCompression   | 1        | 5.6775       |
|                       | NoCompression – Parallel| 4        | 5.1775       |
| *airlineWithPageComp* | PageCompression | 1        | 6.7875       |
|                       | PageCompression-Parallel | 4        | 5.3225       |
| *airlineWithRowComp*  | RowCompression  | 1        | 6.1325       |
|                       | Unicompactação-paralela  | 4        | 5.2375       |

**Conclusões**

A compactação sozinha não parece ajudar. Neste exemplo, o aumento na CPU para lidar com a compactação compensa a diminuição no tempo de e/s.

No entanto, quando o teste é executado em paralelo configurando *numTasks* como 4, o tempo médio diminui.

Para conjuntos de dados maiores, o efeito da compactação pode ser mais visível. A compactação depende do conjunto de dados e valores, portanto pode ser necessário experimentar para determinar o efeito da compactação sobre seu conjunto de dados.

### <a name="effect-of-windows-power-plan-options"></a>Efeito das opções do plano de energia do Windows

Nesse experimento, `rxLinMod` foi usado com o a tabela *airlineWithIntCol*. O plano de energia do Windows foi definido como equilibrado ou **alto desempenho**. Para todos os testes, *numTasks* foi definido como 1. O teste foi executado seis vezes e foi executado duas vezes em ambas as opções de energia para investigar a variabilidade dos resultados.

Opção de energia de **alto desempenho** :

| Nome do teste | Execute \# | Tempo decorrido | Tempo médio |
|-----------|--------|--------------|--------------|
| IntCol    | 1      | 3,57 segundos |              |
|           | 2      | 3,45 segundos |              |
|           | 3      | 3,45 segundos |              |
|           | 4      | 3,55 segundos |              |
|           | 5      | 3,55 segundos |              |
|           | 6      | 3,45 segundos |              |
|           |        |              | 3.475        |
|           | 1      | 3,45 segundos |              |
|           | 2      | 3,53 segundos |              |
|           | 3      | 3,63 segundos |              |
|           | 4      | 3,49 segundos |              |
|           | 5      | 3,54 segundos |              |
|           | 6      | 3,47 segundos |              |
|           |        |              | 3.5075       |

Opção de energia **Equilibrado**:

| Nome do teste | Execute \# | Tempo decorrido | Tempo médio |
|-----------|--------|--------------|--------------|
| IntCol    | 1      | 3,89 segundos |              |
|           | 2      | 4,15 segundos |              |
|           | 3      | 3,77 segundos |              |
|           | 4      | 5 segundos    |              |
|           | 5      | 3,92 segundos |              |
|           | 6      | 3,8 segundos  |              |
|           |        |              | 3.91         |
|           | 1      | 3,82 segundos |              |
|           | 2      | 3,84 segundos |              |
|           | 3      | 3,86 segundos |              |
|           | 4      | 4,07 segundos |              |
|           | 5      | 4,86 segundos |              |
|           | 6      | 3,75 segundos |              |
|           |        |              | 3.88         |

**Conclusões**

O tempo de execução é mais consistente e mais rápido ao usar o plano de energia de **alto desempenho** do Windows.

#### <a name="using-integer-vs-strings-in-formulas"></a>Usando Integer versus cadeias de caracteres em fórmulas

Este teste avaliou o impacto da modificação do código R para evitar um problema comum com fatores de cadeia de caracteres. Especificamente, um modelo foi treinado com `rxLinMod` o uso de duas tabelas: na primeira, os fatores são armazenados como cadeias de caracteres; na segunda tabela, os fatores são armazenados como inteiros.

+ Para a tabela *aérea* , a coluna [DayOfWeek] contém cadeias de caracteres. O parâmetro _colInfo_ foi usado para especificar os níveis de fator (segunda-feira, terça-feira,...)

+  Para a tabela *airlineWithIndex* , [DayOfWeek] é um número inteiro. O parâmetro _colInfo_ não foi especificado.

+ Em ambos os casos, a mesma fórmula foi usada: `ArrDelay ~ CRSDepTime + DayOfWeek`.

| Nome da tabela          | Nome do teste   | Tempo médio |
|---------------------|-------------|--------------|
| *Vôo*           | *FactorCol* | 10.72        |
| *airlineWithIntCol* | *IntCol*    | 3.4475       |

**Conclusões**

Há um benefício claro ao usar inteiros em vez de cadeias de caracteres para fatores.

### <a name="avoiding-transformation-functions"></a>Evitando funções de transformação

Neste teste, um modelo foi treinado usando `rxLinMod`, mas o código foi alterado entre as duas execuções:

+ Na primeira execução, uma função de transformação foi aplicada como parte da construção do modelo. 
+ Na segunda execução, os valores de recurso foram computacionais e disponíveis, de modo que nenhuma função de transformação era necessária.

| Nome do teste             | Tempo médio |
|-----------------------|--------------|
| WithTransformation    | 5.1675       |
| WithoutTransformation | 4.7          |

**Conclusões**

O tempo de treinamento foi mais curto quando **não** está usando uma função de transformação. Em outras palavras, o modelo foi treinado mais rapidamente ao usar colunas que são previamente computadas e mantidas na tabela.

Espera-se que a economia seja maior se houver muito mais transformações e o conjunto de dados fosse maior\> (100 ms).

### <a name="using-columnar-store"></a>Usando o repositório de coluna

Este teste avaliou os benefícios de desempenho do uso de um armazenamento de dados de coluna e índice. O mesmo modelo foi treinado usando `rxLinMod` e não há transformações de dados.

+ Na primeira execução, a tabela de dados usou um armazenamento de linha padrão.
+ Na segunda execução, um repositório de coluna foi usado.

| Nome da tabela         | Nome do teste | Tempo médio |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4.67         |
| *airlineColumnar*  | ColStore  | 4.555        |

**Conclusões**

O desempenho é melhor com o repositório de colunas do que com o armazenamento de linha padrão. Uma diferença significativa no desempenho pode ser esperada em conjuntos de dados\> maiores (100 M).

### <a name="effect-of-using-the-cube-parameter"></a>Efeito de usar o parâmetro Cube

A finalidade desse teste era determinar se a opção em RevoScaleR para usar o parâmetro de **cubo** precomputado pode melhorar o desempenho. Um modelo foi treinado usando `rxLinMod`esta fórmula:

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

Na tabela, os fatores *DayOfWeek* são armazenados como uma cadeia de caracteres.

| Nome do teste     | Parâmetro de cubo | numTasks | Tempo médio | Previsão de linha única (ArrDelay_Pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91.0725      | 9.959204                        |
|               |                | 4        | 44.09        | 9.959204                        |
|               | `cube = T`     | 1        | 21.1125      | 9.959204                        |
|               |                | 4        | 8.08         | 9.959204                        |

**Conclusões**

O uso do argumento de parâmetro Cube melhora claramente o desempenho.

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>Efeito da alteração de maxDepth para modelos de rxDTree

Neste experimento, o `rxDTree` algoritmo foi usado para criar um modelo na tabela *airlineColumnar* . Para este teste, *numTasks* foi definido como 4. Vários valores diferentes para *MaxDepth* foram usados para demonstrar como a alteração da profundidade da árvore afeta o tempo de execução.

| Nome do teste       | maxDepth | Tempo médio |
|-----------------|----------|--------------|
| TreeDepthEffect | 1        | 10.1975      |
|                 | 2        | 13.2575      |
|                 | 4        | 19.27        |
|                 | 8        | 45.5775      |
|                 | 16       | 339.54       |

**Conclusões**

À medida que aumenta a profundidade da árvore, o número total de nós aumenta exponencialmente. O tempo decorrido para a criação do modelo também aumentou significativamente.

### <a name="prediction-on-a-stored-model"></a>Previsão em um modelo armazenado

A finalidade desse teste era determinar os impactos de desempenho na pontuação quando o modelo treinado é salvo em uma tabela SQL Server em vez de ser gerado como parte do código atualmente em execução. Para pontuação, o modelo armazenado é carregado do banco de dados e as previsões são criadas usando um quadro de dado de uma linha na memória (contexto de computação local).

Os resultados do teste mostram o tempo para salvar o modelo e o tempo necessário para carregar o modelo e prever.

| Nome da tabela | Nome do teste | Tempo médio (para treinar o modelo) | Tempo para salvar/carregar o modelo|
|------------|------------|------------|------------|
| airline    | SaveModel| 21.59| 2.08|
| airline    | LoadModelAndPredict | | 2,09 (inclui o tempo de previsão) |

**Conclusões**

Carregar um modelo treinado de uma tabela é claramente uma maneira mais rápida de fazer a previsão. Recomendamos que você evite criar o modelo e executar a pontuação em todos no mesmo script.

## <a name="case-study-optimization-for-the-resume-matching-task"></a>Estudo de caso: Otimização para a tarefa de retomada-correspondência

O modelo de correspondência de retomada foi desenvolvido pelo cientista de dados da Microsoft ke Huang para testar o desempenho do código R no SQL Server e, ao fazer isso, ajuda os cientistas de dados a criar soluções escalonáveis e de nível corporativo.

### <a name="methods"></a>Métodos

Os pacotes RevoScaleR e MicrosoftML foram usados para treinar um modelo de previsão em uma solução de R complexa que envolve grandes conjuntos de altos. Consultas SQL e código R eram idênticos em todos os testes. Testes foram conduzidos em uma única VM do Azure com o SQL Server instalado. Em seguida, o autor comparou os tempos de pontuação com e sem as seguintes otimizações fornecidas pelo SQL Server:

- Tabelas na memória
- Soft-NUMA
- Administrador de Recursos

Para avaliar o efeito do soft-NUMA na execução do script R, a equipe de ciência de dados testou a solução em uma máquina virtual do Azure com 20 núcleos físicos. Nesses núcleos físicos, quatro nós soft-NUMA foram criados automaticamente, de modo que cada nó continha cinco núcleos.

A CPU affinitization foi imposta no cenário de correspondência de retomada, para avaliar o impacto em trabalhos de R. Quatro **pools de recursos do SQL** e quatro pools de **recursos externos** foram criados, e a afinidade de CPU foi especificada para garantir que o mesmo conjunto de CPUs seria usado em cada nó.

Cada um dos pools de recursos foi atribuído a um grupo de carga de trabalho diferente para otimizar a utilização do hardware. O motivo é que a afinidade de CPU e de soft-NUMA não pode dividir a memória física nos nós NUMA físicos; Portanto, por definição, todos os nós NUMA suaves baseados no mesmo nó NUMA físico devem usar a memória no mesmo bloco de memória do so. Em outras palavras, não há afinidade de memória para processador.

O processo a seguir foi usado para criar essa configuração:

1. Reduza a quantidade de memória alocada por padrão para SQL Server.

2. Crie quatro novos pools para executar os trabalhos do R em paralelo.

3. Crie quatro grupos de cargas de trabalho, de modo que cada grupo de carga de trabalho esteja associado a um pool de recursos.

4. Reinicie Resource Governor com os novos grupos e atribuições de carga de trabalho.

5. Crie uma UDF (função de classificação) definida pelo usuário para atribuir tarefas diferentes em grupos de carga de trabalho diferentes.

6. Atualize a configuração de Resource Governor para usar a função para grupos de carga de trabalho apropriados.

### <a name="results"></a>Resultados

A configuração que tinha o melhor desempenho no estudo retomar correspondência foi a seguinte:

-   Quatro pools de recursos internos (por SQL Server)

-   Quatro pools de recursos externos (para trabalhos de script externo)

-   Cada pool de recursos é associado a um grupo de cargas de trabalho específico

-   Cada pool de recursos é atribuído a CPUs diferentes

-   Uso máximo de memória interna (para SQL Server) = 30%

-   Memória máxima para uso por sessões de R = 70%

Para o modelo de correspondência de retomada, o uso de script externo era pesado e não havia outros serviços de mecanismo de banco de dados em execução. Portanto, os recursos alocados para scripts externos foram aumentados para 70%, o que provou a melhor configuração para o desempenho do script.

Essa configuração foi recebida em experimentando valores diferentes. Se você usar um hardware diferente ou uma solução diferente, a configuração ideal poderá ser diferente. Sempre Experimente encontrar a melhor configuração para seu caso!

Na solução otimizada, 1,1 milhões linhas de dados (com recursos 100) foram pontuadas em até 8,5 segundos em um computador de 20 núcleos. Otimizações melhoraram significativamente o desempenho em termos de tempo de pontuação.

Os resultados também sugeriram que o **número de recursos** teve um impacto significativo no tempo de pontuação. A melhoria foi ainda mais proeminente quando mais recursos eram usados no modelo de previsão.

Recomendamos que você leia este artigo de blog e o tutorial de acompanhamento para uma discussão detalhada.

-   [Dicas e truques de otimização para o aprendizado de máquina no SQL Server](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

Muitos usuários observaram que há uma pequena pausa, pois o tempo de execução de R (ou Python) é carregado pela primeira vez. Por esse motivo, conforme descrito nesses testes, a hora da primeira execução geralmente é medida, mas posteriormente descartada. O cache subsequente pode resultar em diferenças de desempenho notáveis entre a primeira e a segunda execuções. Também há alguma sobrecarga quando os dados são movidos entre SQL Server e o tempo de execução externo, especialmente se os dados são passados pela rede em vez de serem carregados diretamente do SQL Server.

Por todos esses motivos, não há uma solução única para mitigar esse tempo de carregamento inicial, pois o impacto no desempenho varia significativamente dependendo da tarefa. Por exemplo, o Caching é executado para Pontuação de linha única em lotes; Portanto, as operações de Pontuação sucessivas são muito mais rápidas e nem o modelo nem o tempo de execução do R é recarregado. Você também pode usar a [Pontuação nativa](../sql-native-scoring.md) para evitar o carregamento completo do tempo de execução do R.

Para treinar modelos grandes ou pontuação em grandes lotes, a sobrecarga pode ser mínima em comparação com os ganhos, evitando a movimentação de dados ou de streaming e processamento paralelo. Consulte esta postagem de blog para obter diretrizes adicionais de desempenho:

+ [Usando o R para detectar fraude em 1 milhão transações por segundo](https://blog.revolutionanalytics.com/2016/09/fraud-detection.html/)

## <a name="resources"></a>Recursos

Veja a seguir links para informações, ferramentas e scripts usados no desenvolvimento desses testes.

+ Scripts de teste de desempenho e links para os dados: [Estudo de dados de exemplo e scripts para SQL Server de otimização](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ Artigo que descreve a solução de retomada-correspondência: [Dica de otimização e truques para SQL Server R Services](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

+ Scripts usados na otimização do SQL para a solução de correspondência de retomada: [Repositório do GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)

### <a name="learn-about-windows-server-management"></a>Saiba mais sobre o gerenciamento do Windows Server

+ [Como determinar o tamanho do arquivo de paginação apropriado para versões de 64 bits do Windows](https://support.microsoft.com/kb/2860880)

+ [Noções básicas sobre o NUMA](https://technet.microsoft.com/library/ms178144.aspx)

+ [Como SQL Server dá suporte a NUMA](https://technet.microsoft.com/library/ms180954.aspx)

+ [NUMA suave](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>Saiba mais sobre otimizações de SQL Server

+ [Reorganizar e recompilar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

+ [Introdução às tabelas com otimização de memória](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ [Demonstração: Melhoria de desempenho do OLTP na memória](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [Compactação de dados](../../relational-databases/data-compression/data-compression.md)

+ [Habilitar a compactação em uma tabela ou um índice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Desabilitar a compactação em uma tabela ou um índice](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>Saiba mais sobre como gerenciar SQL Server

+ [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)

+ [Introdução ao Resource Governor](https://technet.microsoft.com/library/bb895232.aspx)

+ [Governança de recursos para o R Services](resource-governance-for-r-services.md)

+ [Como criar um pool de recursos para R](how-to-create-a-resource-pool-for-r.md)

+ [Um exemplo de configuração de Resource Governor](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>Ferramentas

+ [Ferramenta de teste de desempenho/gerador de carga de armazenamento DISKSPD](https://github.com/microsoft/diskspd)

+ [Referência do utilitário FSUtil](https://technet.microsoft.com/library/cc753059.aspx)


## <a name="other-articles-in-this-series"></a>Outros artigos desta série

[Ajuste de desempenho para R-introdução](sql-server-r-services-performance-tuning.md)

[Ajuste de desempenho para configuração de SQL Server R](sql-server-configuration-r-services.md)

[Ajuste de desempenho para otimização de dados e código R-R](r-and-data-optimization-r-services.md)

[Ajuste de desempenho-resultados do estudo de caso](performance-case-study-r-services.md)
