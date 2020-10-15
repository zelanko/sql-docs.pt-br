---
title: Ajuste de desempenho para resultados
description: Este artigo resume os métodos, as descobertas e as conclusões de dois estudos de caso que testaram vários métodos de otimização.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 03/29/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b317c09026eb6baa0e9d0f8f2957c7c7c717af55
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956567"
---
# <a name="performance-for-r-services-results-and-resources"></a>Desempenho para R Services: resultados e recursos
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Este artigo é a quarta e última etapa de uma série que descreve a otimização de desempenho para o R Services. Este artigo resume os métodos, as descobertas e as conclusões de dois estudos de caso que testaram vários métodos de otimização.

Os dois estudos de caso tinham metas diferentes:

+ O primeiro estudo de caso, feito pela equipe de desenvolvimento do R Services, procurou medir o impacto de técnicas de otimização específicas
+ O segundo estudo de caso, feito por uma equipe de cientista de dados, experimentou vários métodos para determinar as melhores otimizações para um cenário de pontuação de alto volume específico.

Este tópico lista os resultados detalhados do primeiro estudo de caso. Para o segundo estudo de caso, um resumo descreve as descobertas gerais. Ao final deste tópico, há links para todos os scripts e dados de exemplo e os recursos usados pelos autores originais.

## <a name="performance-case-study-airline-dataset"></a>Estudo de caso de desempenho: Conjunto de dados da Companhia Aérea

Este estudo de caso da equipe de desenvolvimento do SQL Server R Services testou os efeitos de várias otimizações. Um único modelo rxLogit foi criado e a pontuação foi executada no conjunto de dados da Companhia Aérea. Foram aplicadas otimizações durante os processos de treinamento e pontuação para avaliar os impactos individuais.

- GitHub: [Scripts e dados de exemplo](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning) para o estudo de otimizações do SQL Server

### <a name="test-methods"></a>Métodos de teste

1. O conjunto de dados de Companhia Aérea consiste em uma única tabela de 10 milhões de linhas. Ele foi baixado e carregado em massa para o SQL Server.
2. Foram feitas seis cópias da tabela.
3. Várias modificações foram aplicadas às cópias da tabela para testar os recursos do SQL Server, como compactação de página, compactação de linha, indexação, armazenamento de dados de coluna etc.
4. O desempenho foi medido antes e depois da aplicação de cada otimização.

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
4. Cada teste foi executado seis vezes. A hora da primeira execução (a "execução fria") foi descartada. Para comportar a exceção ocasional, o tempo **máximo** entre as cinco execuções restantes também foi descartado. A média das quatro execuções restantes foi obtida para calcular o runtime decorrido médio de cada teste.
5. Os testes foram executados usando o parâmetro *reportProgress* com o valor 3 (= tempos de relatório e progresso). Cada arquivo de saída contém informações sobre o tempo gasto em E/S, tempo de transição e tempo de computação. Esses tempos são úteis para diagnóstico e solução de problemas.
6. A saída do console também foi direcionada para um arquivo no diretório de saída.
7. Os scripts de teste processaram os horários nesses arquivos para computar o tempo médio em execuções.

Por exemplo, os resultados a seguir são os horários de um único teste. Os intervalos principais de interesse são **Tempo total de leitura** (tempo de E/S) e **Tempo de transição** (sobrecarga na configuração de processos de computação).

**Tempos de amostra**

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

Recomendamos baixar e modificar os scripts de teste para ajudar você a solucionar problemas com o R Services ou com as funções RevoScaleR.

### <a name="test-results-all"></a>Resultados de teste (todos)

Esta seção compara os resultados antes e depois de cada um dos testes.

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>Tamanho dos dados com compactação e um repositório de tabelas colunares

O primeiro teste vai comparar o uso de compactação e uma tabela colunar para reduzir o tamanho dos dados.

