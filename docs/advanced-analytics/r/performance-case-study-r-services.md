---
title: Desempenho do SQL Server R Services – resultados e recursos – SQL Server Machine Learning Services
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3ee5a1d2c656ef420c410c75333546ab8fbf539c
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645465"
---
# <a name="performance-for-r-services-results-and-resources"></a>Desempenho para R Services: recursos e os resultados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo é o quarto e o final de uma série que descreve a otimização de desempenho para R Services. Este artigo resume os métodos, as descobertas e conclusões de dois estudos de caso que testou vários métodos de otimização.

Dois estudos de caso tinha metas diferentes:

+ O primeiro estudo de caso, pela equipe de desenvolvimento do R Services, procurado medir o impacto de técnicas de otimização específicas
+ O segundo estudo de caso, por uma equipe de cientista de dados, experimentamos vários métodos para determinar as melhores otimizações para um cenário específico de pontuação de alto volume.

Este tópico lista os resultados detalhados do primeiro estudo de caso. Para o segundo estudo de caso, um resumo descreve as descobertas geral. No final deste tópico são links para todos os recursos usados pelos autores originais e dados de exemplo e scripts.

## <a name="performance-case-study-airline-dataset"></a>Estudo de caso de desempenho: Conjunto de dados de companhia aérea

Este estudo de caso pela equipe de desenvolvimento do SQL Server R Services testado os efeitos de várias otimizações. Foi criado um modelo único rxLogit e pontuação realizadas no conjunto de dados de companhia aérea. As otimizações foram aplicadas durante o treinamento e pontuação processos para avaliar os impactos individuais.

- GitHub: [Dados e scripts de exemplo](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning) para estudar em otimizações do SQL Server

### <a name="test-methods"></a>Métodos de teste

1. O conjunto de dados de companhia aérea consiste em uma única tabela de 10 milhões de linhas. Ele foi baixado e em massa carregados no SQL Server.
2. Foram feitas seis cópias da tabela.
3. Várias modificações foram aplicadas às cópias da tabela, para testar os recursos do SQL Server, como compactação de página, a compactação de linha, indexação, armazenamento de dados Colunar, etc.
4. O desempenho foi medido antes e após cada otimização foi aplicada.

| Nome da tabela| Descrição|
|------|------|
| *airline* | Dados convertidos do arquivo xdf original usando `rxDataStep`|                          |
| *airlineWithIntCol*   | *DayOfWeek* convertido em um número inteiro em vez de uma cadeia de caracteres. Também adiciona uma coluna *rowNum*.|
| *airlineWithIndex*    | Os mesmos dados que a tabela *airlineWithIntCol*, mas com um único índice clusterizado usando a coluna *rowNum*.|
| *airlineWithPageComp* | Os mesmos dados que a tabela *airlineWithIndex*, mas com a compactação de página habilitada. Também adiciona duas colunas, *CRSDepHour* e *Late*, que são calculadas de *CRSDepTime* e *ArrDelay*. |
| *airlineWithRowComp*  | Os mesmos dados que a tabela *airlineWithIndex*, mas com a compactação de linha habilitada. Também adiciona duas colunas, *CRSDepHour* e *Late*, que são calculadas de *CRSDepTime* e *ArrDelay*. |
| *airlineColumnar*     | Um repositório de colunas com um único índice clusterizado. Essa tabela é populada com os dados de um arquivo csv limpo.|

Cada teste é formada por uma dessas etapas:

1. A coleta de lixo de R foi induzida antes de cada teste.
2. Um modelo de regressão logística foi criado com base nos dados da tabela. O valor de *rowsPerRead* de cada teste foi definido como 500000.
3. Pontuações foram geradas usando o modelo treinado
4. Cada teste foi executado seis vezes. A hora da primeira execução (o "executar frio") foi descartada. Para permitir a exceção ocasional, o **máximo** tempo entre as cinco execuções restantes também foi descartado. A média das quatro execuções restantes foi obtida para calcular o tempo de execução decorrido médio de cada teste.
5. Os testes foram executados usando o *reportProgress* parâmetro com valor 3 (= os intervalos de relatório e o progresso). Cada arquivo de saída contém informações sobre o tempo gasto em e/s, tempo de transição e tempo de computação. Esses tempos são úteis para diagnóstico e solução de problemas.
6. A saída do console também foi direcionada para um arquivo no diretório de saída.
7. Os scripts de teste processado os tempos de nesses arquivos para calcular o tempo médio em execuções.

