---
title: "Desempenho de serviços de R - resultados e recursos | Microsoft Docs"
ms.custom: 
ms.date: 11/09/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0e902312-ad9c-480d-b82f-b871cd1052d9
caps.latest.revision: "8"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 65e3ca0b62da2a8412b92485316074a5f52fa080
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="performance-for-r-services-results-and-resources"></a>Desempenho de serviços de R: resultados e recursos

Este artigo é o quarto e o final de uma série que descreve a otimização de desempenho para serviços de R. Este artigo resume os métodos, descobertas e conclusões de dois estudos de caso que testados vários métodos de otimização.

Dois estudos de caso tinha metas diferentes:

+ O primeiro estudo de caso, pela equipe de desenvolvimento de R Services procurado medir o impacto de técnicas de otimização específicas
+ O segundo estudo de caso, por uma equipe de cientista de dados, experiência com vários métodos para determinar as melhor otimizações para um cenário específico de pontuação de alto volume.

Este tópico lista os resultados detalhados do primeiro estudo de caso. Para o segundo estudo de caso, um resumo descreve as descobertas gerais. No final deste tópico são links para todos os recursos usados pelos autores originais e dados de exemplo e scripts.

## <a name="performance-case-study-airline-dataset"></a>Estudo de caso de desempenho: aérea de conjunto de dados

Este estudo de caso pela equipe de desenvolvimento do SQL Server R Services testado os efeitos de várias otimizações. Foi criado um modelo único rxLogit e pontuação executada no conjunto de dados aérea. Otimizações foram aplicadas durante o treinamento e pontuação processos para avaliar o impacto individual.

- GitHub: [dados e scripts de exemplo](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning) para estudo de otimizações do SQL Server

### <a name="test-methods"></a>Métodos de teste

1. O conjunto de dados aérea consiste em uma única tabela de 10 milhões de linhas. Ela foi baixada e carregados em massa no SQL Server.
2. Seis cópias da tabela foram feitas.
3. Várias modificações foram aplicadas as cópias da tabela, para testar os recursos do SQL Server, como compactação de página, a compactação de linha, indexação, armazenamento de dados Colunar, etc.
4. O desempenho foi medido antes e após cada otimização foi aplicada.

| Nome da tabela| Description|
|------|------|
| *airline* | Dados convertidos do arquivo xdf original usando `rxDataStep`|                          |
| *airlineWithIntCol*   | *DayOfWeek* convertido em um número inteiro em vez de uma cadeia de caracteres. Também adiciona uma coluna *rowNum*.|
| *airlineWithIndex*    | Os mesmos dados que a tabela *airlineWithIntCol*, mas com um único índice clusterizado usando a coluna *rowNum*.|
| *airlineWithPageComp* | Os mesmos dados que a tabela *airlineWithIndex*, mas com a compactação de página habilitada. Também adiciona duas colunas, *CRSDepHour* e *Late*, que são calculadas de *CRSDepTime* e *ArrDelay*. |
| *airlineWithRowComp*  | Os mesmos dados que a tabela *airlineWithIndex*, mas com a compactação de linha habilitada. Também adiciona duas colunas, *CRSDepHour* e *Late*, que são calculadas de *CRSDepTime* e *ArrDelay*. |
| *airlineColumnar*     | Um repositório de colunas com um único índice clusterizado. Essa tabela é populada com os dados de um arquivo csv limpo.|

Cada teste consistiu estas etapas:

1. A coleta de lixo de R foi induzida antes de cada teste.
2. Um modelo de regressão logística foi criado com base nos dados da tabela. O valor de *rowsPerRead* de cada teste foi definido como 500000.
3. Pontuações geradas com o modelo treinado
4. Cada teste foi executado seis vezes. A hora da primeira execução (o "executar frio") foi descartada. Para permitir a exceção ocasional, o **máximo** tempo entre as execuções de cinco restantes também foi descartado. A média das quatro execuções restantes foi obtida para calcular o tempo de execução decorrido médio de cada teste.
5. Os testes foram executados usando o *reportProgress* parâmetro com valor 3 (= os intervalos de relatório e o andamento). Cada arquivo de saída contém informações sobre o tempo gasto na e/s, tempo de transição e tempo de computação. Esses tempos são úteis para diagnóstico e solução de problemas.
6. A saída do console também foi direcionada para um arquivo no diretório de saída.
7. Os scripts de teste processadas as horas nesses arquivos para calcular o tempo médio em execuções.