| Nome da tabela            | Linhas     | Reservado   | Dados       | index_size | Não usado  | % de economia (reservado) |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10000000 | 2978816 KB | 2972160 KB | 6128 KB    | 528 KB  | 0                   |
| *airlineWithPageComp* | 10000000 | 625784 KB  | 623744 KB  | 1352 KB    | 688 KB  | 79%                 |
| *airlineWithRowComp*  | 10000000 | 1262520 KB | 1258880 KB | 2552 KB    | 1088 KB | 58%                 |
| *airlineColumnar*     | 9999999  | 201992 KB  | 201624 KB  | n/d        | 368 KB  | 93%                 |

**Conclusões**

A maior redução no tamanho dos dados foi obtida com a aplicação de um índice columnstore, seguida pela compactação de página.

#### <a name="effects-of-compression"></a>Efeitos da compactação

Esse teste vai comparar os benefícios da compactação de linha, da compactação de página e de nenhuma compactação. Um modelo foi treinado usando `rxLinMod` em dados de três tabelas de dados diferentes. A mesma fórmula e consulta foi usado para todas as tabelas.

| Nome da tabela            | Nome do teste       | numTasks | Tempo médio |
|-----------------------|-----------------|----------|--------------|
| *airlineWithIndex*    | NoCompression   | 1        | 5.6775       |
|                       | NoCompression – paralela| 4        | 5.1775       |
| *airlineWithPageComp* | PageCompression | 1        | 6.7875       |
|                       | PageCompression – paralela | 4        | 5.3225       |
| *airlineWithRowComp*  | RowCompression  | 1        | 6.1325       |
|                       | RowCompression – paralela  | 4        | 5.2375       |

**Conclusões**

A compactação sozinha não parece ajudar. Neste exemplo, o aumento na CPU para lidar com a compactação compensa a diminuição no tempo de E/S.

No entanto, quando o teste é executado em paralelo configurando *numTasks* como 4, o tempo médio diminui.

Para conjuntos de dados maiores, o efeito da compactação pode ser mais visível. A compactação depende do conjunto de dados e valores, portanto pode ser necessário experimentar para determinar o efeito da compactação sobre seu conjunto de dados.

### <a name="effect-of-windows-power-plan-options"></a>Efeito de opções de plano de energia do Windows

Nesse experimento, `rxLinMod` foi usado com o a tabela *airlineWithIntCol*. O plano de energia do Windows foi definido para **Equilibrado** ou **Alto desempenho**. Para todos os testes, *numTasks* foi definido como 1. O teste foi executado seis vezes e foi realizado duas vezes em ambas as opções de energia para investigar a variabilidade dos resultados.

Opção de energia de **Alto desempenho**:

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

O tempo de execução é mais consistente e mais rápido ao usar o plano de energia de **Alto desempenho** do Windows.

#### <a name="using-integer-vs-strings-in-formulas"></a>Como usar inteiros versus cadeias de caracteres em fórmulas

Este teste avaliou o impacto da modificação do código R para evitar um problema comum com fatores de cadeia de caracteres. Especificamente, um modelo foi treinado usando `rxLinMod` com duas tabelas: na primeira, os fatores são armazenados como cadeias de caracteres; na segunda, os fatores são armazenados como inteiros.

+ Para a tabela *airline*, a coluna [DayOfWeek] contém cadeias de caracteres. O parâmetro _colInfo_ foi usado para especificar os níveis de fator (segunda-feira, terça-feira etc.)

+  Para a tabela *airlineWithIndex*, [DayOfWeek] é um número inteiro. O parâmetro _colInfo_ não foi especificado.

+ Em ambos os casos, a mesma fórmula foi usada: `ArrDelay ~ CRSDepTime + DayOfWeek`.

| Nome da tabela          | Nome do teste   | Tempo médio |
|---------------------|-------------|--------------|
| *Airline*           | *FactorCol* | 10.72        |
| *airlineWithIntCol* | *IntCol*    | 3.4475       |

**Conclusões**

Há um benefício claro ao usar inteiros, em vez de cadeias de caracteres, para fatores.

### <a name="avoiding-transformation-functions"></a>Como evitar funções de transformação