Por exemplo, os resultados a seguir estão as horas de um único teste. Os intervalos principais de interesse são **Tempo total de leitura** (tempo de E/S) e **Tempo de transição** (sobrecarga na configuração de processos de computação).

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

É recomendável que você baixe e modifique os scripts de teste para ajudar a solucionar problemas com o R Services ou com as funções de RevoScaleR.

### <a name="test-results-all"></a>Testar resultados (todos)

Esta seção compara antes e depois os resultados para cada um dos testes.

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>Tamanho dos dados com a compactação e um armazenamento de tabela Colunar

O primeiro teste em comparação com o uso de compactação e uma tabela Colunar para reduzir o tamanho dos dados.

| Nome da tabela            | Linhas     | Reservado   | Dados       | index_size | Não usado  | % de economia (reservado) |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10000000 | 2978816 KB | 2972160 KB | 6128 KB    | 528 KB  | 0                   |
| *airlineWithPageComp* | 10000000 | 625784 KB  | 623744 KB  | 1352 KB    | 688 KB  | 79%                 |
| *airlineWithRowComp*  | 10000000 | 1262520 KB | 1258880 KB | 2552 KB    | 1088 KB | 58%                 |
| *airlineColumnar*     | 9999999  | 201992 KB  | 201624 KB  | n/d        | 368 KB  | 93%                 |

**Conclusões**

A maior redução no tamanho dos dados foi obtida por meio da aplicação de um índice columnstore, seguido de compactação de página.

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

Apenas a compactação parece não ajudar. Neste exemplo, o aumento de CPU para lidar com a compactação compensa a diminuição no tempo de e/s.

No entanto, quando o teste é executado em paralelo configurando *numTasks* como 4, o tempo médio diminui.

Para conjuntos de dados maiores, o efeito da compactação pode ser mais visível. A compactação depende do conjunto de dados e valores, portanto pode ser necessário experimentar para determinar o efeito da compactação sobre seu conjunto de dados.

### <a name="effect-of-windows-power-plan-options"></a>Efeito de opções de plano de energia do Windows

Nesse experimento, `rxLinMod` foi usado com o a tabela *airlineWithIntCol*. O plano de energia do Windows foi definido como **equilibrado** ou **alto desempenho**. Para todos os testes, *numTasks* foi definido como 1. O teste foi executado seis vezes e foi executado duas vezes em ambas as opções de energia para investigar a variabilidade de resultados.

**Alto desempenho** opções de energia:

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

O tempo de execução é mais consistente e mais rápido ao usar o Windows **de alto desempenho** plano de energia.

#### <a name="using-integer-vs-strings-in-formulas"></a>Usando o inteiro versus cadeias de caracteres em fórmulas

Esse teste avaliar o impacto de modificar o código R para evitar um problema comum com fatores de cadeia de caracteres. Especificamente, um modelo foi treinado usando `rxLinMod` usando duas tabelas: na primeira, fatores são armazenados como cadeias de caracteres; na segunda tabela, fatores são armazenadas como inteiros.

+ Para o *airline* tabela, a coluna [DayOfWeek] contém cadeias de caracteres. O _colInfo_ parâmetro foi usado para especificar os níveis de fator (segunda-feira, terça-feira,...)

+  Para o *airlineWithIndex* tabela, [DayOfWeek] é um inteiro. O _colInfo_ parâmetro não foi especificado.

+ Em ambos os casos, a mesma fórmula foi usada: `ArrDelay ~ CRSDepTime + DayOfWeek`.

| Nome da tabela          | Nome do teste   | Tempo médio |
|---------------------|-------------|--------------|
| *Companhia aérea*           | *FactorCol* | 10.72        |
| *airlineWithIntCol* | *IntCol*    | 3.4475       |

**Conclusões**

Há um benefício claro ao usar números inteiros em vez de cadeias de caracteres para fatores.