Por exemplo, os resultados a seguir são os tempos de um único teste. Os intervalos principais de interesse são **Tempo total de leitura** (tempo de E/S) e **Tempo de transição** (sobrecarga na configuração de processos de computação).

**Intervalos de amostra**

```
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

É recomendável que você baixe e modifique os scripts de teste para ajudar a solucionar problemas com serviços de R ou com funções de RevoScaleR.

### <a name="test-results-all"></a>Testar os resultados (todos)

Esta seção compara antes e depois dos resultados para cada um dos testes.

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>Tamanho dos dados com a compactação e um repositório de colunas de tabela

O primeiro teste em comparação com o uso de compactação e uma tabela Colunar para reduzir o tamanho dos dados.

| Nome da tabela            | Linhas     | Reservado   | data       | index_size | Não usado  | % de economia (reservado) |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10000000 | 2978816 KB | 2972160 KB | 6128 KB    | 528 KB  | 0                   |
| *airlineWithPageComp* | 10000000 | 625784 KB  | 623744 KB  | 1352 KB    | 688 KB  | 79%                 |
| *airlineWithRowComp*  | 10000000 | 1262520 KB | 1258880 KB | 2552 KB    | 1088 KB | 58%                 |
| *airlineColumnar*     | 9999999  | 201992 KB  | 201624 KB  | n/d        | 368 KB  | 93%                 |

**Conclusões**

A redução maior tamanho de dados foi obtida pela aplicação de um índice columnstore, seguido pela compactação de página.

#### <a name="effects-of-compression"></a>Efeitos da compactação

Este teste em comparação com os benefícios da compactação de linha, compactação de página e nenhuma compactação. Um modelo foi treinado usando `rxLinMod` em dados de três tabelas de dados diferentes. A mesma fórmula e consulta foi usado para todas as tabelas.

| Nome da tabela            | Nome do teste       | numTasks | Tempo médio |
|-----------------------|-----------------|----------|--------------|
| *airlineWithIndex*    | NoCompression   | 1        | 5.6775       |
|                       | NoCompression - paralelo| 4        | 5.1775       |
| *airlineWithPageComp* | PageCompression | 1        | 6.7875       |
|                       | PageCompression - paralelo | 4        | 5.3225       |
| *airlineWithRowComp*  | RowCompression  | 1        | 6.1325       |
|                       | RowCompression - paralelo  | 4        | 5.2375       |

**Conclusões**

Compactação sozinha não parece ajuda. Neste exemplo, o aumento de CPU para lidar com a compactação compensa a redução no tempo de e/s.

No entanto, quando o teste é executado em paralelo configurando *numTasks* como 4, o tempo médio diminui.

Para conjuntos de dados maiores, o efeito da compactação pode ser mais visível. A compactação depende do conjunto de dados e valores, portanto pode ser necessário experimentar para determinar o efeito da compactação sobre seu conjunto de dados.

### <a name="effect-of-windows-power-plan-options"></a>Efeito de opções de plano de energia do Windows

Nesse experimento, `rxLinMod` foi usado com o a tabela *airlineWithIntCol*. O plano de energia do Windows foi definido como **equilibrado** ou **alto desempenho**. Para todos os testes, *numTasks* foi definido como 1. O teste foi executado seis vezes e foi executado duas vezes em ambas as opções de energia para investigar a variabilidade de resultados.

**Alto desempenho** opção de energia:

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

O tempo de execução é mais consistente e mais rápido ao usar o Windows **alto desempenho** plano de energia.

#### <a name="using-integer-vs-strings-in-formulas"></a>Usando inteiro versus cadeias de caracteres em fórmulas

Esse teste avaliar o impacto de modificar o código de R para evitar um problema comum com os fatores de cadeia de caracteres. Especificamente, um modelo foi treinado usando `rxLinMod` usando duas tabelas: primeiro, fatores são armazenados como cadeias de caracteres; na segunda tabela, fatores são armazenados como números inteiros.

+ Para o *aérea* tabela, a coluna [DayOfWeek] contém cadeias de caracteres. O _colInfo_ parâmetro foi usado para especificar os níveis de fator (segunda-feira, terça-feira,...)

+  Para o *airlineWithIndex* tabela, [DayOfWeek] é um inteiro. O _colInfo_ parâmetro não foi especificado.

+ Em ambos os casos, a mesma fórmula foi usada: `ArrDelay ~ CRSDepTime + DayOfWeek`.

| Nome da tabela          | Nome do teste   | Tempo médio |
|---------------------|-------------|--------------|
| *Aéreo*           | *FactorCol* | 10.72        |
| *airlineWithIntCol* | *IntCol*    | 3.4475       |

**Conclusões**

Há um benefício claro ao usar números inteiros em vez de cadeias de caracteres de fatores.

### <a name="avoiding-transformation-functions"></a>Evitando funções de transformação

Nesse teste, um modelo foi treinado usando `rxLinMod`, mas o código foi alterado entre as duas execuções:

+ Na primeira execução, uma função de transformação foi aplicada como parte da criação de modelos. 
+ Na segunda execução, os valores do recurso foram pré-calculadas e disponível, para que nenhuma função de transformação foi necessária.

| Nome do teste             | Tempo médio |
|-----------------------|--------------|
| WithTransformation    | 5.1675       |
| WithoutTransformation | 4.7          |

**Conclusões**

O tempo de treinamento foi mais curto quando **não** usando uma função de transformação. Em outras palavras, o modelo foi treinado mais rapidamente ao usar colunas que são pré-computadas e persistidas na tabela.

A economia deve ser maior se houve muitas transformações mais e o conjunto de dados maior (\> 100 M).

### <a name="using-columnar-store"></a>Usando o armazenamento Colunar

Esse teste avaliar os benefícios de desempenho do uso de um índice e um repositório de dados de colunas. O mesmo modelo foi treinado usando `rxLinMod` e sem transformações de dados.

+ Na primeira execução, a tabela de dados usado um repositório de linha padrão.
+ Na segunda execução, um repositório de coluna foi usado.

| Nome da tabela         | Nome do teste | Tempo médio |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4.67         |
| *airlineColumnar*  | ColStore  | 4.555        |

**Conclusões**

O desempenho será melhor com o repositório de coluna que com o repositório de linha padrão. Uma diferença significativa no desempenho pode ser esperada em grandes conjuntos de dados (\> M 100).

### <a name="effect-of-using-the-cube-parameter"></a>Efeito de usar o parâmetro de cubo

O objetivo desse teste era determinar se a opção de RevoScaleR para usar o pré-computadas **cubo** parâmetro pode melhorar o desempenho. Um modelo foi treinado usando `rxLinMod`, usando esta fórmula:

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

Na tabela, os fatores *DayOfWeek* é armazenado como uma cadeia de caracteres.

| Nome do teste     | Parâmetro de cubo | numTasks | Tempo médio | Única linha prever (ArrDelay_Pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91.0725      | 9.959204                        |
|               |                | 4        | 44.09        | 9.959204                        |
|               | `cube = T`     | 1        | 21.1125      | 9.959204                        |
|               |                | 4        | 8.08         | 9.959204                        |

**Conclusões**

O uso do argumento de parâmetro de cubo claramente melhora o desempenho.

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>Efeito da alteração maxDepth para modelos de rxDTree

Nesse experimento, o `rxDTree` algoritmo foi usado para criar um modelo no *airlineColumnar* tabela. Para este teste, *numTasks* foi definido como 4. Vários valores diferentes para *maxDepth* foram usados para demonstrar como a alteração de profundidade de árvore afeta o tempo de execução.

| Nome do teste       | maxDepth | Tempo médio |
|-----------------|----------|--------------|
| TreeDepthEffect | 1        | 10.1975      |
|                 | 2        | 13.2575      |
|                 | 4        | 19.27        |
|                 | 8        | 45.5775      |
|                 | 16       | 339.54       |

**Conclusões**

À medida que aumenta a profundidade da árvore, o número total de nós aumenta exponencialmente. O tempo decorrido para criar o modelo também aumentou significativamente.

### <a name="prediction-on-a-stored-model"></a>Previsão em um modelo armazenado

O objetivo desse teste era determinar os impactos de desempenho na pontuação quando o modelo treinado é salvo em uma tabela do SQL Server em vez de gerado como parte do código em execução no momento. Para pontuação, o modelo armazenado é carregado do banco de dados e previsões são criadas usando um quadro de dados de uma linha na memória (contexto de computação local).

Os resultados mostram o tempo para salvar o modelo e o tempo necessário para carregar o modelo e prever.

| Nome da tabela | Nome do teste | Tempo médio (para treinar o modelo) | Tempo para salvar/carregar o modelo|
|------------|------------|------------|------------|
| airline    | SaveModel| 21.59| 2.08|
| airline    | LoadModelAndPredict | | 2,09 (inclui o tempo de previsão) |

**Conclusões**

Carregar um modelo treinado de uma tabela é claramente uma maneira mais rápida para fazer a previsão. É recomendável que você evite criar o modelo e executar todos no mesmo script de pontuação.

## <a name="case-study-optimization-for-the-resume-matching-task"></a>Estudo de caso: otimização para a tarefa continuar correspondente

O modelo de correspondência de retomada foi desenvolvido pelo cientista de dados do Microsoft Ke Huang para testar o desempenho do código R no SQL Server e, ao fazer caso dados ajuda cientistas criar escalonáveis, soluções de nível corporativo.

### <a name="methods"></a>Métodos

Pacotes de RevoScaleR e MicrosoftML foram usados para treinar um modelo de previsão em uma solução R complexo que envolvem grandes conjuntos de dados. Consultas SQL e código R foram idênticos em todos os testes. Testes foram realizados em uma única VM do Azure com o SQL Server instalado. O autor, em seguida, em comparação com pontuação vezes com e sem otimizações a seguir fornecidas pelo SQL Server:

- Tabelas na memória
- Soft-NUMA
- Administrador de Recursos

Para avaliar o efeito de de software na execução do script R, a equipe de ciência de dados testado a solução em uma máquina virtual do Azure com 20 núcleos físicos. Nesses núcleos físicos, quatro nós de software foram criado automaticamente, de forma que cada nó contido cinco núcleos.

A relação de CPU foi imposta no cenário de correspondência de retomada, para avaliar o impacto sobre trabalhos em R. Quatro **pools de recursos SQL** e quatro **pools de recursos externos** foram criados, e a afinidade de CPU foi especificada para garantir que o mesmo conjunto de CPUs seria usado em cada nó.

Cada um dos pools de recursos foi atribuída a um grupo de carga de trabalho diferente, para otimizar a utilização do hardware. O motivo é que o Soft-NUMA e afinidade de CPU não é possível dividir a memória física em nós NUMA físicos; Portanto, por definição, todos os nós NUMA flexíveis que se baseiam no mesmo nó NUMA físico devem usar memória no mesmo bloco de memória do sistema operacional. Em outras palavras, não há nenhuma afinidade de processador de memória.

O processo a seguir foi usado para criar esta configuração:

1. Reduza a quantidade de memória alocada por padrão para o SQL Server.

2. Crie quatro novos pools para executar os trabalhos de R em paralelo.

3. Crie quatro grupos de cargas de trabalho, de modo que cada grupo de carga de trabalho está associado um pool de recursos.

4. Reinicie o administrador de recursos com as atribuições e novos grupos de carga de trabalho.

5. Crie uma função de classificador definida pelo usuário (UDF) para atribuir tarefas diferentes em grupos de cargas de trabalho diferentes.

6. Atualize a configuração do administrador de recursos para usar a função para grupos de cargas de trabalho apropriado.

### <a name="results"></a>Resultados

A configuração que tiveram o melhor desempenho da correspondência de retomar estudar foi da seguinte maneira:

-   Quatro pools de recursos internos (para SQL Server)

-   Quatro pools de recursos externos (para trabalhos de script externo)

-   Cada pool de recursos é associado um grupo de carga de trabalho específica

-   Cada pool de recursos é atribuída a CPUs diferentes

-   Uso máximo de memória interna (para SQL Server) = 30%

-   Memória máxima para uso por sessões de R = 70%

Para o modelo de correspondência para continuar, use script externo foi intensamente e não nenhum outro banco de dados serviços de mecanismo de execução. Portanto, os recursos alocados para scripts externos foram aumentados para 70%, que foi a melhor configuração para o desempenho do script.

Essa configuração foi acessou experimentando valores diferentes. Se você usar outro hardware ou uma solução diferente, a configuração ideal pode ser diferente. Sempre teste para encontrar a melhor configuração para seu caso!

Na solução otimizada, 1.1 milhões de linhas de dados (com 100 recursos) de pontuação em menos de 8,5 segundos em um computador de 20 núcleos. Otimizações melhorou significativamente o desempenho em termos de tempo de pontuação.

Os resultados também sugeridos que o **número de recursos** tinha um impacto significativo no tempo de pontuação. A melhoria foi ainda mais proeminente quando mais recursos que foram usados no modelo de previsão.

É recomendável que você leia este artigo de blog e o tutorial que acompanha uma discussão detalhada.

-   [Dicas de otimização e truques para aprendizado de máquina no SQL Server](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

Muitos usuários observou que há uma pequena pausa conforme o tempo de execução de R (ou Python) é carregado pela primeira vez. Por esse motivo, conforme descrito nesses testes, o tempo para a primeira execução é geralmente medido mas descartado posteriormente. Armazenamento em cache subsequente pode resultar em diferenças de desempenho importantes entre o primeiro e segundo é executado. Também há alguma sobrecarga quando dados são movidos entre o SQL Server e o tempo de execução externo, especialmente se os dados são passados pela rede, em vez de carregar diretamente do SQL Server.

Por esses motivos, não há nenhuma solução para reduzir o tempo de carregamento inicial, como o impacto no desempenho significativamente varia dependendo da tarefa. Por exemplo, o cache é executado para uma linha de pontuação em lotes; Portanto, operações sucessivas de pontuação são muito mais rápidas e o modelo, nem o tempo de execução de R é recarregado. Você também pode usar [pontuação nativo](../sql-native-scoring.md) para evitar o carregamento de tempo de execução de R inteiramente.

Para treinar modelos grandes ou pontuação em lotes grandes, a sobrecarga poderá ser mínima em comparação com os ganhos de evitando a movimentação de dados ou de transmissão e processamento paralelo. Consulte esses blogs recentes e exemplos para obter diretrizes de desempenho adicionais:

+ [Classificação de empréstimo usando o SQL Server 2016 R Services](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/09/27/loan-classification-using-sql-server-2016-r-services/)
+ [Experiências de clientes iniciais ao R Services](https://blogs.msdn.microsoft.com/sqlcat/2016/06/16/early-customer-experiences-with-sql-server-r-services/)
+ [Usando o R para detectar fraudes em 1 milhão de transações por segundo](http://blog.revolutionanalytics.com/2016/09/fraud-detection.html/)

## <a name="resources"></a>Recursos

A seguir estão links para informações, ferramentas e scripts usados no desenvolvimento dos testes.

+ Testes de scripts e links para os dados de desempenho: [scripts para estudo de otimizações do SQL Server e dados de exemplo](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ Artigo sobre a solução de correspondência de retomar: [dica de otimização e truques para SQL Server R Services](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

+ Scripts usados na otimização de SQL para a solução de correspondência de retomar: [repositório GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)

### <a name="learn-about-windows-server-management"></a>Saiba mais sobre o gerenciamento do Windows server

+ [Como determinar o tamanho do arquivo de paginação apropriado para versões de 64 bits do Windows](https://support.microsoft.com/kb/2860880)

+ [Noções básicas sobre NUMA](https://technet.microsoft.com/library/ms178144.aspx)

+ [Como o SQL Server oferece suporte a NUMA](https://technet.microsoft.com/library/ms180954.aspx)

+ [NUMA temporário](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>Saiba mais sobre otimizações do SQL Server

+ [Reorganizar e recompilar índices](../../relational-databases\indexes\reorganize-and-rebuild-indexes.md)

+ [Introdução às tabelas com otimização de memória](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ [Demonstração: Aprimoramento do desempenho do OLTP na memória](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [Compactação de dados](../../relational-databases/data-compression/data-compression.md)

+ [Habilitar a compactação em uma tabela ou um índice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Desabilitar a compactação em uma tabela ou um índice](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>Saiba mais sobre o gerenciamento do SQL Server

+ [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)

+ [Introdução ao administrador de recursos](https://technet.microsoft.com/library/bb895232.aspx)

+ [Governança de recursos para o R Services](resource-governance-for-r-services.md)

+ [Como criar um pool de recursos para R](how-to-create-a-resource-pool-for-r.md)

+ [Um exemplo de configuração do administrador de recursos](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>Ferramentas

+ [Ferramenta de teste de desempenho/gerador de carga de armazenamento DISKSPD](https://github.com/microsoft/diskspd)

+ [Referência do utilitário FSUtil](https://technet.microsoft.com/library/cc753059.aspx)


## <a name="other-articles-in-this-series"></a>Outros artigos nesta série

[Desempenho de ajuste para R – Introdução](sql-server-r-services-performance-tuning.md)

[Ajuste de desempenho para R - configuração do SQL Server](sql-server-configuration-r-services.md)

[Ajuste de desempenho para R - R otimização de código e dados](r-and-data-optimization-r-services.md)

[Ajuste de desempenho - resultados de estudo de caso](performance-case-study-r-services.md)