Neste teste, um modelo foi treinado usando `rxLinMod`, mas o código foi alterado entre as duas execuções:

+ Na primeira execução, uma função de transformação foi aplicada como parte da compilação do modelo. 
+ Na segunda execução, os valores de recurso eram pré-computados e disponíveis, de modo que nenhuma função de transformação era necessária.

| Nome do teste             | Tempo médio |
|-----------------------|--------------|
| WithTransformation    | 5.1675       |
| WithoutTransformation | 4.7          |

**Conclusões**

O tempo de treinamento foi menor ao **não** usar uma função de transformação. Em outras palavras, o modelo foi treinado mais rapidamente ao usar colunas pré-computadas e mantidas na tabela.

A expectativa é que as economias sejam maiores se houver muitas transformações e o conjunto de dados for maior (\> 100 milhões).

### <a name="using-columnar-store"></a>Como usar repositório colunar

Este teste avaliou os benefícios de desempenho de usar índice e armazenamento de dados colunar. O mesmo modelo foi treinado usando `rxLinMod` e nenhuma transformação de dados.

+ Na primeira execução, a tabela de dados usou um repositório de linhas padrão.
+ Na segunda execução, um repositório de colunas foi usado.

| Nome da tabela         | Nome do teste | Tempo médio |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4.67         |
| *airlineColumnar*  | ColStore  | 4.555        |

**Conclusões**

O desempenho é melhor com o repositório colunar do que com o repositório de linhas padrão. Podemos esperar uma diferença significativa no desempenho em conjuntos de dados maiores (\> 100 milhões).

### <a name="effect-of-using-the-cube-parameter"></a>Efeito do parâmetro de cubo

A finalidade desse teste era determinar se a opção no RevoScaleR para usar o parâmetro de **cubo** pré-computado podia melhorar o desempenho. Um modelo foi treinado usando `rxLinMod` com esta fórmula:

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

Na tabela, os fatores *DayOfWeek* são armazenados como uma cadeia de caracteres.