### <a name="avoiding-transformation-functions"></a>Evitando a funções de transformação

Nesse teste, um modelo foi treinado usando `rxLinMod`, mas o código foi alterado entre as duas execuções:

+ Na primeira execução, uma função de transformação foi aplicada como parte da criação de modelos. 
+ A segunda execução, os valores do recurso foram pré-calculadas e disponível, para que nenhuma função de transformação foi necessária.

| Nome do teste             | Tempo médio |
|-----------------------|--------------|
| WithTransformation    | 5.1675       |
| WithoutTransformation | 4.7          |

**Conclusões**

O tempo de treinamento foi quando mais curto **não** usando uma função de transformação. Em outras palavras, o modelo foi treinado com mais rapidez ao usar colunas que são pré-calculadas e mantidas na tabela.

As economias deve ser maior se houvesse muitas transformações e o conjunto de dados fosse maior (\> 100m).

### <a name="using-columnar-store"></a>Usando repositório Colunar

Esse teste avaliado os benefícios de desempenho do uso de um índice e o repositório de dados de colunas. O mesmo modelo foi treinado usando `rxLinMod` e nenhuma transformação de dados.

+ Na primeira execução, a tabela de dados usado um repositório de linha padrão.
+ A segunda execução, um repositório de coluna foi usado.

| Nome da tabela         | Nome do teste | Tempo médio |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4.67         |
| *airlineColumnar*  | ColStore  | 4.555        |

**Conclusões**

O desempenho é melhor com o repositório de colunas que com o repositório de linha padrão. Uma diferença significativa no desempenho pode ser esperada em conjuntos de dados maiores (\> 100m).

### <a name="effect-of-using-the-cube-parameter"></a>Efeito de usar o parâmetro de cubo

O objetivo desse teste era determinar se a opção de RevoScaleR para usar o pré-computadas **cubo** parâmetro pode melhorar o desempenho. Um modelo foi treinado usando `rxLinMod`, usando esta fórmula:

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

Na tabela, os fatores *DayOfWeek* é armazenada como uma cadeia de caracteres.

| Nome do teste     | Parâmetro de cubo | numTasks | Tempo médio | Única linha (arrdelay_pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91.0725      | 9.959204                        |
|               |                | 4        | 44.09        | 9.959204                        |
|               | `cube = T`     | 1        | 21.1125      | 9.959204                        |
|               |                | 4        | 8.08         | 9.959204                        |

**Conclusões**

O uso do argumento de parâmetro de cubo claramente melhora o desempenho.

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>Efeito da alteração de maxDepth para rxDTree modelos

Nesse experimento, o `rxDTree` algoritmo foi usado para criar um modelo em de *airlineColumnar* tabela. Para este teste, *numTasks* foi definido como 4. Vários valores diferentes para *maxDepth* foram usados para demonstrar como a profundidade da árvore a alteração afeta o tempo de execução.

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

O objetivo desse teste era determinar o impacto de desempenho na pontuação quando o modelo treinado é salvo em uma tabela do SQL Server em vez de gerado como parte do código em execução no momento. Para pontuação, o modelo armazenado é carregado do banco de dados e previsões são criadas usando um quadro de dados de uma linha na memória (contexto de computação local).

Os resultados do teste mostram a hora de salvar o modelo e o tempo necessário para carregar o modelo e prever.

| Nome da tabela | Nome do teste | Tempo médio (para treinar o modelo) | Tempo para salvar/carregar o modelo|
|------------|------------|------------|------------|
| airline    | SaveModel| 21.59| 2.08|
| airline    | LoadModelAndPredict | | 2,09 (inclui o tempo de previsão) |

**Conclusões**

Carregar um modelo de treinamento de uma tabela é claramente uma maneira mais rápida de realizar a previsão. É recomendável que você evite criar o modelo e executar tudo no mesmo script de pontuação.

## <a name="case-study-optimization-for-the-resume-matching-task"></a>Estudo de caso: Otimização para a tarefa de correspondência de retomada

O modelo de correspondência de retomada foi desenvolvido pelo cientista de dados do Microsoft Ke Huang para testar o desempenho do código R no SQL Server e, ao fazer então dados ajuda os cientistas criar escalonáveis, soluções de nível empresarial.

### <a name="methods"></a>Métodos

Pacotes de RevoScaleR e MicrosoftML foram usados para treinar um modelo de previsão em uma solução de R complexo que envolvem grandes conjuntos de dados. Consultas SQL e o código R eram idênticas em todos os testes. Testes foram realizados em uma única VM do Azure com o SQL Server instalado. O autor, em seguida, em comparação com tempos de pontuação com e sem as seguintes otimizações fornecidas pelo SQL Server:

- Tabelas na memória
- Soft-NUMA
- Administrador de Recursos

Para avaliar o efeito de soft-em execução do script R, a equipe de ciência de dados testado a solução em uma máquina virtual do Azure com 20 núcleos físicos. Esses núcleos físicos, quatro nós de software foram criado automaticamente, que cada nó contido cinco núcleos.

A relação de CPU foi imposta no cenário de correspondência de retomada, para avaliar o impacto nos trabalhos de R. Quatro **pools de recursos do SQL** e quatro **pools de recursos externos** foram criados, e afinidade de CPU foi especificada para garantir que o mesmo conjunto de CPUs seria usado em cada nó.

Cada um dos pools de recursos foi atribuído a um grupo de carga de trabalho diferentes, para otimizar a utilização de hardware. O motivo é que o Soft-NUMA e afinidade de CPU não é possível dividir a memória física em nós NUMA físicos; Portanto, por definição, todos os nós de software que se baseiam no mesmo nó NUMA físico devem usar memória no mesmo bloco de memória do sistema operacional. Em outras palavras, não há nenhuma afinidade do processador de memória.

O processo a seguir foi usado para criar esta configuração:

1. Reduza a quantidade de memória alocada por padrão para o SQL Server.

2. Crie quatro novos pools para executar os trabalhos de R em paralelo.

3. Crie quatro grupos de carga de trabalho, de modo que cada grupo de carga de trabalho é associado um pool de recursos.

4. Reinicie o administrador de recursos com os novos grupos de carga de trabalho e atribuições.

5. Crie uma função de classificador definida pelo usuário (UDF) para atribuir tarefas diferentes grupos de carga de trabalho diferentes.

6. Atualize a configuração do administrador de recursos para usar a função para grupos de carga de trabalho adequado.

### <a name="results"></a>Resultados

A configuração que tinha o melhor desempenho em que a correspondência de retomar a estudar a era da seguinte maneira:

-   Quatro pools de recursos internos (para SQL Server)

-   Quatro pools de recursos externos (para trabalhos de script externo)

-   Cada pool de recursos é associado um grupo de carga de trabalho específica

-   Cada pool de recursos é atribuído a CPUs diferentes

-   Uso máximo da memória interno (para SQL Server) = 30%

-   Memória máxima para uso por sessões de R = 70%

Para o modelo de correspondência de retomada, o uso de script externo foi pesado e não houvesse nenhum outro banco de dados serviços de mecanismo de execução. Portanto, os recursos alocados para scripts externos foram aumentados para 70%, que provou a melhor configuração para o desempenho de script.

Essa configuração foi acessou experimentando com valores diferentes. Se você usar um hardware diferente ou uma solução diferente, a configuração ideal pode ser diferente. Sempre experimentos para encontrar a melhor configuração para seu caso!

Na solução otimizada, 1,1 milhão de linhas de dados (com 100 recursos) foram pontuadas em menos de 8,5 segundos em um computador de 20 núcleos. Otimizações melhoraram significativamente o desempenho em termos de tempo de pontuação.

Os resultados também sugeriram que o **número de recursos** teve um impacto significativo na hora de pontuação. A melhoria era ainda mais proeminente quando mais recursos que foram usados no modelo de previsão.

É recomendável que você leia este artigo de blog e o tutorial que acompanha este artigo para uma discussão detalhada.

-   [Dicas de otimização e truques para aprendizado de máquina no SQL Server](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

Muitos usuários tem observado que há uma pequena pausa como o tempo de execução de R (ou Python) é carregado pela primeira vez. Por esse motivo, conforme descrito nesses testes, o tempo para a primeira execução é, sendo geralmente medido mas descartado posteriormente. Armazenamento em cache subsequente pode resultar em diferenças de desempenho notável entre o primeiro e segundo é executado. Também há alguma sobrecarga quando dados são movidos entre o SQL Server e o tempo de execução externo, especialmente se os dados são passados pela rede, em vez de que está sendo carregado diretamente do SQL Server.

Por esses motivos, não há nenhuma solução para reduzir esse tempo de carregamento inicial, como o impacto no desempenho significativamente varia dependendo da tarefa. Por exemplo, o cache é executado para uma linha de pontuação em lotes; Portanto, operações sucessivas de pontuação são muito mais rápidas e nem o modelo nem o tempo de execução de R é recarregado. Você também pode usar [pontuação nativa](../sql-native-scoring.md) para evitar o carregamento de tempo de execução de R inteiramente.

Para treinamento de modelos grandes ou de pontuação em lotes grandes, a sobrecarga pode ser mínima em comparação com os ganhos de evitando a movimentação de dados ou de transmissão e processamento paralelo. Consulte estes blogs recentes e exemplos para obter diretrizes de desempenho adicionais:

+ [Classificação de empréstimo usando o SQL Server 2016 R Services](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/09/27/loan-classification-using-sql-server-2016-r-services/)
+ [Experiências de clientes antecipado com o R Services](https://blogs.msdn.microsoft.com/sqlcat/2016/06/16/early-customer-experiences-with-sql-server-r-services/)
+ [Usando o R para detectar fraudes de 1 milhão de transações por segundo](https://blog.revolutionanalytics.com/2016/09/fraud-detection.html/)

## <a name="resources"></a>Recursos

A seguir estão links para informações, ferramentas e scripts usados no desenvolvimento desses testes.

+ Teste os scripts e links para os dados de desempenho: [Dados de exemplo e scripts para estudo de otimizações do SQL Server](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ Artigo que descreve a solução de retomada de correspondência: [Dica de otimização e truques para SQL Server R Services](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

+ Scripts usados na otimização de SQL para a solução de retomada de correspondência: [Repositório do GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)

### <a name="learn-about-windows-server-management"></a>Saiba mais sobre o gerenciamento do Windows server

+ [Como determinar o tamanho do arquivo de paginação apropriado para versões de 64 bits do Windows](https://support.microsoft.com/kb/2860880)

+ [Noções básicas sobre NUMA](https://technet.microsoft.com/library/ms178144.aspx)

+ [Como o SQL Server dá suporte a NUMA](https://technet.microsoft.com/library/ms180954.aspx)

+ [Soft-NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>Saiba mais sobre as otimizações do SQL Server

+ [Reorganizar e recompilar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

+ [Introdução às tabelas com otimização de memória](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ [Demonstração: Aprimoramento do desempenho do OLTP na memória](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [Compactação de dados](../../relational-databases/data-compression/data-compression.md)

+ [Habilitar a compactação em uma tabela ou um índice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Desabilitar a compactação em uma tabela ou um índice](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>Saiba mais sobre o gerenciamento do SQL Server

+ [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)

+ [Introdução ao Resource Governor](https://technet.microsoft.com/library/bb895232.aspx)

+ [Governança de recursos para o R Services](resource-governance-for-r-services.md)

+ [Como criar um pool de recursos para R](how-to-create-a-resource-pool-for-r.md)

+ [Um exemplo de configuração do administrador de recursos](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>Ferramentas

+ [Ferramenta de teste de desempenho/gerador de carga de armazenamento DISKSPD](https://github.com/microsoft/diskspd)

+ [Referência do utilitário FSUtil](https://technet.microsoft.com/library/cc753059.aspx)


## <a name="other-articles-in-this-series"></a>Outros artigos desta série

[Desempenho de ajuste para R – Introdução](sql-server-r-services-performance-tuning.md)

[Ajuste de desempenho para R – configuração do SQL Server](sql-server-configuration-r-services.md)

[Ajuste de desempenho para R – R otimização de código e dados](r-and-data-optimization-r-services.md)

[Ajuste de desempenho - resultados de estudo de caso](performance-case-study-r-services.md)