| Nome do teste     | Parâmetro de cubo | numTasks | Tempo médio | Previsão de uma única linha (ArrDelay_Pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91.0725      | 9.959204                        |
|               |                | 4        | 44.09        | 9.959204                        |
|               | `cube = T`     | 1        | 21.1125      | 9.959204                        |
|               |                | 4        | 8.08         | 9.959204                        |

**Conclusões**

O uso do argumento de parâmetro de cubo melhora claramente o desempenho.

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>Efeito da alteração de maxDepth para modelos rxDTree

Neste experimento, o algoritmo `rxDTree` foi usado para criar um modelo na tabela *airlineColumnar*. Para este teste, *numTasks* foi definido como 4. Diversos valores diferentes para *maxDepth* foram usados para demonstrar como alterar a profundidade da árvore afeta a o runtime.

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

A finalidade desse teste era determinar os impactos de desempenho na pontuação quando o modelo treinado era salvo em uma tabela do SQL Server, em vez de ser gerado como parte do código atualmente em execução. Para a pontuação, o modelo armazenado é carregado do banco de dados e as previsões são criadas usando um quadro de dados em linha na memória (contexto de computação local).

Os resultados de teste mostram a hora de salvar o modelo e o tempo necessário para carregar o modelo e prever.

| Nome da tabela | Nome do teste | Tempo médio (para treinar o modelo) | Tempo para salvar/carregar o modelo|
|------------|------------|------------|------------|
| companhia aérea    | SaveModel| 21.59| 2.08|
| companhia aérea    | LoadModelAndPredict | | 2,09 (inclui o tempo de previsão) |

**Conclusões**

Carregar um modelo treinado de uma tabela é claramente uma maneira mais rápida de fazer previsão. Recomendamos evitar criar o modelo e executar a pontuação no mesmo script.

## <a name="case-study-optimization-for-the-resume-matching-task"></a>Estudo de caso: Otimização para a tarefa de correspondência de currículos

O modelo de correspondência de currículos foi desenvolvido pelo cientista de dados da Microsoft Ke Huang para testar o desempenho do código R no SQL Server e, ao fazer isso, ajuda os cientistas de dados a criar soluções escalonáveis e de nível empresarial.

### <a name="methods"></a>Métodos

Os pacotes RevoScaleR e MicrosoftML foram usados para treinar um modelo de previsão em uma solução do R complexa que envolve grandes conjuntos de dados. AS consultas SQL e código R eram idênticos em todos os testes. Os testes foram realizados em uma única VM do Azure com o SQL Server instalado. Em seguida, o autor comparou os tempos de pontuação com e sem as seguintes otimizações fornecidas pelo SQL Server:

- Tabelas na memória
- Soft-NUMA
- Administrador de Recursos

Para avaliar o efeito do soft-NUMA sobre a execução do script R, a equipe de ciência de dados testou a solução em uma máquina virtual do Azure com 20 núcleos físicos. Nesses núcleos físicos, quatro nós soft-NUMA foram criados automaticamente de modo que cada nó contivesse cinco núcleos.

A definição de afinidade da CPU foi imposta no cenário de correspondência de currículos para avaliar o impacto sobre trabalhos do R. Quatro **pools de recursos do SQL** e quatro **pools de recursos externos** foram criados e a afinidade de CPU foi especificada para garantir que o mesmo conjunto de CPUs seria usado em cada nó.

Cada um dos pools de recursos foi atribuído a um grupo de carga de trabalho diferente para otimizar a utilização do hardware. O motivo é que a afinidade de CPU e de soft-NUMA não pode dividir a memória física nos nós NUMA físicos. Portanto, por definição, todos os nós soft-NUMA baseados no mesmo nó NUMA físico devem usar a memória no mesmo bloco de memória do SO. Em outras palavras, não há afinidade de memória para processador.

O processo a seguir foi usado para criar essa configuração:

1. Reduza a quantidade de memória alocada por padrão ao SQL Server.

2. Crie quatro novos pools para executar os trabalhos do R em paralelo.

3. Crie quatro grupos de cargas de trabalho de modo que cada grupo de carga de trabalho esteja associado a um pool de recursos.

4. Reinicie o Resource Governor com os novos grupos e atribuições de carga de trabalho.

5. Crie uma função de classificador definida pelo usuário para atribuir tarefas diferentes a grupos de carga de trabalho diferentes.

6. Atualize a configuração do Resource Governor para usar a função para grupos de carga de trabalho apropriados.

### <a name="results"></a>Resultados

A configuração com o melhor desempenho no estudo de correspondência de currículos foi a seguinte:

-   Quatro pools de recursos internos (por SQL Server)

-   Quatro pools de recursos externos (para trabalhos de script externos)

-   Cada pool de recursos é associado a um grupo específico de cargas de trabalho

-   Cada pool de recursos é atribuído a CPUs diferentes

-   Uso máximo de memória interna (para o SQL Server) = 30%

-   Memória máxima para uso por sessões do R = 70%

Para o modelo de correspondência de currículos, o uso de script externo era intensivo e não havia outros serviços de mecanismo de banco de dados em execução. Portanto, os recursos alocados a scripts externos foram aumentados para 70%, o que mostrou ser a melhor configuração para o desempenho do script.

Essa configuração foi alcançada experimentando diferentes valores. Se você usar um hardware ou uma solução diferente, a configuração ideal poderá ser diferente. Sempre experimente para encontrar a melhor configuração para seu caso.

Na solução otimizada, 1,1 milhão linhas de dados (com 100 recursos) foram pontuadas em até 8,5 segundos em um computador de 20 núcleos. As otimizações melhoraram significativamente o desempenho em termos de tempo de pontuação.

Os resultados também sugeriram que o **número de recursos** causou um impacto significativo no tempo de pontuação. A melhoria ficou ainda mais clara quando foram usados mais recursos no modelo de previsão.

Recomendamos ler este artigo do blog e o tutorial de acompanhamento para uma discussão detalhada.

-   [Dicas e truques de otimização para aprendizado de máquina no SQL Server](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

Muitos usuários observaram que há uma pequena pausa enquanto o runtime do R (ou do Python) é carregado pela primeira vez. Por esse motivo, conforme descrito nesses testes, o tempo para a primeira execução geralmente é medido, mas depois descartado. O cache subsequente pode resultar em diferenças de desempenho notáveis entre a primeira e a segunda execução. Também há alguma sobrecarga quando os dados são movidos entre o SQL Server e o runtime externo, especialmente se os dados são passados pela rede, em vez de serem carregados diretamente do SQL Server.

Por todos esses motivos, não há uma solução única para mitigar esse tempo de carregamento inicial, pois o impacto sobre o desempenho varia significativamente dependendo da tarefa. Por exemplo, o caching é executado para pontuação de linha única em lotes. Portanto, as operações de pontuação sucessivas são muito mais rápidas e nem o modelo nem o runtime do R é recarregado. Você também pode usar a [Pontuação nativa](../predictions/native-scoring-predict-transact-sql.md) para evitar o totalmente o carregamento do runtime do R.

Para treinar modelos grandes ou pontuação em lotes grandes, a sobrecarga pode ser mínima em comparação aos ganhos de evitar a movimentação de dados ou de streaming e processamento paralelo. Confira esta postagem de blog para obter diretrizes adicionais de desempenho:

+ [Como usar o R para detectar fraude em 1 milhão de transações por segundo](https://blog.revolutionanalytics.com/2016/09/fraud-detection.html/)

## <a name="resources"></a>Recursos

Veja a seguir links para informações, ferramentas e scripts usados no desenvolvimento desses testes.

+ Scripts de teste de desempenho e links para os dados: [Scripts e dados de exemplo para o estudo de otimizações do SQL Server](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ Artigo que descreve a solução de correspondência de currículos: [Dicas e truques de otimização para SQL Server R Services](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

+ Scripts usados na otimização do SQL para a solução de correspondência de currículos: [Repositório do GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips-Resume-Matching)

### <a name="learn-about-windows-server-management"></a>Saiba mais sobre o gerenciamento do Windows Server

+ [Como determinar o tamanho do arquivo de paginação apropriado para versões de 64 bits do Windows](https://support.microsoft.com/kb/2860880)

+ [Compreender NUMA](/previous-versions/sql/sql-server-2008-r2/ms178144(v=sql.105))

+ [Como o SQL Server dá suporte a NUMA](/previous-versions/sql/sql-server-2008-r2/ms180954(v=sql.105))

+ [Soft NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md)

### <a name="learn-about-sql-server-optimizations"></a>Saiba mais sobre otimizações do SQL Server

+ [Reorganizar e recompilar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

+ [Introdução às tabelas com otimização de memória](../../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md)

+ [Demonstração: Aprimoramento do desempenho do OLTP in-memory](../../relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp.md)

+ [Compactação de dados](../../relational-databases/data-compression/data-compression.md)

+ [Habilitar a compactação em uma tabela ou um índice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Desabilitar a compactação em uma tabela ou um índice](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>Saiba mais sobre como gerenciar o SQL Server

+ [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)

+ [Apresentação do Resource Governor](/previous-versions/sql/sql-server-2008-r2/bb895232(v=sql.105))

+ [Um exemplo de configuração do Resource Governor](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>Ferramentas

+ [Ferramenta de teste de desempenho/gerador de carga de armazenamento DISKSPD](https://github.com/microsoft/diskspd)

+ [Referência do utilitário FSUtil](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc753059(v=ws.11))


## <a name="other-articles-in-this-series"></a>Outros artigos nesta série

[Ajuste de desempenho para R – Introdução](sql-server-r-services-performance-tuning.md)

[Ajuste de desempenho para R – configuração do SQL Server](sql-server-configuration-r-services.md)

[Ajuste de desempenho para R – otimização de dados e código do R](r-and-data-optimization-r-services.md)

[Ajuste de desempenho – resultados do estudo de caso](performance-case-study-r-services.md)